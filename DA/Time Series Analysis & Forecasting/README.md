# 📈 Time Series Forecasting Project

This project focuses on forecasting future values of a time series dataset using **R**. It demonstrates a full workflow from data preprocessing and analysis to model building and evaluation. The approach also accounts for structural breaks in the data to enhance forecast accuracy and robustness.

## 🎯 Objectives

- **Accurately forecast** future values of the target time series based on historical data trends.
- **Detect structural breaks** (sudden shifts in the data pattern) that could impact model performance, and adjust for them.
- **Ensure stationarity** of the time series through transformations (like differencing) and statistical tests.
- **Evaluate model performance** using appropriate error metrics and refine the model for better accuracy.

## 🛠️ Tools

- **R** – primary programming language used for analysis and modeling.
- **R Packages** – including `forecast` (for ARIMA modeling), `tseries` (for statistical tests like ADF), `strucchange` (for structural break detection), and `ggplot2` (for visualization).
- **Environment** – RStudio (or an R environment) for running the analysis.
- **Data** – Quarterly series for the U.S. 10-Year (Long-Term) Treasury yield, commonly denoted `rl`, from the `USeconomic` dataset in R.

## 🔍 Methodology

1. **Data Preparation** – Load the time series data into R and perform initial cleaning if the data is not clean.
2. **Exploratory Analysis** – Plot the time series to visualize trends, seasonal patterns, and any anomalies. Compute summary statistics to understand the data’s characteristics.
3. **Stationarity Testing** – Apply statistical tests (such as the Augmented Dickey-Fuller test) to check if the series is stationary. If the series is not stationary, apply transformations like differencing to achieve stationarity.
4. **Structural Break Analysis** – Examine the series for any structural breaks or regime shifts (using the `strucchange` package for tests such as Chow or Bai-Perron). Accounting for structural changes is crucial, as sudden shifts can lead to biased forecasts if left unaddressed (see [Structural Breaks in Time Series Analysis: Managing Sudden Changes](https://maseconomics.com/structural-breaks-in-time-series-analysis-managing-sudden-changes/) for discussion on this issue).
5. **Model Selection & Training** – Fit an appropriate time series forecasting model to the data. In this project, an ARIMA model is used (with parameters selected on the basis of analysis of ACF/PACF plots or you can do it with `auto.arima`). If a structural break was detected, incorporate it into the modeling approach (for example, by splitting the series into pre-break and post-break segments or adding dummy variables to the model).  
    ```r
    # Fit an ARIMA model to the time series
    library(forecast)
    model <- auto.arima(ts_data)  # ts_data is the time series object after preprocessing
    summary(model)
    ```
6. **Forecasting**  
   - Use the trained model to forecast future values over a specified horizon and plot predictions alongside historical data.  
   - **Recommended R Libraries:** `forecast` (classic ARIMA/ETS), `fabletools` (tidy forecasting), `tsibble` (time‐series tibbles), `ggplot2` (plotting).  
   - **Example (using `forecast`):**  
     ```r
     library(forecast)
     # `fit` is your ARIMA/SARIMA model
     fc <- forecast(fit, h = 12)  
     autoplot(fc) +
       ggtitle("Forecast vs. Historical") +
       xlab("Time") +
       ylab("Value")
     ```  
7. **Model Evaluation** – Compare the forecasts with actual outcomes (using a hold-out test set if available). Calculate error metrics such as Mean Absolute Error (MAE) or Root Mean Square Error (RMSE) to assess forecast accuracy. Additionally, examine the residuals of the model to ensure that no significant patterns remain (indicating the model has captured the structure in the data).

## 🚀 How to Use

1. **Clone the repository** to your local machine (or download the project files as a ZIP).  
2. **Open the project** in RStudio (or your preferred R environment).  
3. **Install required packages** if they are not already installed. This includes:
   - `forecast`  
   - `tseries`  
   - `strucchange`  
   - `ggplot2`  
   *(Use `install.packages("package_name")` in R.)*  
4. **Load the data** by ensuring the dataset (CSV file) is available and updating the file path in any scripts if necessary.  
5. **Follow the embedded code in the Report** to run each step of the analysis—data loading, preprocessing, model fitting, and forecasting. All R code snippets are provided within `Report.pdf`.  
6. **Review the output**:  
   - The Report contains all console outputs, plots, and model summaries you need.  
   - Use the guidelines in this section and the code examples from the Report to replicate or adapt the workflow for your own time series data.  

> **Note:** No standalone R script is provided in the repository. If you wish to run the analysis, refer to the code embedded in `Report.pdf`.  
>
> If you have any ideas or suggestions for improving this project—or questions about your own time series work—feel free to connect on [LinkedIn](https://www.linkedin.com/in/dsjaiminpatel).  

## 💡 Key Insights

- The time series displayed a clear upward trend (and possibly a seasonal pattern), indicating that simple models would not suffice without accounting for these components. Transformations like differencing were applied to make the series stationary for modeling.
- A significant **structural break** was observed in the data, corresponding to an external event that altered the underlying pattern. This regime shift highlighted the importance of adjusting our modeling strategy to avoid biased forecasts.
- By accounting for the structural break (e.g., training separate models before and after the break), the forecasting accuracy improved substantially. In contrast, a single model ignoring the break produced biased predictions following the change point.
- The final **ARIMA** model provided a good fit to the data, capturing the trend and variation in the series. The model’s forecasts closely matched the actual values in the test period, demonstrating effective performance with relatively low error margins.

## 📚 Learn More

1. [Impulse Response Functions in Time Series](https://rdrr.io/cran/fabletools/man/IRF.html)  
   📉 Official documentation for the `IRF()` function in the **fabletools** R package—explains how to compute and interpret impulse response functions to analyze the effect of a one-time shock to a time series model.

2. [SARIMA Model Equation Explanation](https://stats.stackexchange.com/questions/129901/sarima-model-equation)  
   📊 Q&A from Cross Validated discussing the mathematical equations, interpretation, and specification of SARIMA (Seasonal ARIMA) models.

3. [Managing Structural Breaks](https://maseconomics.com/structural-breaks-in-time-series-analysis-managing-sudden-changes)  
   ⚡ Blog post explaining structural breaks in time series, their impact on ARIMA models, and practical detection and management strategies.

4. [Lagged Scatter Plots in R](https://rdrr.io/github/jaspershen/laggedcor/man/lagged_scatter_plot.html)  
   🔄 Documentation for the `lagged_scatter_plot()` function in the **laggedcor** R package—shows how to plot a variable against its lagged values to visualize autocorrelation.

5. [Stata: Structural Break Features](https://www.stata.com/features/overview/structural-breaks/)  
   🛠️ Overview of Stata’s features for detecting and analyzing structural breaks in time series and econometric data.

6. [Tsay – Analysis of Financial Time Series](https://onlinelibrary.wiley.com/doi/book/10.1002/9780470644560)  
   📖 Publisher’s page for Ruey Tsay’s foundational book on financial time series modeling, covering theory, methods, and financial applications.

7. [Hamilton – Time Series Analysis (1994)](https://agorism.dev/book/finance/time-series/James%20Douglas%20Hamilton%20-%20Time%20Series%20Analysis%20%281994%2C%20Princeton%20University%20Press%29%20-%20libgen.lc.pdf)  
   📚 Full-text PDF of Hamilton’s classic graduate textbook—a rigorous reference for time series econometrics.

8. [Shumway & Stoffer – Time Series with R](https://www.stat.pitt.edu/stoffer/tsda/)  
   💡 Free website companion to *Time Series Analysis and Its Applications*—provides R code, data, and examples for hands-on learning.

## 📫 Contact

If you have any questions, feedback, or would like to collaborate, feel free to:  
- Open an issue in this repository  
- Connect on [LinkedIn](https://www.linkedin.com/in/dsjaiminpatel)  

Your suggestions and contributions are always welcome to help improve this project!  
