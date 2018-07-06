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
