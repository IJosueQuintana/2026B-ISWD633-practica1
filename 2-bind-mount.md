# BIND MOUNT
En un bind mount mapeamos (montar) un directorio o archivo específico del sistema de archivos del host con una parte del sistema de ficheros del contenedor.

```
docker run -d --name <nombre contenedor> -v <ruta carpeta host>:<ruta carpeta contenedor> <imagen> 
```
ó
```
docker run -d --name <nombre contenedor> --mount type=bind,source=<ruta carpeta host>,target=<ruta carpeta contenedor> <imagen>
```
- destination, dst, target: La ruta donde se monta el archivo o directorio en el contenedor.
- source, src: El origen del montaje.
  
### En tu computador crear una carpeta llamada nginx y dentro de esta carpeta crea otra llamada html. Como se aprecia en la figura.
![Volúmenes](directorio.PNG)

### Crear un contenedor con la imagen nginx:alpine, mapear todos por puertos, para la ruta carpeta host colocar el directorio en donde se encuentra la carpeta html en tu computador y para la ruta carpeta contenedor: /usr/share/nginx/html (esta ruta se obtiene al revisar la documentación de la imagen)
![Volúmenes](volumen-host.PNG)
docker run -d --name srvnginx -P -v "C:/Users/quint/E.P.N/6. Sexto Semestre/CES/Actividades/nginx/html:/usr/share/nginx/html" nginx:alpine

### ¿Qué sucede al ingresar al servidor de nginx?
Al ingresar al servidor Nginx se muestra el error 403 Forbidden, debido a que la carpeta html del host se encuentra vacía. Al utilizar un bind mount, el directorio del host se monta sobre /usr/share/nginx/html, ocultando los archivos predeterminados del contenedor, incluido index.html. Por esta razón, Nginx no encuentra una página principal para mostrar.

### ¿Qué pasa con el archivo index.html del contenedor?
El archivo index.html predeterminado de Nginx queda oculto al realizar el bind mount, ya que el contenido de la carpeta html del host se monta sobre el directorio /usr/share/nginx/html del contenedor. El archivo original no se elimina, pero no puede visualizarse mientras el montaje esté activo.

### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de tu computador en la carpeta html
### ¿Qué sucede al ingresar al servidor de nginx?
Al ingresar nuevamente al servidor Nginx, se visualiza correctamente la plantilla HTML descargada, reemplazando el error 403 Forbidden que aparecía anteriormente. Esto sucede porque, mediante el Bind Mount, el contenedor accede directamente a los archivos almacenados en la carpeta html del host, permitiendo mostrar la página web sin necesidad de reiniciar el contenedor.

### Eliminar el contenedor
docker rm -f srvnginx

### ¿Qué sucede al crear nuevamente un contenedor montado al directorio definidos anteriormente?
Al crear nuevamente el contenedor utilizando el mismo Bind Mount, la página web continúa funcionando y muestra la plantilla HTML previamente descargada, ya que los archivos permanecen almacenados en el directorio del host.

Además, Docker asignó automáticamente un nuevo puerto, cambiando de 32768 a 32769, debido al uso del parámetro -P. Esto demuestra que los datos almacenados mediante un Bind Mount permanecen disponibles incluso después de eliminar y recrear el contenedor.


