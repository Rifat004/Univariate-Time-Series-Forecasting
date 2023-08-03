# Univariate Time Series Regression

In this task, the goal is to apply four traditional algorithms (AR, MA, ARMA, ARIMA) for forecasting univariate time series data. I have used monthly sunspots data for this task.

## Workflow

**1. Background understanding of Time Series**:

**Time Series:** Time series data is a type of data where observations are recorded in chronological order over a period of time. Each data point in a time series is associated with a specific time or date. Time series data can be categorized into two main types: univariate time series and multivariate time series.

Univariate time series consists of a single time-dependent variable, and each data point represents the value of that variable at a particular time. In other words, a univariate time series has only one time series sequence. The goal of analyzing univariate time series is often to understand and forecast the future values of the single variable based on its past observations. Common examples of univariate time series include daily stock prices, monthly/daily temperature readings, and monthly sunspots.

Multivariate time series involves multiple time-dependent variables, and each data point represents the values of these variables at a specific time. In other words, a multivariate time series has multiple time series sequences that are interrelated. The goal of analyzing multivariate time series is to study the relationships and dependencies among the variables and make predictions for each variable based on their historical values. Common examples of multivariate time series include macroeconomic indicators (e.g., GDP, inflation, unemployment), where multiple economic variables are observed over time.

**Autocorrelation and Partial Autocorrelation:** Autocorrelation and Partial Autocorrelation are two important concepts in time series analysis that help identify the underlying patterns and relationships within a time series data.

Autocorrelation measures the correlation of a time series with its own lagged values at different time intervals. It quantifies the linear relationship between observations at different time points. The autocorrelation function (ACF) is a plot that shows the correlation coefficients between the time series and its lags. It helps in identifying the order of the Autoregressive (AR) component in an ARIMA model. Auto Correlation function takes into consideration of all the past observations irrespective of its effect on the future or present time period. It calculates the correlation between the t and (t-k) time period. It includes all the lags or intervals between t and (t-k) time periods. Correlation is always calculated using the Pearson Correlation formula.

The PACF determines the partial correlation between time period t and t-k. It doesn’t take into consideration all the time lags between t and t-k. For e.g. let's assume that today's stock price may be dependent on 3 days prior stock price but it might not take into consideration yesterday's stock price closure. Hence we consider only the time lags having a direct impact on future time period by neglecting the insignificant time lags in between the two-time slots t and t-k.

Let's take an example of sweets sale and income generated in a village over a year. Under the assumption that every 2 months there is a festival in the village, we take out the historical data of sweets sale and income generated for 12 months. If we plot the time as month then we can observe that when it comes to calculating the sweets sale we are interested in only alternate months as the sale of sweets increases every two months. But if we are to consider the income generated next month then we have to take into consideration all the 12 months of last year. So in the above situation, we will use ACF to find out the income generated in the future but we will be using PACF to find out the sweets sold in the next month.

**Correlation and Causation:**

Correlation refers to a statistical measure that quantifies the degree of association or relationship between two or more variables. It measures the strength and direction of a linear relationship between variables. Correlation does not imply a cause-and-effect relationship but indicates how changes in one variable may be associated with changes in another variable. The most common measure of correlation is the Pearson correlation coefficient, which ranges from -1 to 1.

Causation, on the other hand, refers to a cause-and-effect relationship between two or more variables. It suggests that changes in one variable directly or indirectly influence changes in another variable. Determining causation requires more rigorous study and evidence, often through experimental designs or carefully controlled observational studies. Establishing causation involves ruling out other potential explanations for the observed relationship between variables.

A correlation between variables, however, does not automatically mean that the change in one variable is the cause of the change in the values of the other variable. Causation indicates that one event is the result of the occurrence of the other event; i.e. there is a causal relationship between the two events.

**Algorithms:** AR, MA, ARMA, and ARIMA models are used to forecast the observation at (t+1) based on the historical data of previous time spots recorded for the same observation. However, it is necessary to make sure that the time series is stationary over the historical data of observation overtime period. If the time series is not stationary then we could apply the differencing factor on the records and see if the graph of the time series is a stationary overtime period.

The Autoregressive (AR) model is a time series model that uses lagged values of the time series variable to predict its current value. In an AR(p) model, the current value of the variable is assumed to be a linear combination of its past p values (lags). The order 'p' represents the number of lagged values used in the model. The AR model is suitable for stationary time series data with correlation between past and current observations.

The Moving Average (MA) model is a time series model that uses the past forecast errors (residuals) of the time series variable to predict its current value. In an MA(q) model, the current value of the variable is assumed to be a linear combination of its past q forecast errors. The order 'q' represents the number of past forecast errors used in the model. The MA model is suitable for stationary time series data with correlation between past forecast errors.

The Autoregressive Moving Average (ARMA) model combines the AR and MA models. It is a generalization of both models and can capture both the autoregressive and moving average behavior of the time series data. An ARMA(p, q) model includes both AR(p) and MA(q) components. The ARMA model is suitable for stationary time series data with correlation between past observations and forecast errors.

The Autoregressive Integrated Moving Average (ARIMA) model is an extension of the ARMA model that includes a differencing step to handle non-stationary time series data. The ARIMA model is specified by three parameters: p (AR order), d (differencing order), and q (MA order). The differencing order 'd' is used to make the data stationary by differencing the time series. The ARIMA model can handle both autoregressive and moving average components in the presence of non-stationarity.

Another notes,

- Identification of an AR model is often best done with the PACF.

- For an AR model, the theoretical PACF “shuts off” past the order of the model. The phrase “shuts off” means that in theory the partial autocorrelations are equal to 0 beyond that point. Put another way, the number of non-zero partial autocorrelations gives the order of the AR model. By the “order of the model” we mean the most extreme lag of x that is used as a predictor.

- Identification of an MA model is often best done with the ACF rather than the PACF. For an MA model, the theoretical PACF does not shut off, but instead tapers toward 0 in some manner. A clearer pattern for an MA model is in the ACF. The ACF will have non-zero autocorrelations only at lags involved in the model.

- In ARIMA, three parameters p,d,q where p is AR lags, d indicates differencing, q is MA lags

**Augmented Dickey-Fuller (ADF) test:** The Augmented Dickey-Fuller (ADF) test is a statistical hypothesis test used to determine whether a time series is stationary or not. The test compares the characteristics of the time series with and without the assumption of non-stationarity (unit root) to see if the series is better explained by a stationary model. Some of the ADF test outputs are as follows:

ADF Statistic:
The ADF statistic is the test statistic of the ADF test. It is a negative number. The more negative the ADF statistic, the stronger the evidence for rejecting the null hypothesis of non-stationarity. ADF statistic is used to compare against critical values to determine whether to reject or fail to reject the null hypothesis.

P-value:
The p-value is the probability of obtaining the ADF statistic under the null hypothesis of non-stationarity. A lower p-value indicates stronger evidence against the null hypothesis, suggesting that the time series is likely stationary. The conventional significance level is 0.05; if the p-value is less than or equal to 0.05, we reject the null hypothesis and consider the time series to be stationary.

Critical Values:
The critical values are pre-defined thresholds at different confidence levels that are used to compare against the ADF statistic. The critical values help determine the significance of the ADF statistic. If the ADF statistic is less than the critical value at a given confidence level, we reject the null hypothesis of non-stationarity and conclude that the time series is stationary.

In summary, the ADF statistic is used to compare against the critical values, and the p-value is used to assess the significance level to determine if the time series is stationary or not. The critical values provide a benchmark to interpret the ADF statistic correctly.

Interpretation:

If ADF Statistic < Critical Value: Reject the null hypothesis (consider the time series stationary).
If ADF Statistic > Critical Value: Fail to reject the null hypothesis (consider the time series non-stationary).
It's essential to check both the ADF Statistic and the p-value to make an informed decision about the stationarity of the time series. Lower ADF statistic values and p-values below the significance level (e.g., 0.05) indicate a higher likelihood of the time series being stationary.

**2. Loading the dataset**: I have loaded the dataset that contains monthly sunspot data from 1749-01 to 1983-12.

**3. Exploratory Data Analysis (EDA):** I have plotted the time series data to visualize the historical observations over time. I checked for stationarity using ADF test and found both data as stationary.

**4. Train-Test Split**: I slit the time series data into a training set (90%) and a test set (10%).

**5. Model Building, Prediction and Evaluation**: I built model for each algorithm. Since differenciation was not needed (d=0), the ARIMA model becomes equivalent to the ARMA model. I predicted using test set. With the best model, I performed future prediction by making future data with respect to original data. I evaluated the model using RMSE.

## Result

ARMA model performed better compared to other models.

## Conclusion

In this task, I have applied three algorithms as ARMA and ARIMA becomes equivalent due to zero differencing. I have not considered seasonality because I was limited to appying these alogorithms and we know ARIMA model is selected when the data is not seasonal. The main objective of this task is to explore these traditional algorithms and learn how to apply those in univariate time series data.
