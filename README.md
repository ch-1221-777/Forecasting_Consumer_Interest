## Forecasting Consumer Interest in Eco-Friendly Products

In this project I use Google Trends and Facebook's Prophet model to analyze and forecast consumer interest in the following categories:

- Natural fabrics in Shopping > Apparel
- Non-toxic materials in Home & Garden > Kitchen & Dining
- Healthy descripions in Food & Drink

The Google Trends data spans the years 2010-2024 and we use it to forecast one year into the future. 

**Google Trends** allows users to visualize how often specific terms are entered into Google's search engine over time. It helps analyze public interest and identify emerging trends by plotting the relative popularity of search queries which can be filtered based on different categories, by regions and/or time periods. Users can compare up to five search terms in a single query, and the results are normalized on a relative scale from 0 to 100, where 100 represents the peak popularity of a term. Since each query is normalized independently, this means that comparisons accross different queries require careful interpretation.

**Facebook Prophet** is an open-source forecasting model designed for time-series data. It works by decomposing time series as a sum of three components: trend, seasonability and holiday effects. The model fits piecewise linear or logistic trends, captures seasonal patterns using a Fourier series, and uses indicator functions for customizable holiday events causing spikes or dips. To evaluate forecasting accuracy, Prophet supports rolling forward cross-validation where the model is repeatedly trained on an expanding window of historical data and then used to foracast a fixed horizon into the future. This can be used to assess how forecast accuracy changes depending on how far the prediction is made i.e. the length of horizon interval.

#### Natural Fabrics Trends

![](images/natural_fabrics_trend_plot.png)

#### Prophet's Output

The following plot is the fitted time series for the above data which extends to the one-year horizon.

![](images/forecast_plot_all_fabrics.png)

Visualy, the model output seems to match the existing data pretty well, which gives confidence in forecast. 

For the forecast of "cotton" search popularity, we break down into Prophet's modeling components:

![](images/cotton_1yr_forecast_components.png)

For educational purposes, we produce error estimates for Prophet's model output using its built-in cross validation tool.

#### Prophet's cross validation

Prophet’s cross_validation() function evaluates forecast accuracy using a **rolling forecast** approach. You can specify three key parameters: the initial training period, the forecast horizon, and the spacing between cutoff dates (called the period).

The model is first trained on the **initial** window of data, and a forecast is made for the specified **horizon**. For example, if the initial period is 2 years and the horizon is 1 year, Prophet trains on 2 years of data and forecasts the next year.

Then, the training window is extended by the specified **period** (e.g. 6 months), and the process repeats: Prophet retrains on 2 years and 6 months worth of data and again forecasts 1 year ahead. This rolling process continues until the end of the dataset is reached. The result is multiple simulated forecasts or time series up to period-increasing cutoff points.

We take the forecast of the "cotton" search popularity and perform cross validation with the values 
initial = 730 days # (2 years)
period = 180 days  # (6 months)
horizon = 365 days # (1 year)

Prophet's diagnostics module also includes error metrics for each horizon forecast. 
![](images/cotton_1yr_forecast_error_metrics.png)




