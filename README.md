<h1>Análisis de ventas de un E-commerce</h1>

> [!NOTE]
> Este es un proyecto que pretende analizar datos oficiales de un comercio de moda con el objetivo de impulsar las ganancias y el negocio. <br>

> [!CAUTION]
> Utilizar con fines educativos :octocat:

<h2>Problema del negocio</h2>

<table><tr><td> 
  <p align="justify">Una tienda online de moda, con presencia en todo Brasil, necesita impulsar su rendimiento utilizando sus datos de manera estratégica. </p><br>
  <p align="justify">Como científico de datos, hemos sido convocados para analizar sus datos para generar información y ofrecer insights que guíen sus decisiones y respondan al contexto en el que se encuentran. <br><br>
</td></tr></table>

<h2>Stack de tecnologías</h2>

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54) ![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white) ![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=for-the-badge&logo=numpy&logoColor=white) ![Matplotlib](https://img.shields.io/badge/Matplotlib-%23ffffff.svg?style=for-the-badge&logo=Matplotlib&logoColor=black)

![SQLite](https://img.shields.io/badge/SQLite-07405E?style=for-the-badge&logo=sqlite&logoColor=white)

<h2>Configuración del ambiente</h2>

> [!IMPORTANT] 
> Se requiere importar las siguientes tecnologías librerías para poder trabajar con el proyecto
> ```
> import geobr
> import pandas
> import numpy
> import matplotlib
> import seaborn
> import tabulate
> import requests
> from io import BytesIO
> from sqlalchemy import create_engine, MetaData, Table, inspect, text
> global df_items_pedidos, df_pedidos, df_productos, df_vendedores, database
> ```

<h2>Pre-procesamiento de los datos</h2>

<p align="justify">Éste es el proceso más laborioso cuando obtenemos raw data y es el mas importante ya que a partir de datos legibles podemos continuar con el proyecto:</p>

<h3>Preprocesamiento general</h3>

Un resumen de éste proceso:
1. Eliminamos la columna "sku"
2. Eliminamos los registros que no tengan un vendedor o producto conocido, a pedido de nuestro cliente que indico que no desea ningun dato de tipo desconocido
3. Cambiamos los tipos de datos de algunas columnas
4. Eliminamos duplicados

<p align="justify">Para el dataframe_vendedores se encontro que existe una venta de un producto por el valor de U$D780 que corresponde al vendedor 'Unknown'. Por motivos de información relacionada a las ganancias y ventas optamos por no eliminar el vendedor 'Unknown'. Se asume que podría ser un vendedor que ya no existe o se olvidó registrar su nombre y se procedio a explicar la situación al cliente para que decidiera qué medidas tomar y se concluyo que no era de vital importancia esta información, por tanto se elimino el registro que hace referencia a este vendedor con el fin de realizar análisis posteriores sin preocuparnos por esta información.</p>

![registros de vendedores](https://github.com/pabloing93/store-sales-analysis/assets/146877817/3a9e591b-e310-4b42-bafa-509df56526ba)

![registros del vendedor unknown](https://github.com/pabloing93/store-sales-analysis/assets/146877817/4b31a2d1-07e2-4e1d-ac04-52d86bbf7381)


<h2>EDA: Análisis exploratorio de los datos</h2>

<p align="justify">A partir del pre-procesamiento inicial, hemos obtenido perspectivas preliminares de los datos.</p>

<h3>Relaciones entre los datos</h3>
<p align="justify">A través de éste análisis nuestro objetivo fué el comprender qué datos teníamos y cómo se relacionan entre ellos para entender el alcance de la información que podíamos llegar a generar. </p>

![Captura de pantalla de 2024-04-07 21-16-32](https://github.com/pabloing93/store-sales-analysis/assets/32267303/8ff26311-b218-4e7f-bfd2-064625cc60f1)

<p align="justify">Además, detectamos información redundante y no escencial de la cual prescindimos para simplificar el proceso de EDA.</p>

![Captura de pantalla de 2024-04-07 21-18-11](https://github.com/pabloing93/store-sales-analysis/assets/32267303/a5ac39b5-74d9-44f7-abbf-8894301b4868)



<h2>Conclusión</h2>

<p align="justify">Como podemos observar en las imagenes, eliminamos las redundancias encontradas, se elimino la columna producto_id de la tabla df_pedidos y ahora la tabla no se encuentra conectada con la tabla df_productos. En segundo lugar se elimino de la tabla df_pedidos la columna total, ya que esta la podemos encontrar con el nombre de valor_total en la tabla df_items_pedidos, y de esta ultima tabla eliminamos la columna id_recibo, ya que esta información no guarda realación con ninguna otra tabla dentro de la BD.</p>

<p align="justify">En cuanto la información obtenida a través del EDA podemos destacar lo siguiente:</p>


1. <p align="justify">Se encontro en columna total de df_pedidos, la cual hace referencia a la misma columna valor_total en la df_items_pedidos que tenemos outliers dentro de nuestros datos, pero cuando analizamos de cerca la situación nos encontramos que no son outliers hablando estrictamente desde el punto de vista tecnico y estádistico, ya que esta por fuera de los valores normales, sin embargo el caso de estaduio es sobre venta de ropa, donde existen disferentes tipos de marcas, de las cuales algunas son muy costosos, por lo cual no es raro observar que se registraran ventas por montos tan grandes, en las siguientes imagenes podemos observar ambas gráficas boxplot de ambas columnas donde observamos que son iguales.</p>

![Valor_total](https://github.com/pabloing93/store-sales-analysis/assets/146877817/d036db56-a070-4b3d-90ec-7700a7e49d97)

![Total](https://github.com/pabloing93/store-sales-analysis/assets/146877817/80c967d6-e1dc-4942-ae59-128e8c081193)

  * <p align="justify">Tambien podemos observar que tecnicamente hablando existen outliers en las columnas valor unitario y costo_envio, pero esto va acorde con la información que se maneja en este tipo de negocios, donde si observamos existen productos o prendas de ropa con valores hasta por encima de  6000 Reales brasileños lo cual es normal, tendiendo que hablamos de marcas de ropa, y los costos de envios es normal que a sean igual de altos ya que hablamos que muchas veces estos están relacionado o van acorde al valor total de la prenda, al tener compras de más de 10k-40k de Reales Brasileños es normal ver costos de envios elevados </p>

    ![valor_unitario](https://github.com/pabloing93/store-sales-analysis/assets/146877817/9e556716-134c-417a-abfa-1cdc641f8490)
    ![costo_envio](https://github.com/pabloing93/store-sales-analysis/assets/146877817/f72a89cd-b238-4e64-b043-750a1b0d1036)


2. <p align="justify">Dentro del resto de información no encontramos valores insuales, todos los productos estaban bien identificados, no habían valores en blanco. Dentro de los productos hay 3 caegorías los son usados que representan la mayoría, los que están nuevos pero con etiquetas y por ultimo los que están nuevos pero sin etiquetas</p>

![Condición productos](https://github.com/pabloing93/store-sales-analysis/assets/146877817/81ef54f4-079d-4377-8b16-e8e6cd83aba9)

<h2>INSIGHTS</h2>

<h3>Pregunta 1: ¿Cual es el Top 5 productos más vendidos históricamente?</h3>

![Top 5 productos más vendidos históricamente](https://github.com/pabloing93/store-sales-analysis/assets/146877817/f85ecbc6-9a5c-46ec-b6da-dd9adc022767)

<h4>Conclusión</h4>

<p align="justify">Históricamente, el producto más vendido es la Saia Midi Cinto, que es una falda que incluye un cinturón, con 549 ventas. A pesar de ser el producto más vendido, el producto Vestido Nude Reta, es el que consiguió mayores ingresos con $301,000 </p>

<h3>Pregunta 2: ¿Cual es la evolución histórica de las ingresos netos?</h3>

![Evolución histórica de los ingresos netos](https://github.com/pabloing93/store-sales-analysis/assets/146877817/ddd0896b-e600-4524-983c-ade45df4cb8c)

<h4>Conclusión</h4>

<p align="justify">El análisis de los ingresos netos históricos muestra un valor promedio de $80 mil de ingresos netos diarios desde el 2020.</p>

<p align="justify">También podemos visualizar un histórico que el día 24 Nov del 2019, se reportó un ingreso neto de $289mil generado por la venta de algunas marcas famosas.</p>

<h3>Pregunta 3: ¿Cuáles son los ingresos netos por vendedor por año?</h3>

![Ingresos Netos por vendedor y año](https://github.com/pabloing93/store-sales-analysis/assets/146877817/d340c915-2a02-4b59-ae9a-e96cd9078a68)

<h4>Conclusión</h4>

<p align="justify">Podemos destacar a los vendedores Daniel y Ana, quienes aumentaron considerablemente sus ingresos netos hasta $5M en el 2020. Mientras que los vendedores Nadia y Millena, crecieron también hasta $4M en el 2020, el vendedor Paulo muestra una tendencia a la baja que debe ser acompañada de cerca.</p>

<h3>Pregunta 4: ¿Cuáles son las ciudades que proporcionan mayores ingresos netos?</h3>

![Ingresos netos por ciudad en Brasil](https://github.com/pabloing93/store-sales-analysis/assets/146877817/406a7924-392a-4a1a-b09d-5c3b481b0462)

<h4>Conclusión</h4>

<p align="justify"> Alagoas y  Pernambuco son las 2 ciudades con mayores ingresos con R$ 1.5 M respectivamente.</p>

<p align="justify"> Sin embargo, la ciudades de Mato Grosso do sul con R$ 1.2 M y Acre con R$ 1.15 M son las 2 ciudades que menores ventas realizaron</p>


