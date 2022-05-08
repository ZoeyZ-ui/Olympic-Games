# Olympic-Games

## Table of Contents
* [General Info](#general-information)
* [Technologies](#technologies)
* [Questions](#questions)
* [Data](#data)
* [Analysis](#analysis)
* [Conclusion](#conclusion)
* [Contact](#contact)

## General info
The Olympic Games is an internationally celebrated, multi-sports event that takes place every two years. Competition and comradery among countries is what attracts people to this event. 

In this project we plan to examine the important features of the Olympics and the effect their country's size and GDP has on their performance. This information could help the Olympic Coordinators predict how countries will do in future Olympics based on the population and GDP of their country.
	
## Technologies
Project is created with:
* R Stuio: 4.1.3
* Rattle: 5.5.1
* Web scraping 

## Questions
* Are larger or smaller countries more likely to win silver vs gold medals?
* Does a country’s GDP affect whether a country wins a bronze, silver, or gold medal?
* What is the correlation between height, age, and weight between those athletes who won medals in the Olympic games?
* How many sports does each country have competing in the 2016 Olympics?

## Data 
* Years of Olympic History 
	* This dataset consists of 134, 732 values, including ID, name, gender, age, height, weight, team, NOC, games, year, season, city, sport, event, and medal. 
* Country Information 
	* This dataset includes the GDP and Population of each country in 2014. 

## Analysis 
`olympics_allfeatures<- read.csv("olympics_allfeatures.csv", header = TRUE,
                    sep = ",",
                    na.strings = c("NA", "Unknown", "", " ", "N/A"))`


                   

`olympics_allfeatures$GDP<- gsub(",","", olympics_allfeatures$GDP)`
`olympics_allfeatures$GDP<- as.numeric(unlist(olympics_allfeatures$GDP))`
`olympics_allfeatures$Population<- as.numeric(olympics_allfeatures$Population)`

`barplot(table(olympics_allfeatures$Population, olympics_allfeatures$Medal),
        main = "Medal_Population ",
        col=c("black"),
        ylim=c(0,500),
        xlab="Total medal", ylab="Coutry Size")`

`summary(olympics_allfeatures$Population)`

`Size_medal<-table(olympics_allfeatures$Population, olympics_allfeatures$Medal)`

`Size_medal<-data.frame(Size_medal)`
`names(Size_medal)[names(Size_medal)=="Var1"]<-"Population"`
`names(Size_medal)[names(Size_medal)=="Var2"]<-"Medal"`


`large_population<-subset(Size_medal, Size_medal$Population==33986655, select = c("Population", "Medal","Freq"))`

`large_population<-subset(Size_medal, Size_medal$Population==47737941, select = c("Population", "Medal","Freq"))`


`olympics_allfeatures$Medal[is.na(olympics_allfeatures$Medal)] = "No Medal"`

`summ <- group_by(olympics_allfeatures, Medal) `
`medal_summary <- summarize(summ,
                           total_medal = n(),
                           average_GDP = mean(GDP)) `

`mean(olympics_allfeatures$GDP)`
`min(olympics_allfeatures$GDP)`
`max(olympics_allfeatures$GDP)`

`boxplot(GDP~Medal, 
        data=olympics_allfeatures,
        col= c("purple"),
        xlab="Medal", 
        ylab="GDP")`

`olympics_allfeatures1<- read.csv("olympics_allfeatures.csv",
                                header = TRUE,
                                sep = ",",
                                na.strings = c("NA", "Unknown", "", " ", "N/A"))`

`data_subset<- olympics_allfeatures1[ , c("Medal")]  `
`olympics_allfeatures1 <-olympics_allfeatures1[complete.cases(data_subset), ]`
`cs <- olympics_allfeatures1[complete.cases(data_subset), ]`

`oly_fit<-lm(Age~Weight,Height,data=olympics_allfeatures)`

`oly_fit<-lm(Weight~Height,data=olympics_allfeatures1)`

`plot(Weight~Height,data=olympics_allfeatures1)`
`abline(oly_fit, col="red")`


`summ <- group_by(olympics_allfeatures, Country, Sport)`

`country_summary <-summarize(summ,
                            people_competing = n(),
                            average_GDP = mean(GDP))`



The plot indicated that the countries with a larger population win more bronze and silver medals and win more medals overall. In the summary table, we also got the mean population for all countries is 43020000. 

In table 2, Countries that have a population above 43020000 got more medals than countries with a population below 43020000. Based on the findings, we can conclude that the population of countries can influence athletes’ performance. Countries that have a larger population are more likely to win medals.	
While the population plays an important role in how a country will place, the Gross Domestic Product (GDP) for countries also has an impact on the medal a country is most likely to win. We utilized a boxplot to analyze the type of medal won and the Gross Domestic Product (GDP) for the countries that won each type of medal.

In order to determine the number of sports each country had competing in the Olympics; we created a summary table. This summary table shows the level of country participation within each sport. For example, the sport of Archery has two countries participating, Taiwan and France. 

This summary table is important because it shows the distribution of each country’s participation at each sporting event, as well as the number of athletes competing. Many countries participate in the sport “Athletics”, which in this case refers to the Track and Field events. The shows that Kenya has 13 athletes participating, which was significantly more than most of the other countries. This can allude to higher participation increases the likelihood of that country receiving a medal.

  
## Conclusion  
First, athletes coming from countries of large population size are performing better at the Olympic games.

Second, the better a country's economy is doing the higher they placed at the Olympic games for 2014 and 2016. 

Third, the correlation between weight and height of athletes showed us that athletes who have won medals are more likely to have a high weight and height. 

Finally, the summary table we created showed us that not all countries participate in every sporting event that is held at the Olympic Games. 

We suggest countries utilize this information to predict how they will do in future Olympic games. The countries can use this to determine how their current population and GDP will impact their performance. 

Since the size of the country has an influence on the performance of athletes, we also suggest setting different game groups for athletes coming from the different country size.

## Contact 
Contact with me [Email](http://zhiyuan-zhao@uiowa.edu).
