---
title: Electric Vehicle
author: Package Build
date: '2023-04-06'
slug: []
categories:
  - R
tags:
  - R Markdown
authors: []
description: ''
externalLink: ''
series: []
---

# Analyze the Electric Vehicle in Each State


```r
library(readr)
Electric_Vehicle_Population_Data <- read_csv("Electric_Vehicle_Population_Data.csv")
```

```
## Rows: 121978 Columns: 17
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (11): VIN (1-10), County, City, State, Make, Model, Electric Vehicle Typ...
## dbl  (6): Postal Code, Model Year, Electric Range, Base MSRP, Legislative Di...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
Electric_Vehicle_Population_Data
```

```
## # A tibble: 121,978 × 17
##    `VIN (1-10)` County   City  State Posta…¹ Model…² Make  Model Elect…³ Clean…⁴
##    <chr>        <chr>    <chr> <chr>   <dbl>   <dbl> <chr> <chr> <chr>   <chr>  
##  1 5YJ3E1EB2J   Suffolk  Suff… VA      23435    2018 TESLA MODE… Batter… Clean …
##  2 5YJ3E1ECXL   Yakima   Yaki… WA      98908    2020 TESLA MODE… Batter… Clean …
##  3 WA1LAAGE7M   Yakima   Yaki… WA      98908    2021 AUDI  E-TR… Batter… Clean …
##  4 5YJ3E1EA1K   Danville Danv… VA      24541    2019 TESLA MODE… Batter… Clean …
##  5 1FADP5CU9E   Norfolk  Norf… VA      23518    2014 FORD  C-MAX Plug-i… Not el…
##  6 1N4AZ0CP1F   Thurston Olym… WA      98502    2015 NISS… LEAF  Batter… Clean …
##  7 1G1RH6E48D   Thurston Teni… WA      98589    2013 CHEV… VOLT  Plug-i… Clean …
##  8 5YJSA1E13G   Snohomi… Both… WA      98021    2016 TESLA MODE… Batter… Clean …
##  9 1N4AZ1CP0J   King     Seat… WA      98112    2018 NISS… LEAF  Batter… Clean …
## 10 5YJ3E1EB0J   Kittitas Cle … WA      98922    2018 TESLA MODE… Batter… Clean …
## # … with 121,968 more rows, 7 more variables: `Electric Range` <dbl>,
## #   `Base MSRP` <dbl>, `Legislative District` <dbl>, `DOL Vehicle ID` <dbl>,
## #   `Vehicle Location` <chr>, `Electric Utility` <chr>,
## #   `2020 Census Tract` <chr>, and abbreviated variable names ¹​`Postal Code`,
## #   ²​`Model Year`, ³​`Electric Vehicle Type`,
## #   ⁴​`Clean Alternative Fuel Vehicle (CAFV) Eligibility`
```

Let's check the distribution on maker


```r
county_data = table(Electric_Vehicle_Population_Data$Make)

pie(county_data)
```

<img src="{{< blogdown/postref >}}index.en_files/figure-html/unnamed-chunk-2-1.png" width="672" />

The pie chart shows staht Telsa and Nissan contributed more than 50% of the Electric vehicle 

Let see how many electic range of each vechile and it frequency.

```r
Range = table(Electric_Vehicle_Population_Data$`Electric Range`)
hist(Electric_Vehicle_Population_Data$`Electric Range`)
```

<img src="{{< blogdown/postref >}}index.en_files/figure-html/unnamed-chunk-3-1.png" width="672" />

However, most of the item appears in 0 - 50. After observation, we found that it is because most of the vehicle are hybrid power supply. Which means the battery can only provide limited power. Thus the pure electric range is very low.


