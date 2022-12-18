---
title: "Rolling Correlations: Time Series Relationships"
date: 2022-12-17T22:04:08-05:00
draft: false
tags: ["Econometrics", "Economics"]
---
Rolling correlations are correlations between two time series data sets using rolling window. Unlike ordinary correlation analyses, they offer the advantage of visualising the relationship between variables across multiple consecutive time periods. In the Excel chart below, quarterly prices of Spot WTI and Brent crude oil prices are used to produce four-quarter rolling correlations across the period from 2Q1999 to 3Q2022: each point represents a four-quarter correlation between the price of WTI and Brent. (Data from [FRED](https://fred.stlouisfed.org/).)

Such an approach allows us to quickly visualise inconsistencies in data trends: for the data below the 2010 to 2015 period exhibits diverging WTI-Brent trends. (Upon a quick search, it appears that this inconsistency reflects a shift in market fundamentals and sentiment amid events such as the US "Shale Revolution"!)

![Rolling Corr](/Rolling.jpg)

Rolling correlation calculations can be performed in Excel simply by applying the **=CORREL** function to each rolling period (e.g., every consecutive four quarters).
