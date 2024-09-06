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

En esta sección, calculamos las medidas de tendencia central para la variable `actual_price` por categoría.

![image](https://github.com/user-attachments/assets/81301a85-fb6b-4ce1-a104-b4c0e27a390f)

Observamos que algunas categorías tienen menos de 5 productos, por lo que no se incluirán en este análisis. A continuación, se presenta una visualización de histogramas de `actual_price` para cada categoría:

![Captura de pantalla 2024-09-03 135054](https://github.com/user-attachments/assets/08a3e21a-261d-469b-87cc-3f674412e09d)

Se pueden observar valores extremadamente altos que podrían afectar las medidas de tendencia central. Por lo tanto, se excluirán estos valores atípicos para el análisis. Los límites establecidos son:

- **Electronics:** Menores a 80,000
- **Home&Kitchen:** Menores a 20,000
- **Computers&Accessories:** Menores a 10,000
- **OfficeProducts:** Menores a 1,000

![image](https://github.com/user-attachments/assets/e4773405-a16d-4468-a72e-9d1038ca113f)

### Insights por Categoría

**Electronics:**
- Presenta una desviación estándar en el precio actual de 14,514.65, lo que indica una amplia variedad de precios dentro de esta categoría, desde productos económicos hasta artículos de alta gama.
- Tiene el precio máximo más alto (79,990) y un precio promedio elevado (9,867.58), lo que sugiere que esta categoría incluye una considerable cantidad de productos de alto valor.

**Home&Kitchen:**
- Muestra una desviación estándar significativa de 3,597.91, aunque menor que la de Electronics. La variabilidad en los precios de esta categoría es notable, pero menos extrema en comparación.
- Presenta un precio máximo considerable de 19,990 y un precio promedio de 3,370.11, lo que sugiere que la mayoría de los productos en esta categoría son más accesibles en comparación con Electronics.
  
## Análisis de Rating por Categoría

A continuación, se analiza la distribución del rating para cada categoría de productos:

![Captura de pantalla 2024-09-03 140538](https://github.com/user-attachments/assets/295efb5e-b575-44a1-8ac0-276a45b459a8)

En general, se observa que la mayoría de los productos tienen un rating igual o superior a 3. Sin embargo, las categorías **Electronics** y **Home&Kitchen** incluyen algunos productos con ratings inferiores a 3. Por otro lado, **Computers & Accessories** cuenta con productos que tienen calificaciones perfectas de 5.

Para complementar el análisis, se creó un rango de ratings que permite visualizar mejor la agrupación de productos según sus calificaciones:

![image](https://github.com/user-attachments/assets/77ea2d18-3572-4255-9d4d-135abe36fe9d)


## Correlación 

![Captura de pantalla 2024-09-03 142528](https://github.com/user-attachments/assets/7188998c-2e60-44a4-9518-d738b1803387)

Este análisis nos sirve como base para validar o refutar las hipótesis planteadas:

* **1: ¿Los productos con mayores descuentos obtienen mejores calificaciones?**  
  La matriz de correlación muestra un valor muy bajo y negativo de -0.17 entre el descuento y la calificación. Esto indica una relación inversa, sugiriendo que un aumento en el descuento se asocia con una ligera disminución en la calificación. Sin embargo, la correlación es débil, por lo que el impacto es muy leve.

* **2: ¿Los productos con más votaciones tienen mejores calificaciones?**  
  La correlación positiva extremadamente baja de 0.1 entre el número de votaciones y la calificación sugiere que no hay una diferencia significativa en la calificación basada en la cantidad de votaciones. Es decir, tanto los productos con muchas como con pocas votaciones pueden tener calificaciones altas o bajas.

* **3: ¿Un mayor descuento está asociado con un mayor número de votaciones del producto?**  
  No existe la correlación  entre el descuento y el número de votaciones dado que vemos un resultado de 0.00

  
Para asegurar la validez de los resultados obtenidos, procederemos a aplicar técnicas adicionales de análisis, como la regresión lineal y pruebas de significancia. Estas técnicas permitirán una evaluación más rigurosa de nuestras hipótesis y ayudarán a confirmar o refutar las observaciones preliminares.

[Tecnica de Análisis](https://github.com/Maria-Data-Analyst/Amazon_Sales/blob/Consultas-Query/Ficha_tecnica/tecnica_analisis.md)

Para visualizar todo el análisis exploratorio hecho en Google Colab puede ver el siguiente Notebook: [Análisis exploratorio](https://github.com/Maria-Data-Analyst/Amazon_Sales/blob/Consultas-Query/analisis_exploratorio_Amazon.ipynb)
