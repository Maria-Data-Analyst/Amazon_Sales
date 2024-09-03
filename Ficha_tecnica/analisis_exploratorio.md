# Análisis Exploratorio

En esta sección, conectaremos la tabla consolidada, ya procesada y limpia del procedimiento anterior, a Looker Studio y a un nuevo notebook. Esto nos permitirá generar gráficos y realizar un análisis más detallado de los datos.

## Distribución de Variables

Comenzaremos observando la distribución de las variables mediante histogramas:

![Histograma de Variables](https://github.com/user-attachments/assets/e46cf379-e304-4440-a10e-9843955f4c27)

A partir de los histogramas, podemos observar varios sesgos en diferentes variables. Sin embargo, no aplicaremos tratamiento de outliers debido a la amplia gama de productos, que varían considerablemente en precio, porcentaje de descuento y precio con descuento final. 

En particular:
- **Rating**: Solo puede variar de 0 a 5. No se observan valores fuera de este rango, por lo que no tenemos datos atípicos en esta variable.
- **Porcentaje de Descuento**: Ningún valor supera el 100% ni es menor a 0%, por lo que tampoco identificamos datos atípicos en esta métrica.

## Medidas de Tendencia Central 

![image](https://github.com/user-attachments/assets/f03d8c64-fb2f-4fba-a2f1-f595d172a997)

* Electronics muestra la mayor desviación estándar en actual_price (16,018.77), indicando una amplia gama de precios en esta categoría. Esto puede deberse a la inclusión de productos de diferentes segmentos de precio, desde artículos económicos hasta productos de alta gama.tiene el precio máximo más alto (139,900) y un precio promedio alto (10,294.12), lo que sugiere que esta categoría incluye productos de muy alto valor.
Home&Kitchen también muestra una desviación estándar considerable (6,808.87), aunque es menor que la de Electronics. La variabilidad en esta categoría es notable pero no tan extrema.
Electronics tiene el precio máximo más alto (139,900) y un precio promedio alto (10,294.12), lo que sugiere que esta categoría incluye productos de muy alto valor.
Home&Kitchen también tiene un precio máximo considerable (75,990) pero un promedio mucho más bajo (4,165.79), lo que puede indicar que la mayoría de los productos son más asequibles comparados con Electronics.
OfficeProducts muestra precios más bajos en comparación con Electronics y Home&Kitchen, con un máximo de 2,999 y un promedio de 397.19.
