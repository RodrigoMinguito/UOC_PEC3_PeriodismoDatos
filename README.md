# Periodismos de datos - PEC 3 - Rodrigo Minguito Linaje
## Objetivos:

 - Conseguir datos
 - Aplicar mecanismos de selección y filtrado de los datos
 - Utilizar descriptores estadísticos típicos
 - Extraer características
 - Encontrar el hilo argumental a partir del análisis de los datos

## Origen de datos
He ido recorriendo los datos indicados en los comentarios de la propuesta en la PEC2, y siguiendo enlaces. Finalmente, he recogido en el directorio __csv__ los siguientes datos:

Human Development Data - HDI (http://hdr.undp.org/en/data), descargado como csv

Global Peace Index - GPI (https://en.wikipedia.org/wiki/Global_Peace_Index), descargado y guardado como csv

Datos de Desarrollo Mundial del Banco Mundial (https://datos.bancomundial.org/indicador?tab=all), descarga individualizada del fichero comprimido y extracción del csv con los datos. Estos ficheros tienen la ventaja de mantener una interfaz idéntica entre ellos, lo que facilita el tratamiento y análisis. Más concretamente, he descargado para analizar los siguientes indicadores:
 - Médicos (por cada 1.000 personas)                                        
 - Esperanza de vida al nacer                                               
 - Número de muertes de menores de 5 años                                   
 - Población de 65 años de edad y más, total                                
 - Brecha de pobreza a $1,90 por día (2011 PPA) (%)                         
 - Incidencia de tuberculosis (por cada 100.000 personas)                   
 - Acceso a la electricidad BRCS (% de población)                           
 - Consumo de energía renovable (% del consumo total)                       
 - Acceso a tecnologías limpias para cocinar (% población)                  
 - Gasto de consumo final de los hogares (US$ a precios actuales)           
 - Ratio niñas/niños en educación primaria y secundaria                     
 - Turismo internacional, número de arribos BRCS                            
 - Turismo internacional, gastos (US$ a precios actuales)                   
 - Inversión extranjera directa, entrada neta de capital (% del PIB)        
 - Gasto en investigación y desarrollo (% del PIB)                          
 - Exportaciones alta tecnología (% de exportaciones manufacturadas)        
 - Índice de valor de exportación (2000 = 100))                             
 - Desempleo, mujeres (% de la población activa femenina) (OIT)             
 - Desempleo, hombres (% de la población activa masculina) (OIT)            
 - Desempleo, total (% de la población activa total) (OIT)                  
 - Jóvenes sin educación, empleo ni capacitación (% total jóvenes)          
 - Suscripciones a banda ancha fija (por cada 100 personas)                 
 - Suscripciones a teléfono móvil (por cada 100 personas)                   
 - Personas que usan Internet (% de la población)                           

He descargado más ficheros de índices del Banco Mundial (Brecha de Género, uso de anticonceptivos, población en tugurios...) pero no era factible su análisis al no contener valores para alguno de los países en alguno de los años. Estos ficheros están en el directorio __no__

Así mismo, he descartado otros índices acumulados, como BLI o SPI porque no suministran datos previos a hace cinco años.

Los ficheros están almacenados en el directorio csv y su análisis se lleva a cabo con el fichero __pec3.Rmd__. El resultado estadístico puro está disponible en los ficheros __Informe.html__ (ver instrucciones para visualizarlo más adelante) e __Informe.pdf__

### Contacto con experto

He contactado con Francesc González, (https://www.uoc.edu/webs/fgonzalezre/ES/curriculum/index.html) doctor en Geografía por la UAB y profesor de los Estudios de Economía y Empresa de la UOC, que hace análisis de impacto de eventos. La comunicación que mantengamos estará disponible en el fichero __contactoFrancesc.txt__


## Trabajo estadístico

### HDI y GPI
Una vez descargados los ficheros de los índices HDI y GPI he procedido a representar los valores de cada uno de los países gráficamente, incluyendo la recta de regresión, a la espera de ver cambios de tendencias a partir del año en el que tiene lugar el evento. También he representado a otros países que comparten características con los BRCS.

### Datos del Banco Mundial
En primer lugar he tenido que limpiar y adaptar los datos:
 - Para los países a analizar, cuando no existían datos para un año he rellenado el valor con el promedio de valores de ese rango.
 - Para calcula el promedio mundial he usado los países que tienen datos para ese año

Posteriormente, para llevar este análisis para los índices he desarrollado una función que muestra tres gráficas y una tabla. 

La _primera gráfica_ contiene la evolución del índice para los cuatro países BRCS, representando las rectas de ajuste usando los puntos anteriores (línea punteada) y puntos posteriores (línea continua)
La _segunda gráfica_ representa los mismo que la anterior, pero para el promedio los países que serían candidatos al grupo BRCS (India, México, Corea del Sur y Argentina)
La _tercera gráfica_ muestra lo mismo, pero usando el promedio de todos los países del mundo, excluyendo a los BRCS.

El objetivo de estas gráficas es visualizar cambios de tendencias que tengan como punto de ruptura el año del evento.

La _tabla_ constituye una visualización numérica, y con indicadores de color, de las características de las gráficas. Para cada uno de los BRCS muestra dos rangos de años (2000-evento y evento-2017) y detalla primeramente cual era la tendencia de ese periodo (obtenida a partir de la pendiente de la recta de ajuste) y después indica cómo de parecida es la distribución en ese rango respecto a los países candidatos a BRCS y respecto al promedio mundial.

Con la tabla, además de visualizar más rápido los cambios de tendencia que se veían en las gráficas se puede ver también si el país pasa a comportarse de una manera distinta a como lo hace la mayoría.

#### Ejemplificación

Todo esto parece algo enrevesado, así que lo explicaré con un ejemplo, usando los ficheros adjunto __EjGraficas.PNG__ y __EjTablas.PNG__.

![Ejemplo Graficas](/EjGraficas.PNG)

En __EjGraficas.PNG__ puede verse, por ejemplo para Brasil que la tendencia de % de mujeres paradas era descendente (línea verde discontinua), y a partir de su evento se vuelve ascendente (línea verde continua).

![Ejemplo Tablas](/EjTablas.PNG)

En __EjTablas.PNG__, para Brasil, hay dos rangos, 2000-2014 y 2014-2017. La tendencia, como ya se ha visto en el gráfico es negativa (decreciente) en el primer rango y positiva en el segundo. 

Si ahora lo comparo con los países candidatos a BRCS observo que en el primera rango se comportaba como ellos (coeficiente de correlacion > 0.7) y en el segundo rango se comporta de una forma diferentes (correlacion < 0.7).

Si la comparación se hace ahora contra el resto de países del mundo no BRCS, se observa que en el primer rango no se comportan de forma semejante, y que en el segundo se comportan de una forma inversa (correlacion < -0.7), esto es, de 2000 a 2014 se comportaba de una forma diferente y de 2014 a 2017 se comporta de una forma totalmente contraria, ya que mientras ellos disminuyen él aumenta.

### Instrucciones para ver el fichero de informe
El fichero, desde el visor de github no es legible.
Para poder visualizarse apropiadamente debe descargarse en el equipo y abrirse de nuevo. 
Por si este procedimiento no funciona, almaceno también el fichero en formato pdf

## Características

## Hilo Argumental

