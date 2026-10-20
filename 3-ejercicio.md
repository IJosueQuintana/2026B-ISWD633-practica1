## Esquema para el ejercicio
![Imagen](esquema-ejercicio3.PNG)

### Crear red net-wp
docker network create net-wp

### Para que persista la información es necesario conocer en dónde mysql almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio, la carpeta del contenedor (a) es `/var/lib/mysql`.

Ruta carpeta host: `C:/Users/quint/E.P.N/6. Sexto Semestre/CES/Actividades/ejercicio3/db`

### ¿Qué contiene la carpeta db del host?
Inicialmente, la carpeta db del host se encuentra vacía, debido a que todavía no se ha creado ni inicializado el contenedor MySQL. Esta carpeta se utilizará posteriormente para almacenar los archivos de la base de datos mediante un Bind Mount.

### Crear un contenedor con la imagen mysql:8  en la red net-wp, configurar las variables de entorno: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER y MYSQL_PASSWORD
docker run -d --name srv-mysql-wp --network net-wp -e MYSQL_ROOT_PASSWORD="RootDemo2026!" -e MYSQL_DATABASE=wordpress_db -e MYSQL_USER=wpuser -e MYSQL_PASSWORD="WpDemo2026!" -v "C:/Users/quint/E.P.N/6. Sexto Semestre/CES/Actividades/ejercicio3/db:/var/lib/mysql" mysql:8

### ¿Qué observa en la carpeta db que se encontraba inicialmente vacía?
Después de crear e inicializar el contenedor MySQL, se observa que la carpeta db del host contiene archivos y directorios generados automáticamente por el sistema gestor de bases de datos. Estos archivos almacenan información necesaria para su funcionamiento y las bases de datos creadas. Esto demuestra que el Bind Mount permite almacenar los datos del contenedor directamente en el sistema de archivos del host.

### Para que persista la información es necesario conocer en dónde wordpress almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio, la carpeta del contenedor (b) es `/var/www/html`.

Ruta carpeta host: `C:/Users/quint/E.P.N/6. Sexto Semestre/CES/Actividades/ejercicio3/www`.

### Crear un contenedor con la imagen wordpress en la red net-wp, configurar las variables de entorno WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD y WORDPRESS_DB_NAME (los valores de estas variables corresponden a los del contenedor creado previamente)
docker run -d --name srv-wordpress --network net-wp -p 9500:80 -e WORDPRESS_DB_HOST=srv-mysql-wp:3306 -e WORDPRESS_DB_USER=wpuser -e WORDPRESS_DB_PASSWORD="WpDemo2026!" -e WORDPRESS_DB_NAME=wordpress_db -v "C:/Users/quint/E.P.N/6. Sexto Semestre/CES/Actividades/ejercicio3/www:/var/www/html" wordpress

### Personalizar la apariencia de wordpress y agregar una entrada

### Eliminar el contenedor y crearlo nuevamente, ¿qué ha sucedido?

Al eliminar y recrear los contenedores de WordPress y MySQL utilizando los mismos Bind Mounts, se comprobó que la información almacenada en las carpetas del sistema anfitrión se conserva. Esto permite recuperar la configuración del sitio, los temas instalados, las publicaciones y los datos de los usuarios sin necesidad de realizar una nueva instalación de WordPress.

Por lo tanto, los Bind Mounts permiten mantener la persistencia de los datos independientemente de la eliminación y recreación de los contenedores Docker.
