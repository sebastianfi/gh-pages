Car statistics presentation
========================================================
author: Sebastian ILINCA
date: 15 November 2018
autosize: true

The application will give simple statistics about cars
========================================================

Source file is mtcars.csv with info about brand, consumption, myleage, etc.

Application uses some of the data to present:
- consumption depending on mileage
- consumption depending on gears used
- consumption depending on no of cylinders

Use the dropdown list to adjust the criteria (mileage, gears or cylinders)
and obtain the calculation illustrated directly in the box plot

Code used to obtain the calculation
========================================================


```r
library(shiny)
library(datasets)
mpgData <- mtcars
mpgData$am <- factor(mpgData$am, labels = c("Automatic", "Manual"))
shinyServer(function(input, output) {
       formulaText <- reactive({
                paste("mpg ~", input$variable)
        })
        
        output$caption <- renderText({
                formulaText()
        })
        
        output$mpgPlot <- renderPlot({
                boxplot(as.formula(formulaText()), 
                        data = mpgData,
                        outline = input$outliers)
        })
})
```

Box Plot CODE
========================================================


```r
library(shiny)
library(ggplot2)
library(shiny)
library(dplyr)
shinyUI(pageWithSidebar(
        
        # Application title
        headerPanel("Miles Per Gallon"),
        
        # Sidebar with controls to select the variable to plot against mpg
        # and to specify whether outliers should be included
        sidebarPanel(
                selectInput("variable", "Variable:",
                            list("Cylinders" = "cyl", 
                                 "Transmission" = "am", 
                                 "Gears" = "gear")),
                
                checkboxInput("outliers", "Show outliers", FALSE)
        ),
        
        # Show the caption and plot of the requested variable against mpg
        mainPanel(
                h3(textOutput("caption")),
                
                plotOutput("mpgPlot")
        )
))
```

<!--html_preserve--><div class="container-fluid">
<div class="row">
<div class="col-sm-12">
<h1>Miles Per Gallon</h1>
</div>
</div>
<div class="row">
<div class="col-sm-4">
<form class="well">
<div class="form-group shiny-input-container">
<label class="control-label" for="variable">Variable:</label>
<div>
<select id="variable"><option value="cyl" selected>Cylinders</option>
<option value="am">Transmission</option>
<option value="gear">Gears</option></select>
<script type="application/json" data-for="variable" data-nonempty="">{}</script>
</div>
</div>
<div class="form-group shiny-input-container">
<div class="checkbox">
<label>
<input id="outliers" type="checkbox"/>
<span>Show outliers</span>
</label>
</div>
</div>
</form>
</div>
<div class="col-sm-8">
<h3>
<div id="caption" class="shiny-text-output"></div>
</h3>
<div id="mpgPlot" class="shiny-plot-output" style="width: 100% ; height: 400px"></div>
</div>
</div>
</div><!--/html_preserve-->

Box Plot Miles per gallon
========================================================

<!--html_preserve--><div class="container-fluid">
<div class="row">
<div class="col-sm-12">
<h1>Miles Per Gallon</h1>
</div>
</div>
<div class="row">
<div class="col-sm-4">
<form class="well">
<div class="form-group shiny-input-container">
<label class="control-label" for="variable">Variable:</label>
<div>
<select id="variable"><option value="cyl" selected>Cylinders</option>
<option value="am">Transmission</option>
<option value="gear">Gears</option></select>
<script type="application/json" data-for="variable" data-nonempty="">{}</script>
</div>
</div>
<div class="form-group shiny-input-container">
<div class="checkbox">
<label>
<input id="outliers" type="checkbox"/>
<span>Show outliers</span>
</label>
</div>
</div>
</form>
</div>
<div class="col-sm-8">
<h3>
<div id="caption" class="shiny-text-output"></div>
</h3>
<div id="mpgPlot" class="shiny-plot-output" style="width: 100% ; height: 400px"></div>
</div>
</div>
</div><!--/html_preserve-->
