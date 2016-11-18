---
title: "Greenpeace Insight Skillshare"
author: "Martin Hou"
date: '18 November, 2016'
output:
  ioslides_presentation:
    <!--css: styles.css -->
    incremental: yes
    logo: sb7ixc5z.png
    transition: default
    widescreen: yes
  slidy_presentation:
    incremental: yes
job: Data Specialist
logo: sb7ixc5z.png
license: by-nc-sa
mode: selfcontained
hitheme: tomorrow
highlighter : highlight.js
subtitle: R Programming Demo
framework: io2012
widgets: []
github      :
  user      : martinhyy
  repo      : Insight_Skillshare
---




<style>
pre code, pre, code {

  overflow-x: scroll !important;


}


aside.gdbar img{
  
  width: 80px;
  height: 80px;


}

div.centered {

  text-align: left;


}

</style>


## Introducing R
<!--
This is an R Markdown presentation. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document.-->
<br> </br>
> - # R is a programming language for statistical computing

> - # khskshdkfjh

> - # kdfhkhdfkhsd

> - # skdfkhsfkh

---

## Why R
<br> </br>

> - # R is free and open source

> - # Reading different data from different platform

> - # Provides different data manipulation packages and functions

> - # Data modelling, forecasting and a lot other analytic functions

> - # Data visualization: basic R plot and interactive plots integrated with Google visualization and javascript libraries 

> - # `shiny` dashboard: integrate analysis output to dashboard and share with others

> - # Markdown Documentation

---

## Some stats about R
<!--

- Bullet 1
- Bullet 2
- Bullet 3

-->

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

--- .dark .nobackground

<p style='font-size:100px'>
<font color='white'>
R Connectivity 
</font>
</p>


--- 

## Connect to different data

<br> </br>

> - # flat/txt file: `read.table()`

> - # csv file: `read.csv()`

> - # MySQL/SQL database: `odbcConnect("ServerName", uid = "UserName", pwd = "Password")`

> - # Online data

> - # GIS data: `readOGR()`

> - # Graph database: <a href="https://neo4j.com/developer/r/"> `RNeo4j` </a>



--- &twocol

## R to flat file 
<!--
comment = NA helps remove the # in the output
echo = FLASE means only show the final output make all R code and relating comments invisible
prompt = TRUE you will see a little + symbol 
-->

*** =left

Load a txt file into R


```r
df <- read.table("X:\\Box Sync\\Fundraising\\Analysis\\Martin\\Bangkok_Skillshare\\Data\\SMS.txt",
                 header = T,
                 sep = "\t")
```

```
Warning in file(file, "rt"): cannot open file 'X:\Box Sync\Fundraising
\Analysis\Martin\Bangkok_Skillshare\Data\SMS.txt': No such file or
directory
```

```
Error in file(file, "rt"): cannot open the connection
```

```r
head(df)
```

```
                                              
1 function (x, df1, df2, ncp, log = FALSE)    
2 {                                           
3     if (missing(ncp))                       
4         .Call(C_df, x, df1, df2, log)       
5     else .Call(C_dnf, x, df1, df2, ncp, log)
6 }                                           
```
<!--make these two examples side by side-->

*** =right

Load a csv file into R


```r
df <- read.csv("X:\\Box Sync\\Fundraising\\Analysis\\Martin\\Bangkok_Skillshare\\Data\\SMS.csv",
               header = T,
               stringsAsFactors = F)
```

```
Warning in file(file, "rt"): cannot open file 'X:\Box Sync\Fundraising
\Analysis\Martin\Bangkok_Skillshare\Data\SMS.csv': No such file or
directory
```

```
Error in file(file, "rt"): cannot open the connection
```

```r
head(df)
```

```
                                              
1 function (x, df1, df2, ncp, log = FALSE)    
2 {                                           
3     if (missing(ncp))                       
4         .Call(C_df, x, df1, df2, log)       
5     else .Call(C_dnf, x, df1, df2, ncp, log)
6 }                                           
```

---

## R to MySQL and SQL
<style type="text/css">

code.r{ /* Code block */
  font-size: 15px;
}

code.vhdl{

  font-size: 15px;

}


</style>

<!--
Base functions in R don't have the ability to connect to database
R packages needed here

-->

```r
library(RODBC)
RE_connect <- odbcConnect("RE7", uid = "SSRS", pwd = "xH^SfWJ2R4")
gift <- sqlQuery(RE_connect, 
               query = "
               select RECORDS.CONSTITUENT_ID, ...Truncated
               where GIFT.DTE between '2016-09-01' and '2016-09-30'
               and GIFT.TYPE in (31) and (FUND.FUND_ID like '%AQ-PHONE%' or FUND.FUND_ID like '%AQ-DDC%')
               ")
head(gift)
```


```
Error in sqlQuery(RE_connect, query = "\n               select RECORDS.CONSTITUENT_ID,\n                      GIFT.DTE,\n                      GiftSplit.Amount,\n                      GIFT.TYPE,\n                      APPEAL.APPEAL_ID,\n                      FUND.FUND_ID,\n                      case \n                        when APPEAL.APPEAL_ID like 'DDC%' then 'Street Recurring'\n                        when APPEAL.APPEAL_ID like 'DTD%' then 'Door Recurring'\n                        else 'Telefundraising Recurring'\n                      end as [GROUP] \n              from GiftSplit\n              left join GIFT\n              on GiftSplit.GiftId = GIFT.ID\n              left join APPEAL\n              on GiftSplit.AppealId = APPEAL.ID\n              left join FUND\n              on GiftSplit.FundId = FUND.ID\n              left join RECORDS\n              on GIFT.CONSTIT_ID = RECORDS.ID\n              where GIFT.DTE between '2013-01-01' and '2016-09-30'\n              and GIFT.TYPE in (31)\n              and (FUND.FUND_ID like '%AQ-PHONE%' \n              or FUND.FUND_ID like '%AQ-DDC%')\n               "): first argument is not an open RODBC channel
```

```
Error in head(gift): object 'gift' not found
```



---

## R to online data

--- &twocol

## R to GIS data

Shapefile and raster data can be imported into R

- Shapefile into R

*** =left

```r
library(rgdal)
london.shp <- readOGR(dsn = "X:\\Box Sync\\Fundraising\\Analysis\\Martin\\Bangkok_Skillshare\\Data\\ESRI", 
    layer = "London_Borough_Excluding_MHW")
plot(london.shp)
```

*** =right


```
## Error in library(rgdal): there is no package called 'rgdal'
```

```
## Error in eval(expr, envir, enclos): could not find function "readOGR"
```

```
## Error in eval(expr, envir, enclos): object 'london.shp' not found
```

```
## Error in plot(london.shp): object 'london.shp' not found
```

---

## R to GIS data

- Raster data into R

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



--- .dark


<p style='font-size:100px'>
<font color='white'>
R data manipulation 
</font>
</p>

--- &twocol

## Data manipulation using base R functions
<!--
data.frame()
aggregate()

The problem of using R base functions to manipulate data is sometimes when the dataset gets larger the process could be slower

why?

It's the problem of how R works

-->

Base function like `aggregate()` gives us the ability to aggregate raw data without using any external packages.

However `aggregate()` is not really efficient when dataset gets larger and aggregation becomes complex. 

*** =left





```r
start.time <- Sys.time()
gift.ag1 <- as.data.frame(as.list(aggregate(Amount ~ Year + month + GROUP,
                      data = gift, 
                      FUN = function(x) c(Count = length(x), Average = mean(x), Total = sum(x)))
                                 )
                         )

Sys.time() - start.time
Time difference of 2.710633 secs
```

*** =right


```
  Year month          GROUP Amount.Count Amount.Average Amount.Total
1 2013     1 Door Recurring        10648       16.94191     180397.5
2 2014     1 Door Recurring         9753       18.46033     180043.6
3 2015     1 Door Recurring         9383       19.80147     185797.2
4 2016     1 Door Recurring         8614       20.28150     174704.9
5 2013     2 Door Recurring        10264       17.15470     176075.8
6 2014     2 Door Recurring         9370       18.67224     174958.9
```



--- &twocol

## Data manipulation using functions from R packages

<!--

data.table() shorter code and memory efficient but hard to learn
dplyr() pipe operator easy to learn but consumes memory


-->

Using external packages like `library(data.table)` can really solve the efficiency problem.

When dealing with large data aggregation, it can shrink the time significantly.

Other packages like `dplyr`, `reshape2` can also help aggregate data for different purposes


*** =left



```r
library(data.table)
load("F:\\Software backup\\gift.RData")
start.time <- Sys.time()
gift.dt <- data.table(gift)
gift.ag <- gift.dt[,list(Count = length(Amount), 
                         Average = mean(Amount), 
                         Total = sum(Amount)), 
                   by = list(Year, month, GROUP)]
Sys.time() - start.time
Time difference of 0.1627851 secs
```



*** =right

```
   Year month                     GROUP Count  Average     Total
1: 2014     3 Telefundraising Recurring  4037 24.68985  99672.92
2: 2014     3            Door Recurring  9486 18.59677 176408.92
3: 2014     3          Street Recurring 14565 15.40297 224344.26
4: 2014     4          Street Recurring 14246 15.17175 216136.76
5: 2014     4            Door Recurring  9448 18.27036 172618.36
6: 2014     4 Telefundraising Recurring  4125 24.63313 101611.67
```


--- .dark

<p style='font-size:100px'>
<font color='white'>
R data visualization 
</font>
</p>

---

## Base R plot
<!--
plot()


-->


---

## ggplot2 (<font color="red">G</font>rammar of <font color="red">G</font>raphics)

<br>
# The basic idea of ggplot
> - # ggplot2 deals with long table

> - # ggplot2 pivots a long table into a Excel like pivot table and then visualize the data
       > - specify columns/fields to be used in x and y axis
       > - specify which column/fields you want to break the data by
       > - specify the plot type by adding (`+`) layers on the canvas 
           - geom_bar()
           - geom_line()
           - geom_point()
           - etc
       > - Add other layers to customize colour, label, title, caption and background     

---

## ggplot2
# Example of ggplot


```r
library(ggplot2)
gift.ag <- gift.ag[order(gift.ag$GROUP, descending = FALSE),]

ggplot(data = gift.ag , aes(x=date, y=Count, fill = GROUP)) +
  geom_bar(stat = "identity") +
  ggtitle("Number of Recurring Gift by FR Programme")
```

![plot of chunk unnamed-chunk-15](assets/fig/unnamed-chunk-15-1.png)



<!--

<div class="red2">
This text is red
</div>sdfsfdf

-->

--- &twocol

## Interactive plot




```r
library(googleVis)
options(gvis.plot.tag='chart')
M1 <- gvisMotionChart(Fruits, idvar = "Fruit", timevar = "Year")
show(M1$html$chart)
```

                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             jsHeader 
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                "<!-- MotionChart generated in R 3.3.1 by googleVis 0.6.1 package -->\n<!-- Wed Nov 16 23:59:45 2016 -->\n\n\n<!-- jsHeader -->\n<script type=\"text/javascript\">\n" 
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               jsData 
                                                                                                                                                                                                                                                                                                                    "\n// jsData \nfunction gvisDataMotionChartIDd6474c15e96 () {\nvar data = new google.visualization.DataTable();\nvar datajson =\n[\n [\n\"Apples\",\n2008,\n\"West\",\n98,\n78,\n20,\n\"2008-12-31\"\n],\n[\n\"Apples\",\n2009,\n\"West\",\n111,\n79,\n32,\n\"2009-12-31\"\n],\n[\n\"Apples\",\n2010,\n\"West\",\n89,\n76,\n13,\n\"2010-12-31\"\n],\n[\n\"Oranges\",\n2008,\n\"East\",\n96,\n81,\n15,\n\"2008-12-31\"\n],\n[\n\"Bananas\",\n2008,\n\"East\",\n85,\n76,\n9,\n\"2008-12-31\"\n],\n[\n\"Oranges\",\n2009,\n\"East\",\n93,\n80,\n13,\n\"2009-12-31\"\n],\n[\n\"Bananas\",\n2009,\n\"East\",\n94,\n78,\n16,\n\"2009-12-31\"\n],\n[\n\"Oranges\",\n2010,\n\"East\",\n98,\n91,\n7,\n\"2010-12-31\"\n],\n[\n\"Bananas\",\n2010,\n\"East\",\n81,\n71,\n10,\n\"2010-12-31\"\n] \n];\ndata.addColumn('string','Fruit');\ndata.addColumn('number','Year');\ndata.addColumn('string','Location');\ndata.addColumn('number','Sales');\ndata.addColumn('number','Expenses');\ndata.addColumn('number','Profit');\ndata.addColumn('string','Date');\ndata.addRows(datajson);\nreturn(data);\n}\n" 
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          jsDrawChart 
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 "\n// jsDrawChart\nfunction drawChartMotionChartIDd6474c15e96() {\nvar data = gvisDataMotionChartIDd6474c15e96();\nvar options = {};\noptions[\"width\"] = 600;\noptions[\"height\"] = 500;\noptions[\"state\"] = \"\";\n\n\n    var chart = new google.visualization.MotionChart(\n    document.getElementById('MotionChartIDd6474c15e96')\n    );\n    chart.draw(data,options);\n    \n\n}\n  \n" 
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       jsDisplayChart 
"\n// jsDisplayChart\n(function() {\nvar pkgs = window.__gvisPackages = window.__gvisPackages || [];\nvar callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];\nvar chartid = \"motionchart\";\n  \n// Manually see if chartid is in pkgs (not all browsers support Array.indexOf)\nvar i, newPackage = true;\nfor (i = 0; newPackage && i < pkgs.length; i++) {\nif (pkgs[i] === chartid)\nnewPackage = false;\n}\nif (newPackage)\n  pkgs.push(chartid);\n  \n// Add the drawChart function to the global list of callbacks\ncallbacks.push(drawChartMotionChartIDd6474c15e96);\n})();\nfunction displayChartMotionChartIDd6474c15e96() {\n  var pkgs = window.__gvisPackages = window.__gvisPackages || [];\n  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];\n  window.clearTimeout(window.__gvisLoad);\n  // The timeout is set to 100 because otherwise the container div we are\n  // targeting might not be part of the document yet\n  window.__gvisLoad = setTimeout(function() {\n  var pkgCount = pkgs.length;\n  google.load(\"visualization\", \"1\", { packages:pkgs, callback: function() {\n  if (pkgCount != pkgs.length) {\n  // Race condition where another setTimeout call snuck in after us; if\n  // that call added a package, we must not shift its callback\n  return;\n}\nwhile (callbacks.length > 0)\ncallbacks.shift()();\n} });\n}, 100);\n}\n" 
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             jsFooter 
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         "\n// jsFooter\n</script>\n" 
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              jsChart 
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              "\n<!-- jsChart -->  \n<script type=\"text/javascript\" src=\"https://www.google.com/jsapi?callback=displayChartMotionChartIDd6474c15e96\"></script>\n" 
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             divChart 
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    "\n<!-- divChart -->\n  \n<div id=\"MotionChartIDd6474c15e96\" \n  style=\"width: 600; height: 500;\">\n</div>\n" 

```r
#gmotion
```

---

## Motion chart example


```r
library(googleVis)
options(gvis.plot.tag='chart')
Pie <- gvisPieChart(CityPopularity,
                    options=list(width=400, height=200))
print(Pie, tag = 'chart')
```

<!-- PieChart generated in R 3.3.1 by googleVis 0.6.1 package -->
<!-- Wed Nov 16 23:42:05 2016 -->


<!-- jsHeader -->
<script type="text/javascript">
 
// jsData 
function gvisDataPieChartIDd6447a4b9c () {
var data = new google.visualization.DataTable();
var datajson =
[
 [
"New York",
200
],
[
"Boston",
300
],
[
"Miami",
400
],
[
"Chicago",
500
],
[
"Los Angeles",
600
],
[
"Houston",
700
] 
];
data.addColumn('string','City');
data.addColumn('number','Popularity');
data.addRows(datajson);
return(data);
}
 
// jsDrawChart
function drawChartPieChartIDd6447a4b9c() {
var data = gvisDataPieChartIDd6447a4b9c();
var options = {};
options["allowHtml"] = true;
options["width"] = 400;
options["height"] = 200;

    var chart = new google.visualization.PieChart(
    document.getElementById('PieChartIDd6447a4b9c')
    );
    chart.draw(data,options);
    

}
  
 
// jsDisplayChart
(function() {
var pkgs = window.__gvisPackages = window.__gvisPackages || [];
var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
var chartid = "corechart";
  
// Manually see if chartid is in pkgs (not all browsers support Array.indexOf)
var i, newPackage = true;
for (i = 0; newPackage && i < pkgs.length; i++) {
if (pkgs[i] === chartid)
newPackage = false;
}
if (newPackage)
  pkgs.push(chartid);
  
// Add the drawChart function to the global list of callbacks
callbacks.push(drawChartPieChartIDd6447a4b9c);
})();
function displayChartPieChartIDd6447a4b9c() {
  var pkgs = window.__gvisPackages = window.__gvisPackages || [];
  var callbacks = window.__gvisCallbacks = window.__gvisCallbacks || [];
  window.clearTimeout(window.__gvisLoad);
  // The timeout is set to 100 because otherwise the container div we are
  // targeting might not be part of the document yet
  window.__gvisLoad = setTimeout(function() {
  var pkgCount = pkgs.length;
  google.load("visualization", "1", { packages:pkgs, callback: function() {
  if (pkgCount != pkgs.length) {
  // Race condition where another setTimeout call snuck in after us; if
  // that call added a package, we must not shift its callback
  return;
}
while (callbacks.length > 0)
callbacks.shift()();
} });
}, 100);
}
 
// jsFooter
</script>
 
<!-- jsChart -->  
<script type="text/javascript" src="https://www.google.com/jsapi?callback=displayChartPieChartIDd6447a4b9c"></script>
 
<!-- divChart -->
  
<div id="PieChartIDd6447a4b9c" 
  style="width: 400; height: 200;">
</div>



<!--

associate with javascript


-->

--- .dark

<p style='font-size:100px'>
<font color='white'>
R shiny dashboard 
</font>
</p>

---
## Integrate R output with dashboard

<br></br>

> - # [shiny](http://shiny.rstudio.com/tutorial/) is an external R package (`library(shiny)`) that can be used to integrated analysis results and share with others.

> - # Shiny application can make the results from your output interactive and dynamic.

> - # Structure of a shiny application
       > - ui.R: <br>
           Control the layout, `input` value and present `output`.
       > - server.R:<br>
           Process the calculation based on the `input` value and produce `output`.
       > - global.R (optional):<br>
           Preload static information needed

---

## Realtion between ui.R and server.R

<!--![relation](http://www.alternatestack.com/wp-content/uploads/2014/03/UiServerInteraction.png =100x) -->
<br></br>
<center><img src="http://www.alternatestack.com/wp-content/uploads/2014/03/UiServerInteraction.png" width="80%" height="80%"></center>



---

## Shiny application demo

<br></br>

> - # Demo 1: <br>
    # Google Motion Chart and Twitter WordCloud
    
> - # Demo 2: <br>
    # [Saves Report](https://martinhyy.shinyapps.io/SaveReport/) for Supporter Relationship Team
    
> - # Demo 3: <br>
    # [Geographic Gallery](https://martinhyy.shinyapps.io/ShinyApp/)


---
## Publish/deploy dashboard online

--- .dark

<p style='font-size:100px'>
<font color='white'>
Write document in R
</font>
</p>

---
## Knitr in R

---
## Presentation in R slidify

---



























