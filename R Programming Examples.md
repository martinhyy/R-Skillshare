---
title: Greenpeace Insight Skillshare
author: Martin Hou
date: '02 November, 2016'
output:
  ioslides_presentation:
    css: styles.css
    incremental: yes
    logo: sb7ixc5z.png
    transition: default
    widescreen: yes
  slidy_presentation:
    incremental: yes
job: Data Specialist
license: by-nc-sa
logo: sb7ixc5z.png
mode: selfcontained
hitheme: tomorrow
subtitle: R Programming Demo
framework: io2012
widgets: interactive
---


## Introducing R

<!--
This is an R Markdown presentation. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document.-->

---

## Some stats about R

- Bullet 1
- Bullet 2
- Bullet 3

---

## Something in between


```r
summary(cars)
```

```
##      speed           dist       
##  Min.   : 4.0   Min.   :  2.00  
##  1st Qu.:12.0   1st Qu.: 26.00  
##  Median :15.0   Median : 36.00  
##  Mean   :15.4   Mean   : 42.98  
##  3rd Qu.:19.0   3rd Qu.: 56.00  
##  Max.   :25.0   Max.   :120.00
```

--- .segue.dark

R Connectivity

---

## R to flat file 
<!--
comment = NA helps remove the # in the output
echo = FLASE means only show the final output make all R code and relating comments invisible
prompt = TRUE you will see a little + symbol 
-->
Load a txt file into R

```r
df <- read.table("X:\\Box Sync\\Fundraising\\Analysis\\Martin\\Bangkok_Skillshare\\Data\\SMS.txt",
                 header = T,
                 stringsAsFactors = F,
                 sep = "\t")

head(df)
```
<!--make these two examples side by side-->
Load a csv file into R


```r
df <- read.csv("X:\\Box Sync\\Fundraising\\Analysis\\Martin\\Bangkok_Skillshare\\Data\\SMS.csv",
               header = T,
               stringsAsFactors = F)
head(df)
```

---

## R to MySQL and SQL


<!--
Base functions in R don't have the ability to connect to database
R packages needed here

-->

```r
library(RODBC)
RE_connect <- odbcConnect("RE7", uid = "SSRS", pwd = "xH^SfWJ2R4")
df <- sqlQuery(RE_connect, 
               query = "
               select RECORDS.CONSTITUENT_ID,
                      GIFT.DTE,
                      GiftSplit.Amount,
                      GIFT.TYPE,
                      APPEAL.APPEAL_ID,
                      FUND.FUND_ID,
                      case 
                        when APPEAL.APPEAL_ID like 'DDC%' then 'Street Recurring'
                        when APPEAL.APPEAL_ID like 'DTD%' then 'Door Recurring'
                        else 'Telefundraising Recurring'
                      end as [GROUP] 
              from GiftSplit
              left join GIFT
              on GiftSplit.GiftId = GIFT.ID
              left join APPEAL
              on GiftSplit.AppealId = APPEAL.ID
              left join FUND
              on GiftSplit.FundId = FUND.ID
              left join RECORDS
              on GIFT.CONSTIT_ID = RECORDS.ID
              where GIFT.DTE between '2016-09-01' and '2016-09-30'
              and GIFT.TYPE in (31)
              and (FUND.FUND_ID like '%AQ-PHONE%' 
              or FUND.FUND_ID like '%AQ-DDC%')
               ")

head(df)
```

---

## R to online data

---

## R to GIS data

Shapefile and raster data can be imported into R

> - Shapefile into R


```r
library(rgdal)

london.shp <- readOGR(dsn = "X:\\Box Sync\\Fundraising\\Analysis\\Martin\\Bangkok_Skillshare\\Data\\ESRI",
                      layer = "London_Borough_Excluding_MHW")

plot(london.shp)
```

---

## R to GIS data

> - Raster data into R

<!--
word temperature data

-->



```r
library(raster)
World.Temp <- getData('worldclim', var = 'tmax', res = 10)
plot(World.Temp)
```


---

## R to Graph database



---

# R data manipulation

---

## Data manipulation using base R functions
<!--
data.frame()
aggregate()

The problem of using R base functions to manipulate data is sometimes when the dataset gets larger the process could be slower

why?

It's the problem of how R works

-->

---

## Data manipulation using functions from R packages

<!--

data.table() shorter code and memory efficient but hard to learn
dplyr() pipe operator easy to learn but consumes memory


-->



```r
library(data.table)
load("X:\\Box Sync\\Fundraising\\Analysis\\Martin\\Bangkok_Skillshare\\Data\\gift.RData")
start.time <- Sys.time()

gift.dt <- data.table(gift)
gift.ag <- gift.dt[,list(Count = length(Amount), Average = mean(Amount), Total = sum(Amount)), by = list(Year, month, GROUP)]
Sys.time() - start.time

head(gift.ag)
```

---

# R data visualization

---

## Base R plot
<!--
plot()


-->

---

## ggplot2 (Grammar of Graphics)





<!--

<div class="red2">
This text is red
</div>sdfsfdf

-->

---

## Interactive plot

<!--

associate with javascript


-->

---
# R shiny dashboard

---
## Integrate R output with dashboard

---
## Publish/deploy dashboard online

---
# Write document in R 

---
## Knitr in R

---
## Presentation in R slidify

---



























