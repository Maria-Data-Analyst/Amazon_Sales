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

### Separación de Categorías

La variable `category` contiene múltiples categorías asociadas a cada producto, separadas por el símbolo `|`. Para facilitar el análisis, se han dividido estas categorías en tres columnas: `main_category`, `second_category` . Esta separación permite un análisis más claro y detallado de las categorías asociadas a cada producto.

![image](https://github.com/user-attachments/assets/a8997cb2-5942-42d9-b125-7e7c0d6d7706)


## Tabla: `amazon_review`

### Tipo de dato
 ![image](https://github.com/user-attachments/assets/2e66e4f8-8abd-48fe-92d2-62e4c2c9378d)
   
   Observamos que tanto `rating` como `rating_count` están en formato `object`. Para poder realizar cálculos y análisis, es necesario convertir estas columnas a un tipo numérico, para esto primero vamos a visualizar todo que no sea numerico.


   - **rating:** Tiene un registro con un valor no válido. Dado que es un único registro y no afecta significativamente el análisis, se eliminará este dato y convertiremos la columna a tipo `float`.
     
   ![image](https://github.com/user-attachments/assets/df8c41f2-c6ab-4d83-909a-b10fe9030afd)

   * **rating_count:** Utiliza comas como separador de miles, lo cual convierte los valores en caracteres no válidos para conversiones numéricas. Eliminaremos las comas y todo lo que no sea numerico de los valores y convertiremos la columna a tipo `float`.
     
   ![image](https://github.com/user-attachments/assets/e5cda7b0-f4eb-4897-a527-d86e1cbc5513)

### Resultados

  ![image](https://github.com/user-attachments/assets/d221f566-d5f6-4c5f-b719-22df83d248cd)

 ![image](https://github.com/user-attachments/assets/eac5192a-c7ea-4055-ab9f-290fe072360a)


## Variables

![Captura de pantalla 2024-09-02 192936](https://github.com/user-attachments/assets/0aecd7a1-4550-4822-a844-89b999c92ead)

En la tabla `amazon_review`, podemos observar que las variables contienen mucha información. A continuación, desglosaremos algunas variables para entender mejor los datos.


* **user_id**
  
![image](https://github.com/user-attachments/assets/7e0fef6d-2736-4f8d-a556-bea0b009d48b)

  La columna `user_id` contiene identificadores únicos de usuarios. Parece que hay varios `user_id` en cada registro único de `product_id`. 

* **user_name**

  ![image](https://github.com/user-attachments/assets/c3597216-80ec-4a4e-84f6-c735eb5cd08a)

  La columna `user_name` muestra los nombres de los usuarios. Al igual que con `user_id`, hay múltiples nombres de usuario en cada registro de `product_id`, que parecen estar separados por comas.

* **review_content**

  ![image](https://github.com/user-attachments/assets/dd569c1e-c816-426d-81e4-7bb89eab80a8)

  La columna `review_content` contiene las reseñas de los productos. Un problema significativo aquí es que las reseñas también utilizan comas para estructurar el texto. Esto hace difícil diferenciar dónde termina una reseña y comienza la siguiente, ya que las comas en las reseñas pueden confundirse con los delimitadores entre reseñas distintas.

### Observaciones:

En resumen, la información está separada por comas, y parece que el primer `user_id` corresponde al primer `user_name`, y así sucesivamente. Sin embargo, la presencia de comas en `review_content` complica la separación de reseñas individuales, ya que las comas también se utilizan dentro del contenido de las reseñas. 

### Evaluación de la Cantidad de Reseñas

Para tomar decisiones informadas, es esencial analizar la cantidad de reseñas disponibles para cada producto. Comparamos el número de reseñas, estimado a partir de las variables `user_id` y `user_name` (asumiendo que cada `user_id` y `user_name` corresponde a una reseña individual), con `rating_count`, que representa el número total de votaciones para el producto. Este análisis es crucial para evaluar si la muestra de reseñas es representativa del total de votaciones y si los datos son fiables.

Se crearon dos variables, `user_id_count` y `user_name_count`, para obtener una visión más clara. Sin embargo, se encontraron discrepancias entre estos valores, lo que sugiere que no siempre cada `user_id` corresponde a un `user_name` y que la cantidad de reseñas puede no ser consistente entre las dos variables.

![Discrepancia en la cantidad de reseñas](https://github.com/user-attachments/assets/7011ae62-a81f-4c5a-9798-9c32797d4c44)

Además, se obtuvo el máximo valor para cada variable: 8 para `user_id` y 9 para `user_name`. Para que 8 reseñas representen al menos el 10% de las votaciones, es necesario filtrar la cantidad de votos por producto.

![Distribución de votos por producto](https://github.com/user-attachments/assets/c5bf84bb-bd6c-4bf9-b074-86529f74770d)

La observación revela que 8 reseñas solo serían significativas en 63 productos. Esto indica que el análisis de reseñas no es significativo para la mayoría de los datos. Debido al problema de tener todas las reseñas agrupadas sin una forma clara de separarlas sin perder información, se decidió no utilizar las variables que contienen información conjunta y, en su lugar, centrarse en las siguientes variables: `img_link`, `product_link`, `product_id`, `rating`, y `rating_count`.

## Valores Nulos 

![image](https://github.com/user-attachments/assets/7a96b00c-418b-4dcd-9c6e-0d9ea1e91cff)


### Análisis de Enlaces de Imagen

Debido a la imposibilidad de imputar los valores nulos, conservaremos estos registros y realizaremos un análisis más detallado de los enlaces de imagen. Algunos enlaces funcionan correctamente, mientras que otros generan un mensaje de error al intentar acceder a ellos. A continuación, se identificaron los problemas:

#### Estructura Base del Enlace

La estructura base del enlace debe ser la siguiente:

**https://m.media-amazon.com/images/I**

Para identificar enlaces incorrectos, se realizó un análisis en Python para encontrar códigos erróneos en la base de los enlaces.

![Estructura Incorrecta](https://github.com/user-attachments/assets/148691a3-9f10-4aa7-a38b-e3c52a70cb99)

#### Estructura Adicional Requerida

Los enlaces también deben tener la siguiente estructura adicional:

**._SX300_SY300**


Se buscaron y se identificaron los enlaces que no cumplen con esta estructura.

![Estructura Incorrecta](https://github.com/user-attachments/assets/076dbf4b-740a-4ed7-8cb0-de4a32d3ebe0)

Con estas dos estructuras definidas, podremos corregir todos los enlaces y asegurar que funcionen correctamente.

## Valores Duplicados

### 1. Identificación de Duplicados por `product_id`, `rating` y `rating_count`

Primero, buscamos duplicados utilizando las columnas `product_id`, `rating`, y `rating_count` para identificar entradas que podrían estar registradas más de una vez con las mismas características.

![Identificación de duplicados por product_id, rating y rating_count](https://github.com/user-attachments/assets/6d689bca-eb19-4586-9cd3-96160648ca0b)

### 2. Eliminación de Duplicados

Después de identificar los duplicados, procedemos a eliminarlos para mantener un único registro por cada producto, asegurando que los datos sean consistentes y precisos.

![Eliminación de duplicados](https://github.com/user-attachments/assets/bd1c022a-8da0-4a97-b5d3-1d4b7af855e3)

### 3. Búsqueda de Duplicados por `product_id` Únicamente

A continuación, realizamos una búsqueda de duplicados considerando solo el `product_id`. Esto nos permite identificar si existen discrepancias en productos únicos que podrían tener diferentes características, como `rating` y `rating_count`.

![Búsqueda de duplicados solo por product_id](https://github.com/user-attachments/assets/9a17803e-ea20-4f90-b978-9450f381098a)

### 4. Resolución de Discrepancias

Al observar los duplicados restantes, notamos que las diferencias entre ellos en `rating_count` son pequeñas, entre 1 y 3 votaciones. Para resolver estas discrepancias, decidimos mantener el registro con el mayor número de votaciones (`rating_count`) y eliminar los otros.

![Resolución de discrepancias y eliminación de registros](https://github.com/user-attachments/assets/82f7f40d-f1ae-4d61-a8b3-4aa3716ac3eb)


## Union de Tablas 
Primero, descargamos los dos archivos limpios desde Google Colab y los subimos a BigQuery como tablas separadas. A continuación, realizamos un Inner Join entre estas tablas en BigQuery para combinar la información y obtener una tabla consolidada con datos completos. Esto nos permite visualizar y consultar los datos de manera más eficiente y completa en la siguiente sección.

[Análisis Exploratorio](https://github.com/Maria-Data-Analyst/Amazon_Sales/blob/Consultas-Query/Ficha_tecnica/analisis_exploratorio.md)

En el siguiente Notebook encontraras todos los procesos de limpieza realizados [Procesamiento con Python](

