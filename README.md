# odoo-folder

# Permiso
sudo chmod 777 -R *

# Crear Usuario
adduser --system --home=/opt/odoo10 --group odoo10


# Base de Datos

docker run -d  -e PGDATA=/var/lib/postgresql/data/pgdata -v {Tu-Ruta}:/var/lib/postgresql/data/pgdata -e POSTGRES_USER=odoo -e POSTGRES_PASSWORD=odoo -e POSTGRES_DB=postgres -p 5432:5432 --name db postgres:10 

# ODOO

docker run -v {Tu-Ruta}/config:/etc/odoo -v {Tu-Ruta}/odoo-data:/var/lib/odoo  -v {Tu-Ruta}/extra-addons:/mnt/extra-addons -p 8069:8069 --name odoo --link db:db -t odoo:14.0

# Update Modulos

python3 /usr/bin/odoo -c ./etc/odoo/odoo.conf -d {DATABASE} -u "all" --workers=0 --no-http --i18n-overwrite --without-demo=WITHOUT_DEMO --stop-after-init