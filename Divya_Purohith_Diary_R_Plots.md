---
title: "Diary"
author: "Divya Purohith"
date: "November 16, 2018"
output: 
  html_document: 
    keep_md: yes
---

I have chosen base R to learn..

**Data Visualization**


```r
library(MASS)
```

Two types of data visualization:

**Exploratory visualizations** help us understand the data. It keeps as much details as possible.
**Explanatory visualizations** help us share our
understanding with others. It highlights the key features you want to emphasize in the data.

R supports both types of visualization.

**There are 4 graphics systems in R**
Base graphics: Easiest to learn and focus of this course
Grid graphics: powerful set of modules for building other
tools
La!ice graphics: general purpose system based on grid
graphics 
ggplot2: Grammar of graphics


```r
str(whiteside)
```

```
## 'data.frame':	56 obs. of  3 variables:
##  $ Insul: Factor w/ 2 levels "Before","After": 1 1 1 1 1 1 1 1 1 1 ...
##  $ Temp : num  -0.8 -0.7 0.4 2.5 2.9 3.2 3.6 3.9 4.2 4.3 ...
##  $ Gas  : num  7.2 6.9 6.4 6 5.8 5.8 5.6 4.7 5.8 5.2 ...
```

```r
plot(whiteside)
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

```r
plot(whiteside$Temp, whiteside$Gas, xlab = "Outside temperature", ylab = "Heating gas consumption")
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-2-2.png)<!-- -->
Example of plot:
plot(data$cars,data$minds). It will take data$cars automatically as X and the other one as y. We can also add title with title("cars vs minds").

For grid graphics we need to load the grid package.

**There are different plors in R**
1. Scatter plot
2. Sunflower plot
3. Boxplot (Used to know the range of numerical variables in the data. This is to see the distrubution, I am gonna use this for my drosophila egg laying data).
4. Mosaic plot(Relationship between the variables)
5. Pie charts are the poor choice to use.

**Graphics**
Graphics can be low level or high level
we can even add colour and shapes to the points,lines and texts in our graphs. Shapes of the points can be specified either by the number or single alphabetic letter.


**CHARACTERIZING A SINGLE  VARIABLE**
histogram is the best way to look how the numeric variables are disturbuted over their range
hist() is the function used. truehist() is the alternate form of hist.

qqPlot()


Visualization relations between two variables



```r
library(MASS) 
plot(rad ~zn, data = Boston) #Gives scatterplot. 
title("Scatter plot")
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-3-1.png)<!-- -->


```r
library(MASS)
sunflowerplot(rad ~zn, data = Boston)
title("Sunflower plot")
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-4-1.png)<!-- -->


```r
boxplot(crim ~ rad, #showing the distribution of numerical crim values over the different distinct rad values
  data = Boston, 
  varwidth = T,
  log = "y", #logtransformed values for y
  las = 1) #horizontal labels for both x and y
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-5-1.png)<!-- -->


```r
mosaicplot(carb ~ cyl, 
  data = mtcars,
  color = T) #color true will keep the color 
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

```r
  #mosaic with inbuilt mtcars R example
```


#For bagplot we need to load aplpack


```r
library(aplpack)
```

```
## Loading required package: tcltk
```

```r
bagplot(Cars93$Min.Price, Cars93$Max.Price, cex= 1.20) #cex to make the point size bigger
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-7-1.png)<!-- -->

#showing more complex relationships
corplot() library(corplot)
sapply(dataset, is.numeric) 
#corelation matrices for multiple variables 


```r
library(corrplot)
```

```
## corrplot 0.84 loaded
```

```r
col_numeric <- sapply(Boston, is.numeric)
numericalVars <- Boston[, col_numeric]
str(numericalVars)
```

```
## 'data.frame':	506 obs. of  14 variables:
##  $ crim   : num  0.00632 0.02731 0.02729 0.03237 0.06905 ...
##  $ zn     : num  18 0 0 0 0 0 12.5 12.5 12.5 12.5 ...
##  $ indus  : num  2.31 7.07 7.07 2.18 2.18 2.18 7.87 7.87 7.87 7.87 ...
##  $ chas   : int  0 0 0 0 0 0 0 0 0 0 ...
##  $ nox    : num  0.538 0.469 0.469 0.458 0.458 0.458 0.524 0.524 0.524 0.524 ...
##  $ rm     : num  6.58 6.42 7.18 7 7.15 ...
##  $ age    : num  65.2 78.9 61.1 45.8 54.2 58.7 66.6 96.1 100 85.9 ...
##  $ dis    : num  4.09 4.97 4.97 6.06 6.06 ...
##  $ rad    : int  1 2 2 3 3 3 5 5 5 5 ...
##  $ tax    : num  296 242 242 222 222 222 311 311 311 311 ...
##  $ ptratio: num  15.3 17.8 17.8 18.7 18.7 18.7 15.2 15.2 15.2 15.2 ...
##  $ black  : num  397 397 393 395 397 ...
##  $ lstat  : num  4.98 9.14 4.03 2.94 5.33 ...
##  $ medv   : num  24 21.6 34.7 33.4 36.2 28.7 22.9 27.1 16.5 18.9 ...
```

```r
corrMat <- cor(numericalVars)
corrplot(corrMat, method = "ellipse")
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-8-1.png)<!-- -->


rpart() library(rpart)
#gives us tree models


```r
library(rpart)
library(MASS)
tree_model <- rpart(medv ~ ., data = Boston)
plot(tree_model)
text(tree_model, cex = .7) #label easier to read
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

pch 
pch = 0,square
pch = 1,circle
pch = 2,triangle point up
pch = 3,plus
pch = 4,cross
pch = 5,diamond
pch = 6,triangle point down
pch = 7,square cross
pch = 8,star
pch = 9,diamond plus
pch = 10,circle plus
pch = 11,triangles up and down
pch = 12,square plus
pch = 13,circle cross
pch = 14,square and triangle down
pch = 15, filled square
pch = 16, filled circle
pch = 17, filled triangle point-up
pch = 18, filled diamond
pch = 19, solid circle
pch = 20,bullet (smaller circle)
pch = 21, filled circle blue
pch = 22, filled square blue
pch = 23, filled diamond blue
pch = 24, filled triangle point-up blue
pch = 25, filled triangle point down blue

***linear regression model***

```r
linear_model <- lm(Gas ~ Temp, data = whiteside)
plot(whiteside$Temp, whiteside$Gas, xlab ="Temperature", ylab="Gas", pch=15,col="blue")
abline(linear_model, lty = 2)
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-10-1.png)<!-- -->
#The font "face" (1=plain, 2=bold, 3=italic, 4=bold-italic)
#srt can be positive or negative numbers. It rotates the labels
par sets the parameters to the graphs


```r
plot(whiteside$Temp, whiteside$Gas, pch=17)
indecB <- which(whiteside$Insul == "Before")
text(x = whiteside$Temp, y = whiteside$Gas,
     labels = "Before", col = "blue", srt = 30, cex = .8) #srt here is positive. cex .8 will reduce 80% text size from default. 
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-11-1.png)<!-- -->

```r
#include text in the graph. 
```

#Adding legend to the plot
adj moves the text to right or left.


```r
plot(whiteside$Temp, whiteside$Gas,
     type = "n", 
     xlab = "Outside temperature",
     ylab = "Heating gas consumption")
indexB <- which(whiteside$Insul == "Before")
indexA <- which(whiteside$Insul == "After")
points(whiteside$Temp[indexB], whiteside$Gas[indexB], pch = 17) 
points(whiteside$Temp[indexA],whiteside$Gas[indexA], pch = 1)
legend("topright", pch = c(17,1), 
       legend = c("Before", "After")) #legend is used to label the legend
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-12-1.png)<!-- -->

#axis() adds axis to the plot. axis=1 is below, axis=2 is left, axis=3 is top, axis=4 is right.
if axis is fales, it creates no axis to the plot


```r
boxplot(sugars ~ shelf, data = UScereal, axes = F)
axis(side = 2)
axis(side = 1, at = c(1,2,3)) #at add thes axis at specific numerics
axis(side = 3, at = c(1,2,3),
     labels = c("floor","middle","top")) #labels the given names at 1,2,3
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-13-1.png)<!-- -->

supsmu() smooth values to the trendline, takes x and y values and incorporates to the graph.


```r
plot(Cars93$Horsepower, Cars93$MPG.city)
trend1 <- supsmu(Cars93$Horsepower, Cars93$MPG.city)
lines(trend1)
trend2 <- supsmu(Cars93$Horsepower, Cars93$MPG.city, bass = 10)
lines(trend2, lty = 3, lwd = 2) #lwd is line-width #lty 3 is dotted line
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-14-1.png)<!-- -->

***Managing visual complexity***
matplot() , generates plot with various scatter plots on the same axes.
matrix on y axis.


```r
matplot(
  UScereal$calories, 
  UScereal[,c('protein', 'fat')], 
  xlab = "calories",
  ylab = "")
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-15-1.png)<!-- -->

wordcloud()
wordclouds, displays that present words in varying sizes depending on their frequency. That is, more frequent words appear larger in the display, while rarer words appear in a smaller font.
wordcloud(words = names(___), 
          freq = as.numeric(___), 
          scale =c(max,min)


```r
library(wordcloud)
```

```
## Loading required package: RColorBrewer
```

```r
model_table <- table(Cars93$Model)
wordcloud(words = names(model_table), 
          freq = as.numeric(model_table), 
          scale = c(0.75,0.25), #tells how the wordcloud appears
          min.freq = 1)
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-16-1.png)<!-- -->

***multple plot arrays***
par() sets parameters to the graphs


```r
par(mfrow = c(2,2))
plot(geyser$duration, main = "Raw data")
truehist(geyser$duration, main = "Histogram")
plot(density(geyser$duration), main = "Density")
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-17-1.png)<!-- -->

layout()


```r
layoutMatrix <- matrix(
  c( 0, 1, 2, 0,0, 3), byrow = T,nrow = 3) #nrow, tells there are 3
layout(layoutMatrix) #used the matrix constructed 
layout.show(n = 3) #see layout of all 3 plots
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-18-1.png)<!-- -->

barplot() function has the side effect of creating the plot we want, but it also returns a numerical vector with the center positions of each bar in the plot.


```r
tbl <- table(Cars93$Cylinders)
mids <- barplot(tbl, horiz = T,
                col = "transparent",
                names.arg = "")
text(20, mids, names(tbl)) #at the horizontal position 20
text(35, mids, as.numeric(tbl))
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-19-1.png)<!-- -->

symbols() function to display relations between more than two variables
The symbols() function allows us to extend scatterplots to show the influence of other variables.


```r
symbols(Cars93$Horsepower, Cars93$MPG.city,
        circles = sqrt(Cars93$Price))
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-20-1.png)<!-- -->

```r
        symbols(Cars93$Horsepower, Cars93$MPG.city,
        circles = sqrt(Cars93$Price),
        inches = 0.1)
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-20-2.png)<!-- -->


```r
# Call png() with the name of the file we want to create
png('bubbleplot.png')
# Save our file and return to our interactive session
dev.off()
```

```
## png 
##   2
```
#Using colour to enhance bubble plot




```r
IScolors <- c("red", "green", "yellow", "blue",
              "black", "white", "pink", "cyan",
              "gray", "orange", "brown", "purple")
cylinderLevel <- as.numeric(Cars93$Cylinders)
symbols(
  Cars93$Horsepower, Cars93$MPG.city, 
  circles = as.numeric(Cars93$Cylinders), 
  inches = 0.2, #size of bubbles
  bg = IScolors[cylinderLevel]) #bg is color of each bubble
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-22-1.png)<!-- -->

Thetableplot() function constructs a set of side-by-side horizontal barplots, one for each variable


```r
library(insuranceData)
data(dataCar)
suppressPackageStartupMessages(library(tabplot))
tableplot(dataCar)
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-23-1.png)<!-- -->
lattice xyplot()
lattice is a general-purpose graphics package that provides alternative implementations of many of the plotting functions available in base graphics. Specific examples include scatterplots with the xyplot() function, bar charts with the barchart() function, and boxplots with the bwplot() function.


```r
library(lattice)
calories_vs_sugars_by_shelf <- calories ~ sugars | shelf
xyplot(calories_vs_sugars_by_shelf, data = UScereal)
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-24-1.png)<!-- -->

ggplot2()


```r
# Load the ggplot2 package
library(ggplot2)

# Create the basic plot (not displayed): basePlot
basePlot <- ggplot(Cars93, aes(x = Horsepower, y = MPG.city))

# Display the basic scatterplot
basePlot + 
  geom_point()
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-25-1.png)<!-- -->

```r
# Color the points by Cylinders value
# Color the points by Cylinders value
basePlot + 
  geom_point(colour = IScolors[Cars93$Cylinders])
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-25-2.png)<!-- -->

```r
# Make the point sizes also vary with Cylinders value
basePlot + 
  geom_point(colour = IScolors[Cars93$Cylinders], 
             size = as.numeric(Cars93$Cylinders))
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-25-3.png)<!-- -->


I want to try what I have learnt on my own data. Introduction to my data.

There are three populations (described more completely in the "material and methods section")   
1) C:  "uncontrolled mating" (control)   
2) (O)M: "older male mated with younger female"   
3) (O)F: "older female mated with younger male"   
![Experimental Design](experimental_design.jpeg)

Pair "(3-23 d) fertility" was measured by mating a 20 day old Control virgin male with a 3 day old (O)M virgin female and recording eggs per day from 3 - 23 d.


```r
egg_data <- read.csv("CE_egg_transposed.csv",header=TRUE)
str(egg_data) # for structure of egg_data
```

```
## 'data.frame':	40 obs. of  51 variables:
##  $ Days_of_egg_laying: int  NA 1 NA 2 NA 3 NA 4 NA 5 ...
##  $ X1M_1             : int  NA 52 NA 54 NA 41 NA 17 NA 21 ...
##  $ X1M_2             : int  NA 53 NA 41 NA 39 NA 43 NA 19 ...
##  $ X1M_3             : int  NA 49 NA 43 NA 29 NA 17 NA 18 ...
##  $ X1M_4             : int  NA 47 NA 39 NA 43 NA 28 NA 23 ...
##  $ X1M_5             : int  NA 33 NA 36 NA 46 NA 38 NA 31 ...
##  $ X1M_6             : int  NA 48 NA 51 NA 42 NA 36 NA 21 ...
##  $ X1M_7             : int  NA 42 NA 38 NA 31 NA 37 NA 14 ...
##  $ X1M_8             : int  NA 36 NA 39 NA 27 NA 30 NA 22 ...
##  $ X1M_9             : int  NA 36 NA 43 NA 29 NA 40 NA 26 ...
##  $ X1M_10            : int  NA 43 NA 39 NA 47 NA NA NA NA ...
##  $ X2M_1             : int  NA 42 NA 40 NA 46 NA 37 NA 22 ...
##  $ X2M_2             : int  NA 37 NA 29 NA 35 NA 33 NA 17 ...
##  $ X2M_3             : int  NA 43 NA 36 NA 39 NA 36 NA 14 ...
##  $ X2M_4             : int  NA 39 NA 37 NA 36 NA 43 NA 20 ...
##  $ X2M_5             : int  NA 39 NA 37 NA 37 NA 44 NA 21 ...
##  $ X2M_6             : int  NA 38 NA 34 NA 26 NA 19 NA 18 ...
##  $ X2M_7             : int  NA 48 NA 43 NA 29 NA 23 NA 14 ...
##  $ X2M_8             : int  NA 39 NA 40 NA 39 NA 27 NA 20 ...
##  $ X2M_9             : int  NA 52 NA 43 NA 48 NA 23 NA 19 ...
##  $ X2M_10            : int  NA 51 NA 47 NA 39 NA 29 NA 23 ...
##  $ X3M_1             : int  NA 51 NA 48 NA 62 NA 26 NA 23 ...
##  $ X3M_2             : int  NA 49 NA 38 NA 47 NA 30 NA 29 ...
##  $ X3M_3             : int  NA 45 NA 41 NA 38 NA 36 NA 38 ...
##  $ X3M_4             : int  NA 48 NA 41 NA 38 NA 35 NA 27 ...
##  $ X3M_5             : int  NA 41 NA 48 NA 47 NA 39 NA 29 ...
##  $ X3M_6             : int  NA 38 NA 35 NA 39 NA 23 NA 21 ...
##  $ X3M_7             : int  NA 43 NA 49 NA 37 NA 31 NA 29 ...
##  $ X3M_8             : int  NA 42 NA 47 NA 38 NA 29 NA 21 ...
##  $ X3M_9             : int  NA 46 NA 49 NA 36 NA 32 NA 39 ...
##  $ X3M_10            : int  NA 41 NA 46 NA 39 NA 32 NA 17 ...
##  $ C_1               : int  NA 78 NA 58 NA 61 NA 59 NA 54 ...
##  $ C_2               : int  NA 69 NA 49 NA 64 NA 59 NA 57 ...
##  $ C_3               : int  NA 67 NA 60 NA 65 NA 71 NA 69 ...
##  $ C_4               : int  NA 77 NA NA NA NA NA NA NA NA ...
##  $ C_5               : int  NA 65 NA 59 NA 48 NA 46 NA 47 ...
##  $ C_6               : int  NA 63 NA 52 NA 71 NA 67 NA 63 ...
##  $ C_7               : int  NA 71 NA 72 NA 71 NA 77 NA 73 ...
##  $ C_8               : int  NA 69 NA 61 NA 89 NA 76 NA 75 ...
##  $ C_9               : int  NA 73 NA 58 NA 49 NA 41 NA 39 ...
##  $ C_10              : int  NA 88 NA 85 NA 49 NA 49 NA 47 ...
##  $ C_11              : int  NA 71 NA 87 NA 61 NA 59 NA 57 ...
##  $ C_12              : int  NA 62 NA 64 NA 68 NA 64 NA 61 ...
##  $ C_13              : int  NA 61 NA 59 NA 58 NA 48 NA 43 ...
##  $ C_14              : int  NA 68 NA 62 NA 89 NA 76 NA 74 ...
##  $ C_15              : int  NA 73 NA 69 NA 71 NA 68 NA 69 ...
##  $ C_16              : int  NA 71 NA 61 NA 52 NA 51 NA 49 ...
##  $ C_17              : int  NA 77 NA 62 NA 70 NA 65 NA 61 ...
##  $ C_18              : int  NA 83 NA 76 NA 78 NA 63 NA 60 ...
##  $ C_19              : int  NA 64 NA 53 NA 62 NA 59 NA 55 ...
##  $ C_20              : int  NA 61 NA 59 NA 58 NA 57 NA 53 ...
```


```r
colnames(egg_data) # column names 
```

```
##  [1] "Days_of_egg_laying" "X1M_1"              "X1M_2"             
##  [4] "X1M_3"              "X1M_4"              "X1M_5"             
##  [7] "X1M_6"              "X1M_7"              "X1M_8"             
## [10] "X1M_9"              "X1M_10"             "X2M_1"             
## [13] "X2M_2"              "X2M_3"              "X2M_4"             
## [16] "X2M_5"              "X2M_6"              "X2M_7"             
## [19] "X2M_8"              "X2M_9"              "X2M_10"            
## [22] "X3M_1"              "X3M_2"              "X3M_3"             
## [25] "X3M_4"              "X3M_5"              "X3M_6"             
## [28] "X3M_7"              "X3M_8"              "X3M_9"             
## [31] "X3M_10"             "C_1"                "C_2"               
## [34] "C_3"                "C_4"                "C_5"               
## [37] "C_6"                "C_7"                "C_8"               
## [40] "C_9"                "C_10"               "C_11"              
## [43] "C_12"               "C_13"               "C_14"              
## [46] "C_15"               "C_16"               "C_17"              
## [49] "C_18"               "C_19"               "C_20"
```


```r
print(head(egg_data,n=10L)) # first 6 examples (rows) (by default)  
```

```
##    Days_of_egg_laying X1M_1 X1M_2 X1M_3 X1M_4 X1M_5 X1M_6 X1M_7 X1M_8
## 1                  NA    NA    NA    NA    NA    NA    NA    NA    NA
## 2                   1    52    53    49    47    33    48    42    36
## 3                  NA    NA    NA    NA    NA    NA    NA    NA    NA
## 4                   2    54    41    43    39    36    51    38    39
## 5                  NA    NA    NA    NA    NA    NA    NA    NA    NA
## 6                   3    41    39    29    43    46    42    31    27
## 7                  NA    NA    NA    NA    NA    NA    NA    NA    NA
## 8                   4    17    43    17    28    38    36    37    30
## 9                  NA    NA    NA    NA    NA    NA    NA    NA    NA
## 10                  5    21    19    18    23    31    21    14    22
##    X1M_9 X1M_10 X2M_1 X2M_2 X2M_3 X2M_4 X2M_5 X2M_6 X2M_7 X2M_8 X2M_9
## 1     NA     NA    NA    NA    NA    NA    NA    NA    NA    NA    NA
## 2     36     43    42    37    43    39    39    38    48    39    52
## 3     NA     NA    NA    NA    NA    NA    NA    NA    NA    NA    NA
## 4     43     39    40    29    36    37    37    34    43    40    43
## 5     NA     NA    NA    NA    NA    NA    NA    NA    NA    NA    NA
## 6     29     47    46    35    39    36    37    26    29    39    48
## 7     NA     NA    NA    NA    NA    NA    NA    NA    NA    NA    NA
## 8     40     NA    37    33    36    43    44    19    23    27    23
## 9     NA     NA    NA    NA    NA    NA    NA    NA    NA    NA    NA
## 10    26     NA    22    17    14    20    21    18    14    20    19
##    X2M_10 X3M_1 X3M_2 X3M_3 X3M_4 X3M_5 X3M_6 X3M_7 X3M_8 X3M_9 X3M_10 C_1
## 1      NA    NA    NA    NA    NA    NA    NA    NA    NA    NA     NA  NA
## 2      51    51    49    45    48    41    38    43    42    46     41  78
## 3      NA    NA    NA    NA    NA    NA    NA    NA    NA    NA     NA  NA
## 4      47    48    38    41    41    48    35    49    47    49     46  58
## 5      NA    NA    NA    NA    NA    NA    NA    NA    NA    NA     NA  NA
## 6      39    62    47    38    38    47    39    37    38    36     39  61
## 7      NA    NA    NA    NA    NA    NA    NA    NA    NA    NA     NA  NA
## 8      29    26    30    36    35    39    23    31    29    32     32  59
## 9      NA    NA    NA    NA    NA    NA    NA    NA    NA    NA     NA  NA
## 10     23    23    29    38    27    29    21    29    21    39     17  54
##    C_2 C_3 C_4 C_5 C_6 C_7 C_8 C_9 C_10 C_11 C_12 C_13 C_14 C_15 C_16 C_17
## 1   NA  NA  NA  NA  NA  NA  NA  NA   NA   NA   NA   NA   NA   NA   NA   NA
## 2   69  67  77  65  63  71  69  73   88   71   62   61   68   73   71   77
## 3   NA  NA  NA  NA  NA  NA  NA  NA   NA   NA   NA   NA   NA   NA   NA   NA
## 4   49  60  NA  59  52  72  61  58   85   87   64   59   62   69   61   62
## 5   NA  NA  NA  NA  NA  NA  NA  NA   NA   NA   NA   NA   NA   NA   NA   NA
## 6   64  65  NA  48  71  71  89  49   49   61   68   58   89   71   52   70
## 7   NA  NA  NA  NA  NA  NA  NA  NA   NA   NA   NA   NA   NA   NA   NA   NA
## 8   59  71  NA  46  67  77  76  41   49   59   64   48   76   68   51   65
## 9   NA  NA  NA  NA  NA  NA  NA  NA   NA   NA   NA   NA   NA   NA   NA   NA
## 10  57  69  NA  47  63  73  75  39   47   57   61   43   74   69   49   61
##    C_18 C_19 C_20
## 1    NA   NA   NA
## 2    83   64   61
## 3    NA   NA   NA
## 4    76   53   59
## 5    NA   NA   NA
## 6    78   62   58
## 7    NA   NA   NA
## 8    63   59   57
## 9    NA   NA   NA
## 10   60   55   53
```


```r
keep <- seq(from=2, to=40, by=2)
egg_data <- egg_data[keep,]
```


```r
print(head(egg_data,n=10L)) # first 6 examples (rows) (by default)  
```

```
##    Days_of_egg_laying X1M_1 X1M_2 X1M_3 X1M_4 X1M_5 X1M_6 X1M_7 X1M_8
## 2                   1    52    53    49    47    33    48    42    36
## 4                   2    54    41    43    39    36    51    38    39
## 6                   3    41    39    29    43    46    42    31    27
## 8                   4    17    43    17    28    38    36    37    30
## 10                  5    21    19    18    23    31    21    14    22
## 12                  6    19    13    18    16    23    16    18    19
## 14                  7    15    11    13    14    23    16    11    14
## 16                  8    15    13    14    14    19    13    15    14
## 18                  9    17    14    15    11    17    14    16    13
## 20                 10    14    16    15    16    16    16    11     9
##    X1M_9 X1M_10 X2M_1 X2M_2 X2M_3 X2M_4 X2M_5 X2M_6 X2M_7 X2M_8 X2M_9
## 2     36     43    42    37    43    39    39    38    48    39    52
## 4     43     39    40    29    36    37    37    34    43    40    43
## 6     29     47    46    35    39    36    37    26    29    39    48
## 8     40     NA    37    33    36    43    44    19    23    27    23
## 10    26     NA    22    17    14    20    21    18    14    20    19
## 12    19     NA    17    16    17    18    20    19    14    19    19
## 14    16     NA    12    13    11    18    17    12    13    19    15
## 16    14     NA    11    13    14    17    17    18    13    16    19
## 18    14     NA    10     9     9    16    15    11    12    15    13
## 20    15     NA     9     9     7    13    11    11    12    14    12
##    X2M_10 X3M_1 X3M_2 X3M_3 X3M_4 X3M_5 X3M_6 X3M_7 X3M_8 X3M_9 X3M_10 C_1
## 2      51    51    49    45    48    41    38    43    42    46     41  78
## 4      47    48    38    41    41    48    35    49    47    49     46  58
## 6      39    62    47    38    38    47    39    37    38    36     39  61
## 8      29    26    30    36    35    39    23    31    29    32     32  59
## 10     23    23    29    38    27    29    21    29    21    39     17  54
## 12     19    21    29    26    23    21    19    20    21    29     28  NA
## 14     15    21    21    21    22    19    19    17    19    16     19  NA
## 16     15    19    17    18    17    19    17    NA    18    18     19  NA
## 18     12    17    15    15    14    17    16    NA    18    17     16  NA
## 20     12    13    13    16    13    19    19    NA    17    19     16  NA
##    C_2 C_3 C_4 C_5 C_6 C_7 C_8 C_9 C_10 C_11 C_12 C_13 C_14 C_15 C_16 C_17
## 2   69  67  77  65  63  71  69  73   88   71   62   61   68   73   71   77
## 4   49  60  NA  59  52  72  61  58   85   87   64   59   62   69   61   62
## 6   64  65  NA  48  71  71  89  49   49   61   68   58   89   71   52   70
## 8   59  71  NA  46  67  77  76  41   49   59   64   48   76   68   51   65
## 10  57  69  NA  47  63  73  75  39   47   57   61   43   74   69   49   61
## 12  33  37  NA  37  41  46  30  37   45   51   37   38   39   66   47   41
## 14  31  36  NA  33  39  41  28  21   51   38   33   25   39   30   36   36
## 16  27  35  NA  31  37  39  26  19   38   38   29   37   36   28   39   36
## 18  21  33  NA  31  28  37  26  19   31   35   21   23   29   21   27   29
## 20  19  29  NA  27  21  28  21  29   39   41   23   19   19   28   23   31
##    C_18 C_19 C_20
## 2    83   64   61
## 4    76   53   59
## 6    78   62   58
## 8    63   59   57
## 10   60   55   53
## 12   40   49   46
## 14   39   33   35
## 16   30   28   22
## 18   25   15   19
## 20   29   17   19
```

#I actually tried learning about matplot, and what I can do to neaten up the grap is add type='l'. We can customize our mat plot graphs. type=l will give us the line graph instead of alphabets. 

#One more thing I have learnt is labelling x and y axis. xlab and ylab is what we use to label the x and y axis is matplot.

#We can also, add title to the graph, main does that


```r
# plot(egg_data$Days_of_egg_laying,egg_data$X1M_1)
# plot(egg_data$Days_of_egg_laying,egg_data$X1M_2)
y <- egg_data[2:51]
#print(y)
matplot(egg_data$Days_of_egg_laying,y, type='l', xlab = 'Days of egg laying', ylab = 'Number of eggs laid', main = 'Overall eggs laying in Control and Experimental')
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-31-1.png)<!-- -->

```r
# matplot used because y is a matrix
```

#Now I have the line matplot but I am still learning to customize it more properly. I have class on plots next week on November 19th, so I hope to learn there. Now I am gonna change everything in to line graphs and add titles 

Here X1M

```r
y <- y <- egg_data[2:11]
# print(y)
matplot(egg_data$Days_of_egg_laying,y, type='l', xlab = 'Days of egg laying', ylab = 'Number of eggs laid', main = 'X1M egg laying')
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-32-1.png)<!-- -->

Here X2M

```r
y <- egg_data[12:21]
# print(y)
matplot(egg_data$Days_of_egg_laying,y, type='l', xlab = 'Days of egg laying', ylab = 'Number of eggs laid', main = 'X2M egg laying')
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-33-1.png)<!-- -->

Here X3M

```r
y <- egg_data[22:31]
# print(y)
matplot(egg_data$Days_of_egg_laying,y, type='l', xlab = 'Days of egg laying', ylab = 'Number of eggs laid', main = 'X3M egg laying')
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-34-1.png)<!-- -->

Here C

```r
y <- egg_data[32:51]
# print(y)
matplot(egg_data$Days_of_egg_laying,y, type='l', xlab = 'Days of egg laying', ylab = 'Number of eggs laid', main = 'Control egg laying')
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-35-1.png)<!-- -->

*** Total eggs laid ***   
One measure of the female's fecundity is the total number of eggs laid, obtained from the number of eggs per day summed from day 1 to 20 (female age 3 to 23 days post-eclosion).
This I obtained using numbers (excel) and coverted to a .cvs file, loaded here.


```r
total_egg_data <- read.csv("total_eggs.csv",header=TRUE)
#print(str(total_egg_data))
#print("column names")
#print(names(total_egg_data))
print(head(total_egg_data,n=20L))
```

```
##    Female X1M X2M X3M   C
## 1       1 320 297 399 310
## 2       2 317 256 363 545
## 3       3 300 263 390 636
## 4       4 275 336 361  77
## 5       5 368 315 393 547
## 6       6 335 267 354 597
## 7       7 291 277 226 674
## 8       8 292 333 384 619
## 9       9 335 325 392 470
## 10     10 129 332 368 654
## 11     11  NA  NA  NA 675
## 12     12  NA  NA  NA 586
## 13     13  NA  NA  NA 508
## 14     14  NA  NA  NA 650
## 15     15  NA  NA  NA 645
## 16     16  NA  NA  NA 565
## 17     17  NA  NA  NA 654
## 18     18  NA  NA  NA 665
## 19     19  NA  NA  NA 556
## 20     20  NA  NA  NA 534
```
The columns are the four different "experiments", !M, 2M, 3M, C
The rows are the different females (observations of female fecundity as measured by total eggs laid). There are 10 observations for 1M, 2M, 3M and 20 for C.

Next do a boxplot of this data

```r
boxplot(total_egg_data)
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-37-1.png)<!-- -->
The "Female" column is ignored (just female number). The other boxplots show 4 outliers. These are the 4 females that died before the full 20 days. 

I removed the egg totals for these females and made a new file, "total_revised_egg_data,cvs", loaded here


```r
total_egg_revised_data <- read.csv("total_eggs_revised.csv",header=TRUE)
#print(str(total_egg_revised_data))
#print("column names")
#print(names(total_egg_revised_data))
print(head(total_egg_revised_data,n=18L))
```

```
##    Female X1M X2M X3M   C
## 1       1 320 297 399 545
## 2       2 317 256 363 636
## 3       3 300 263 390 547
## 4       4 275 336 361 597
## 5       5 368 315 393 674
## 6       6 335 267 354 619
## 7       7 291 277 384 470
## 8       8 292 333 392 654
## 9       9 335 325 368 675
## 10     10  NA 332  NA 586
## 11     11  NA  NA  NA 508
## 12     12  NA  NA  NA 650
## 13     13  NA  NA  NA 645
## 14     14  NA  NA  NA 565
## 15     15  NA  NA  NA 654
## 16     16  NA  NA  NA 665
## 17     17  NA  NA  NA 556
## 18     18  NA  NA  NA 534
```
Next do a boxplot of this data

```r
boxplot(total_egg_revised_data)
```

![](Divya_Purohith_Diary_R_Plots_files/figure-html/unnamed-chunk-39-1.png)<!-- -->
Now the data looks resonable for analysis of variance.

Its just a little what I have applied to my own data because of short of time. But its a good thing to practice. Thank you.
