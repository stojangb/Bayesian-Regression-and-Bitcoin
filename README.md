#Conclusión: La idea de generar dinero a partir de las criptomonedas es alucinante, este proyecto busca justo eso, sin embargo creo que vamos por el camino equivocado.

#Las transacciones sobre Bitcoin - o cualquier otra criptomoneda - son extremadamente volátiles, por lo menos hasta ahora, ya veremos que pasa con RadixDlt (Hay que estar muy pendientes), al ser tan extrema la volatilidad no hay predicción que logre una sombra de éxito.

#Existen estudios que analizan twitter, y los trending topic o #hashtag que han intentando predecir con indicadores hacia donde se podría dirigir el precio del bitcoin, hasta ahora no han logrado resultados concluyentes.

#A pesar de eso, creo firmemente que el análisis de internet puede predecir en parte el precio del Bitcoin, sobre todo por la cantidad de información existente, y se pueden hacer comparaciones entre las noticias y el precio de la criptomoneda.

#El principal problema es el poco tiempo de vida del Bitcoin, aún no podemos analizar la reacción de la criptomoneda ante diferentes crisis financieras, actualmente con la crisis del covid-19 se están dando diferentes escenarios que están poniendo la criptomoneda a prueba, sobre todo porque las personas buscan un refugio para su dinero, en próximas crisis estas curvas se pueden repetir.

#La mejor forma de saber que es lo que se viene es estar atentos, analizar el precio del bitcoin en diferentes fechas, probablemente no lo sepamos pero nuestro cerebro genere un aprendizaje inconsciente sobre el precio del bitcoin.

#Sí existiera una forma de predecir el valor del bitcoin en un futuro, la formula serviría solo para unos pocos, al tener un gran número de personas la misma formula, la formula se desvanece, no podemos ganar dinero invirtiendo en acciones si todos compramos y retiramos el dinero al mismo tiempo, lo mismo pasa con el bitcoin.


# Bayesian-Regression-and-Bitcoin
Predicting Bitcoin Price Variations using Bayesian Regression

Reference paper: http://arxiv.org/pdf/1410.1231.pdf

Datasets:

The original raw data can be found here: http://api.bitcoincharts.com/v1/csv/. The datasets from this site have three attributes: (1) time in epoch, (2) price in USD per bitcoin, and (3) bitcoin amount in a transaction (buy/sell). However, only the first two attributes are relevant to this project.

To make the data to have evenly space records, all the records within a 20 second window was taken and replaced by a single record as the average of all the transaction prices in that window. Not every 20 second window had a record; therefore those missing entries were filled using the prices of the previous 20 observations and assuming a Gaussian distribution. The raw data that has been cleaned is given in the file dataset.csv.
Finally, as discussed in the paper, the data was divided into a total of 9 different datasets. The whole dataset is partitioned into three equally sized (50 price variations in each) subsets: train1, train2, and test. The train sets are used for training a linear model, while the test set is for evaluation of the model. There are three csv files associated with each subset of data: *_90.csv, *_180.csv, and *_360.csv. In _90.csv, for example, each line represents a vector of length 90 where the elements are 30 minute worth of bitcoin price variations (since we have 20 second intervals) and a price variation in the 91st column. Similarly, the *_180.csv represents 60 minutes of prices and *_360.csv represents 120 minutes of prices.

Following are the steps which were taken in this project:

1. Compute the price variations (Δp1, Δp2, and Δp3) for train2 using train1 as input to the Bayesian Regression equation (Equations 6). The similarity metric (Equation 9) was used in place of the Euclidean distance in Bayesian Regression (Equation 6).
2. Compute the linear regression parameters (w0, w1, w2, w3) by finding the best linear fit (Equation 8). Here you will need to use the ols function of statsmodels.formula.api. Your model should be fit using Δp1, Δp2, and Δp3 as the covariates. Note: the bitcoin order book data was not considered and hence rw4 term is not there in the model.
3. Use the linear regression model computed in Step 2 and Bayesian Regression estimates, to predict the price variations for the test dataset. Bayesian Regression estimates for test dataset are computed in the same way as they are computed for train2 dataset – using train1 as an input.
4. Once the price variations are predicted, compute the mean squared error (MSE) for the test dataset (the test dataset has 50 vectors => 50 predictions).
