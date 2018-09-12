# Documentación

![](https://raw.githubusercontent.com/gchervet/Documentacion/master/images/kennedy_logo.jpg)

**Índice**

* [1. Generando un ambiente de pruebas](#1.GenerandoUnAmbienteDePruebas)
	* [a. Software a instalar](#1a.SoftwareAInstalar)
	* [b. Configuración de software](#1b.ConfiguracionSoftware)
* [2. Apuntes sobre SQL y Base de datos](#2.ApuntesSobreSQLyBDD)
	* [a. Invocar un Web service desde una SQL Stored procedure](#2a.InvocarWebServiceDesdeSQLSP)
	* [b. Generar un iterador con CURSOR](#2b.generarCURSOR)
* [3. Apuntes sobre Desarrollo](#3.ApuntesSobreDesarrollo)
	* [a. Json Web Token](#3a.JWT)
	* [b. Promesas en Javascript](#3b.PromesasJavascript)
	* [c. Manejo de notificaciones](#3c.ManejoNotificaciones)
	* [d. Autenticación LDAP/AD](#3d.AutenticacionAD)
	* [e. Manejo de Modals](#3e.ManejoModals)
	* [f. Convertir un JSON a clases .CS](#3f.ConvertirJSONaCS)
	* [g. Generar una solución .exe y asignarla a una tarea de Windows](#3g.ExeAUnaTareaWindows)	
	* [h. Manejo de Librería JSPDF](#3h.jspdf)
* [4. Resolución de problemas - Web Config](#4.ResolucionProblemas_WebConfig)
	* [a. Los métodos devuelven 404 en el servidor pero funcionan localmente](#4a.Metodos404Servidor)
	* [b. La seguridad integrada en el connection string no puede ser suplida, y no deja ingresar a la base](#4b.ConnectionStringSeguridadNoSuplida)
	* [c. Desactivar autenticación obligatoria](#4c.DesactivarAutenticacion)
	* [d. Desactivar caché en todas las llamadas](#4d.DesactivarCache)
	* [e. Habilitar CORS para el ingreso desde cualquier URL](#4e.HabilitarCORS)
	* [f. Error 401.0](#4f.Error401.0)
	* [g. Error 404.8](#4g.Error404.8)
	* [h. Custom errors mode Off](#4h.CustomErrorsOff)
* [5. Resolución de problemas - Node JS](#5.ResolucionProblemas_NodeJS)
	* [a. Can't set headers after they are sent](#5a.CantSetHeaders)
* [6. Apuntes varios](#6.ApuntesVarios)
	* [a. Buscar procesos INET Service](#6a.BuscarProcesosINETService)
* [7. Apuntes de PHP](#7ApuntesPHP)
	* [a. Debuggear PHP con XAMPP](#7DEBUGPHPXAMPP)
	* [b. CORS con PHP](#7CORS)
	
---------------------------------------

<a name="1.GenerandoUnAmbienteDePruebas" />

# 1. Generando un ambiente de pruebas

Para instalar un ambiente de pruebas en un servidor desde cero, es recomendable tener los siguientes puntos en cuenta:

- Es necesario tener permisos de administrador local sobre el servidor
- Los sistemas web deben testearse en todos los navegadores que puedan utilizarlos.
- Para el desarrollo web es recomendable actualizar la última versión de .NET framework
- Para el desarrollo web es recomendable utilizar una versión del IIS 7+
- El servidor debe tener al menos 30 gb de espacio

<a name="1a.SoftwareAInstalar" />

## 1 a. Software a instalar

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

<a name="1b.ConfiguracionSoftware" />
	
## 1 b. Configuración de software

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

Nota

	Para que se publiquen los sitios de XAMPP hay que abrir el XAMPP Control panel y hacer click en **start** sobre el servidor apache.

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

Nota: 

	En algunos casos, en vez de correr npm start, es necesario correr node app. Estos casos se dan cuando la configuración del servidor se encuentra en el archivo app.js
	Si el archivo de configuración tiene otro nombre (no app.js), correr el comando node <<nombre.js>>.
	
	Los elementos que aparezcan en consola se mostrarán en el cmd donde se publicó el servicio.

<a name="2.ApuntesSobreSQLyBDD" />

# 2. Apuntes sobre SQL y Base de datos

<a name="2a.InvocarWebServiceDesdeSQLSP" />

## a. Invocar un Web Service desde una SQL Stored Procedure

Es necesario activar ciertas funciones en la BDD mediante este código

```sql
sp_configure 'show advanced options', 1 

GO 
RECONFIGURE WITH OVERRIDE; 
GO 
sp_configure 'Ole Automation Procedures', 1 
GO 
RECONFIGURE WITH OVERRIDE; 
GO 
sp_configure 'show advanced options', 1 
GO 
RECONFIGURE WITH OVERRIDE;
```

Luego realizamos la SP:

```sql
CREATE PROCEDURE [dbo].[sp_CallWebServices]
@param varchar(100) = NULL

AS

	DECLARE @obj INT
	DECLARE @return INT
	DECLARE @sUrl VARCHAR(200)
	DECLARE @response VARCHAR(8000)
	DECLARE @hr INT
	DECLARE @src VARCHAR(255)
	DECLARE @desc VARCHAR(255)

	SET @sUrl = 'http://10.9.0.112:9000/api/test' -- WEB SERVICE URL

	EXEC sp_OACreate 'MSXML2.ServerXMLHttp', @obj OUT
	EXEC sp_OAMethod @obj, 'Open', NULL, 'GET', @sUrl, false
	EXEC sp_OAMethod @obj, 'send'
	EXEC sp_OAGetProperty @obj, 'responseText', @response OUT

	SELECT @response [response]
	EXEC sp_OADestroy

RETURN
```
De esta forma se puede ejecutar la SP de la siguiente manera:

```sql
EXEC sp_CallWebServices 'parametro'
```

Nota importante:

	SQL no entiende quién es localhost. 
	Si se quiere llamar a un servicio local, suplantar localhost con la IP del equipo 
	(aunque sea el mismo propio). 

Otra forma de SP:

```sql
Declare @Object as Int;
Declare @ResponseText as Varchar(8000);
 
--Code Snippet
Exec sp_OACreate 'MSXML2.XMLHTTP', @Object OUT;
Exec sp_OAMethod @Object, 'open', NULL, 'get',
'http://10.9.0.112:9000/api/test', -- WEB SERVICE URL
'false'
Exec sp_OAMethod @Object, 'send'
Exec sp_OAMethod @Object, 'responseText', @ResponseText OUTPUT
 
Select @ResponseText
 
Exec sp_OADestroy @Object

```

<a name="2b.generarCURSOR" />

## b. Generar un iterador con CURSOR

SQL puede generar una iteración mediante el instructivo **CUSOR**, aplicándolo a un SELECT, de la siguiente manera:

```sql
DECLARE @valorInt int

DECLARE mi_cursor CURSOR  
	FOR select DISTINCT valorInt from Tabla  
OPEN mi_cursor  

FETCH NEXT FROM mi_cursor
INTO @valorInt

WHILE @@FETCH_STATUS = 0  
BEGIN  

	PRINT ' ' + @valorInt
	FETCH NEXT FROM mi_cursor
	INTO @valorInt

END   
CLOSE mi_cursor;  
DEALLOCATE mi_cursor; 
```

Primero se debe declarar las variables que nos darán el select:

```sql
DECLARE @valorInt int
```

Luego declaramos el cursor y lo iniciamos con **OPEN**:

```sql
DECLARE mi_cursor CURSOR  
	FOR select DISTINCT EnrollmentId from Tabla  
OPEN mi_cursor  
```

Mediante **FETCH** obtenemos el primer valor del ciclo:
```sql
FETCH NEXT FROM mi_cursor
INTO @valorInt
```

Con un **WHILE @@FETCH_STATUS=0** recorremos el ciclo en su enteridad, cuando termine el ciclo, se cierra el cursor:
```sql
WHILE @@FETCH_STATUS = 0  
BEGIN  

	-- INTERIOR DEL CICLO

END   
CLOSE mi_cursor;  
DEALLOCATE mi_cursor; 
```

Y no olvidar obtener el siguiente valor mediante un **FETCH**:
```sql
PRINT ' ' + @valorInt
FETCH NEXT FROM mi_cursor
INTO @valorInt
```

<a name="3.ApuntesSobreDesarrollo" />

# 3. Apuntes sobre Desarrollo

<a name="3a.JWT" />

## a. Json Web Token

Librería tomada del siguiente link: https://github.com/auth0/node-jsonwebtoken

Para instalar el package mediante Node:

	npm install jsonwebtoken

Para utilizar el package desde un service js:

```js
var JWT = require('jsonwebtoken');
```

Para generar un nuevo token:

```js
var token = JWT.sign(user, process.env.SECRET_KEY, {
	expiresIn: 9999
});
```

Donde

	user es el JSON que solicita JWT para la creación de un token por usuario, como mínimo se esperan "username":"username" y "password":"password"
	process.env.SECRET_KEY es la string secreta encargada de encriptar el token
	expiresIn es el valor en segundos de expiración.

<a name="3b.PromesasJavascript" />

## b. Promesas en Javascript

Las promesas son llamadas asincrónicas a un servicio web que, al dar una respuesta, activan un evento de finalización para realizar un proceso a partir del mismo.

Este evento se llama **.then()**, y es muy útil a la hora de esperar a una respuesta del servicio.

Una buena forma de utilizar las promesas es al momento de generar un servicio javascript.

Imaginemos que tenemos un servicio llamado utilityService.js el cual tiene la siguiente estructura:

```js
angular.module("app")
    .factory('utilityService', ['$http', '$rootScope',
function utilityService($http, $rootScope, $uibModal) {

	var service = {
        metodo1: metodo1,
        metodo2: metodo2,
        metodo3: metodo3
    };

    return service;

}]);
```

En este caso, tenemos un servicio básico que devuelve tres métodos llamados 1, 2, y 3.

Lo que vamos a hacer es transformar alguno de estos métodos en una promesa, para que cualquier componente angular/controlador que implemente a utilityService pueda utilizarlo mediante el comando **then**.

Por ejemplo, el método 1 puede ser el siguiente:

```js

	...

	return service;

	function metodo1(){

        return new Promise(function(resolve, reject){
            
			resolve("has alcanzado al método 1");
            
        })  
    }
	
}]);
```

De esta forma, podemos llamar al método 1 desde un controlador de la siguiente forma:

```js
angular.module("app").controller('exampleController',
function ($scope, $rootScope, utilityService) {

	utilityService.metodo1().then(function(response){
	
		console.log(response);
	
	});

}]);
```

En este caso, primero referenciamos a utilityService en la declaración del controlador, y luego utilizamos uno de sus métodos, en este caso el **metodo1**.

Al pedir la devolución de metodo1 indicándole el **then**, cuando el método 1 corra la línea **resolve(...)**, devolverá una respuesta que será capturada por el then.

Una vez obtenida la respuesta, se loguea en consola cuál fue la misma.


<a name="3c.ManejoNotificaciones" />	

## Manejo de Notificaciones

El manejo de notificaciones se da mediante la libreria **socket.io**. Esta librería funciona como enlace a tiempo real para captar notificaciones y triggers. Utiliza tecnología **web socket**.

Los archivos importantes son 

	- app/shared/services/notificationServices.js 
	- app/shared/services/socket.js

Tener en cuenta lo siguiente:

	- Para poder usar estos servicios en un controller, hay que asignarlos a los parámetros, ver por ejemplo app/components/main/headerController.js.
		
		- .controller('headerController', function ($scope, $rootScope, $location, $sessionStorage, utilityService, Auth, socket, notificationService) {
		
	- Cualquier tipo de notificación debe ir con una variable options para enviar todos los datos de la misma.

### Notificaciones.1 Generar una nueva notificación

Para generar una nueva notificación, es necesario tener un objeto de **notificationService** y de **socket** en el controlador.

Una vez que los objetos estén referenciados, con estas líneas es posible generar una nueva notificación:

```js	
$scope.sendMessage = function () {
	notificationService.emit('show:notification', {
		message: $scope.message
	});
};
```

La clave de este codigo está en la linea que dice **notificationService.emit('show:notification', {**, donde:

	- notificationService es nuestro objeto del servicio de notificaciones
	- emit es el método que levanta un llamado web socket (librería socket.io)
	- 'show:notification' es el código de evento que vamos a levantar, este código se espera en un callback de web socket
	- message es el objeto de mensaje que vamos a enviar al callback
	
El callback del web socket se encuentra en **notificationService** y es el siguiente:

```js
socket.on('show:notification', function (message) {     
	showNotification();        
});
```

Donde 

	- on es el método del servicio web socket que obtiene el evento levantado.
	- 'show:notification' es el código del evento levantado que vamos a capturar.
	- message es el objeto de mensaje que llega desde el evento
	- el interior es la función a implementar cuando se levanta el callback. En este caso llama a showNotification();

### Notificaciones.2 Generar una nueva notificación alternativa

Si lo que se quiere es realizar una nueva notificación, va a ser necesario generar el método socket.on en notificationService de la siguiente forma:

```js
socket.on('CUSTOM:NOTIFICATION', function (objeto) {     
	. . .
});
```
	
Y para llamar a dicha notificación desde un controlador, el mismo deberá obtener **socket** y **notificationService**, llamando al callback de esta forma:

```js	
notificationService.emit('CUSTOM:NOTIFICATION', {
	objeto: {}
});
```

<a name="3d.AutenticacionAD" />	

## Autenticación

La autenticación se maneja mediante Active Directory, utilizando la librería node **activedirectory DEL SERVICIO**

	https://github.com/gheeres/node-activedirectory
	
Ver 

	app/components/service/configuration/session-service.js
	
En dicho archivo se encuentra la configuración LDAP para ingresar al AD del servidor.

Tener en cuenta el JSON de configuración **config**

La llamada para autenticar un usuario es la siguiente:

**POST**

http://<<SERVICE>>/api/authenticate

```json
{
	"username":"usuario@kennedy.edu.ar",
	"password":"password"
}
```


<a name="3e.ManejoModals" />

## Manejo de Modals (popups)

El manejo de modal se da mediante la libreria ui.bootstrap, perteneciente a Angular.

	Tomar de ejemplo base el template html de modal ubicado en **app/components/gestionDeTramites/modal/modalDetalleDeTramite.html**

Tener en cuenta lo siguiente:

	- Cada modal que se realice será un .html separado.
	- La ubicación de los modal será definida por la carpeta app/components/<<componente>>/modal
	- Todos los modal comparten un controlador en comun, **app/components/modal/ModalInstanceCtrl.js**, solicitado por index.html
	- Este controlador puede, además, tener extras dependiendo de las necesidades de cada modal en particular (ver Modal.4.)

### Modal.1. Realizar un template de modal

La ubicación de los template se define en la carpeta **app/components/<<componente>>/modal**, por ejemplo, el componente **home** tendría un modal en **app/components/home/modal/modalDeHome.html**.

De esta forma, el HTML interno de un modal será basicamente el siguiente:


```html
<div class="modal-header">
	<h3 class="modal-title">Título del Modal</h3>
</div>
<div class="modal-body">

	{{variableAngular}}
	...Contenido del modal...
	
</div>
<div class="modal-footer">
	<button class="btn btn-primary" type="button" ng-click="ok()">OK</button>
</div>
```
	
Este template podrá utilizar variables de angular, siempre y cuando estas pertenzcan a $scope, en el controlador.

### Modal.2. Invocar a un modal

Los modal serán invocados desde los distintos controladores en cada componente.

Para invocar a un popup, se debe usar la siguiente sintaxis:

```js
.controller('gestionarUnTramiteController', function ($scope, $uibModal) {
	
	var modalInstance = $uibModal.open({
		animation: $scope.animationsEnabled,
		templateUrl: 'app/components/<<componente>>/modal/<<modal>>.html',
		controller: 'ModalInstanceCtrl'
	});
	
};
```

Donde 

	- El controlador del componente debe recibir como mínimo a **$scope** y **$uibModal**
	- **ModalInstanceCtrl** es el controlador general para todos los modal
	- **animation** es un valor fijo
	- **templateUrl** debe ser la ruta física desde app/components/<<componente>>/modal/<<modal>>.html

De esta forma estaríamos invocando al modal ubicado en el valor dado en **templateUrl**, dándole el controlador general.

Dicho controlador general, **ModalInstanceCtrl**, tiene los valores mínimos y necesarios para que los componentes dentro del modal funcionen:

```js
angular.module('app')
.controller('ModalInstanceCtrl', function ($scope, $uibModalInstance, data) {
	
	$scope.modalInternalData = data;    
	$scope.ok = function() {        
		$uibModalInstance.dismiss('cancel');
	};

	$scope.cancel = function() {
		$uibModalInstance.dismiss('cancel');
	};

});
```

### Modal.3. Darle valores internos al Modal

El controlador general de modal, **ModalInstanceCtrl**, tiene un valor que maneja los datos internos que son traspasados desde un componente a un modal.

De esta forma los modal pueden recibir parametros mediante su invocación y aplicarlos al $scope, para poder utilizarlos.

Para ello existe la variable **data**, recibida en el controlador **ModalInstanceCtrl**. Esta variable es luego asignada al $scope del modal, de modo que el modal podra usar **{{modalInternalData}}** como una variable de angular.

Para enviar un valor interno al modal, hay que agregarlo al objeto de su invocación de la siguiente manera:

```js
var modalInstance = $uibModal.open({
	animation: $scope.animationsEnabled,
	templateUrl: 'app/components/<<componente>>/modal/<<modal>>.html',
	controller: 'ModalInstanceCtrl',
	
	resolve: {
		data: function () {
			return <<controller>>.<<variable>>;
		} 
	}
});
```

Donde *resolve* envía como parámetro **data** (que luego es el que recibe el modal en su firma). Esta variable retornada puede ser de cualquier tipo.

### Modal.4. Agregar nuevas funciones al controlador general de modal

El controlador general de modal, **ModalInstanceCtrl**, puede tener extras agregados, dependiendo de las necesidades de los distintos componentes que llamarán a los modal.

De esta forma, cada agregado se dará en el mismo archivo controlador de cada componente que necesite dicho extra.

Por ejemplo, si el componente **menu** necesita un agregado en modal, como un método, lo hará en el mismo **homeController.html**:

```js
angular.module('app')
.controller('homeController', function ($scope, $rootScope, $location, $sessionStorage, utilityService, Auth) {

	...

})
.controller('ModalInstanceCtrl', function ($scope, $uibModalInstance, data) {

	$scope.NuevoMetodo = function (){};
	
});
```

<a name="3f.ConvertirJSONaCS" />

## f. Convertir JSON a clases CS

Visual Studio tiene una opción de pegado especial para convertir estructuras JSON en clases .CS

1. Por ejemplo, teniendo el siguiente JSON:


```json
{
    "entries": {
        "entry": [
            {
                "attempt": 1,
                "enrollmentId": 1321321,
                "points_possible": 321321,
                "grade": 321321,
                "activity_name": "ASDADSA",
                "graded_at": "2017-11-20T19:11:04.122-05:00",
                "submitted_at": "2017-11-20T19:11:04.048-05:00"
            }
        ]
    }
}
```

2. Se copia el mismo, y en VS generamos un nuevo archivo .CS
3. Ya dentro del mismo archivo, en VS seleccionamos *edit -> paste special -> json as classes*

En este caso, nos generaria lo siguiente:

```c#
public class ClaseInicial_NombrarAGusto
{
	public Entries entries { get; set; }
}

public class Entries
{
	public Entry[] entry { get; set; }
}

public class Entry
{
	public int attempt { get; set; }
	public int enrollmentId { get; set; }
	public int? points_possible { get; set; }
	public float grade { get; set; }
	public string activity_name { get; set; }
	public DateTime graded_at { get; set; }
	public DateTime? submitted_at { get; set; }
}
```

<a name="3h.jspdf" />

## h. Manejo de JSPDF

Para probar la librería de forma online:

	https://parall.ax/products/jspdf


```js
var imgData = 'data:image/png;base64,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'
var doc = new jsPDF('p', 'mm', [297, 210])

var alumnoRegularPDFText = 'Conste por la presente que la /el Sra./ Sr. MATÍAS ARIEL PORTA, que acredita su identidad con DNI N° 37375737 y a quien le corresponde el legajo Nº 123123, es alumna/o regular de 1° año de ODONTOLOGÍA en esta Universidad, estando matriculada/o para el ciclo lectivo 2017.\n\nSe extiende la presente a solicitud de la /el interesada/o, para ser presentado ante las autoridades que correspondan al 12 día del mes de septiembre del año 2017.';
var splitTitle = doc.splitTextToSize(alumnoRegularPDFText, 230);

doc.setFontSize(16)
doc.text(10, 55, 'Constancia de Alumno Regular')
doc.setFontSize(12)
doc.addImage(imgData, 'JPEG', 10, 10, 70, 20)
//                            x    y   w   h
doc.text(10, 75, splitTitle)
//       x    y
```


<a name="4.ResolucionProblemas_WebConfig" />

# 4. Resolución de problemas - Web Config

<a name="4a.Metodos404Servidor" />

## a. Los métodos devuelven 404 en el servidor pero funcionan localmente

Tener en cuenta que en el servidor debería estar **instalada la versión de ASP.NET framework 4 y superior**.

- Agregar estas líneas al web.config de la app. Dentro de **<system.webserver>**

```xml
<modules runAllManagedModulesForAllRequests="true" >
  <remove name="FormsAuthentication"/>
</modules>
```

- Chequear en cada aplicación que el Framework sea el correcto. Si la aplicación sigue tirando errores de framework, cambiar los siguientes valores:

```xml
<system.web>
	<authentication mode="None"/>
	<compilation targetFramework="4.5" />
	<httpRuntime targetFramework="4.5" maxRequestLength="2147483647" executionTimeout="3000" />	
	<customErrors mode="Off"/>
</system.web>
```

- Por los siguientes:

```xml
  <system.web>
    <authentication mode="None"/>
    <compilation targetFramework="4.0" />
    <httpRuntime targetFramework="4.0" maxRequestLength="2147483647" executionTimeout="3000" />	
    <customErrors mode="Off"/>
  </system.web>
```

Notar el cambio en los decimales del valor de **targetFramework**.

<a name="4b.ConnectionStringSeguridadNoSuplida" />

## b. La seguridad integrada en el connection string no puede ser suplida, y no deja ingresar a la base.

**Esta resolución NO es definitiva, sólo sirve para realizar un workaround temporal.**

Sólo en casos de necesidad, se puede superar la seguridad integrada del connection string cambiando lo siguiente:

```xml
<connectionStrings>
	<add name="Uni_Entities" connectionString="metadata=res://*/Uni_Model.csdl|res://*/Uni_Model.ssdl|res://*/Uni_Model.msl;provider=System.Data.SqlClient;provider connection string=&quot;data source=SVRSQL01;initial catalog=prod_Uni;integrated security=True;Connect Timeout=300;MultipleActiveResultSets=True;App=EntityFramework&quot;" providerName="System.Data.EntityClient" />
</connectionStrings>
```

Por esto:

```xml
<add name="Uni_Entities" connectionString="metadata=res://*/Uni_Model.csdl|res://*/Uni_Model.ssdl|res://*/Uni_Model.msl;provider=System.Data.SqlClient;provider connection string=&quot;data source=SVRSQL01;initial catalog=prod_Uni; persist security info=True;user id=UKSync;password=kennedy2017;Connect Timeout=300;MultipleActiveResultSets=True;App=EntityFramework&quot;" providerName="System.Data.EntityClient" />
```

Notar el cambio en **persist security info=True**

**La solución definitive sería verificar con la primera versión del web.config si las credenciales del app pool son las correctas:**

![](https://raw.githubusercontent.com/gchervet/Documentacion/master/images/ConnectionStringSeguridadNoSuplida_00.png)


<a name="4c.DesactivarAutenticacion" />

## c. Desactivar autenticación obligatoria

```xml
<system.web>
	<authentication mode="None" />
</system.web>
```

<a name="4d.DesactivarCache" />

## d. Desactivar caché en todas las llamadas

```xml
<staticContent>
<clientCache cacheControlMode="DisableCache" />
</staticContent>
```

<a name="4e.HabilitarCORS" />

## e. Habilitar CORS para el ingreso desde cualquier URL

```xml
<system.webServer>
<httpProtocol>
  <customHeaders>
	<add name="Access-Control-Allow-Origin" value="*" />
	<add name="Access-Control-Allow-Headers" value="Origin, X-Requested-With, Content-Type, Accept, Authorization" />
	<add name="Access-Control-Allow-Methods" value="GET, POST, PUT, DELETE, OPTIONS" />
  </customHeaders>
</httpProtocol>
<modules>
  <remove name="FormsAuthentication" />
</modules>
<handlers>
  <remove name="ExtensionlessUrlHandler-Integrated-4.0" />
  <remove name="OPTIONSVerbHandler" />
  <remove name="TRACEVerbHandler" />
  <add name="ExtensionlessUrlHandler-Integrated-4.0" path="*." verb="*" type="System.Web.Handlers.TransferRequestHandler" preCondition="integratedMode,runtimeVersionv4.0" />
</handlers>
<security>
  <requestFiltering>
	<requestLimits maxAllowedContentLength="40960000" />
  </requestFiltering>
</security>
<validation validateIntegratedModeConfiguration="false"/>
</system.webServer>
```

<a name="4f.Error401.0" />

## f. Error 401.0

```xml
<system.webServer>
  <modules>
      <remove name="FormsAuthentication" />
    </modules>
</system.webServer>
```

<a name="4g.Error404.8" />
	
## g. Error 404.8
	
```xml
<system.webServer>
    <validation validateIntegratedModeConfiguration="false"/>
</system.webServer>
```

<a name="4h.CustomErrorsOff" />

## h. Custom erros mode Off
	
```xml
<configuration>
    <system.web>
        <customErrors mode="Off"/>
    </system.web>
</configuration>
```

<a name="5.ResolucionProblemas_NodeJS" />

# 5. Resolución de problemas - Node JS

<a name="5a.CantSetHeaders" />

## a. Can't set headers after they are sent

Este error se suele dar por diversas razones, pero aquí se enumeran algunas:

- En alguna promesa hay más de un res.json(...)
- Se suele dar por la dupla express - mssql, pero tiene más que ver con las promesas no bien resueltas

**Cómo solucionar:**

Recordar que **res.json(...)** no es lo mismo que **return ...**, por lo que el código continuará e intentará dar dos devoluciones en la respuesta, duplicando los headers. 

La mejor opción es directamente eliminar los res.json duplicados.


<a name="6.ApuntesVarios" />

# 6. Apuntes varios

<a name="6a.BuscarProcesosINETService" />

## a. Buscar procesos INET Service

Esto se utiliza para ver los procesos que se generan al levantar un servicio web local, además de los puertos que utilizan.

Correr esta línea en un MS DOS:

	%windir%\system32\inetsrv\appcmd.exe list wp


<a name="7ApuntesPHP" />

# 7. Apuntos de PHP

<a name="7DEBUGPHPXAMPP" />

## a. Debuggear PHP con XAMPP

Basado en el siguiente video

	https://www.youtube.com/watch?v=eE6oxEhqqoU

1. Abrir el *Manager de Nuget* en VS Code.
2. Descargar el módulo *PHPDebug*, este utiliza una aplicación llamada *XDebug* que hay que bajar luego y configurar.
3. Antes de continuar, necesitamos saber qué versión tenemos de PHP. Para ello, vamos a la carpeta raíz de nuestra página en XAMPP, por ejemplo:

	C:\xampp\htdocs\angular-filemanager
	
4. Allí, en la raíz, generamos un archivo llamado test.php con el siguiente contenido:

```php
<?php
$var = "Hello";
$output = $var. " world!";
phpinfo();
```

5. En XAMPP corremos el servidor apache en el puerto especifico, en este ejemplo será el 80
6. Una vez corriendo, abrimos el test.php generado de la siguiente manera:

	http://localhost/angular-filemanager/test.php

7. Si todo funciona correctamente, nos va a abrir una tabla html con los datos del PHP local. Hacemos click derecho en la pantalla y seleccionamos *Mostrar código fuente*.
8. Copiamos el código fuente de la página y lo pegamos en el textbox de la siguiente url:

	https://xdebug.org/wizard.php
	
9. Seleccionamos el botón que dice *Analyze phpinfo()* y nos dará una serie de instrucciones a seguir. Hacemos lo que nos dice.
10. Al seguir todas las instrucciones de la página, el archivo 

	C:\xampp\php\php.ini
	
debería tener las siguientes líneas:

	[XDebug]
	xdebug.remote_enable = 1
	xdebug.remote_autostart = 1
	zend_extension = C:\xampp\php\ext\php_xdebug-2.6.0-7.2-vc15.dll (O la extensión que nos haya dicho la página)

11. Una vez hecho esto, vamos al VS Code, File -> Preferences -> Settings y agregamos la siguiente línea al JSON:

	"php.validate.executablePath": "C:\\xampp\\php\\php.exe"

12. Ahora en el menú **Debug** del VS Code deberíamos poder accionar en cualquier momento nuestro debugger. Quizás nos pida permisos de administrador para correr el debugger. Es necesario resetear el servidor XAMPP.

<a name="7CORS" />

## b. CORS con PHP

Generar un archivo llamado **Cors.php** en la raíz del proyecto con el siguiente contenido:

```php
<?php
namespace <<NAMESPACE_NAME>>;

class Cors
{
    public function __construct($basePath = null, $lang = 'en', $muteErrors = true)
    {
       // Allow from any origin
       if (isset($_SERVER['HTTP_ORIGIN'])) {
            // Decide if the origin in $_SERVER['HTTP_ORIGIN'] is one
            // you want to allow, and if so:
            header("Access-Control-Allow-Origin: {$_SERVER['HTTP_ORIGIN']}");
            header('Access-Control-Allow-Credentials: true');
            header('Access-Control-Max-Age: 86400');    // cache for 1 day
        }

        // Access-Control headers are received during OPTIONS requests
        if ($_SERVER['REQUEST_METHOD'] == 'OPTIONS') {

            if (isset($_SERVER['HTTP_ACCESS_CONTROL_REQUEST_METHOD']))
                // may also be using PUT, PATCH, HEAD etc
                header("Access-Control-Allow-Methods: GET, POST, OPTIONS");         

            if (isset($_SERVER['HTTP_ACCESS_CONTROL_REQUEST_HEADERS']))
                header("Access-Control-Allow-Headers: {$_SERVER['HTTP_ACCESS_CONTROL_REQUEST_HEADERS']}");

            exit(0);
        }
    }
}
```

Y finalmente, en **index.php** agregar la siguientes líneas:

```php
include 'Cors.php';

// CORS
$CORS = new Cors();
```

El constructor de la clase Cors agregará los permisos necesarios.
