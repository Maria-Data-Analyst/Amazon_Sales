# Procesamiento y Preparación de la Base de Datos

En esta sección, detallaremos los pasos necesarios para el procesamiento y limpieza de los datos, con el objetivo de dejar las tablas preparadas para el análisis exploratorio.

## Descripción de las Tablas y Variables

Antes de proceder al análisis, es crucial entender la estructura de los datos disponibles. A continuación, se describen las tablas `amazon_product` y `amazon_review` junto con sus respectivas variables:

### Tabla: `amazon_product`

| **Variable**           | **Descripción**                               |
|------------------------|-----------------------------------------------|
| `product_id`           | Identificador único del producto              |
| `product_name`         | Nombre del producto                           |
| `category`             | Categoría a la que pertenece el producto      |
| `discounted_price`     | Precio con descuento aplicado al producto     |
| `actual_price`         | Precio original del producto                  |
| `discount_percentage`  | Porcentaje de descuento aplicado al producto  |
| `about_product`        | Descripción detallada del producto            |

### Tabla: `amazon_review`

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

