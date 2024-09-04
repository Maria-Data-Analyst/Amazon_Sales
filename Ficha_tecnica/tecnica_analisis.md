# Regresión Lineal
Para corroborar la validacion de las hipotesis en el apartado anterior se llevara a cabo tres regresiones lineales para ver en que medida estas variables se estan afectando. 

## 1. Hipótesis: ¿Los productos con mayores descuentos obtienen mejores calificaciones?
  
  ![image](https://github.com/user-attachments/assets/28a96e49-140d-4be6-9b5e-082361a919f9)

### Resumen del Modelo

- **Intercepto (const):** 4.1976  
  El rating estimado es 4.1976 cuando el porcentaje de descuento es 0. Este valor representa el punto de partida del rating sin descuento.

- **Coeficiente (discount_percentage):** -0.0023  
  Por cada unidad adicional en el porcentaje de descuento, el rating disminuye en 0.0023 unidades. Aunque el cambio es pequeño, es negativo, indicando que un mayor descuento está asociado con un menor rating. 

- **Error estándar (const):** 0.0190  
 Este valor mide la precisión del estimado del intercepto (constante) del modelo de regresión. El intercepto es el valor del rating cuando el porcentaje de descuento es 0. Un error estándar bajo (como 0.0190) indica que el valor del intercepto está estimado con bastante precisión.

- **Error estándar (discount_percentage):** 0.0004  
  Este valor mide la precisión del estimado del coeficiente del porcentaje de descuento. El coeficiente indica cuánto cambia el rating por cada unidad adicional de descuento. Un error estándar bajo (como 0.0004) significa que el coeficiente se ha estimado con alta precisión, lo que sugiere que el efecto del descuento en el rating está bastante bien definido.

- **Valor p (discount_percentage):** 0.0000  
  El valor p muy bajo indica que el coeficiente de `discount_percentage` es significativamente diferente de cero. Hay evidencia estadística sólida para que el porcentaje de descuento tenga un efecto en el rating.

- **R-squared:** 0.0275  
  Solo el 2.75% de la variabilidad en el rating es explicada por `discount_percentage`. Esto sugiere que el modelo no explica bien la variabilidad en el rating.

- **Adj. R-squared:** 0.0268  
  El R-cuadrado ajustado, que tiene en cuenta el número de variables en el modelo. En este caso, es similar al R-cuadrado, indicando que la inclusión de `discount_percentage` como única variable predictora no mejora mucho el ajuste del modelo.

**Conclusión:**  
El análisis muestra que el porcentaje de descuento tiene un efecto estadísticamente significativo en el rating, aunque el impacto es muy pequeño. El coeficiente negativo sugiere que a mayor porcentaje de descuento, el rating tiende a disminuir. Sin embargo, el modelo tiene una capacidad limitada para explicar la variabilidad en las calificaciones. Dado que el efecto es sutil y el modelo no captura bien las diferencias en el rating, la hipótesis de que los mayores descuentos conducen a mejores calificaciones no se sostiene de manera significativa en este caso. **Hipótesis rechazada**

## 2. Hipótesis: ¿Los productos con más votaciones tienen mejores calificaciones?**

![image](https://github.com/user-attachments/assets/9a54b162-ec78-43d1-9d82-f8a36324d37d)

### Resumen del Modelo:

- **Intercepto (const):** 4.0794  
  Este es el rating estimado cuando el número de votaciones es 0. En este caso, el rating promedio es de 4.0794 cuando no hay votaciones.

- **Coeficiente (rating_count):** 0.0000  
  Por cada unidad adicional en el número de votaciones, el rating aumenta en 0.0000 unidades. Este valor cercano a 0 sugiere que el número de votaciones tiene un impacto muy pequeño en el rating.

- **Error estándar (const):** 0.0087  
  Indica la precisión del estimado del intercepto. Un valor bajo sugiere que el intercepto está estimado con alta precisión.

- **Error estándar (rating_count):** 0.0000  
  Mide la precisión del coeficiente del número de votaciones. Un valor cercano a 0 indica que el coeficiente se ha estimado con alta precisión.

- **Valor p (rating_count):** 0.0003  
  El valor p indica que el coeficiente del número de votaciones es significativamente diferente de cero. Aunque el coeficiente es muy pequeño, hay evidencia estadística que sugiere que el número de votaciones tiene un efecto en el rating.

- **R-squared:** 0.0095  
  Solo el 0.95% de la variabilidad en el rating es explicada por el número de votaciones. Esto indica que el modelo no explica bien la variabilidad en el rating.

- **Adj. R-squared:** 0.0088  
  El R-cuadrado ajustado, que considera el número de variables en el modelo, es similar al R-cuadrado. Esto sugiere que la inclusión del número de votaciones como única variable predictora no mejora significativamente el ajuste del modelo.

**Conclusión:**

Aunque el valor p indica que el número de votaciones tiene un efecto estadísticamente significativo en el rating, el coeficiente es extremadamente pequeño y el R-squared es muy bajo. Esto sugiere que el número de votaciones tiene un impacto mínimo en el rating y que el modelo no explica bien la variabilidad en las calificaciones. Por lo tanto, la hipótesis de que los productos con más votaciones tienen mejores calificaciones no está respaldada por los datos, ya que el impacto de las votaciones en el rating es casi insignificante.  **Hipótesis rechazada**

## 3. Hipótesis: ¿Un mayor descuento está asociado con un mayor número de votaciones del producto?

![image](https://github.com/user-attachments/assets/ced12398-6bb1-4c7c-a99c-928279be4531)

### Resumen del Modelo 

- **Intercepto (const): 17261.3038**
  - El número estimado de votaciones cuando el porcentaje de descuento es 0 es 17,261.30. Este valor es el punto de partida del modelo.

- **Coeficiente (discount_percentage): 8.1216**
  - Por cada unidad adicional en el porcentaje de descuento, el número de votaciones aumenta en 8.1216. Aunque este coeficiente es positivo, el valor p asociado indica que no es estadísticamente significativo (p = 0.8798).

- **Error estándar (const): 2755.4788**
  - Mide la precisión de la estimación del intercepto. Un error estándar alto indica que el intercepto no está estimado con gran precisión.

- **Error estándar (discount_percentage): 53.6915**
  - Mide la precisión del coeficiente del porcentaje de descuento. Un error estándar alto para el coeficiente sugiere que la estimación del efecto del porcentaje de descuento en el número de votaciones es imprecisa.

- **Valor p (discount_percentage): 0.8798**
  - El valor p muy alto indica que el coeficiente del porcentaje de descuento no es significativamente diferente de cero. En otras palabras, no hay evidencia suficiente para afirmar que el porcentaje de descuento tiene un efecto significativo en el número de votaciones.

- **R-squared: 0.0000**
  - Indica que el modelo no explica ninguna  variabilidad en el número de votaciones. 
 
### Conclusión:

La regresión muestra que no hay una asociación significativa entre el porcentaje de descuento y el número de votaciones. El coeficiente del porcentaje de descuento es positivo, pero el valor p alto (0.8798) indica que este efecto no es estadísticamente significativo. Además, el modelo tiene un R-cuadrado en 0, esto significa que el porcentaje de descuento no contribuye en absoluto a explicar las diferencias en el número de votaciones. Por lo tanto, no hay suficiente evidencia para apoyar la hipótesis de que un mayor descuento está asociado con un mayor número de votaciones. **Hipótesis rechazada**


# Regresión Lineal General 

Inicialmente, planteamos dos hipótesis sobre el impacto del porcentaje de descuento y la cantidad de votaciones en el rating de los productos. Sin embargo, al realizar las regresiones lineales, observamos que el modelo no mostraba un ajuste adecuado y podría beneficiarse de la inclusión de más variables.

En consecuencia, reformulamos nuestra hipótesis de manera más amplia: ¿Está el rating influenciado por las variables disponibles que tenemos en la abse de datos? Nuestro objetivo es determinar si estas variables tienen un impacto significativo en el rating, lo cual nos permitirá evaluar su relevancia en la predicción del rating.

Para investigar esto, construimos un modelo de regresión lineal utilizando variables numéricas relevantes. Además, transformamos las principales categorías de la variable main_category en variables dummy para incluirlas en el análisis.

Ahora, procederemos a revisar la correlación de todas las variables utilizadas en el modelo con el rating para comprender mejor sus relaciones.

![Correlación de Variables](https://github.com/user-attachments/assets/963878a1-480a-43cf-bfda-15cb96864b2b)

Observamos nuevas correlaciones entre el rating y las categorías, aunque siguen siendo muy pequeñas e incluso inversas en algunos casos.

**Resultados del Modelo de Regresión Lineal:**

![Resultados del Modelo](https://github.com/user-attachments/assets/371d9778-9e50-4edb-a1a7-f65dd14fa345)

A simple vista, la mayoría de las predicciones no coinciden con los valores reales. Aunque están cercanas, el modelo no predice exactamente el mismo valor. Vamos a revisar esto con las métricas del modelo.

**Verificación de Sobreajuste:**

![Sobreajuste](https://github.com/user-attachments/assets/1a866c00-6a93-4540-b713-ff1edc264a35)

El modelo muestra indicios de sobreajuste, ya que el score en el conjunto de entrenamiento es notablemente mayor que en el conjunto de prueba. Sin embargo, los valores de score (R² en regresión) son bajos en ambos conjuntos (cerca de 0). Esto sugiere que el modelo no está capturando bien la variabilidad en los datos.

**Evaluación del Modelo:**

- **Error Cuadrático Medio (MSE):** 0.0646
- **Raíz del Error Cuadrático Medio (RMSE):** 0.2542

**Interpretación:**  
El RMSE indica que, en promedio, las predicciones del modelo se desvían en aproximadamente 0.25 unidades del valor real, dentro de un rango de 1 a 5. Esto sugiere un nivel de precisión moderado en las predicciones del modelo.

**Conclusión**

El análisis del modelo de regresión lineal muestra que las predicciones están relativamente cerca de los valores reales, pero no son exactas. Las métricas del modelo revelan un Error Cuadrático Medio (MSE) de 0.0646 y una Raíz del Error Cuadrático Medio (RMSE) de 0.2542, lo que indica que, en promedio, las predicciones se desvían en aproximadamente 0.25 unidades de los valores reales, en un rango de 1 a 5. Aunque el error es moderado, el modelo presenta indicios de sobreajuste, ya que el score en el conjunto de entrenamiento es significativamente mayor que en el de prueba. Los bajos valores de R² en ambos conjuntos sugieren que el modelo no está capturando bien la variabilidad en los datos. En general, el modelo tiene una precisión moderada, pero se recomienda ajustar o explorar otras técnicas para mejorar el desempeño y la generalización.
