# Documentación

![](https://filer.365.clarin.com/filer/materiales-salesforce/prod/201701/06/201701-06-165ca1fa-6859-4207-9b79-ca74eea05647.jpg)

**Índice**

* [1. Generando un ambiente de pruebas](#1.Generando un ambiente de pruebas)
	* [a. Software a instalar](#1a.Software a instalar)

---------------------------------------

<a name="1.Generando un ambiente de pruebas" />

## 1. Generando un ambiente de pruebas

Para instalar un ambiente de pruebas en un servidor desde cero, es recomendable tener los siguientes puntos en cuenta:

- Es necesario tener permisos de administrador local sobre el servidor
- Los sistemas web deben testearse en todos los navegadores que puedan utilizarlos.
- Para el desarrollo web es recomendable actualizar la última versión de .NET framework
- Para el desarrollo web es recomendable utilizar una versión del IIS 7+
- El servidor debe tener al menos 30 gb de espacio

<a name="1a.Software a instalar" />

### 1 a. Software a instalar

**Browsers/Navegadores**

- Chrome
	- https://www.google.com/chrome/
- Firefox
	- https://www.mozilla.org/es-AR/firefox/new/
- Edge
	- https://www.microsoft.com/es-ar/windows/microsoft-edge
- Opera (no siempre es necesario)
	- https://www.opera.com/es/download

Agregados:
- AdBlock
	- https://chrome.google.com/webstore/detail/adblock/gighmmpiobklfepjocnamgkkbiglidom?hl=es-419

**Servicios web**

- IIS v7+
	- https://www.microsoft.com/es-ar/download/details.aspx?id=2299
- XAMPP
	- https://www.apachefriends.org/es/download.html
- Node js
	- https://nodejs.org/en/download/

Agregados:
- Web platform installer
	- https://www.microsoft.com/web/downloads/platform.aspx

**Git/Repositorios**

- GIT Bash
	- https://git-scm.com/download/win
- Tortoise GIT
	- https://tortoisegit.org/download/

### 1 b. Configuración de software

#### IIS

1. El IIS se encuentra ya instalado en el equipo, pero hay que indicarle al sistema que el usuario conectado pueda visualizarlo.
2. Ingresar a **Panel de control**
3. Ingresar a **Activar o desactivar características de Windows**
4. Marcar todos los items dentro del apartado  **Internet Information Services**, salvo por **Servidor FTP**
5. Aceptar

#### XAMPP

1. Instalar XAMPP. Descargarlo desde la siguiente URL, cualquiera de los clientes es útil debido a que sólo es necesaria la configuración de un servidor Apache, tarea básica de XAMPP

    https://www.apachefriends.org/download.html

2. Una vez instalado, abrir la configuración de apache **httpd.config** y buscar la linea que dice **Listen 80**, suele estar por la parte de arriba. Cambiarla a otro puerto disponible, por ejemplo **Listen 8085**. El puerto 80 suele ser utilizado por el IIS u otros servicios.

3. Una vez cambiado el puerto, creamos una nueva carpeta en el directorio **C:\xampp\htdocs** llamada **TEST_Client**.

4. Copiar los archivos de este repositorio dentro de la carpeta.

5. Poner en funcionamiento el servidor apache desde el panel de control de XAMPP.

6. Abrir http://localhost:<<puerto>>/TEST_Client/

    en el caso del ejemplo, sería http://localhost:8085/TEST_Client/

7. Si aparece el sitio, ya se encuentra en funcionamiento.

    Los archivos y carpetas se generan en la carpeta **C:\xampp\htdocs\UKAng_Client\files**.

#### Node JS

El **Node Js**, al igual que el **IIS**, **es un servidor local para publicar sitios** y servicios web, por lo que ambos pueden ser utilizados sin necesidad del otro.

Sin embargo algunas aplicaciones web utilizan **Node** y requieren sí o sí ser publicadas en este tipo de servidor. 

Una vez instalado, **Node** ofrece, entre otras cosas, la posibilidad de configurar un archivo llamado **package.json** que obtendrá todas las librerías que utiliza el sitio/servicio mediante simples comandos.

1. Ubicar en el servidor una carpeta especifica para las aplicaciones que utilizarán **Node** como servidor local, por ejemplo **C:/Node_Apps/...**
2. En esta carpeta se ingresarán todos los sitios y/o servicios en forma de distintas carpetas. Por ejemplo, si tenemos el servicio **Test**, será ubicado como **C:/Node_Apps/Test/...**
3. Una vez ubicada la carpeta en cuestion, presionar la tecla **shift** y **hacer click derecho** sobre la misma.
4. Seleccionar **Abrir ventana de comandos aquí**
5. Escribir el comando **npm install** y presionar **enter**
6. Una vez que se hayan instalado todos los paquetes, escribir el comando **npm start** y presionar enter.
7. Si no hubo error, **Node ya tendrá publicado el sitio correspondiente**, en el puerto en el que fue configurado desde el código.
8. Si hubo error, volver a correr el comando **npm install**
9. Para ingresar al sitio o servicio, en el ejemplo dado sería mediante **la siguiente** **url: http://localhost:<<puerto>>/Test/...**