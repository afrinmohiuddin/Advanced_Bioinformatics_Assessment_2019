### Question 1

    sum(5:55)

    ## [1] 1530

    ###sum of all integers between 5 and 55

### Question 2

    sumfun<- function (n) ###sumfun means summary fuction by assigning the n as a fuction to interpret the following sum when n is changed.
      sum(5:n)### formula ###
    sumfun(10) ### sum(5:10) ###

    ## [1] 45

    sumfun (20)### sum(5:20) ###

    ## [1] 200

    sumfun(100) ### sum (5:100) ###

    ## [1] 5040

### Question 3

    fibseq<-seq(1,12)
    fibseq[1]=1 ### assignment of the first entry as given ###
    fibseq[2]=1 ### assignment of second entry as given ###

    for (i in 3:12) ### to find the entries between the third and twelth###

    fibseq[i]<-fibseq[i-1]+fibseq[i-2]
    fibseq### print out of the first 12 entries of the Fibonacci series after the first two entries as they are already given.###

    ##  [1]   1   1   2   3   5   8  13  21  34  55  89 144

### Question 4

    library(ggplot2)
    data<-mtcars### assigning what data being used###
    data$gear<-as.factor(mtcars$gear) ###convert the gear variable from numeric into factor###
    p<-ggplot(data, aes(x=gear, y=mpg, fill=gear )) + geom_boxplot()
    p

![](https://github.com/afrinmohiuddin/Advanced_Bioinformatics_Assessment_2019/blob/master/unnamed-chunk-4-1.png)

    ### to plot box plots with the x axis as gear, y axis as mpg and fill in the gears with colour###

### Question 5

    cars.lm<- lm(formula = dist~speed, data = cars)
    summary(cars.lm)

    ## 
    ## Call:
    ## lm(formula = dist ~ speed, data = cars)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -29.069  -9.525  -2.272   9.215  43.201 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) -17.5791     6.7584  -2.601   0.0123 *  
    ## speed         3.9324     0.4155   9.464 1.49e-12 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 15.38 on 48 degrees of freedom
    ## Multiple R-squared:  0.6511, Adjusted R-squared:  0.6438 
    ## F-statistic: 89.57 on 1 and 48 DF,  p-value: 1.49e-12

    ###linear relationship between speed (in units of mph) and breaking distance (in units of feet) in the variable distance###

### the fitted slope = 3.9324

### the intercept of line = -17.5791

### the standard deviation = 0.4155

### Question 6

    library(ggplot2)
    data("cars")
    ggplot(cars, aes(x=speed, y=dist)) + 
      geom_point(color='Blue', size = 1) +xlim(c(0, 25)) +
      geom_smooth(method=lm, color='Black', fullrange=TRUE) + labs(title= 'Linear relationship between speed and breaking distance in the variable distance ', x= 'Speed ( in units mph)', y= 'Breaking distance (in units of feet) ')### plot the data points from Question 5 and the linear fit.###

![](https://github.com/afrinmohiuddin/Advanced_Bioinformatics_Assessment_2019/blob/master/unnamed-chunk-6-1.png)

### Question 7

    library(ggplot2)


    data <- cars
    reg_data <- lm(dist ~ speed + I(speed^2), data=data)
    reg_data

    ## 
    ## Call:
    ## lm(formula = dist ~ speed + I(speed^2), data = data)
    ## 
    ## Coefficients:
    ## (Intercept)        speed   I(speed^2)  
    ##     2.47014      0.91329      0.09996

    reg_data$coefficients[3]

    ## I(speed^2) 
    ##  0.0999593

    data$new_speed <- data$speed * (5280/3600)###converting speed miles per housr to feet per second.###


    reg_data <- lm(dist ~ 0 + new_speed + I(new_speed^2), data=data)
    summary(reg_data) ### Adding the 0 term tells the lm() to fit the line through the origin

    ## 
    ## Call:
    ## lm(formula = dist ~ 0 + new_speed + I(new_speed^2), data = data)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -28.836  -9.071  -3.152   4.570  44.986 
    ## 
    ## Coefficients:
    ##                Estimate Std. Error t value Pr(>|t|)   
    ## new_speed       0.84479    0.38180   2.213  0.03171 * 
    ## I(new_speed^2)  0.04190    0.01366   3.067  0.00355 **
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 15.02 on 48 degrees of freedom
    ## Multiple R-squared:  0.9133, Adjusted R-squared:  0.9097 
    ## F-statistic: 252.8 on 2 and 48 DF,  p-value: < 2.2e-16

    ### Yes the data output is reasonable.


    ggplot(data, aes(x = new_speed, y = dist)) + 
     geom_point(color='Black', size = 1) + xlim(c(0,40)) +
     geom_smooth(method = "lm", formula = "y ~ 0 + x + I(x^2)",  color="red", fullrange='TRUE') + labs(title= 'Reaction time for the driver to start breaking ', y = 'Stopping Distance of a Car in Feet', x = "The Speed of a Car in Feet per second")

![](https://github.com/afrinmohiuddin/Advanced_Bioinformatics_Assessment_2019/blob/master/unnamed-chunk-7-1.png)

    ### ggplot defining the data being used and how to plot it.

    ###geom_point = defines the colour and size of the data.

    ###xlim = defines the x axis limit which shows the full scale and indicates where the intercept on the y-axis which supports the data.

    ###geom_smooth = gives the fitted relationship.
