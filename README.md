# Odoo Folder Oasis

# Crear Usuario
adduser --system --home=/opt/oasis --group oasis
su - oasis -s /bin/bash

# Permiso
sudo chmod 777 -R /opt/oasis/*

* Agregar permiso al usuario  Oasis para usar docker
sudo usermod -aG docker oasis


# Base de Datos

docker run -d   -e POSTGRES_USER=odoo -e POSTGRES_PASSWORD=odoo -e POSTGRES_DB=postgres -p 5432:5432 --name db postgres:10 

# ODOO

docker run -v /opt/oasis/config:/etc/odoo -v /opt/oasis/odoo-data:/var/lib/odoo  -v /opt/oasis/extra-addons:/mnt/extra-addons -p 8069:8069 --name odoo --link db:db -t odoo:14.0

# Update Modulos

python3 /usr/bin/odoo -c ./etc/odoo/odoo.conf -d {DATABASE} -u "all" --workers=0 --no-http --i18n-overwrite --without-demo=WITHOUT_DEMO --stop-after-init