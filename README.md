Solemne 1 v-5

En este archivo de texto se tiene el propósito de explicar el proceso que seguimos en Docker y en qué consistió nuestra actividad práctica.

La tarea consistía en desarrollar una aplicación web para una tienda de bicicletas, con los siguientes requerimientos:

- Visualizar el menú de productos
- Agregar productos a un carrito de compras simulado 
- Realizar un pago electrónico simulado
- La aplicación debe estar en Docker y publicada en GitHub

Inicio del Proyecto en Docker

Como primer paso, iniciamos la configuración del entorno utilizando PowerShell. Ejecutamos los siguientes comandos:

mkdir C:\Users\danie\sitio-bicicletas
cd C:\Users\danie\sitio-bicicletas

Con esto, creamos la carpeta base donde se almacenará todo el contenido de nuestro proyecto.

Posteriormente, procedimos a crear el archivo Dockerfile, que será fundamental para definir cómo se construye la imagen de Docker que contendrá nuestra aplicación. Para ello, ejecutamos los siguientes comandos:

New-Item -Path . -Name "DockerFile" -ItemType "File"
notepad Dockerfile

Una vez abierto el archivo Dockerfile en el Bloc de Notas, se procedió a ingresar las siguientes instrucciones:

# Usa la imagen oficial de Apache
FROM httpd:2.4

# Instala git
RUN apt-get update && apt-get install -y git

# Clona el repositorio con la página HTML
RUN rm -rf /usr/local/apache2/htdocs/*
RUN git clone https://github.com/DaniBOD/Solemne-1.git /usr/local/apache2/htdocs/

# Expone el puerto 80
EXPOSE 80

# Comando para iniciar Apache
CMD ["httpd-foreground"]

Construcción de la Imagen Docker

Con el Dockerfile ya preparado, se construyó la imagen de Docker ejecutando el siguiente comando en PowerShell, asegurándose de estar en el directorio del proyecto (C:\Users\danie\sitio-bicicletas):

docker build -t bicicletas-web .

Ejecución del Contenedor Docker

El siguiente paso fue ejecutar el contenedor a partir de la imagen recién creada. Para ello, se utilizó el siguiente comando:

docker run -d -p 8080:80 bicicletas-web

Visualización del Sitio en el Navegador

Finalmente, para comprobar que todo funciona correctamente, se abrió un navegador web y se ingresó la siguiente dirección:

http://localhost:8080
