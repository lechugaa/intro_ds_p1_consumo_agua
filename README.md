# intro_ds_p1_consumo_agua
Análisis exploratorio de datos del suministro de agua de la Ciudad de México a septiembre de 2020. Este análisis fue efectuado empleando la información bimestral por el concepto de suministro de agua a nivel manzana, considerando la facturación por servicio de consumo medido y promedio otorgada por el Gobierno de la Ciudad de México y disponible [en el portal de Datos Abiertos Ciudad de México](https://datos.cdmx.gob.mx/explore/dataset/consumo-agua/information/). 

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

Para poder  correr el análisis sin modificaciones del código, es necesario agregar el archivo `consumo-agua.csv` en el siguiente directorio:
```
intro_ds_p1_consumo_agua
└───datos
        consumo-agua.csv
```

Los análisis efectuados por *pandas profiling* estarán disponibles en el siguiente directorio:
 ```
intro_ds_p1_consumo_agua
└───reportes
        profiling_final.html
        profiling_inicial.html
```
