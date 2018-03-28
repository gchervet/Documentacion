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

**Desarrollo**

Sólo si se quiere agregar desarrollo desde el ambiente de testeo.

- VS Code:
	- https://code.visualstudio.com/download

### 1 b. Configuración de software

1. Instalar XAMPP. Descargarlo desde la siguiente URL, cualquiera de los clientes es útil debido a que sólo es necesaria la configuración de un servidor Apache, tarea básica de XAMPP

    https://www.apachefriends.org/download.html

2. Una vez instalado, abrir la configuración de apache **httpd.config** y buscar la linea que dice **Listen 80**, suele estar por la parte de arriba. Cambiarla a otro puerto disponible, por ejemplo **Listen 8085**.

3. Una vez cambiado el puerto, creamos una nueva carpeta en el directorio **C:\xampp\htdocs** llamada **TEST_Client**.

4. Copiar los archivos de este repositorio dentro de la carpeta.

5. Poner en funcionamiento el servidor apache desde el panel de control de XAMPP.

6. Abrir http://localhost:<<puerto>>/TEST_Client/

    en el caso del ejemplo, sería http://localhost:8085/TEST_Client/

7. Si aparece el sitio, ya se encuentra en funcionamiento.

    Los archivos y carpetas se generan en la carpeta **C:\xampp\htdocs\UKAng_Client\files**.