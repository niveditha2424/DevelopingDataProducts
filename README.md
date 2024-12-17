# DevelopingDataProducts
# Analysis of the mtcars Dataset

This project explores the `mtcars` dataset, extracted from the 1974 Motor Trend US magazine. The dataset includes fuel consumption and several aspects of automobile design and performance for 32 different car models.

## Overview

The goal of this analysis is to explore relationships between various variables in the `mtcars` dataset, specifically focusing on predicting miles per gallon (`mpg`) based on other car attributes. A Shiny application was also created to enable interactive exploration of these relationships.

## Dataset

The dataset includes 32 observations on 11 variables:

| Variable | Description |
|----------|-------------|
| `mpg`    | Miles per gallon |
| `cyl`    | Number of cylinders |
| `disp`   | Displacement (cu.in.) |
| `hp`     | Gross horsepower |
| `drat`   | Rear axle ratio |
| `wt`     | Weight (lb/1000) |
| `qsec`   | 1/4 mile time |
| `vs`     | V/S |
| `am`     | Transmission (0 = automatic, 1 = manual) |
| `gear`   | Number of forward gears |
| `carb`   | Number of carburetors |

### Source:
- Henderson and Velleman (1981), *Building Multiple Regression Models Interactively*, Biometrics, 37, 391-411.

## Key Insights and Analysis

The project includes regression analysis to model `mpg` as a function of other car features. Using R, the following key insights were identified:

1. **Exploratory Data Analysis (EDA):** Visualization of correlations between variables.
2. **Linear Model:** A linear regression model was developed to predict `mpg` based on the number of cylinders, horsepower, weight, and other variables.

## Interactive Shiny Application

An interactive Shiny app was developed to explore the regression models and visualize how different features impact `mpg`. The app allows users to dynamically adjust inputs and see real-time predictions.

## Example Code

```r
library(datasets)
data(mtcars)

# Linear model formula
formulaTextPoint <- reactive({
  paste("mpg ~", "as.integer(", input$variable, ")")
})

# Fit the model
fit <- reactive({
  lm(as.formula(formulaTextPoint()), data=mpgData)
})

# Render the model summary
output$fit <- renderPrint({
  summary(fit())
})

# Plot the data
output$mpgPlot <- renderPlot({
  with(mpgData, {
    plot(as.formula(formulaTextPoint()))
    abline(fit(), col=2)
  })
})
