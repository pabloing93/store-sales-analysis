<h1>Análisis de ventas de un E-commerce</h1>

> [!NOTE]
> Este es un proyecto que pretende analizar datos oficiales de un comercio de moda con el objetivo de impulsar las ganancias y el negocio. <br>

> [!CAUTION]
> Utilizar con fines educativos :octocat:

<h2>Problema del negocio</h2>

<table><tr><td> 
  Una tienda online de moda, con presencia en todo Brasil, necesita impulsar su rendimiento utilizando sus datos de manera estratégica. <br>
  Como científico de datos, hemos sido convocados para analizar sus datos para generar información y ofrecer insights que guíen sus decisiones y respondan al   
  contexto en el que se encuentran. <br><br>
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

Éste es el proceso más laborioso cuando obtenemos raw data y es el mas importante ya que a partir de datos legibles podemos continuar con el proyecto:

<h3>Preprocesamiento general</h3>

Un resumen de éste proceso:
1. Tratamiento de nulos y duplicados.
2. Eliminamos la columna SKU (df_productos). No aportaba información para nuestro análisis.
5. Análisis y tratamiento de los tipos de datos de las columnas.


<h2>EDA: Análisis exploratorio de los datos</h2>

<h3>Estadística Descriptiva</h3>

<p>A partir del pre-procesamiento inicial, hemos obtenido perspectivas preliminares de los datos.</p>


<h2>Conclusión</h2>
