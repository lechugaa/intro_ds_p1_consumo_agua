---
slideOptions:
  theme: white
  transition: slide
  controls: true
  progress: true
  slideNumber: true
---

# EDA suministro de agua de la CDMX

Octubre 2020 

**Equipo 5:**
* Carlos Bautista (125761)
* Enrique Ortiz (150644)
* Mario Heredia (197863)
* José Antonio Lechuga (192610)

---

<!-- .slide: style="font-size: 40px;" -->

# Contenido

1. Exploración inicial
1. Limpieza y manipulación de datos
1. Detección de errores en los datos
1. Datos faltantes
1. Comportamiento del consumo bimestral
1. Estudio de alcadías y colonias
1. Estudio de consumo total
1. Estudio de consumo promedio
1. Características de los datos para la definición de un modelo


---

# Exploración inicial

----

## ¿Cuántas variables existen? ¿Cuántas observaciones existen?

Contamos con 71,102 observaciones para 17 variables

----

<!-- .slide: style="font-size: 18px;" -->

## ¿Cuántas observaciones únicas se tienen por variables?


|       Variable       | Observaciones únicas |
|:--------------------:|:--------------------:|
|       Geo Point      |        22,930        |
|       Geo Shape      |        22,922        |
|  consumo_total_mixto |        24,339        |
|         anio         |           1          |
|        nomgeo        |          17          |
|   consumo_prom_dom   |        52,060        |
|   consumo_total_dom  |        47,051        |
|       alcaldia       |          16          |
|        colonia       |         1,340        |
|  consumo_prom_mixto  |        31,911        |
|     consumo_total    |        56,015        |
|     consumo_prom     |        62,214        |
|  consumo_prom_no_dom |        37,440        |
|       bimestre       |           3          |
| consumo_total_no_dom |        27,336        |
|          gid         |        71,102        |
|      indice_des      |           4          |

----

## ¿Cuántas variables numéricas existen?

<!-- .slide: style="font-size: 25px;" -->

|       Variable       | Tipo de dato |
|:--------------------:|:------------:|
|  consumo_total_mixto |    float64   |
|         anio         |     int64    |
|   consumo_prom_dom   |    float64   |
|   consumo_total_dom  |    float64   |
|  consumo_prom_mixto  |    float64   |
|     consumo_total    |    float64   |
|     consumo_prom     |    float64   |
|  consumo_prom_no_dom |    float64   |
|       bimestre       |     int64    |
| consumo_total_no_dom |    float64   |
|          gid         |     int64    |


Tenemos 11 variables numéricas

----

## ¿Cuántas variables de fecha tenemos?

No existe ninguna variable de tipo fecha

----

## ¿Cuántas variables categóricas existen

Las siguientes pueden ser consideradas variables categóricas: 
* `nomgeo`
* `alcaldia`
* `colonia`
* `indice_des`

----

## ¿Cuántas variables de texto hay?

No tenemos variables que como tal contengan texto a analizar (como palabras u oraciones)

---

# Limpieza y manipulación de datos

Para realizar una limpieza de los datos, se realizaron las siguientes actividades

----

* Transformación del nombre de las columnas a formato estándar
* Estandarizamos los valores de las variables
    * `alcaldia`
    * `colonia`
    * `indice_des`
    * `nomgeo`

----

* Agregar las variables `latitud` y `longitud` generadas a partir de `geo_point`
* Transformar la variables `latitud` y `longitud` a numéricas
* Eliminar la columna `geo_point`
* Eliminar la columna `geo_shape`

----

* Sustituir los valores de `nomgeo` donde se escribió "Talpan" en lugar de "Tlalpan"
* Homogenizar los valores de `nomgeo` y `alcaldia` sustituyendo en `nomgeo` 
    * La Magdalena Contreras -> Magdalena Contreras
    * Cuajimalpa de Morelos -> Cuajimalpa 

---

# Detección de errores

* ¿Existen consumos negativos?
* ¿Existen valores igual a cero para el consumo?
* ¿Existen observaciones donde la suma de los consumos no equivalga al consumo total?
* ¿Existen observaciones donde el total de tomas de agua no sea la suma de los 3 tipos de tomas?

----

No existen datos de consumos negativos

----

<!-- .slide: style="font-size: 25px;" -->

| Tipo de consumo               | Porcentaje de consumos igual a cero|
|-------------------------------|------------|
| Consumo total mixto           | 24.9       |
| Consumo promedio mixto        | 24.9       |
| Consumo total doméstico       | 13.9       |
| Consumo promedio doméstico    | 13.9       |
| Consumo total no doméstico    | 11.4       |
| Consumo promedio no doméstico | 11.4       |
| Consumo total                 | 3.4        |
| Consumo total promedio        | 3.4        |

----

<!-- .slide: style="font-size: 25px;" -->

Debido a que el consumo total (i.e. `consumo_total`) se calcula como la suma de los consumos:
* mixto
* doméstico
* no doméstico

se comprobó el número de observaciones que divergían de dicho cálculo obteniendo los siguientes resultados:

* 0 observaciones divergen al nivel de unidades
* 6 observaciones divergen al nivel de décimas
* 149 observaciones divergen al nivel de centésimas

----

<!-- .slide: style="font-size: 25px;" -->

Considerando a los consumos promedios como:

$$ consumo\_promedio = \frac{consumo\_total}{no\_tomas} $$

Se comprobó que el número total de tomas equivalga a la suma de las tomas de agua domésticas, no domésticas y mixtas obteniendo los siguientes resultados:

* En 5,650 observaciones el número de tomas (medidores) de agua no cuadran
* Estos representan el 9.1% de las observaciones sin datos faltantes

----

<!-- .slide: style="font-size: 25px;" -->

| Diferencia en tomas | No observaciones | Fracción |
|:----------------------:|:----------------:|:--------:|
|           0.0          |       56,564      |   90.9   |
|           1.0          |       4,742       |    7.6   |
|           2.0          |        707       |    1.1   |
|           3.0          |        139       |    0.2   |
|           4.0          |        34        |    0.1   |
|           5.0          |        16        |    0.0   |
|           6.0          |         1        |    0.0   |
|           7.0          |         6        |    0.0   |
|           8.0          |         3        |    0.0   |
|          16.0          |         2        |    0.0   |

---

# Data profiling

* Datos faltantes
* Comportamiento bimestral del consumo

----

## Datos faltantes

<!-- .slide: style="font-size: 14px;" -->
Los datos faltantes corresponden a variables de algún tipo de consumo, en particular:

 ID | Variable | Total| Porcentaje |
| --- | --- | --- | --- |
| 1 | consumo_total_mixto | 8,327 | 11.7 |
| 2 | consumo_prom_mixto | 8,327 | 11.7 |
| 3 | consumo_total_dom | 4,820 | 6.8 |
| 4 | consumo_prom_dom | 4,820 | 6.8 |

Recordamos que: 

$$consumo\_total = consumo\_total\_dom + consumo\_total\_no\_dom + consumo\_total\_mixto$$

Comprobamos que los datos faltantes corresponden a manzanas donde no existe ese tipo de consumo específico.

----

## Comportamiento bimestral del consumo

<!-- .slide: style="font-size: 14px;" -->
**¿Existen diferencias considerables entre el consumo por bimestre?** 

Exploramos por alcaldía, para el consumo total

![](https://i.imgur.com/p2jBFrP.png)

----

<!-- .slide: style="font-size: 14px;" -->

... y para el consumo promedio:

![](https://i.imgur.com/U7gOURa.png)

----

<!-- .slide: style="font-size: 14px;" -->

Hacemos el mismo procedimiento para el consumo total pero desagregado por índice de desarrollo:

![](https://i.imgur.com/syt6gxJ.png)

----

<!-- .slide: style="font-size: 14px;" -->

... y observamos que también el comportamiento es similar para el consumo promedio:

![](https://i.imgur.com/wUgPs09.png)


---

<!-- .slide: style="font-size: 35px;" -->

# Estudio de alcaldías y colonias en la CDMX

* ¿Cuántas alcaldías existen?
* ¿Se tienen números de observaciones similares para cada alcadía?
* ¿Cuántas colonias diferentes existen?
* ¿Cuántas colonias se tienen por alcaldía?
* ¿Coincide este dato con los datos oficiales?
* ¿Cuantás colonias existen por índice de desarrollo?

----

Existen 16 alcaldías diferentes

----

![](https://i.imgur.com/AbGsjDh.png)

----

Se encontraron en el set de datos 1,340 colonias

----

![](https://i.imgur.com/0Cokdln.png)

----

<!-- .slide: style="font-size: 20px;" -->


|       Alcaldía      | Colonias | Colonias Reales | Fracción |
|:-------------------:|:--------:|:---------------:|:--------:|
|    Álvaro Obregón   |    188   |       249       |   76.0   |
|     Azcapotzalco    |    88    |       111       |   79.0   |
|    Benito Juárez    |    53    |        64       |   83.0   |
|       Coyoacán      |    96    |       153       |   63.0   |
|      Cuajimalpa     |    39    |        43       |   91.0   |
|      Cuauhtémoc      |    35    |        64       |   55.0   |
|  Gustavo A. Madero  |    167   |       232       |   72.0   |
|      Iztacalco      |    38    |        55       |   69.0   |
|      Iztapalapa     |    193   |       293       |   66.0   |
| Magdalena Contreras |    38    |        52       |   73.0   |
|    Miguel Hidalgo   |    86    |        88       |   98.0   |
|      Milpa Alta     |    33    |        12       |   275.0  |
|       Tláhuac       |    70    |        58       |   121.0  |
|       Tlalpan       |    130   |       178       |   73.0   |
| Venustiano Carranza |    67    |        80       |   84.0   |
|      Xochimilco     |    90    |        80       |   112.0  |

----

![](https://i.imgur.com/cZdlrJv.png)

----

| Índice de desarrollo | Número de colonias |
|:--------------------:|:------------------:|
|         Alto         |         512        |
|         Medio        |         558        |
|        Popular       |        1,124        |
|         Bajo         |         958        |

![](https://i.imgur.com/JSwlJLM.png)

---

## Consumo total

##### Consumo doméstico + Consumo no doméstico + Consumo mixto





----


##### Consumo total por alcaldía e índice de desarrollo

<style>
.reveal section img { background:none; border:none; box-shadow:none; }
</style>

![](https://i.imgur.com/zKeWRgp.png =400x)

----

### Consumo total por índice de desarrollo

#### Boxplot
![](https://i.imgur.com/wNNKDnl.png)




----

#### Histograma

![](https://i.imgur.com/oTnouVO.png)


----

### Consumo total por alcaldía en $m^3$

![](https://i.imgur.com/npcmJbB.png =550x)


----

#### Tipo de consumo

###### Por alcaldía

![](https://i.imgur.com/ycDZ5Zl.png =400x)

----

### Por índice de desarrollo

![](https://i.imgur.com/GN8xPJR.png)


---

## Consumo promedio por bimestre. 



En promedio, ¿cómo se comporta el promedio de consumo?


----



### Consumo promedio doméstico

![Consumo promedio](https://i.imgur.com/e1e0ESn.png)


----

### Consumo promedio no doméstico

![Consumo Promedio No Doméstico Corregido](https://i.imgur.com/KIWshqQ.png)

----

### Consumo promedio mixto

![Consumo Promedio Mixto Final](https://i.imgur.com/eNUhUwb.png)




----

### Algunas alcaldías son líderes, otras no.
<!-- .slide: style="font-size: 18px;" -->
> 
| Alcaldía | Ranking Doméstico | Ranking No Doméstico| Ranking Mixto |
| --- | --- | --- | --- |
| Miguel Hidalgo | 1| 2 |  2 |
| Álvaro Obregón | 2| 5 |  5 |
| La Magdalena Contreras | 3| 8 | 11 |
| Cuajimalpa de Morelos | 4| 3 |  3 |
| Azcapotzalco | 5| 7 |  7 |
| Iztacalco| 6| 11 |  8 |
| Venustiano Carranza | 7| 12 |  6 |
| Gustavo A. Madero | 8| 10 |  9 |
| Coyoacán | 9| 6 |  10 |
| Tlalpan | 10| 1 |  12 |
| Cuauhtémoc | 11| 4 |  1 |
| Benito Juárez | 12| 9 |  4 |
| Xochimilco | 13| 14 |  14 |
| Iztapalapa| 14| 13 |  13 |
| Tláhuac | 15| 16 |  15 |
| Milpa Alta | 16| 15 |  16 |

----

### Esta fue su distribución de bimestre a bimestre

![Dist Bim](https://i.imgur.com/xQ1fJgY.png)




----

## Distribución de consumo promedio por índice de desarrollo





----

### Consumo promedio doméstico

![Consumo Promedio Dom Box Plot](https://i.imgur.com/lny8K01.png)

----

### Consumo promedio no doméstico

![Consumo Promedio no Dom Box Plot](https://i.imgur.com/SsbzrNt.png)

----

### Consumo promedio mixto

![Consumo Promedio Mixto Box Plot](https://i.imgur.com/2fFfuAE.png)


---

# Características de los datos para definición de un modelo

<!-- .slide: style="font-size: 18px;" -->
Se realizaron gráficas de dispersión con coloración por índice de desarrollo para determinar si con las variables originales se podía obtener una segmentación de las categorías.

Todas las gráficas realizadas (a excepción de latitud contra longitud que se muestra más adelante) no lograron este propósito. Un ejemplo del resultado típico de muestra a continuación:

----

<!-- .slide: style="font-size: 14px;" -->
Como es posible observar, no existe una segmentación adecuada de las categorías de índice de desarrollo. 

![](https://i.imgur.com/gm4hirI.png)


(Las demás gráficas se omiten para evitar aglomerar el reporte).

----

<!-- .slide: style="font-size: 14px;" -->
El único caso de parcial éxito es la gráfica de longitud contra latitud que se muestra a continuación:

![](https://i.imgur.com/sYLzWTX.png)

----

## Consideraciones finales

<!-- .slide: style="font-size: 18px;" -->

La información **no** es suficiente ni completa para generar un modelo correcto para predecir el índice de desarrollo.

Nos gustaría contar con información adicional como número de tomas, tarifa promedio y población por manzana. 

En general se concluye que:
* Las variables con las que contamos no permiten una segmentación de los datos
* Es conveniente tener datos de población por manzana para perfilar el tipo de consumo per cápita
* Las gráficas de cajas y brazos demuestran que las distribuciones son más o menos similares y no hay patrones evidentes con los datos con los que se cuentan
* Es relevante contar con más contexto.
 

---

¡Gracias! 

![PIE](https://i.imgur.com/Js8lyZO.png)
