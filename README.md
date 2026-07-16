# Valoración de Empresas con Datos Financieros

Proyecto de ciencia de datos que analiza qué indicadores financieros 
predicen si una empresa está sobrevalorada o infravalorada en bolsa.

## Estado
Completado - julio 2026

## Pregunta de investigación
¿Qué indicadores financieros explican la valoración de una empresa medida por su PER (Price-to-Earnings Ratio)?

## Datos
10 empresas cotizadas en bolsa americana obtenidas via API de Yahoo Finance (yfinance).
Variables: trailingPE, forwardPE, priceToBook, debtToEquity, profitMargins, returnOnEquity, revenueGrowth, earningsGrowth

## Metodología
Fase 1 - Descarga 
Descargé los datos financieros reales de Yahoo Finance que dispone de cotizaciones históricas, beneficios, deuda, márgenes etc... 

Fase 2 - Limpieza 
Como no teníamos muchos datos, 10 empresas y 11 características, se podían observar los datos en crudo para ver si había algún fallo o algo que pudiera causar problemas en el estudio. Con ello, vi que el debtToEquity de JPM aparecía como NaN. Para solucionarlo, le pusimos un valor usando la mediana, ya que, en esta misma fase, pude ver que algunos valores de Tesla eran extremadamente elevados, y si usaba la media para ello, el resultado se vería afectado. 

Fase 3 - EDA 
En cuanto al análisis exploratorio de los datos, realicé un barplot con el trailingPE, que certificaría el valor tan elevado de Tesla. Para poder estudiar el PE de las demás empresas con el gráfico de barras, eliminé Tesla. Luego, realicé un estudio de correlaciones con el correspondiente gráfico heatmap, y la relación entre el profitMargin y el PE con un diagrama de dispersión. Por último, usé un gráfico de cajas que relacionaba el PE y los sectores. 

Fase 4 - Modelo
En este estudio realizamos un modelo lineal múltiple para predecir el trailingPE a partir de las variables explicativas. Sin embargo, tuvimos un problema de overfitting, es decir, que el modelo memoriza los datos en lugar de aprender patrones generales. Así,  usaremos el modelo para entender las relaciones entre variables, no para hacer predicciones fiables. En cuanto al modelo, la variable a explicar es 'trailingPE' y las explicativas serían 'profitMargins', 'revenueGrowth', 'earningsGrowth', 'debtToEquity', 'returnOnEquity'. Esto nos deja una matriz de 10 filas y 5 columnas, 10 empresas y 5 variables. Además, evaluamos el coeficiente de R^2 y el MAE, y se obtuvo un R^2 muy cercano a 1, pero con 10 datos es señal de alarma por lo comentado anteriormente sobre el overfitting. En cuanto al MAE, es de 11.939, influenciado en gran medida por el PE de Tesla.

## Hallazgos
Hallazgo 1: sobre el sector y el PE
Tras los pertinentes estudios, he observado que el PE se ve muy influenciado según el sector. Por ejemplo, en el sector tecnológico, el PE suele ser de los más elevados, mientras que en el sector de las finanzas es todo lo contrario, aunque tendríamos que realizar estudios con más empresas ya que solo tenemos una empresa de dicho sector en el estudio (JPM). 
Otro ejemplo sería el sector de Consumo Cíclico. En nuestro estudio tenemos a Tesla y a Amazon de ese sector, y aunque el PE de Tesla es el más elevado con una gran diferencia con respecto a las demás empresas, el PE de Amazon también es de los más elevados, lo que sugiere que las empresas de ese sector también tienen un PE elevado.

Hallazgo 2: sobre la relación profitMargins/PE
Para este hallazgo, realicé un diagrama de dispersión con el trailingPE en el eje y, y con profitMargins en el eje x, y los resultados fueron bastante claros. En primer lugar, la mayoría de empresas se situaron en una zona parecida de PE (20-45) y de profitMargins (0'1-0'4). Sin embargo, hay dos empresas que rompieron esos esquemas. Una de ellas fue tesla, que alcanzó un PE de más de 350 y un profitMargin inferior a 0'05, mientras que NVIDIA solo logró un PE de poco más de 25 y un profitMargin de más de 0'6. Estos resultados sugieren una relación inversamente proporcional entre el profitMargins y el PE

Hallazgo 3: sobre Tesla como outlier y lo que implica
En este estudio ha habido una empresa que ha supuesto una dificultad para el de venir del mismo, ya que ha dado valores extraordinariamente altos en algunos parámetros. Estoy hablando de Tesla, y es que en el gráfico de barras, al compararla con las demás, el PE es tan superior, que no se percibe la diferencia entre las demás, por lo que tuvimos que suprimirla momentaneamente para poder estudiar el resto de empresas con más claridad. Esto puede ser debido a su crecimiento esperado y no a sus beneficios actuales, lo que refleja un PE extremadamente alto.


## Tecnologías utilizadas
pandas, matplotlib, seaborn, scikit-learn, jupyter

## Cómo ejecutar el proyecto
1. Clona este repositorio o descarga los archivos.
2. Instala las dependencias necesarias:
```bash
   pip install pandas numpy matplotlib seaborn scikit-learn yfinance
```
3. Abre el notebook:
```bash
   jupyter notebook 01_descarga_datos.ipynb
```
4. Ejecuta las celdas en orden. El notebook descargará los datos financieros directamente desde Yahoo Finance (mediante `yfinance`), por lo que se necesita conexión a internet.
5. Al finalizar, se generarán los gráficos del análisis exploratorio (barplot, heatmap, dispersión, boxplot) y los resultados del modelo de regresión lineal múltiple (R² y MAE).

## Autor
Héctor Nieto
GitHub: https://github.com/hector-n-c

