
---
title: "Posgres en github Actions."
date: 9 de mayo del 2020
description: 'Pequeña prueba con github actions y contenedores de servicios '
---

# Gitghub actions y postgresQl


En este post te hablare sobre una fascinante función que provee GitHub Actions. Que creo esencial conocer y profundizar sobre ello. Se trata de los contenedores de servicios. Estos son contenedores que nos permiten alojar servicios como bases de datos y almacenamiento en caché. Al ser un tema tan extenso solo nos enfocaremos en la implementación del servicio de postgres.

No soy experto en esto, pero al final de este post espero poder ayudarte con tus dudas e implementar postgres dentro de tus pruebas en github actions. si ya conoces docker puedes saltarte esta breve explicación.

#### Que es un contenedor de [Docker](https://www.docker.com/)? 

Un contenedor de Docker agrupa el código de una aplicación con las dependencias y archivos de configuración necesarios, así como también puede incluir entornos de tiempo de ejecución o compiladores necesarios para que la aplicación se ejecute. Esta agrupación permite aislar nuestra aplicación y poderla ejecutar en diferentes entornos sin comprometer la compatibilidad.

![docker example]( https://i.imgur.com/9jYW7FY.png ) 

#### Que son las imágenes de docker ?

Las imágenes son plantillas construidas a partir de un dockerfile (un archivo de configuración). Que contiene las instrucciones específicas para instalar lo que necesita, como se va a ejecutar, y que es lo que va a ejecutar. Esta imagen compilada es lo que nos permitirá ejecutar un contenedor con estas especificaciones.

### Contenedores de servicios

Ahora que sabemos un poco sobre docker es más fácil entender cómo es que este servicio puede correr dentro de nuestro entorno virtual de GitHub actions. Por qué sí, estos contenedores de servicios son imágenes de docker !. Esto es bastante útil porque los workflows de GitHub actions pueden correr en diferentes entornos virtuales y de esta manera no perdemos compatibilidad. 

- [aquí puedes ver los entornos virtuales disponibles](https://github.com/actions/virtual-environments)

- [aquí puedes leer más sobre los contenedores de servicios](https://docs.github.com/es/actions/using-containerized-services/about-service-containers)

### Comencemos

haz un fork de este reposotio y clonalo en el lugar de tu preferencia: [app demo](https://github.com/MauroMontan/postgres-gh-actions-demo).

> si quieres correrlo localmente sigue las instrucciones dentro del mismo repositorio. ( No es necesario probarlo localmente )

- esta es la estructura de nuestro proyecto, te recomiendo observar cada uno de los archivos.

![project structure](https://i.imgur.com/tdtW5K3.png)

### Tests

En este punto nostros podemos ejecutar nuestras pruebas localmente, pero probar que nuestra aplicación funciona en un equipo de trabajo es muuy importante, esto nos da la confianza de que nuestra aplicación funcionará correctamente en producción. y la comunicación entre el equipo sera mejor.


##### En nuestra aplicación podremos encontrar un test para nuestro modelo y un test para saber si nuestra base de datos esta conectada correctamente.

Esta es nuestra prueba para el model del Post. su unica función es conocer el modelo esta siendo instanciado correctamente.

![post model test](https://i.imgur.com/hAFdBT5.png) 

Esta es nuestra prueba para conocer si la base de datos se encuentra conectada. 

![prisma test](blob:https://imgur.com/70d30c87-680e-4b85-8ed2-f8ac61ec47ea) 



Hasta ahora nuestros estas están corriendo correctamente localmente.

![tests passed](https://i.imgur.com/7PNaLjY.png) 


> Conoce un poco sobre la sintaxis de yaml en los workflows [aquí](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions) 
