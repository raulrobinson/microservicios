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







```
<dependency>
    <groupId>io.swagger</groupId>
    <artifactId>swagger-codegen-maven-plugin</artifactId>
    <version>2.4.28</version>
</dependency>
```