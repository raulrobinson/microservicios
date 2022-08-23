# Microservicios

<img src="https://i.imgur.com/fpl0rGF.png">

Definimos la arquitectura de microservicios:

>  Se trata de una arquitectura que propone descomponer los distintos
> componentes que forman una aplicación hasta transformarlos en módulos
> encargados de realizar una única función con una serie de  interfaces
> bien definidas. Estos módulos han de ser capaces de operar por sí
> mismos y estás totalmente abstraídos del resto del entorno de la
> aplicación.

---
### Objetivos teóricos a desarrollar
- Arquitectura de Microservicios:
	- Conceptos clave
	- Service Discovery
	- Gateway
	 - Server Config
	- Ventajas
	- Inconvenientes


- Api REST


- Docker
- Spring Boot y Spring Cloud

---
Todo ello será estudiado e investigado a través del desarrollo de una aplicación basada en
Microservicios que se tomará como ejemplo práctico y a través de la cual se intentaran entender los
conceptos clave de esta arquitectura y su posición actual y a futuro en el mundo Software.

---
### Tareas de desarrollo


- Definir los conceptos de nuestro proyecto:
  - Problema: Introducción al problema y reglas de negocio
  -  Modelo: Dominio y entidades
   - Servicios: Tecnologías y organización


- Desarrollo
  - Desarrollo de microservicios basados en Api REST
  - Arquitectura de microservicios basada en Spring Cloud
  - Despliegue: Imágenes Docker y Docker-compose


---
### Estructura de la aplicación


La arquitectura basada en microservicios puede tener tantas capas, servicios o componentes, como se requieran. Generalmente, las capas básicas de esta arquitectura son: API Gateway, Service Discovery, Servicios y sus correspondientes bases de datos.


Algunos ejemplos de arquitecturas de aplicaciones basadas en microservicios pueden ser:

<img src="https://i.pinimg.com/originals/ce/b4/a5/ceb4a506ef82dee71643bfa6bec8f498.png">

<img src="https://docs.huihoo.com/apache/mesos/chrisrc.me/assets/microservice_ms_overview.png">

Como vemos, una arquitectura de Microservicios se basa en dividir los grandes servicios web utilizados hasta ahora, en pequeños servicios independientes con un dominio más ligero y una lógica con una menor complejidad.

En el caso anterior, por ejemplo, podemos ver como la aplicación posee hasta seis micro-servicios para dar un servicio común a través de la interfaz de aplicación, o API, llamada Gateway en este caso.

Como vemos, estos servicios también pueden respaldarse entre sí, aunque estos se mantengan totalmente independientes. Esto se debe al principio de deslocalización en el que se basan los microservicios.

Por otro lado, podemos ver como no es necesario que todos los servicios mantengan los mismos protocolos de comunicación, es decir, generalmente existirá un mismo protocolo de comunicación, que normalmente será el REST, pero es posible que cada servicio pueda implementar otro u otros protocolos para hacer más flexible la aplicación.


---
## Desarrollando un sistema de Microservicios

Se busca mantener un intercambio de información sobre las tareas diarias de las materias, entre los alumnos y el profesor, de una forma ordenada y eficiente.


Es decir, nuestro problema reside en encontrar una forma de realizar un seguimiento centralizado para todas las tareas de una materia. De tal forma que el profesor pueda saber qué alumnos han realizado la tarea, y en caso de no haberla realizado, poder encontrar una breve explicación de por
qué.


Por otro lado, el profesor desea conocer qué opinan los alumnos de la dificultad, o el volumen de trabajo, de las tareas que se han pedido. De tal forma que cada alumno pueda valorarla y, además, escribir un breve comentario.


Finalmente, es importante que los alumnos puedan tener acceso a las tareas que se han pedido de forma ordenada cronológicamente. Es decir, de alguna forma, que dichas tareas estén reflejadas en un calendario para que sea fácil para los alumnos, y a la vez para el profesor, organizar dichas tareas en el tiempo.

---
### Modelo


Una vez abordado el problema, se puede construir el modelo para la aplicación. Para ello han de definirse los conceptos con los que se van a trabajar:


- Tareas : Son las distintas actividades que se realizan en una materia. Pueden ser de distintos tipos, entre los que se contemplan: Deberes, Exámenes, Talleres, Entregas de trabajos, etc.


- Seguimientos : Representan los datos que intercambian los alumnos para cada tarea con el profesor.Corresponden a la valoración del trabajo realizado, la valoración de la dificultad de la tarea y los respectivos comentarios a ambas valoraciones.


- Profesores : Son los encargados de administrar las tareas, es decir, son los encargados de crear, modificar y eliminar las tareas. Además, podrán acceder a los comentarios de los alumnos.


- Alumnos : Pueden acceder a la información de cada tarea. Además, deberán interactuar con cada tarea para realizar el seguimiento de éstas. Para ello deberán valorar cada tarea y escribir un comentario para cada valoración antes de la fecha de fin de la tarea. Aunque podrán escribir comentarios tras la fecha de fin que, por defecto, valorarán su trabajo realizado como “Fuera de plazo”.

<img src="https://i.imgur.com/RrsCJl1.png">


---
### Servicios

#### Calendario (Tareas)


- Descripción : Este servicio soporta las peticiones referidas a las tareas de cada materia en una fecha y horario concreto sobre un calendario y un profesor concreto.


- Tecnología : Api Rest, Spring-Boot, Spring-MVC, Lombock, Java 8.


- Funcionalidad : Manejo de tareas: Creación, modificación, borrado y lectura de las tareas generadas.


- Modelo : Una colección “Tareas” que maneja documentos de tipo “Tarea” que contienen referencias a las materias, alumnos y profesores que la componen.


- Base de datos : MongoDB.

#### Seguimiento (Valoraciones y comentarios)


- Descripción : Servicio encargado de manejar las peticiones sobre la realización de las tareas por parte de los alumnos y la valoración de la carga de trabajo y la dificultad de las tareas asignadas.


- Tecnología : Api Rest, Spring-Boot, Spring-MVC, Lombock, Java 8.



- Funcionalidad : Manejo de controles o seguimientos para las tareas existentes. Creación de un control para una tarea, borrado, modificación y lectura.


- Modelo : Una tabla “Seguimientos” que contiene elementos “Seguimiento” los cuales, cada uno, tienen una referencia a cada tarea y cada alumno correspondiente.


- Base de datos : PostgreSQL.

#### API Gateway


- Descripción : Servicio encargado de centralizar las llamadas a los demás servicios a través de una URI que hace de entrada de peticiones.


- Tecnología : Api Rest, Spring-Boot, Spring-Cloud Gateway sobre Java 8.


- Funcionalidad : Se encarga de centralizar las llamadas a la aplicación en una URI principal que redirige las llamadas a los servicios configurados internamente.

#### Service-Discovery


- Descripción : Servicio encargado de registrar las direcciones a los microservicios que componen la aplicación y redireccionar las peticiones hacia estos.


- Tecnología : Spring-Boot, Spring-Cloud y Netflix Eureka sobre Java 8


- Funcionalidad : Encargado de redirigir las llamadas realizadas a cada servicio a través de una URI genérica a la dirección del servidor en el que se encuentra dicho servicio.

#### Server Config


- Descripción : Este servicio está a la espera de recibir peticiones por parte del resto de servicios, para que se les proporcione la configuración necesaria para su ejecución en el entorno definido. Cuando este servicio recibe estas peticiones, recoge los archivos de configuración para cada servicio (de extensión “.yml” o “.properties”) de un repositorio definido para luego proporcionárselo al servicio que haya realizado la petición.


- Tecnología : Spring-Boot y Spring-Cloud: Spring Cloud Config Server sobre Java8


- Funcionalidad : Busca sobre un repositorio los archivos de configuración de cada servicio que los solicite.



En nuestro caso, la arquitectura de nuestra aplicación será la siguiente:

<img src="https://i.imgur.com/kvNxe7K.png">

---

## Herramientas de Desarrollo

###  Entorno de desarrollo

#### IntelliJ IDEA- JetBrains
#### Maven – Apache
#### Spring Framework
#### Postman

---

#### Proyecto Multimódulo


Desde siempre se ha hecho uso de librerías, externas o internas, para ser reutilizadas durante el desarrollo software. Es decir, reutilizar software ya existente y de esta forma generalizar ciertas funcionalidades comunes.


En este caso, si nos basamos en el servicio desarrollado para el Control de las tareas de clase para cada alumno, dicho servicio se encuentra dividido en seis módulos distintos:

<img src="https://i.imgur.com/CRR6sFP.png">


- Boot: Es el módulo donde encontraremos la clase de ejecución principal o “main”. Contendrá cierta configuración de importancia y será el módulo hijo del paquete principal.


- Controller: Define el manejo de las peticiones HTTP recibidas. En este caso, se definirá con la anotación @RestController y se deberán definir las rutas para las uris de acceso, así como el método de cabecera que deberá llevar la petición (GET, POST, PUT, PATCH, etc.)


- Service: Se trata de la capa donde reside la lógica de nuestra aplicación, es decir, será el módulo encargado de interactuar con el modelo de datos, el repositorio y los datos y peticiones recibidos desde la capa controlador.


- Repository: En este módulo se definirá el manejo de datos. Estos datos podrán ser recibidos a través de interfaces de conexión con bases de datos, o datos externos recibidos a través de APIs externas o propias.


- Model: Se trata de la capa “dominio” de nuestra aplicación, y define las entidades y objetos con los que nuestra aplicación trabajará.


  - DTO: Se trata de un módulo opcional que será hijo del módulo “Model” y contendrá sólo los objetos DTO para que puedan ser integrados por otras aplicaciones gracias a que son un módulo.


  - VO: Al igual que el anterior, se trata de un módulo opcional que trata de modularizar la capa de dominio de la aplicación.

De esta forma, a través del gestor Maven, nos encontramos con la posibilidad de construir proyectos basados en módulos, los cuales son gestionados como dependencias Maven a través de los archivos POM que cada uno contiene.

<img src="https://i.imgur.com/iQqoBis.png">

---

## Spring Boot - API Rest


Llamamos API al conjunto de funciones y procedimientos que realizan distintas funciones con el fin de ser utilizadas por otro software. Este concepto se encuentra incluido en el concepto software de librería.


Las siglas API vienen del inglés Application Programming Interface, que en español sería Interfaz de Programación de Aplicaciones. Esto se debe a que una API nos permite implementar las funciones y procedimientos que engloba en nuestro proyecto sin la necesidad de programarlas de nuevo. En términos de programación, es una capa de abstracción.


Por otro lado, API REST se define como una librería que se basa totalmente en el estándar de
comunicación HTTP. Dicho de otra forma, una API REST es un servicio que nos aporta funciones
heredadas a través de un servicio web que no es nuestro, dentro de una aplicación propia, de
manera segura.


REST, REpresentational State Transfer, es un tipo de arquitectura de desarrollo web que se apoya totalmente en el estándar HTTP. Por ello, al ser un estándar de red, requiere de ciertas restricciones que permitan la correcta comunicación entre usuarios. Estas restricciones son:


- Conexión cliente-servidor libre ; El cliente no necesita saber los detalles de la implementación del server, y este tampoco debe preocuparse por cómo se usan los datos que envía.


- Cada petición enviada al servidor es independiente.


- Compatibilidad con un sistema de almacenamiento en caché.


- Cada recurso del servicio REST debe tener una única dirección , manteniendo una interfaz genérica.


- Permite utilizar diferentes capas para la implementación del servidor.


En nuestro caso, los servicios desarrollados siguen este patrón, ya que a día de hoy, REST y JSON, son la combinación más utilizada para el desarrollo de APIs, y la que un mayor apoyo de parte de la comunidad poseen.

<img src="https://pngimage.net/wp-content/uploads/2018/06/introduccion-png-3.png">


Con esto, además, Spring Framework posee toda una serie de librerías, módulos y funcionalidades a disposición de los desarrolladores para crear nuevas APIs REST. 


La anotación @RestController , que indica que la clase Java que la contenga será la encargada de manejar las peticiones HTTP que nuestra aplicación recibirá, y que, además, nuestra aplicación ofrecerá respuestas acordes a las restricciones REST. En nuestro caso, como se ha indicado anteriormente, se oferecerán respuestas JSON.


Además, Spring nos ofrece una serie de anotaciones para indicar al controlador REST qué métodos Java manejaran qué peticiones HTTP. Estas peticiones HTTP, pueden ser desde GET, POST, PUT PATCH, OPTIONS, DELETE, etc. Por lo tanto, Spring nos ofrece las siguientes anotaciones para cada operación: @GetMapping, @PostMapping, @PutMapping, @DeleteMapping , etc.


Es recomendable, que los métodos de la clase “Controller” devuelvan objetos del tipo ResponseEntity<T> , donde “T” hace referencia al tipo de objeto que será transformado a JSON a través del traductor interno de Spring, llamado JackSon. Estos objetos, además de incluir el objeto Java a traducir como respuesta, nos permiten personalizar las cabeceras HTTP para dar unas respuestas más complejas y completas.

Como ya hemos dicho, REST nos permite implementar los métodos HTTP y es fácil observar, que existen similitudes entre estos y las operaciones de una interfaz CRUD. Esto se debe a que realmente, una petición GET estará asociada a un query SELECT, una petición POST estará asociada a un query INSERT, una petición PUT a un UPDATE y así sucesivamente. Esto no tiene por qué ser
siempre así, ya que por ejemplo, podría darse el caso de que una API consulte información de los recursos o procese ciertos datos para dar una respuesta sencilla. Esto dependerá de las necesidades del proyecto, pero en general funciona de la manera antes mencionada.

Para nuestro desarrollo, en el servicio “Task Control”, podemos ver cómo queda definido una interfaz API y su implementación “Controller”:

```java
@RequestMapping(EndPointUris. _CONTROLS_ )
public interface TaskControlApi {
    @PostMapping
    ResponseEntity<ControlDTO> create(@Valid @RequestBody final ControlDTO controlDTO);

    @GetMapping
    ResponseEntity<List<ControlDTO>> getAll(final ControlFilterCriteriaDTO search);

    @GetMapping(EndPointUris.CONTROL)
    ResponseEntity<ControlDTO> getById(@PathVariable(value = "id")
    final int controlId);

    @DeleteMapping(EndPointUris.CONTROL)
    ResponseEntity<Void> delete(@PathVariable(value = "id") final int controlId);

    @PutMapping(EndPointUris.CONTROL)
    ResponseEntity<ControlDTO> update(@PathVariable(value = "id") final int controlId, @Valid @RequestBody final ControlDTO controlDTO);
 }
```

En la Interfaz TaskControlAPI, definimos los métodos que manejará nuestro servicio junto con las anotaciones pertinentes, con la intención de que se puedan abordar varias implementaciones si fuera necesario.

```java
@RestController
public class TaskControlController implements TaskControlApi {
    @Autowired
    private TaskControlService taskControlService;

    @Override
    public ResponseEntity<ControlDTO> create(@Valid ControlDTO controlDTO) {
        return ResponseEntity.ok(taskControlService.create(controlDTO));
    }

    @Override
    public ResponseEntity<List<ControlDTO>> getAll(ControlFilterCriteriaDTO search) {
        return ResponseEntity.ok(taskControlService.getAll(search));
    }

    public ResponseEntity<ControlDTO> getById(@PathVariable(value = "id") final int controlId) {
        return ResponseEntity.ok(taskControlService.getById(controlId));
    }

    @Override
    public ResponseEntity<Void> delete(int controlId) {
        return ResponseEntity.noContent().build();
    }

    @Override
    public ResponseEntity<ControlDTO> update(int controlId, @Valid ControlDTO controlDTO) {
        return ResponseEntity.ok(taskControlService.update(controlId, controlDTO));
    }
}
```

Para la documentación de estas APIs, es recomendable utilizar librerías ya existentes que permiten acceder a un índice con los métodos permitidos por la API, sus respuestas, requerimientos, accesibilidad, etc.
A día de hoy, una de las mayores librerías o herramientas que da este soporte es Swagger. Con Swagger es posible documentar una API de forma sencilla sin la necesidad de mucha configuración o escritura.
Para utilizar Swagger, tan solo es necesario incluir la dependencia principal a esta librería Maven en el POM principal del proyecto: 

```xml
<dependency> 
    <groupId>io.springfox</groupId> 
    <artifactId>springfox-swagger2</artifactId> 
    <version>2.9.2</version> 
</dependency>
```

Además, será necesario activar esta utilidad en la clase ejecutable principal de nuestra aplicación, en este caso, tendríamos algo como: 

```java
@EnableSwagger2
```

Con esta dependencia nuestro proyecto contará con unos “endpoints” a través de los cuales cualquier persona que acceda a la dirección referente a Swagger, la cual es ***/v2/api-docs**, obtendrá toda la información en formato JSON sobre los métodos de la API en cuestión.
Por otro lado, tenemos una interfaz gráfica ofrecida por Swagger para documentar nuestra aplicación de forma más sencilla y dinámica, que nos ofrece toda esta información en una pantalla HTML a través de la dirección ***/swagger-ui.html**:
<img src="https://i.imgur.com/BaASx07.png">
Para el uso de esta herramienta, será necesario incluir la dependencia correspondiente en el POM: 

```xml
<dependency> 
    <groupId>io.springfox</groupId> 
    <artifactId>springfox-swagger-ui</artifactId> 
    <version>2.9.2</version> 
</dependency>
```
----

### Spring Boot - API Rest Manejo de Excepciones
Para el control de excepciones de un servicio REST con Spring existen varias opciones.
Una de las más fáciles, aunque sólo puede usarse a partir de Spring 5, consiste en utilizar la excepción aportada por Spring llamada **“ResponseStatusException”**.

```java
@GetMapping(value = "/{id}")
public Foo findById(@PathVariable("id") Long id, HttpServletResponse response) {
try {
    Foo resourceById = RestPreconditions.checkFound(service.findOne(id));
    eventPublisher.publishEvent(new SingleResourceRetrievedEvent(this, response));
    return resourceById;
} catch (MyResourceNotFoundException exc) {
    throw new ResponseStatusException( HttpStatus.NOT_FOUND, "Foo Not Found", exc); }
}
```

Esta excepción la debemos lanzar en el “catch” de un bloque ��try-catch” o al controlar algún comportamiento indebido en nuestra aplicación a nivel de controlador. Es útil para realizar prototipos de métodos y ver las posibles excepciones que puede lanzar un método, antes de implementar un manejador global de excepciones.
*AVISO : Si se controlan las excepciones con un manejador @ControllerAdvice y además lanzando este tipo de excepción, se crean conflictos.*
Otra opción, es utilizar la notación de Spring @ControllerAdvice que permite implementar manejadores globales @ExceptionHandler para distintas excepciones:

```java
@ControllerAdvice
public class RestResponseEntityExceptionHandler extends ResponseEntityExceptionHandler {
@ExceptionHandler(value = { IllegalArgumentException.class, IllegalStateException.class})
    protected ResponseEntity<Object> handleConflict(RuntimeException ex, WebRequest request) {
        String bodyOfResponse = "This should be application specific";
        return handleExceptionInternal(ex, bodyOfResponse, new HttpHeaders(), HttpStatus.CONFLICT, request);
    }
}
```
Está pensado para ser utilizado a nivel de controlador de nuestro servicio rest, ya que hace uso de los objetos de tipo ResponseEntity.
*AVISO : Si no se especifica una excepción para ser controlada en la anotación
“@ExceptionHandler(value= {...AQUÍ...})” se producirá un error indicando que no se ha encontrado manejador definido para esa excepción.*
Por último, se suele utilizar una combinación de dos métodos que consiste en la creación de excepciones propias las cuales no será necesario que lancen a través de la anotación “@ResponseStatus(value = HttpStatus.ERROR_TYPE)” un error de tipo HTTP como respuesta, ya que de eso se encargará el manejador global. Dicho manejardor controlará estas excepciones como un error REST y dará una respuesta a través de los ResponseEntity que le indiquemos (con archivos HTML estáticos por ejemplo).
Por lo tanto, debemos crear una clase controladora y utilizar la anotación @RestControllerAdvice par definir un manejador de excepciones global que controle estas excepciones.

---

### Modelo
Se sigue el patrón usual para los modelos de las aplicaciones web. Se distinguen dos tipos de objetos
diferenciados, que son los Value Objects y los Data Transfer Objects:
VO (Value Object) → Son los datos que se pueden o se encuentran persistidos en la BD. Es decir, son
el tipo de datos que se intercambian con la base de datos y que quizás requieran tener ciertas
propiedades específicas para su manejo en la base de datos. Además, en el contexto de Spring,
existen ciertas anotaciones que pertenecen al módulo de Spring Boot, llamado Spring Data, y que
permiten configurar de forma sencilla este tipo de objetos.

```java
@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
@Builder
@Entity
public class ControlVO {
    @GeneratedValue
    @Id
    private Integer id;
    private String task_reference;
    private String alum_reference;
    private Date controlDate;
    private Integer workDoneQuantityValuation;
    private String workDoneQuantityComment;
    private Integer workLoadValuation;
    private String workLoadComment;
    private Integer difficultValuation;
    private String difficultComment;
}
```

- DTO (Data Transfer Object):  Son la representación de los datos que se manejan en la aplicación para ser transferidos o recibidos como recursos en las peticiones realizadas hacia la aplicación. Solo son utilizados en el intercambio de datos en las peticiones web.

```java
@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
@Builder
public class ControlDTO {
    private Integer id;
    private String task_reference;
    private String alum_reference;

    @DateTimeFormat(pattern = "yyyy-MM-dd'T'HH:mm:ss.SSSXXX")
    private Date controlDate;
    
    @NotNull(message = "The evaluation for the quantity of the work
    done can't be null!")
    private Integer workDoneQuantityValuation;
    
    @NotBlank(message = "The comment for the quantity of the work
    done can't be null!")
    private String workDoneQuantityComment;
    
    @NotNull(message = "The evaluation for the workload can't be
    null!")
    private Integer workLoadValuation;
    
    @NotBlank(message = "The comment for the workload can't be
    null!")
    private String workLoadComment;
    
    @NotNull(message = "The evaluation for the difficult can't be
    null!")
    private Integer difficultValuation;
    
    @NotBlank(message = "The comment for the difficult can't be
    null!")
    private String difficultComment;
}
```

<img src="https://i.imgur.com/Z4Epg6Y.png">
Para la creación de las clases de objetos POJO que definen nuestros objetos, se ha utilizado la herramienta LOMBOK. Lombok consiste en una librería para Java que nos ofrece, a través de anotaciones, reducir el código de las clases POJO de nuestra aplicación.
Para poder usar esta librería, ha de definirse como dependencia en el archivo POM.xml de la aplicación:

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <optional>true</optional>
</dependency>
```

Además, generalmente, será necesario activar el procesador de anotaciones del IDE, así como, a veces, instalar un plugin que procese estas anotaciones:
<img src="https://i.imgur.com/T34OUka.png">
<img src="https://i.imgur.com/gbukY3x.png">
Las anotaciones le indican a Lombok qué métodos debe generar escaneando los atributos de la clase donde haya sido utilizado en tiempo de compilación. Las anotaciones más importantes son:
- **@Getter** Genera los métodos “get” para los atributos definidos.
- **@Setter**: Genera los métodos “set”
- **@AllArgsConstructor**: Genera un constructor con todos los atributos como argumentos
- **@NoArgsConstructor**: Genera un constructor sin argumentos
- **@Builder**: Permite utilizar el patrón “builder” para crear nuevos objetos, como por ejemplo:

```java
ControlVO.builder().alum_reference(controlDTO.getAlum_reference())
        .controlDate(controlDTO.getControlDate())
        .difficultComment(controlDTO.getDifficultComment())
        .difficultValuation(controlDTO.getDifficultValuation())
        .id(controlDTO.getId())
        .task_reference(controlDTO.getTask_reference())
        .workLoadComment(controlDTO.getWorkLoadComment())
        .workLoadValuation(controlDTO.getWorkLoadValuation())
        .build();
```

Generalmente, los datos se intercambian con formato “JSON” o “XML” entre otros. Luego, estos datos son manejados por el controlador de la API y son traducidos al contexto del lenguaje orientado a objetos.

```yml
{
    "alum_reference": "string",
    "controlDate": "2019- 06 - 10T18:19:51.802Z",
    "difficultComment": "string",
    "difficultValuation": 0,
    "id": 0,
    "task_reference": "string",
    "workDoneQuantityComment": "string",
    "workDoneQuantityValuation": 0,
    "workLoadComment": "string",
    "workLoadValuation": 0
}
```

Más tarde, interiormente, los servicios encargados manejar las peticiones llegadas al controlador del API, transforman y manejan esos objetos según las necesidades de la aplicación.
Por ello, la traducción de los datos de DTO a VO se ha de realizar en la capa de Servicio de nuestra aplicación. Esta recibirá los DTOs del controlador y guardará los objetos VO a través de la capa de datos o repositorio.
En nuestra aplicación, se ha seguido este patrón para la conversión y mapeo de datos entre objetos DTO y objetos VO o entidad. Uno de estos convertidores podemos verlo en el siguiente ejemplo:

```java
@Component
public class ControlConverter {
public ControlDTO convertEntityToDTO(ControlVO controlVO) {
    return ControlDTO.builder().alum_reference(controlVO.getAlum_reference())
            .controlDate(controlVO.getControlDate()).difficultComment(controlVO.
            getDifficultComment())
            .difficultValuation(controlVO.getDifficultValuation()).id(controlVO.
            getId())
            .task_reference(controlVO.getTask_reference()).workLoadComment(contr
            olVO.getWorkLoadComment())
            .workLoadValuation(controlVO.getWorkLoadValuation()).build();
    }

    public ControlVO convertDTOToEntity(ControlDTO controlDTO) {
        return ControlVO.builder().alum_reference(controlDTO.getAlum_reference())
                .controlDate(controlDTO.getControlDate()).difficultComment(controlDT
                O.getDifficultComment())
                .difficultValuation(controlDTO.getDifficultValuation()).id(controlDT
                O.getId())
                .task_reference(controlDTO.getTask_reference()).workLoadComment(cont
                rolDTO.getWorkLoadComment())
                .workLoadValuation(controlDTO.getWorkLoadValuation()).build();
    }
}
```

---
### Spring Data - MongoDB
Como ya se ha comentado anteriormente, Spring Framework proporciona una potente interfaz para el manejo de datos con las principales tecnologías de base de datos. Estas interfaces se aúnan bajo el módulo de Spring-Data, el cual se subdivide en distintas librerías de las que el desarrollador dispone.
Para MongoDB, Spring Data tiene dos formas de abordar esta estructura de datos. Una es utilizando su implementación a través de la interfaz MongoRepository. Y la otra es utilizando el java-bean MongoTemplate, el cual ofrece una implementación totalmente configurable por el desarrollador a través de código o XML.
Para el uso de MongoRepository tan solo es necesario crear una interfaz que extienda de esta clase:

```java
@Repository
public interface TaskRepository extends MongoRepository<TaskVO, String>, CustomTaskRepository {
}
```

Spring Data MongoRepository nos ofrece la posibilidad de definir métodos en la interfaz que hemos creado que extiende al repository, que Spring mapeará como queries de mongo.
Por otro lado, MongoTemplate nos permite realizar un abordamiento más clásico para la creación de un repositorio. En este caso, tendremos la posibilidad utilizar un java-bean llamado MongoTemplate el cual nos es ofrecido por Spring Data y el cual es cargado en el contexto de Spring.
Esta interfaz nos permite implementar los métodos que nos sean necesarios, creando queries propias y funciones complejas para el manejo de datos con mongo.

```java
public interface CustomTaskRepository {
    List<TaskVO> findAllFilteredByQuery(final Query query);
}
```

```java
public class CustomTaskRepositoryImpl implements CustomTaskRepository {
    @Autowired
    private MongoTemplate mongoTemplate;

    @Override
    public List<TaskVO> findAllFilteredByQuery(final Query query) {
        return mongoTemplate.find(query, TaskVO.class);
    }
}
```

En el caso de necesitar ambas implementaciones, es necesario crear una interfaz que extienda de MongoRepository y al mismo tiempo realizar una implementación propia de algunos métodos utilizando el java-bean MongoTemplate, como se puede ver en el ejemplo anterior.
---

### Spring Data - PostgreSQL
Se crea una clase Interfaz que extienda a “JPARepository<R,T>” donde “R” es el tipo Java de la ID y “T” el tipo de los objetos que se van a guardar. La implementación de JPA hace uso de algunos ORMs como Hibernate.
- **@Entity**: Señala que esta clase es un objeto que se puede persistir en la estructura de datos.
- **@Id**: Señaliza que será la ID del objeto a persistir
- **@GeneratedValue**: Genera automáticamente la id cuando un objeto se persiste
Para las relaciones Uno a Muchos unidireccionales, la estructura básica de anotación es:

```java
@OneToMany(cascade = CascadeType. ALL , orphanRemoval = true)
@JoinColumn(name = "employee")
private List<WorkExperienceVO> workExperiences;
```

Donde “@OneToMany” señala qué tipo de relación es, el “cascadeType” hace referencia a la forma de comportarse la “cascada” de acciones de los datos. Es decir, si se borra un objeto de la lista de objetos referenciados también se borrará su persistencia y etc. En este caso, “ALL” hace referencia a que están todos los modos activados.
El atributo “orphanRemoval” indica si se desea que cuando se borre un objeto padre persistido, también se borren todos sus hijos.

---
### Service Discovery
El Service Discovery es un proyecto en sí mismo basado en Spring Boot y Spring Cloud. Lo que hace es resolver las peticiones a los servicios de una aplicación compuesta por microservicios. Esto quiere decir, que es el encargado de llamar a las direcciones (endpoints o uris) de cada servicio.
Dicho de otra forma, será el que tenga la “libreta de direcciones” de los demás servicios que componen la aplicación. Es el encargado de buscar a qué dirección corresponde el servicio que se está tratando de consumir y ofrecer dicho servicio a la petición tras ser recibida.
En Spring, se utilizan las librerías de Spring Cloud, concretamente, éstas se llaman Eureka. Estas librerías te ofrecen las funcionalidades para la implementación de un Service Discovery bastante completo para una aplicación basada en arquitectura de microservicios e implementada con Spring.
Para ello, ha de crearse un proyecto Spring que tenga las dependencias de Spring Cloud dentro.
Además, en el main de la aplicación Spring Boot, ha de aparecer la siguiente anotación:
- **@EnableEurekaServer**
En cuanto al archivo properties de la aplicación, ha de tener una forma similar a: server.port= 8761
```properties
eureka.client.register-with-eureka=false
eureka.client.fetch-registry=false
```
Esto nos permitirá acceder a una consola de información sobre el Service Discovery, con información sobre los servicios a los que hace referencia y a la máquina en la que está corriendo.
De otra forma, también puede utilizarse la configuración en formato “.yml”, la cual es más limpia y más legible. Entre estas propiedades que se definen, se pueden configurar elementos del tipo:

```yml
server:
    port: ${PORT:8761}
```

Donde la notación con el dólar, indica el uso de una variable global ya definida. En este caso, con la notación **“DEFAULT:new”**, se está indicando que primeramente se buscará la variable definida por defecto “PORT” para la propiedad server. En caso de no existir, los dos puntos indicar un operador
lógico “OR” que indica qué puerto ha de usarse en caso de no existir uno por defecto ya definido. Esto nos sirve para parametrizar la configuración de nuestra aplicación.
---

### Spring Cloud Gateway:
El Gateway es un servicio basado en Spring Boot y Spring Cloud. Resumidamente, se encarga de resolver las peticiones realizadas a la aplicación de forma centralizada y distribuirla entra los servicios de una aplicación compuesta por microservicios.
Esto quiere decir, que es el encargado de recibir y organizar las peticiones hacia los distintos recursos entre los distintos servicios.
El Gateway, como su nombre indica, hace de “portero” en la conexión entre las peticiones externas y los microservicios que componen nuestra aplicación.
Para la implementación del Gateway, como para otros servicios ya creados, primero se ha generado un proyecto inicializado desde la web spring-initializr. En este caso, es necesario añadir las dependencias referentes a la librería spring cloud y el artefacto gateway:

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-gateway</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-config</artifactId>
</dependency>
```

A estas dependencias, debemos sumarles las nombradas anteriormente para que nuestro servicio
solicite su configuración al servidor config de forma ordenada y, además, que se registre en nuestro
service discovery.
En esta ocasión, a configuración del servicio deberá ser algo más exhaustiva, ya que es necesario que
le especifiquemos los servicios a los que debe redirigir de forma automática las peticiones que se le
realicen a través de su URI.
Para nuestro caso, se han implementado dos configuraciones correspondientes a los perfiles Spring
declarados, en nuestro caso, local y develop.
Para el caso del perfil local:

- **bootstrap-local.yml →**

```yml
spring:
    application:
        name: gateway
    cloud:
        config:
            name: gateway
            retry:
                max-attempts: 10
                initial-interval: 5000
            fail-fast: true
```

-----
- **application-local.yml →**

```yml
spring:
    cloud:
        gateway:
            routes:
                - id: task-calendar-service _#Order service route declaration_
                uri: "http://localhost:8095"
                predicates:
                    - Path=/calendar/** _#Path to access the service_
                filters:
                    - StripPrefix=1
                - id: task-control-service _#Task-Control service route declaration_
                uri: "http://localhost:8098"
                predicates:
                    - Path=/task-control/** _#Path to access the service_
                filters:
                    - StripPrefix=1
```
En este caso, la configuración inicial, o “bootstrap”, nos indica que no se desea que el servicio
busque su configuración en el servidor y que, además, no se registre en el servidor Eureka. Esto se
debe a que, en un entorno local, quizás no es deseable levantar todos los servicios, y solo es
necesario ejecutar los servicios individualmente para probar su funcionamiento.
Junto a esta configuración inicial, se encuentra la configuración principal de la aplicación, en la que,
en este caso, se declaran las rutas que nuestro servicio ha de redirigir junto con los predicados a los
que el usuario tendrá acceso.

---
### Spring Cloud Config Server
Spring, ofrece una implementación del llamado Config Server muy útil y sencilla. En nuestro caso, se ha creado un proyecto con la herramienta antes mencionada “spring-initializr”, con las dependencias correspondientes a Spring Cloud, que es la librería padre que nos ofrece Spring Cloud Config Server:

```xml
<properties>
    <java.version>1.8</java.version>
    <spring-cloud.version>Greenwich.SR1</spring-cloud.version>
</properties>
<dependencies>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-config-server</artifactId>
    </dependency>
</dependencies>
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-dependencies</artifactId>
            <version>${spring-cloud.version}</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

Una vez hecho esto, tendremos un proyecto sencillo con una clase main que se ejecutará el contexto de spring. A esta clase, habrá que añadirle obligatoriamente la siguiente anotación:
- **@EnableConfigServer**
Además, para este servicio es necesario que implementemos una configuración concreta en el archivo “application.yml”, que debe ser la siguiente:

```yml
server:
    port: 8888
spring:
    application:
        name: server-config
    cloud:
        config:
            server:
                git:
                    uri: https://gitlab.com/task-control-app-config/config-repo.git
                    force-pull: true
                    clone-on-start: true
                    default-label: master

                    repos:
                        develop:
                            uri: https://gitlab.com/task-control-app-config/config-repo.git
                            force-pull: true
                            clone-on-start: true
                            default-label: develop
                        local:
                            uri: https://gitlab.com/task-control-app-config/config-repo.git
                            force-pull: true
                            clone-on-start: true
                            default-label: local
```
Donde podremos definir distintos repositorios asociados a los perfiles de la aplicación spring. Por ejemplo, en nuestro caso, se han definido dos repositorios, que corresponden a dos perfiles definidos: local y develop.
En el caso del repositorio local, la configuración se establece para un entorno de pruebas local en el que se pretende desplegar todos los servicios de forma local. Por otro lado, en el perfil develop, tenemos un repositorio en el que se encontrará la configuración para el despliegue en un entorno más avanzado posiblemente en remoto.
Para que cada servicio pueda encontrar su archivo de configuración, estos archivos deben de tener como nombre, el nombre del servicio y extensión “.yml” o “.properties”.
En nuestro caso, se ha creado un repositorio GIT donde se contienen todos estos archivos:
<img src="https://i.imgur.com/jvTVj3Q.png">
Para que el resto de los servicios puedan encontrar su configuración apuntando a este servicio, también han de tener una configuración previa a su ejecución, en la que se definirán ciertos aspectos como el puerto o la dirección donde se encuentra el servicio, que no se encuentra registrado en el Service Discovery ya que es un servicio extra y totalmente independiente, y el nombre con el que buscará su configuración en el repositorio.
Por ejemplo, en el caso del servicio Gateway, tendremos una configuración en el archivo “bootstrap.yml” de la siguiente forma:

```yml
spring:
    application:
        name: gateway
    cloud:
        config:
            name: gateway
            retry:
                max-attempts: 10
                initial-interval: 5000
            fail-fast: true
```

Con esta configuración, estamos definiendo el nombre del servicio, junto con una configuración mínima para la política de reintentos en caso de no encontrar el servicio en la dirección determinada
al inicio de la aplicación. Por defecto el puerto en el que el servicio buscará el servidor de configuración es el “8888”.
Además, será necesario que el servicio que desee obtener su configuración del servidor tenga varias dependencias necesarias, como son:

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-config</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.retry</groupId>
    <artifactId>spring-retry</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-aop</artifactId>
</dependency>
```

