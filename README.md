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





```
<dependency>
    <groupId>io.swagger</groupId>
    <artifactId>swagger-codegen-maven-plugin</artifactId>
    <version>2.4.28</version>
</dependency>
```