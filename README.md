# Análisis Explotario de Datos
Análisis exploratorio de datos del suministro de agua de la Ciudad de México a octubre de 2020. Este análisis fue efectuado empleando la información de  los primeros 3 bimestres del año 2019 por el concepto de suministro de agua a nivel manzana en metros cúbicos, considerando la facturación por servicio de consumo medido y promedio otorgada por el Gobierno de la Ciudad de México y disponible [en el portal de Datos Abiertos Ciudad de México](https://datos.cdmx.gob.mx/explore/dataset/consumo-agua/information/).

Este análisis fue efecutado por el equipo de Ciencia de Datos conformado por:
* Carlos Bautista (125761)
* Enrique Ortiz (150644)
* Mario Heredia (197863)
* José Antonio Lechuga (192610)

Los requisitos para correr este análsis se encuentran en el archivo `requirements.txt`. Se sugiere
correr el siguiente comando en un nuevo ambiente virtual de python 3.7.4:
```
$ pip install -r requirements.txt
```

Los elementos de este directorio son los siguientes
 ```
eda
└───equipo_5
        requirements.txt:requerimientos de ambiente virtual de python 3.7.4 para correr el código
        agua_profiling_reporte_cliente.ipynb: notebook para generar PDF de reporte
        agua_profiling_reporte_cliente.pdf: reporte en versión PDF para el cliente
        agua_profiling_expo.ipynb: notebook de todos los análisis efectuados
        exposicion_equipo_5.pdf: slideck de exposición de trabajo
        profiling_cliente.html
```

Estos tienen el siguiente significado:

* **requirements.txt:**requerimientos de ambiente virtual de python 3.7.4 para correr el código
* **agua_profiling_reporte_cliente.ipynb:** notebook para generar PDF de reporte
* **agua_profiling_reporte_cliente.pdf:** reporte en versión PDF para el cliente
* **agua_profiling_expo.ipynb:** notebook de todos los análisis efectuados
* **exposicion_equipo_5.pdf:** slideck de exposición de trabajo
* **profiling_cliente.html:** profiling generando por `pandas_profiling` de las variables después de la limpieza