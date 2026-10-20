# COMPLETAR  
Comparando sus conocimientos antes de hacer la práctica con sus conocimientos después de hacer la tarea, explicar los principales aprendizajes logrados para beneficio de su formación profesional.  
Si solucionó un problema presentado o utilizó otros comandos que no se mencionan al realizar la práctica también se debe documentar.


## Aprendizajes logrados

Antes de realizar esta práctica, tenía conocimientos básicos sobre Docker, principalmente relacionados con la creación y ejecución de contenedores. Sin embargo, no comprendía completamente cómo gestionar la persistencia de los datos, cómo se comunicaban los contenedores entre sí ni las diferencias entre los tipos de volúmenes.

Durante el desarrollo de la práctica, aprendí a utilizar tres mecanismos de almacenamiento: Bind Mounts, volúmenes nombrados y volúmenes anónimos. Comprendí que los Bind Mounts permiten vincular directorios del sistema anfitrión con los contenedores, mientras que los volúmenes nombrados son administrados directamente por Docker. Por otro lado, los volúmenes anónimos se generan automáticamente sin necesidad de asignarles un nombre.

Uno de los aprendizajes más importantes fue comprobar la persistencia de los datos mediante la implementación de WordPress y MySQL. Al eliminar y recrear los contenedores utilizando las mismas carpetas del sistema anfitrión, pude verificar que las publicaciones, configuraciones y archivos se conservaban.

También aprendí a crear redes de tipo bridge para permitir la comunicación entre contenedores. Esto lo apliqué al conectar WordPress con MySQL y posteriormente Drupal y pgAdmin con PostgreSQL. Comprendí que los contenedores pueden comunicarse utilizando sus nombres dentro de una misma red Docker, sin necesidad de publicar todos sus puertos en el equipo anfitrión.

Estos conocimientos son importantes para mi formación como ingeniero de software, porque permiten implementar aplicaciones con múltiples servicios, administrar su almacenamiento y comprender cómo funcionan los entornos de desarrollo basados en contenedores.

## Problemas presentados y soluciones aplicadas

Durante la práctica se presentaron algunos inconvenientes que permitieron reforzar mis conocimientos sobre Docker y la resolución de problemas.

**1. Error al inicializar MySQL**

Al crear el contenedor de MySQL, este se detenía debido a que el directorio utilizado para almacenar sus datos contenía una carpeta adicional llamada `www`. Mediante la revisión de los registros del contenedor, identifiqué que MySQL necesitaba un directorio adecuado para inicializar su base de datos.

Para solucionarlo, revisé la estructura de carpetas en Windows, corregí su ubicación y volví a crear el contenedor.

Comandos utilizados:

```powershell
docker logs srv-mysql-wp
docker ps -a
docker rm srv-mysql-wp
```

**2. Problema con el correo electrónico de pgAdmin**

Al crear el contenedor de pgAdmin, inicialmente ejecuté el comando sin reemplazar el campo `<correo>` por una dirección válida. Para corregirlo, eliminé el contenedor y lo creé nuevamente con un correo de prueba.

Comando adicional utilizado:

```powershell
docker rm -f client-postgres
```

**3. Problema de acceso a pgAdmin desde el navegador**

Aunque el contenedor de pgAdmin aparecía en ejecución, inicialmente no podía acceder a su interfaz web mediante el navegador. Para diagnosticar el problema, revisé los registros y comprobé la conectividad del puerto 9500.

Comandos utilizados:

```powershell
docker logs --tail 40 client-postgres
Test-NetConnection 127.0.0.1 -Port 9500
curl.exe -I http://127.0.0.1:9500
```

Los resultados confirmaron que el puerto estaba disponible y que pgAdmin respondía correctamente mediante una redirección HTTP 302 hacia su pantalla de inicio de sesión. Finalmente, pude ingresar utilizando la dirección `http://127.0.0.1:9500/login`.

## Conclusión

Esta práctica me permitió pasar de conocer los comandos básicos de Docker a comprender su aplicación en escenarios que involucran varios servicios, redes y mecanismos de almacenamiento. Además, aprendí a utilizar los registros y herramientas de diagnóstico para identificar y solucionar errores.

Considero que estos aprendizajes serán útiles en mi formación profesional, especialmente para desarrollar, desplegar y mantener aplicaciones que requieran bases de datos, servidores web y persistencia de información.
