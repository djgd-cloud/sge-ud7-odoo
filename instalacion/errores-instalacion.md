# Errores encontrados en la instalación

| Error / mensaje | Causa | Solución aplicada | Fuente consultada |
|---|---|---|---|
| `no configuration file provided: not found` | Ejecuté `docker-compose up -d` en una carpeta sin `docker-compose.yaml`. | Ejecutar el comando dentro de `odoo-main`, donde está el fichero. | Mensaje de error de Docker Compose en la terminal. |
| `KeyError: 'options'` y `NoSectionError: No section: 'options'` en `wait-for-psql.py`, con `No such file` sobre `/etc/odoo/odoo.conf` | El contenedor necesita `/etc/odoo/odoo.conf`, montado desde `./config`. La carpeta no existía y después el fichero se creó con el nombre `oddo.conf` y quedó vacío. | Crear `config\odoo.conf` con la sección `[options]` y los datos de conexión a la base de datos. | Logs del contenedor (`docker compose logs odoo`). |
| `ERR_EMPTY_RESPONSE` en `localhost:8200` | Odoo escuchaba solo en `127.0.0.1:8069` dentro del contenedor, así que el puerto reenviado no recibía respuesta. | Añadir `http_interface = 0.0.0.0` a `odoo.conf` y reiniciar el contenedor. | Línea `HTTP service running on 127.0.0.1:8069` de los logs. |
| `Wrong login/password` | Intenté entrar con las credenciales de mi cuenta online, que no existen en la base local. | Entrar con el usuario por defecto de la base nueva (`admin`) y cambiar la contraseña. | [Confirma si lo hiciste así.] |
| `option addons_path, invalid addons directory '/mnt/extra-addons'` | La carpeta `addons` montada en el contenedor no existía en el host. | Crear la carpeta `addons` dentro de `odoo-main`. | [Confirma si lo hiciste.] |