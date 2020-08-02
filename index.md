---
title       : Developing Data Products Week 4 Assignment pitch Presentation
subtitle    :  Interactive Plot Presentation
author      : Yash Prakash
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---



## Overview: This Presentation describes the features of the  shiny app used to generate an interactive BoxPlot using the data from mtcars data.
 Features:
 1. The User Interface consists of a title panel, sidebar layout and the main panel.
 2. The side bar layout consists of a radio button group which gives an option to the user to provide
    number of cylinders and describes the colour of the boxPlot which will be rendered based on the choice
    of the number of cylinders.
 3. The back end server component takes the input of the number of cylinders and subsets the mtcars data based on the cyl = <the input value>
 4.  boxPlot is filled with the appropriate colour based on the input provided.

--- .class #id

## Source Code. ui.r

```r
library(shiny)
# Define UI for application that draws a histogram
shinyUI(fluidPage(
    titlePanel("Dynamic Box Plot Generation using shiny UI"),
    sidebarLayout(
        sidebarPanel(
            radioButtons("cylinderNumbers", "Cylinder Numbers:",
                         c("4- Red" = 4,
                           "6- Blue" = 6,
                           "8- Green" = 8))
        ),
        mainPanel(
            plotOutput("boxPlot")
        )
    )))
```

--- .class #id
## Source Code. server.r

```r
library(shiny)
library(ggplot2)
shinyServer(function(input, output) {
    output$boxPlot <- renderPlot({
        boxColor <- c("blue") 
         cyl1 = input$cylinderNumbers
         if (cyl1 == 4) {
            boxColor <- c("red")
         }
         if (cyl1 == 6) {
           boxColor <- c("blue")
         }
        if (cyl1 == 8) {
            boxColor <- c("green")
         }
         mtcars1 <-subset(mtcars, cyl == cyl1)
         ggplot(mtcars1, aes(x=as.factor(cyl), y=mpg)) + geom_boxplot(fill = boxColor)
         p <- ggplot(mtcars1, aes(x=as.factor(cyl), y=mpg)) + geom_boxplot(fill = boxColor)
         p + ggtitle("BoxPlot MPG vs Cyl") + xlab("Number of Cylinders")+ylab("Miles Per Gallon")})})
```

--- .class #id
## mtcars sample data used for analysis

```r
head(mtcars)
```

```
##                    mpg cyl disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
## Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1
## Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2
## Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1
```
Following is the Link to the shiny.io where the application is deployed
https://yash07.shinyapps.io/shiny/






