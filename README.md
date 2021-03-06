# SC1015 Mini-Project

Team 6: Eddy, Yue Zhong, & Bryan

# Table of Contents

- [Welcome Message](#welcome-message)
- [Team 6 Members](#team-6-members)
- [Question/Problem Definition](#questionproblem-definition)
- [Dataset Selection & Preparation](#dataset-selection--preparation)
    - [Kaggle](https://www.kaggle.com/datasets/teyang/singapore-hdb-flat-resale-prices-19902020)
- [Exploratory Data Analysis](#exploratory-data-analysis)
    - [EDA.ipynb](https://github.com/BLTech-py/sc1015/blob/main/EDA.ipynb)
    - [Flat Type](#flat-type)
    - [Town](#town)
    - [General Trend](#general-trend)
    - [Interesting Outlier](#interesting-outlier)
- [Machine Learning](#machine-learning)
    - [ARIMA.ipynb](https://github.com/BLTech-py/sc1015/blob/main/ARIMA.ipynb)
    - [ARIMA Introduction](#arima-introduction)
    - [Best Blk for ML](#best-blk-for-ml)
    - [p, d, q value Optimisation](#p-d-q-value-optimisation)
    - [Obtaining Test Data](#obtaining-test-data)
    - [Future Price Prediction](#future-price-prediction)
- [Insights of Data & Conclusion](#insights-of-data--conclusion)
- [Closing Remarks](#closing-remarks)
- [Version History](#version-history)
- [Extras](#extras)
- [References](#references)

# Welcome Message

Welcome to Team 6's SC1015 Mini-Project. This Mini-Project gave our team the opportunity to venture beyond the syllabus
and gain insightful skills & knowledge through the analysis of real world data.

We would also like to thank our TA Guo Xiaobao for constantly encouraging us to experiment with new methods in
approaching our problems and this Mini-Project would not have been possible without her valuable feedback and expertise
in the field of Data Science.

# Team 6 Members

| Name              |                     Area of Focus                     |GitHub Acount|
|---|:---:|---|
| Eddy Cheng Kuan Quan |        Kaggle Dataset, Problem Definition, EDA        |@eddy-ckq|
| Koh Yue Zhong     |     Video Presentation, SG Economy Research, EDA      |@yuezhonggg|
| Lee Wei Jie Bryan |       Machine Learning, GitHub Repository, EDA        |@BLTech-py|

# Question/Problem Definition

Buying a HDB flat in Singapore is a rite of passage of every Singaporean and nobody wants to make a losing deal when
dealing with property. This piqued our team's curiosity on the resale prices of HDB flats in singapore, leading us to
our question:

> *In Singapore, when is it the best time to sell your HDB flat if you are planning to upgrade?*

# Dataset Selection & Preparation

After extensive online searching, our team has identified an interesting and suitable dataset which we could use for
this Mini-Project on [Kaggle](https://www.kaggle.com/datasets/teyang/singapore-hdb-flat-resale-prices-19902020).

However, the datasets on Kaggle are separated
into [multiple files](https://github.com/BLTech-py/sc1015/tree/main/data_hdb) spanning across different years and there
were quite a lot of missing data. Thus, our team had to develop
a [python script](https://github.com/BLTech-py/sc1015/blob/main/data_hdb/clean.py) which would clean up the data by
combining all the different csv files into a
clean [single file](https://github.com/BLTech-py/sc1015/blob/main/data_hdb/hdb.csv) and fill in the missing data via
recalculation which we could then use for our Exploratory Data Analysis.

# Exploratory Data Analysis

For our Exploratory Data Analysis we conducted it in a jupyter notebook
titled [EDA.ipynb](https://github.com/BLTech-py/sc1015/blob/main/EDA.ipynb) and here are our findings:

## Flat Type

Majority of the data are 3-5 room HDB flats, therefore our team decided that this would be our focus for our
Mini-project.

<ins>Number of Data Points for each Flat Type</ins>

```
4 ROOM              309314
3 ROOM              272580
5 ROOM              170408
EXECUTIVE            62641
2 ROOM                9863
1 ROOM                1273
MULTI GENERATION       279
MULTI-GENERATION       223
```

## Town

When clustering the towns together, we noticed that the HDB flats in the `CENTRAL AREA` has a much steeper price
compared to the other towns for `4 ROOM` AND `5 ROOM` flats.

<ins>5 Room Top 3 Highest Resale Price</ins>

```
CENTRAL AREA         800000.0
QUEENSTOWN           526000.0
BUKIT MERAH          500000.0
```

## General Trend

When analyzing the general trend of `resale_price` by taking the median value for each year, we noticed 2 major
characteristics which are:

- Sharp Fall in `resale_price` during 1997
- Gradual Fall in `resale_price` after 2013

![image](https://github.com/BLTech-py/sc1015/blob/main/graphs/General%20Trend.png)

This could be due to the [1997 Asian Financial Crisis](https://www.britannica.com/event/Asian-financial-crisis)
and the
Singapore [HDB Cooling Measures](https://www.mortgagesupermart.com.sg/resources/mas-property-cooling-measures#:~:text=MAS%20announced%20new%20cooling%20measure,stamp%20duty%20for%20industrial%20properties.)
respectively.

![image](https://www.grips.ac.jp/teacher/oono/hp/image_f2/lec11_1cc.gif)

## Interesting Outlier

During our Exploratory Data Analysis, we chanced upon an interesting outlier which
is [Geylang Blk 60 Dakota Crescent (5 Room)](https://www.propertyguru.com.sg/singapore-property-listing/hdb/geylang/dakota-crescent_104886/60)
.

![image](https://sg1-cdn.pgimgs.com/projectnet-project/10164/ZPPHO.96911146.R800X800.jpg)

Despite all other flats decreasing in `resale_price` after 2013, the `resale_price` for this specific flat was
increasing over the years with the current `resale_price` being as high
as [$1,100,000](https://www.propertyguru.com.sg/singapore-property-listing/hdb/geylang/dakota-crescent_104886/60).

One possible reason our team has identified to explain this phenomenon could be due to its proximity to
the [Singapore National Stadium](https://www.stadiumguide.com/singapore-national-stadium/) which was open in 2014
leading to the spike in `resale_price`.

# Machine Learning

Now that we know some possible attributes that might affect the `resale_price` of a flat, let us attempt to predict the
future `resale_price` of a given flat to find out when would be the most optimal time to sell in order to maximise our
return of investment (ROI). The machine learning model we have chosen
is [ARIMA](https://www.investopedia.com/terms/a/autoregressive-integrated-moving-average-arima.asp#:~:text=An%20autoregressive%20integrated%20moving%20average%2C%20or%20ARIMA%2C%20is%20a%20statistical,values%20based%20on%20past%20values.)
and the jupyter notebook is titled [ARIMA.ipynb](https://github.com/BLTech-py/sc1015/blob/main/ARIMA.ipynb).

## ARIMA Introduction

ARIMA stands for Autoregressive (AR) Integrated (I) Moving Average (MA) which is a statistical analysis model that uses
time series data to predict future trends.

ARIMA consists of 3 variables which are used to fit the machine learning model:

- p-value: the number of lag observations (which a value of 1 represents 1 month)
- d-value: the number of times that observations are differenced (degree of differencing)
- q-value: the size of the moving average window (order of moving average)

In order for the ARIMA model to give a good prediction, we need as much data we can have over the spread of 1990-2020.
Thus, we need to identify which HDB block would be the best candidate to train our ARIMA model.

## Best Blk for ML

By grouping data points to a unique block we can observe the amount of data that each block has and the block with the
most data
is [Jurong West Blk 211 (3 Room)](https://www.propertyguru.com.sg/singapore-property-listing/hdb/jurong-west/boon-lay-place_103145/211)
.

<ins>Blk with the Most Data Points</ins>

|town|flat_type|block|street_name|floor_area_sqm|lease_commence_date|counts|
|---|---|---|---|---|---|---|
|JURONG WEST|3 ROOM|211|BOON LAY PL|65.0|1976|667|

![image](https://sg2-cdn.pgimgs.com/projectnet-project/8437/ZPPHO.96902193.R800X800.jpg)

## p, d, q value Optimisation

By observing the degree of differencing, we noticed the following:

![image](https://github.com/BLTech-py/sc1015/blob/main/graphs/d%20value.png)

- d-value = 0 (not stationary)
- d-value = 1 (good)
- d-value = 2 (over differentiated)

> Best d-value: 1

Through extensive optimisations in obtaining the highest `R^2` and the lowest `MSE` values, our team have derived the
best `p_value` & `q_value` for our `ARIMA` model:

> Best p-value: 44

> Best d-value: 25

## Obtaining Test Data

Although now we have the best `p_value`, `d_value`, & `q_value`, we are still missing test data to evaluate the accuracy
of our `ARIMA` prediction.

To obtain the latest real world `resale_price` of our best HDB blk we decided to web scrape the most recent resale
prices
on [PropertyGuru](https://www.propertyguru.com.sg/singapore-property-listing/hdb/jurong-west/boon-lay-place_103145/211)
using `selenium` in our python
script [web_scrape_test_data.py](https://github.com/BLTech-py/sc1015/blob/main/web_scrape_test_data.py).

## Future Price Prediction

Now that we have `train_data`, `test_data` and the best `p_value`, `d_value`, &`q_value`, we can finally train
our `ARIMA` model with the best blk dataset.

```
model = ARIMA(df, order=(best_p_value, best_d_value ,best_q_value))
```

<ins>ARIMA Model (1990-2023)</ins>

This is how our `ARIMA Prediction` (blue) looks like against the `Actual Past` data (orange) which we used to train the
model and the `Actual Future` (green) data which we web scraped online. Since the prediction is from 2019 onwards we
should zoom in to the range of 2018-2023 for a better analysis of our `ARIMA` prediction.

![image](https://github.com/BLTech-py/sc1015/blob/main/graphs/ARIMA%201990-2023.png)

<ins>ARIMA Model (2018-2023)</ins>

For easier analysis, we further broke up the test data in to 3 separate years and colour coded them:

- `2019` (green)
- `2020` (red)
- `2021` (purple)

We can observe from the graph shown below that the `resale_price` prediction is relatively accurate for `2019`
and `2020`, however it is extremely inaccurate for `2021`. Thus, we can conclude that our `ARIMA` prediction model is
suitable for near future predictions, however it would not be recommended for long term predictions (>2 years).

![image](https://github.com/BLTech-py/sc1015/blob/main/graphs/ARIMA%202018-2023.png)

# Insights of Data & Conclusion

From this Mini-Project we can learn a few things:

1. `resale_price` is very heavily influenced by economic performance and government intervention
2. `resale_price` could also be influence by development of new amenities in proximity to the HDB flat
3. `ARIMA` is a relatively good prediction model for the near future, however is not a good predictor in the long
   term (>2 years)

Therefore, going back to our initial question, to determine when is the most optimal time to sell our HDB flat we need
to take into account of all the above by monitoring the economy's growth, studying the latest government HDB cooling
measures, observing new developments in the neighbourhood and last but not least consider using the `ARIMA` prediction
model to analyze the `resale_price` behaviour in the upcoming years to maximise our return of investment (ROI).

# Closing Remarks

This Mini-Project was a product of many weeks of hard work and research. I would like to extend my gratitude to my
teammates for their utmost efforts and collaboration throughout the project. The past few weeks has truly been an
exciting journey, learning many new concepts and ideas. This marks the end of our Mini-Project, however this is not the
end of our programming journey.

*This is only the beginning.*

# Version History

Here is the version history of our Mini-Project over the span of one and a half months.

> Version Format: v*MAJOR*.*MINOR*.*PATCH*

### v0.0.0 Clean Data (2022/03/06)

- Cleaned all data into `hdb.csv`
- `hdb.csv` 826581 data entries
- `remaining_lease` missing 709054 data

### v0.0.1 README Hotfix (2022/03/06)

- Fixed markdown headings issue

### v0.0.2 Clean Data Drop Columns (2022/03/07)

- Dropped `remaining_lease`, `street_name`, `storey_range` columns

### v0.0.3 README Update (2022/03/07)

- Added EDA
- Fixed typo

### v0.1.0 README Update (2022/03/27)

- Added Time Series EDA
- flat_type breakdown
- 3-5 Room Cluster & Median

### v0.1.1 Clean Data Update (2022/03/31)

- Added `remaining_lease` missing data

```
remaining_lease = (lease_commence_date + 99) - year
```

- Added `year` and `month`
- Restored `street_name` and `storey_range` (for unit tracking)

### v0.2.0 ARIMA (2022/04/02)

- Added `ARIMA` model
- Added Interpolation for missing data
- Added `auto_arima` params (failed)
- Added `LSTM` model (failed)

### v0.2.1 ARIMA Web Scrape Test Data (2022/04/03)

- Added `web_scrape_test_data.py` script to scrape test data
- Added `chromedriver` (for `selenium` to work)
- Generated `test_data.csv`
- Added `web_scrape_pd` (failed: 403 forbidden)
- Added `web_scrape_bs4` (failed: 403 forbidden)

### v0.2.2 ARIMA R^2 MSE RMSE (2022/04/03)

- Added `r2`, `mse` and `rmse` fns

### v0.3.0 ARIMA Optimisation & CSV Reorganization (2022/04/17)

- Optimised ARIMA model (found best p-value, d-value, q-value)
- Renamed folder `archive` to `data_hdb`
- Added folder `data_arima`

### v0.3.1 Extras Clean Up (2022/04/17)

- Added folder `extras`
- Renamed & Moved all extra content to `extras` folder
- Renamed `Time Series` to `EDA`

### v1.0.0 Final Submission (2022/04/17)

- Finalized `README` content
- Added hyperlinks to all files

### v1.1.0 Submission Update (2022/04/22)

- NTULearn Mini-Project Submission Announcement (2022/04/21)
- Updated `README`

# Extras

Here are some extra `EDA` jupyter notebooks that our team did to further explore our dataset & also an `alpha version`
of our `ARIMA` model.

<ins>EDA jupyter notebooks</ins>

- [town.ipynb](https://github.com/BLTech-py/sc1015/blob/main/extras/town.ipynb)
- [floor_area_sqm.ipynb](https://github.com/BLTech-py/sc1015/blob/main/extras/floor_area_sqm.ipynb)
- [remaining_lease.ipynb](https://github.com/BLTech-py/sc1015/blob/main/extras/remaining_lease.ipynb)
- [remaining_lease_flat_type.ipynb](https://github.com/BLTech-py/sc1015/blob/main/extras/remaining_lease_flat_type.ipynb)
- [remaining_lease_location.ipynb](https://github.com/BLTech-py/sc1015/blob/main/extras/remaining_lease_location.ipynb)

<ins>ARIMA alpha version</ins>

- [ARIMA_alpha.ipynb](https://github.com/BLTech-py/sc1015/blob/main/extras/ARIMA_alpha.ipynb)

# References

- https://www.kaggle.com/datasets/teyang/singapore-hdb-flat-resale-prices-19902020
- https://www.britannica.com/event/Asian-financial-crisis
- https://www.mortgagesupermart.com.sg/resources/mas-property-cooling-measures#:~:text=MAS%20announced%20new%20cooling%20measure,stamp%20duty%20for%20industrial%20properties
- https://www.grips.ac.jp/teacher/oono/hp/image_f2/lec11_1cc.gif
- https://www.propertyguru.com.sg/singapore-property-listing/hdb/geylang/dakota-crescent_104886/60
- https://sg1-cdn.pgimgs.com/projectnet-project/10164/ZPPHO.96911146.R800X800.jpg
- https://www.stadiumguide.com/singapore-national-stadium/
- https://www.investopedia.com/terms/a/autoregressive-integrated-moving-average-arima.asp#:~:text=An%20autoregressive%20integrated%20moving%20average%2C%20or%20ARIMA%2C%20is%20a%20statistical,values%20based%20on%20past%20values
- https://www.propertyguru.com.sg/singapore-property-listing/hdb/jurong-west/boon-lay-place_103145/211
- https://sg2-cdn.pgimgs.com/projectnet-project/8437/ZPPHO.96902193.R800X800.jpg