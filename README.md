# Gasoline or Diesel
Miguel  
April 7, 2015  




*Ever since my parked car was totaled a couple of weeks ago, I've been in the market for a replacement. I'm considering getting a car that uses diesel rather than gas, but is that economical? And if it is, when do I start seeing a return on my investment?*

### Load Data and Set Parameters

We'll get our gas and diesel data from Quandl. The data sets contain weekly gasoline and diesel prices for the past 15 years.


```r
diesel <- Quandl("BTS_MM/MOTOR_FUEL_DIESEL_PRICE")
```



```r
gas <- Quandl("BTS_MM/MOTOR_FUEL_GASOLINE_PRICE")
```



Next we'll define some of our inputs. These can be adjusted depending on the car models we're comparing or they type of driving I expect to do.


```r
# Calculate a combined MPG with the 45/55 ratio specified by fuel economy.gov:
g_mpg <- 25*0.55 + 34*0.45 
d_mpg <- 31*0.55 + 46*0.45

# Car prices.
dieselcar <- 24075 
gascar <- 22325

# Number of miles I drive in a year and in a day (based on previous car).
mi_year <- (40000-15000)/5
mi_day <- mi_year/365.25

# Average number of miles per day for a 20-30 year old male.
avg_day <- 15000/365.25
```

### Gas and Diesel Prices: Linear Model

Let's take a look at our data, and see if we can fit a linear model to gas prices and another to diesel prices.

![](README_files/figure-html/unnamed-chunk-4-1.png) 

We see that the two are very closely related, but for the past couple of years diesel has been a little bit more expensive. But remember that diesel cars, which are more expenisive, also get better milage. If gasoline and diesel prices continue to increase as they have been, let's see if better milage translates to savings.

### The Options

As an example, let's look at the 2015 VW Jetta SE (with Connectivity), which comes in either a gasoline ($22,325; 25/34 mpg) or a diesel ($24,075; 31/46 mpg) model. These two models have basically the same features (seats, navigation, etc.), save for the fuel they use.  To estimate the combined fuel economy of each car we'll use the standard implemented by fueleconomy.gov, which is 55% city driving and 45% highway driving. This gives us a 29 mpg rating for the gas car and a 38 mpg rating for the diesel car. 

### The Calculation for Current Driving Habits

How long do I need to drive a diesel to make up for the initial price difference? We'll use a simplistic linear model to predict gas and diesel prices over the next couple of years. Then we'll find the cumulative sum of the cost of fuel over time plus the initial cost of the car. 

![](README_files/figure-html/unnamed-chunk-5-1.png) 

The y axis shows the cumulative cost. The diesel price starts off much more expensive, since the diesel engine is about $2000 more than the gasoline engine. Even despite the more expensive diesel prices, the better mileage ends up making the diesel car *cheaper* in the long run! It looks like this model suggests a return on investment after 10 years, which is OK I guess, but it's not great.

### The Calculation for Future Driving Habits

Note that for the above calulation I used an estimate of 5,000 miles per year, which may not be representative of most people, or even representative of my own driving habits once I finish college and get a job. Adjusting this factor to match the average driving distance of a 20-30 year old male (15,000 mi per year), we see that the diesel model ends up being cheaper after about 3.5 to 4 years.

![](README_files/figure-html/unnamed-chunk-6-1.png) 

### Conclusions and Limitations

I was curious about the accuracy of my model, and found [this study](http://www.dieselforum.org/files/dmfile/20130311_cd_umtritcofinalreport_dd2017.pdf) by The University of Michigan Transportation Research Institute. They also found that the return on investment happened around 3 to 5 years for most cars, though they took into account a couple of other factors like depreciation value and repairs. Some positives I haven't considered: diesel cars retain their value better since they are more expensive to begin with, and the engines tend to last much longer. As for negatives, maintenance and repairs tend to be a little costlier for diesel cars. The enviromental aspects are not considered. 

If I plan on driving like the typical 20 to 30 year old male, I guess I'd better get a diesel!
