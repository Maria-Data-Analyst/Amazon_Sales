# Procesamiento y Preparación de la Base de Datos

En esta sección, detallaremos los pasos necesarios para el procesamiento y limpieza de los datos, con el objetivo de dejar las tablas preparadas para el análisis exploratorio.

* ## Descripción de las Tablas y Variables

Antes de proceder al análisis, es crucial entender la estructura de los datos disponibles. A continuación, se describen las tablas `amazon_product` y `amazon_review` junto con sus respectivas variables:

* ### Tabla: `amazon_product`

| **Variable**           | **Descripción**                               |
|------------------------|-----------------------------------------------|
| `product_id`           | Identificador único del producto              |
| `product_name`         | Nombre del producto                           |
| `category`             | Categoría a la que pertenece el producto      |
| `discounted_price`     | Precio con descuento aplicado al producto     |
| `actual_price`         | Precio original del producto                  |
| `discount_percentage`  | Porcentaje de descuento aplicado al producto  |
| `about_product`        | Descripción detallada del producto            |

* ### Tabla: `amazon_review`

| **Variable**           | **Descripción**                                               |
|------------------------|---------------------------------------------------------------|
| `user_id`              | ID del usuario que escribió la reseña del producto            |
| `user_name`            | Nombre del usuario que escribió la reseña del producto        |
| `review_id`            | ID de la reseña del usuario                                   |
| `review_title`         | Título breve de la reseña                                     |
| `review_content`       | Contenido detallado de la reseña                              |
| `img_link`             | Enlace a la imagen del producto                               |
| `product_link`         | Enlace al sitio web oficial del producto                      |
| `product_id`           | ID del producto asociado a la reseña                          |
| `rating`               | Calificación otorgada al producto                             |
| `rating_count`         | Número de personas que votaron por la calificación en Amazon  |


* ## Limpieza de Datos

Con una definición clara de las variables, podemos proceder a la limpieza de los datos. Comenzaremos por visualizar la tabla `amazon_product` para examinar los datos y detectar posibles inconsistencias o problemas que necesiten ser corregidos.

![Captura de pantalla 2024-09-02 123252](https://github.com/user-attachments/assets/99e59b61-99db-4b58-a257-9d1aa14448db)


![image](https://github.com/user-attachments/assets/123bce58-fb64-4e8a-90e3-a7209d6116c7)


Podemos observar que las variables `discounted_price`, `actual_price` y `discount_percentage` contienen símbolos y utilizan comas como separadores de miles. Además, actualmente están en formato `object`. Para poder trabajar con estos datos de manera numérica, iniciaremos el proceso de limpieza eliminando los caracteres no numéricos. Después de realizar estas correcciones, las variables quedarán de la siguiente manera:

![Captura de pantalla 2024-09-02 125832](https://github.com/user-attachments/assets/51ae2765-0e54-4eb0-b5f6-86244ca6d63a)

![Captura de pantalla 2024-09-02 125852](https://github.com/user-attachments/assets/dbdd540c-7466-43cf-a679-bd481195058e)


* ### Valores Nulos

Primero, hemos realizado una verificación de los valores nulos en el DataFrame.

![image](https://github.com/user-attachments/assets/c1ad5f73-a9c8-42e3-8754-05aa5ab32034)

Para tomar decisiones informadas, procederemos a investigar más a fondo los productos que no cuentan con un campo "about" válido.

![image](https://github.com/user-attachments/assets/689fa18c-c678-41af-9c1c-dd69ded3a322)

Hemos identificado que los registros con valores nulos en el campo "about" corresponden a IDs de productos repetidos que sí tienen un "about" en otros registros. Por lo tanto, eliminaremos los registros duplicados que tienen el campo "about" nulo.

![image](https://github.com/user-attachments/assets/5c000cf1-5d7c-4a35-bb66-27c5a4bc9b8c)


* ### Análisis de Valores Duplicados

El siguiente paso es realizar un análisis exhaustivo para identificar y manejar los valores duplicados en el conjunto de datos. Este análisis debe enfocarse no solo en la variable `product_id`, sino también en otras variables relevantes como `discounted_price`, `actual_price` y `discount_percentage`. Este enfoque integral asegura que se detecten duplicados incluso cuando `product_id` sea único pero los precios y descuentos puedan variar.

![Imagen de duplicados](https://github.com/user-attachments/assets/e4e937d9-5e53-46aa-91fe-368439eea384)

Se han detectado 199 registros duplicados en las variables seleccionadas. Por lo tanto, se procederá a eliminar estos duplicados para mantener un único registro para cada combinación de variables.

A continuación, realizaremos un análisis adicional para identificar duplicados únicamente por `product_id`. Este paso nos permitirá verificar si existen identificadores repetidos con características diferentes.

![Imagen de análisis adicional](https://github.com/user-attachments/assets/be3ab8a5-9303-47cb-bc4b-6a5d348f4756)

En esta fase, hemos observado que hay identificadores de producto iguales pero con valores diferentes en `actual_price`, `discounted_price` y `discount_percentage`. Como resultado, procederemos a eliminar todos los registros duplicados para asegurar que cada `product_id` tenga un solo conjunto de características coherentes.


![image](https://github.com/user-attachments/assets/56e3d960-3802-4513-b544-ead1ab404340)


### Análisis entre Precio Actual, Porcentaje de Descuento y Precio con Descuento

Este análisis tiene como objetivo validar la exactitud de los datos de precios y descuentos. Se centra en verificar si el porcentaje de descuento promocionado se ha aplicado correctamente. Para ello, se calcula el porcentaje de descuento real y se compara con el porcentaje promocionado. Las diferencias en el porcentaje de descuento mayores al 10% se consideran significativas, ya que indican una discrepancia notable entre el descuento aplicado y el promocionado.

**Resultados:**

![image](https://github.com/user-attachments/assets/10d14941-9326-4147-a256-45ed6dc3337a)

De los resultados obtenidos, se observa que 1,347 registros muestran diferencias en el porcentaje de descuento aplicado menores al 10%. Estas diferencias podrían deberse a aproximaciones o errores en la captura de datos. Sin embargo, dado que no se encuentran discrepancias del 10% o mayores, estas diferencias menores se consideran insignificantes para el análisis general.

**Conclusión:**

El análisis revela que la mayoría de las discrepancias son menores al 10%, lo que sugiere que, en general, el porcentaje de descuento promocionado se aplica de manera adecuada. Las diferencias menores al 10% podrían ser atribuibles a errores menores de captura o redondeo y no afectan significativamente la validez de los descuentos aplicados.



