# Tests de cobertura y el resto.


## Planteamiento

La calidad en el software es un tema bastante extenso, que incluye tanto técnicas específicas como herramientas en cada uno de los niveles. Hasta ahora hemos tratado de exlicar, de forma práctica, estas herramientas y técnicas; en la última sesión veremos a un nivel un poco más teórico técnicas y conceptos adicionales usuales en este área. También veremos, a nivel práctico, los tests de cobertura y cómo usarlos desde diferentes lenguajes.

## Al final de esta sesión

Se habrá terminado el proyecto, incluyendo tests de integración, y se habrá creado una hoja de ruta para abarcar todos los demás aspectos que necesite.

## Criterio de aceptación

El repositorio tiene que estar corriendo los tests en Travis, y esos
tests deben pasar. Estos tests deben incluir tests de integración.

## Tests de cobertura

Los tests de cobertura miden qué parte de nuestro código está cubierta por los tests unitarios (que, recordemos, son de caja blanca). Estos tests de cobertura funcionan tanto a nivel de línea, como de función o de paquetes, pero generalmente van a dar un porcentaje de líneas cubiertas por los tests unitarios.

Dependiendo del lenguaje, se hará con unas herramientas u otras. En Go, por ejemplo, es parte de la instrumentación del propio lenguaje.

```
go test -coverprofile=coverage.out
go tool cover -html=coverage.out
```

La primera ejecuta los tests y genera un fichero de salida, y la segunda orden abre un navegador con una página en la que nos muestra nuestro código y la cobertura que tiene, señalando las funciones que no están cubiertas. Sobre la clase [`HitosIV`que ya hemos usado anteriormente](https://github.com/JJ/HitosIV), estos serían los resultados.

![Cobertura de los tests en la clase HitosIV](img/gocover.png)

																															    En este caso, las  líneas no cubiertas lanzan errores en caso de que se encuentren algún problema. No hay que cubrir el 100% de las eventualidades (por ejemplo, generar un JSON erróneo a ver si salta la segunda), pero quizás la primera sí merece la pena que se cubra, así que se añade un test adicional, pero debemos [modificar ligeramente el código](https://stackoverflow.com/a/46841524/891440) para asegurar que sigue las mejores prácticas del lenguaje:


![Nueva cobertura de los tests en la clase HitosIV](img/gocover-2.png)

Siempre es mejor en Go devolver un error que enviar a log un error fatal, así que este cambio en el código asegura que se pueda cubrir mejor con los tests.

> Y también demuestra que la calidad en el desarrollo no es siempre cuestión de escribir más o menos tests, sino de seguir buenas prácticas en el diseño de aplicaciones para que estos tests sean posibles y tengan la máxima cobertura.

## Actividad


Hito final del proyecto, con toda la funcionalidad deseada al principio añadida, tests unitarios y de cobertura con una cobertura aceptable, y una hoja de ruta para añadir pruebas de calidad a todos los niveles de ahora en adelante.