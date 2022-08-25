# Time Series Modeling with Fbprophet

This Jupyter Notebook explores time series trends (search, stock price, revenue) for MercadoLibre and uses the fbprophet package to make future predictions. 

Google Colab was used in the development of this Jupyter Notebook. 

## Technologies

This program is written in Python (3.7.13) and developed using Google Colab on a Windows computer. Additional libraries that are used in this application are pandas (1.3.5), hvplot (0.8.0), seaborn (0.11.2), pystan(2.19.1.1), holoviews(1.14.9), and numpy (1.21.6) (see parenthesis for versions used in program development).

In your Google Colab environment, these lines of code should be sufficient for you to get started. 

```python
!pip install pystan
!pip install fbprophet
!pip install hvplot
!pip install holoviews
```

If you experience errors with the install for fbprophet, try Mokey Luffy's [solution](https://stackoverflow.com/questions/73142498/installing-fbprophet-on-colab) from stackoverflow: 

```python
!pip install pystan ~= 2.14
!pip install fbprophet
```

## Installation Guide

Downloading the code & associated files using `git clone` from the repository is sufficient to download the Jupyter Notebook, ensure that the associated libaries (see Technologies section) are installed on your machine (or in the Google Colab environment) as well. If there are any issues with the library functions please refer to the versions used for app development (see Technnologies section for this information as well).  Please note that this is a Jupyter notebook. 

The code in the notebook is written for the Google Colab environment, there are a few lines of code that you may want to take out if running it on your local machine, such as the lines for `!pip install`, the lines to display hvplots in the Colab environment `hv.extension('bokeh')`, and the lines for file uploads, which are `from google.colab import files` and `uploaded = files.upload()`.

## Usage

This notebook is referencing data stored in the Resources folder in the repository. As described above, including these lines of code in your notebook will prompt you to add the files to your Google Colab environment: 

```python
from google.colab import files
uploaded = files.upload()
```

If you're not using Google Colab, in the `pd.read_csv` functions, make sure to specify the correct path to the files.

## Code examples

The hvPlot library is used to display multiple different types of charts (such as line charts, bar charts, and heatmaps) to view and analyze the data. Displaying information using hvPlot is simple and can be done with only one line of code such as:

`df.hvplot(title="my chart")`

A few calculations are done using grouping and group levels, for example:

```python
groupby_levels = [df_mercado_trends.index.year, df_mercado_trends.index.month]
median_monthly_traffic = df_mercado_trends.groupby(by=groupby_levels).sum().median()
```

The fbprophet package is used to make forecasts on the time series data. The `Prophet()` function accepts an input dataframe with two columns named `ds` (for the independent variable) and `ys` (for the predicted variable). 

Creating a model, making predictions, exploring trends, and viewing the data can be done with only a few lines of code: 

```python
model = Prophet()
model.ft(df)
future_predictions = model.make_future_dataframe(periods=2000, freq="H")
forecast_trends = model.predict(future_predictions)
model.plot(forecast_trends)
forecast_trends = forecast_trends.reset_index()
model.plot_components(forecast_trends)
```

The `forecast_trends` dataframe presents you with multiple columns: in this analysis, `yhat` is used for the best estimate, `yhat_upper` is used to represent the best case scenario, and `yhat_lower` is used to represent the worst case scenario. 


## References

For more information about the libraries, check out the documentation!

[Hvplot library](https://hvplot.holoviz.org/)

[Fbprophet library](https://pypi.org/project/fbprophet/)

## Contributors

Project contributors are the Rice FinTech bootcamp program team (instructor Eric Cadena) who developed the tasks for this project along with myself (Paula K) who's written the code in the workbook.
