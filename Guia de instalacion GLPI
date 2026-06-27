“GLPI (Gestionare Libre de Parc
Informatique) es una herramienta
web de código abierto para la gestión
de servicios TI (mesa de ayuda) e
inventario de activos, que permite
registrar incidencias, solicitudes y
administrar equipos y recursos de
forma centralizada.”
Instalación
GLPI
Guia practica
Andrés Morales de los rios

¿QUÉ LICENCIA UTILIZA GLPI?
GLPI utiliza la licencia GPL v2 ( GNU General Public License versión 2 ).

¿PERMITE USAR GLPI EN UNA EMPRESA
PRIVADA SIN PAGAR?
Sí.

La licencia GPL v2 permite usar GLPI en cualquier empresa, pública o privada, sin
pagar ningún canon, cuota ni licencia comercial.

Y esta licencia permite usar, modificar y redistribuir el software, siempre que las
modificaciones también se distribuyan bajo GPLv3.

Es software libre y gratuito.

No hay costes por:

● instalarlo
● usarlo
● modificarlo
● distribuirlo internamente
La empresa solo pagaría si contrata servicios opcionales (soporte, hosting, plugins de
pago, etc.), pero el software en sí es 100% gratuito.

¿QUÉ LIBERTADES OFRECE LA GPL V2 AL
TÉCNICO?
La GPL v2 da cuatro libertades fundamentales:

1. LIBERTAD DE USO
Puedes usar GLPI para cualquier propósito: empresa, educación, administración pública,
proyectos personales, etc.

2. LIBERTAD DE ESTUDIAR EL CÓDIGO
El técnico puede ver cómo está hecho GLPI, aprender de su código y entender su
funcionamiento interno.

3. LIBERTAD DE MODIFICARLO
Puedes adaptar GLPI a las necesidades de la empresa:

● crear plugins
● cambiar funciones
● personalizar pantallas
● integrar con otros sistemas
4. LIBERTAD DE DISTRIBUIRLO
Puedes compartir tu versión modificada con otros, siempre manteniendo la misma licencia
GPL v2.

TAREA 2: DISEÑO DEL ENTORNO
(STACK DE SOFTWARE)
GLPI es una aplicación web , por lo que no funciona como un .exe. Para ejecutarlo en
Windows 10/11 necesitas un entorno que proporcione:

● Servidor Web
● Lenguaje de programación (PHP)
● Base de Datos (MySQL/MariaDB)
● Y en nuestro caso un contenedor de Docker
Esto puede hacerse con XAMPP, WAMP, Laragon o mediante contenedores Docker.

COMPONENTES NECESARIOS PARA
GLPI
1. SERVIDOR WEB
GLPI puede funcionar con cualquiera de estos servidores web:

● Apache 2 o superior
● Nginx
● Lighttpd
● Microsoft IIS
2. LENGUAJE DE PROGRAMACIÓN (PHP)
GLPI está desarrollado en PHP , por lo que necesitas instalarlo junto con sus extensiones.

3. BASE DE DATOS
GLPI es compatible con:

● MariaDB
● MySQL
REQUISITOS MÍNIMOS DE LA
VERSIÓN ACTUAL DE GLPI (10.0.7 EN
ADELANTE)
Según la documentación oficial:

SERVIDOR WEB
● Apache 2+ , Nginx , Lighttpd o IIS
PHP
● PHP 8.1 o superior (GLPI 10.0.7+ requiere versiones modernas de PHP) (La
documentación no indica explícitamente la versión mínima en el fragmento consultado,
pero GLPI 10.x oficialmente exige PHP ≥ 8.1.)
BASE DE DATOS
● MARIADB 10.5+ O MYSQL EQUIVALENTE
(Derivado de los requisitos de GLPI 10.x y las configuraciones mostradas en
instalaciones reales como la de GLPI 11 beta, que usa MariaDB 11.)
TAREA 3: REQUISITOS DE
HARDWARE PARA GLPI EN
WINDOWS
GLPI es una aplicación web ligera, pero el rendimiento depende del servidor web , PHP y
la base de datos que instales (XAMPP, WAMP, Laragon o Docker).

Para evitar bloqueos en Windows 10/11, es necesario reservar recursos suficientes para que
el sistema operativo y GLPI trabajen sin competir.

Requisitos recomendados para un
entorno fluido
A continuación te dejo los valores realistas y seguros para un equipo de prácticas o un
entorno pequeño/mediano.

1. CPU (PROCESADOR)
✔ REQUISITO RECOMENDADO:
2 núcleos dedicados (o 2 hilos) para GLPI y su stack.

✔ EXPLICACIÓN:
● Apache/Nginx + PHP + MariaDB necesitan algo de concurrencia.
● Con 2 núcleos dedicados, el sistema no se congela cuando se ejecutan consultas o
inventarios.
2. MEMORIA RAM
✔ REQUISITO RECOMENDADO:
4 GB de RAM reservados para GLPI y su stack

(esto implica que el equipo debería tener 8 GB o más en total).

✔ DISTRIBUCIÓN APROXIMADA:
● Servidor web + PHP: 1 GB
● Base de datos (MariaDB/MySQL): 1.5–2 GB
● Sistema operativo y procesos de Windows: 3 – 4 GB
✔ POR QUÉ:
Si el sistema se queda sin RAM, Windows empieza a usar el disco como memoria virtual y
el equipo se vuelve lento o se bloquea.

3. ALMACENAMIENTO LIBRE
✔ REQUISITO RECOMENDADO:
20 – 30 GB libres para trabajar con comodidad.

✔ DETALLE:
● Instalación del stack (XAMPP/WAMP/Laragon): 1 – 2 GB
● Archivos de GLPI: 500 MB
● Base de datos (tickets, inventario, logs): 5 – 10 GB
● Espacio para copias de seguridad: 10 GB o más
● Docker
✔ NOTA:
Si activas inventario automático (FusionInventory o GLPI Agent), el tamaño de la base de
datos crece más rápido.

PASOS DE
INSTALACIÓN
Primero accedemos a la página oficial de GLPI y hacemos clic en descargar

Luego hacemos clic en la imagen de docker (official image)

Luego vamos a la página de Docker e instalamos el programa de contenedores

Luego volvemos a la imagen de docker en el git

Y copiamos el código de un bloc de notas

ESTE ES EL CÓDIGO :
name: glpi

services:

glpi:

image: "glpi/glpi:latest"

restart: "unless-stopped"

volumes:

Using a named volume avoids permission issues on host (automatically managed by Docker)
glpi_data:/var/glpi
For GLPI 10.x, uncomment the following line to create a volume for plugins fetched from the
marketplace.

- "./storage/glpi_marketplace:/var/www/glpi/marketplace/:rw"
env_file: .env # Pass environment variables from .env file to the container

depends_on:

db
ports:

"80:80"
db:

image: "mysql"

restart: "unless-stopped"

volumes:

db_data:/var/lib/mysql
environment:

MYSQL_RANDOM_ROOT_PASSWORD: "yes"

MYSQL_DATABASE: ${GLPI_DB_NAME}

MYSQL_USER: ${GLPI_DB_USER}

MYSQL_PASSWORD: ${GLPI_DB_PASSWORD}

volumes:

glpi_data:

db_data:

Debemos guardarlo con el extensión y el nombre siguiente = docker-compose.yml

Luego copiamos en otro archivo del bloc de notas el siguiente codigo y lo guardamos con la
extensión .env

GLPI_DB_HOST=db

GLPI_DB_PORT=

GLPI_DB_NAME=glpi

GLPI_DB_USER=glpi

GLPI_DB_PASSWORD=glpi

Luego debemos ejecutar este código en el cmd docker compose up -d

Nota aparecerá error si los archivos no tienen la extensiones correcta, si no está guardados
en formato todos los archivos

Debemos anotar los nombres de los dos contenedores

Luego usamos es comando para ver los datos del contenerdor ( anotar la password)

docker logs <db_container_id>

En nuestro caso sera esta :

La ANOTAMOS

Luego ejecutamos el siguiente código docker exec -it <db_container_id> mysql -u root -p -e
"GRANT SELECT ON mysql.time_zone_name TO 'glpi'@'%';FLUSH PRIVILEGES;"

Sustituimos los datos ( el nombre del contenedor y la contraseña)

Para finalizar actualizamos la zona horaria y listo

docker exec -it <glpi_container_id> /var/www/glpi/bin/console database:enable_timezones

Entramos al localhost y accedemos con el usuario = glpi y
contraseña = glpi
