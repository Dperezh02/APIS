# ¿Que es una API?
![I1](https://github.com/Dperezh02/APIS/blob/master/Imagenes%20de%20referencia/Que%20es%20una%20API.jpg)

API son las inicialies de **A**pplication **P**rogramming **I**nterface (interfaz de programación de aplicaciones).
Una API es una interface que nos permite dar una o varias instrucciones, ya sea a una aplicación, lenguaje, plataforma, etc.

Ejemplo:
- Para prender un televisor la **interfaz** seria el botón del control (Encender/apagar) que le da instrucción de encender el televisor y el televisor sera ese **sofware** que ejecutara otras instrucciones que desconocemos pero que haran que podamos ver contenido en la pantalla

## APIs / REST / RESTful APIs
Es muy umportante tener en cuenta que hablar de **APIs**, **REST** y **REST *ful* APIs** es total mente diferente 

- **APIs:** Es una abstracción de funciones y procedimientos.
- **REST:** Es una logica de restricciones y recomendaciones bajo la cual se puede construir un API (Puede decirse que es un modelo de arquitectura), REST no es un framework, ni es un protocolo, ni esta atado a un lenguaje de programación, REST es una logica de restricciones y recomendaciones bajo la cual se puede construir un API.
- **REST *ful* APIs:** Y finalmente REST *ful* APIs es una API ya implementada que esta construida utilizando la logica de REST. 

### Especificaciones de REST:
Cada procedimiento de nuestra api esta formada por un **Verbo HTTP** (Post, get, delete), una dirección **URI** unica y la información **(Datos)** necesaria que requiere el servidor para cumplir con el requerimiento 


## El protocolo HTTP, como se usa para la consulta de APIS, verbos y status
"Protocolo de comunicación entre aplicaciones, basada en el intercambio de texto"
Un protocolo especifica reglas en la comunicacion entre dos entes, en este caso entre dos computudoras.

**HTTP** (Hyper Text Transfer Protocol) fue creado especificamente para la web.

Una de las cosas que especifica el protocolo HTTP son los verbos:

- GET: solicitar datos o algun recurso.
- HEAD: traer headers (como una peticion GET pero sin contenidos). Es util cuando vamos a utilizar  APIs, para comprobar si lo que vamos a enviar esta correcto y puede ser procesado.
- POST: enviar datos a un recurso para la creación.
- PUT: reemplazar por completo un recurso.
- PATCH: reemplazar parcialmente un recurso.
- DELETE: eliminar un recurso.

Otra de las cosas que especifica el protocolo HTTP son los codigo de estado (status codes). Sirven para describir el estado de la peticion hecha al servidor.

- 1xx: Indican que la peticion fue recibida y el servidor sigue trabajando en el proceso, es decir, no fue exitosa ni fue errónea, sino que esta siendo procesada aun.
- 2xx: Indican que la peticion fue recibida y procesada correctamente.
- 3xx: Indican que hay que tomar acciones adicionales para completar la solicitud. Por lo general estos codigos indican redireccion. Generalmente en los APIs no se usan redirecciones porque no contienen estados, es decir, toda la informacion esta contenida en una solicitud, no se guarda un estado en el servidor con una sesion por ejemplo.
- 4xx: Indican errores del lado del cliente, por ejemplo: se hizo mal la solicitud, faltan datos, headers o cualquier otro error que pueda ocurrir.
- 5xx: Indican errores del servidor. Suelen aparecer cuando existe un fallo en la ejecución en el servidor.

Los codigos más comunes a la hora de interactuar con un API son:
- 200: Todo esta OK.
- 201: Todo OK cuando se hizo una solicitud POST, el recurso se creo y se guardo correctamente.
- 204: Indica que la solicitud se completo correctamente pero no devolvio informacion. Es muy comun cuando se hacen peticiones con el verbo DELETE.
- 400: Bad Request, algo esta mal en la peticion. Se nos olvido enviar un dato o algo relacionado. Por lo general la respuesta nos especifica cuales fueron los errores a la hora de hacer la peticion.
- 401: Unauthorized, es decir, no estamos autorizados (autenticados) a realizar la peticion.
- 403: Forbidden, yo no tengo acceso a ese recurso aunque este autenticado.
- 404: Not Found, no existe el recurso que se esta intentando acceder.
- 500: Interna Server Error, es un error que retorna el servidor cuando la solicitud no pudo ser procesada. Por lo general, si no tenemos acceso al backend, no tenemos control sobre los errores 500 que retorna un API.
- Y otros como https://http.cat/

## Conceptos importantes a la hora de trabajar con APIs
### Recurso
Es la instancia o la representación de un objeto o la representación de algo, tiene datos y operaciones asociadas a él. Por ejemplo: curso, material y video son recursos que tenemos disponibles en el API con la que trabajaremos y podemos realizar operaciones sobre ellos: crear, actualizar y eliminar.

### Colecciones
Es un conjunto de recursos, por ejemplo: cursos una colección de curso.

### URL
(Uniform Resource Locator) es la ruta en la cual puede ser ubicado un recurso y ejecutar las operaciones sobre él.

### CRUD
Siglas que hacen referencia a las operaciones básicas que se pueden ejecutar sobre un recurso:

C: Create (crear)
R: Read (leer)
U: Update (actualizar)
D: Delete (eliminar)

### Endpoints
Es el punto final de la comunicación con un ente, en este caso, un endpoint está asociado a una URL y a las operaciones que podemos ejecutar. Este término es muy utilizado en las APIs.

Los endpoint definen operaciones que se quieren ejecutar sobre un recurso. Por ejemplo: si queremos un conjunto de operaciones CRUD sobre Cursos podríamos crear los siguientes endpoints:

- /get-all-courses : para obtener una colección de Cursos.
- /add-new-course: para crear un nuevo recurso de Cursos.
- /delete-all-courses: para eliminar todos los Cursos.

Y así sucesivamente. Pero, esto implicaría un problema. El API puede llenarse de endpoints que ejecutan una sola operación, esto no es escalable, significa que si por ejemplo el recurso Cursos pasa a llamarse Clases habría que actualizar absolutamente todas las URLs y asegurarse de ello puede convertirse en un dolor de cabeza.

Entonces, ¿cuál es la buena práctica en este caso?

Como lo vimos en la clase pasada, el protocolo HTTP especifica una serie de verbos que indican acciones. Lo ideal es que la operación que se ejecute sobre un recurso se obtenga a través del verbo HTTP de la petición y no que esté definido en el endpoint. Por ejemplo:

- /courses: Dependiendo del verbo HTTP se ejecutará una operación en particular. Quedaría así:
    - GET /courses: trae la colección de Cursos.
    - POST /courses: crea un nuevo recurso de Cursos.
    - DELETE /courses: elimina todos los cursos.

De esta manera queda mucho más organizado un API. Pero, qué pasa si queremos traer no una colección de cursos como en los casos anteriores, sino un recurso en específico.

Por lo general cada recurso tiene un identificador único, un ID, es con esto que llamaremos a un endpoint para que nos retorne la información del recurso. Por ejemplo:

- GET /courses/2/: vemos que acá se le está pasando algo que en los endpoints anteriores no veíamos, es el número 2, ese es el identificador único, de esta manera el API sabe que tiene que buscar el curso con ID 2 y retornarlo.

Así sucesivamente con cada uno de los verbos, por ejemplo: casi nunca se hace una eliminación en masa en un API, como el ejemplo que tenemos más arriba donde se eliminan todos los cursos. Lo ideal es que se elimine un recurso individualmente y no una colección, igualmente pasa con la actualización.

### Recursos anidados
Hay veces en las que un recurso depende de otro recurso, por ejemplo, comentarios depende de materiales; usualmente en los APIs las anidaciones se hacen hasta dos niveles, es decir:

- materials/1/comments: estos son dos niveles
- materials/1/comments/2/answers/: son tres niveles, ahí lo ideal sería entonces separar el endpoint de comentarios y ejecutar comments/2/answers/

### Nuestro API
Una convención que se usa a la hora de documentar APIs es abstraer el endpoint de la URL del sitio al cual vamos a hacer la petición, puesto que esto al final es redundante de escribir, es decir, usualmente escribimos únicamente /api-token-auth/ en vez de [http://mistioweb.com/api-token-auth/](http://mistioweb.com/api-token-auth/).

###  Los endpoints que tenemos:
/api-token-auth/
/courses
/courses/:id/
/courses/:id/upload_badge/
/materials/
/materials/:id/
/materials/:id/comments/
/comments/
/comments/:id/
/comments/:id/like/
/comments/:id/dislike/

## Instalación de Postman
Es esta dirección https://www.getpostman.com/downloads/ por defecto, el sitio sabe desde qué sistema operativo estás accediendo y te muestra como primera opción, si no, más abajo aparecen los demás sistemas operativos que soporta Postman.

### En windows
La instalación de Postman tiende a ser mucho más sencilla que la de una aplicación tradicional; no hay una serie de configuraciones que se deben aceptar o personalizar. Postman se instala en el sistema listo para utilizarse.

- Descargar Postman
- Abrir el archivo que se descargó, una vez abrá aparecerá una ventana así:
![I1](https://github.com/Dperezh02/APIS/blob/master/Imagenes%20de%20referencia/loading.png)
- Una vez instalado te pedirá que inicies sesión o si es el caso que crees una nueva cuenta.
![I1](https://github.com/Dperezh02/APIS/blob/master/Imagenes%20de%20referencia/login%20postman.png)
- Y ya está postman listo para usarse.
![I1](https://github.com/Dperezh02/APIS/blob/master/Imagenes%20de%20referencia/Interface%20postman.png)