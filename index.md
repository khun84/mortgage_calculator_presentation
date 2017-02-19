---
title       : Mortgage Calculator with IRR 
subtitle    : Shiny App Assignment 
author      : Daniel Lee 
job         :  
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}  
highlighter : highlight.js  # {highlight.js, prettify, highlight}  
hitheme     : tomorrow      #   
widgets     : []            # {mathjax, quiz, bootstrap}  
mode        : selfcontained # {standalone, draft}  
knit        : slidify::knit2slides
---

## Introduction

<style>
em {
    font-style: italic
}
strong {
    font-weight: bold;
}
</style>

The Shiny app that was developed for this assignment is a **Mortgage Calculator With IRR**.

The mission of this application is to explore the possibility of filling up the gaps in most of the publicly available mortgage calculator. 

The users would be able to know their **property investment IRR (interna return rate)** by providing some simple parameter to the app.

---

## Input UI

As we are not able to show the exact same UI layout in this deck, simple variables instead of reactive variables are being used here for demo purpose.


```r
# in m2
area = 100
unitprice = 5000

# in %
deposit = 10
rate = 4

# in year
tenure = 30

annual_rent = 24000

# from - to in year
rental_period = c(1,10)

# monthly rental increment every 2 year
rental_inc = 200

# in year
holding_period = 5

# unit price increment every year
price_inc = 100
```

---

## Output Server

<style>
.r, .preprocessor {
  font-size: 12px;
}
</style>

As the IRR function only works with cash flow vector, the input parameters will be translated into multiple cash flow vectors before arriving at the final net cash flow vector for the IRR calculation.




```r
cf_net = cf_deposit + cf_payment + cf_net_rent + cf_principal + cf_selling_price
cf_net = cf_net[mth <= (holding_period*12+1)]

# First few values of cf_net
head(cf_net)
```

```
## [1] -50000.0000   -148.3688   -148.3688   -148.3688   -148.3688   -148.3688
```

```r
print(paste0('The annual IRR calculated from cf_net is ',formatC(irr(cf_net)*12*100,digits = 2,format = 'f'),'%'))
```

```
## [1] "The annual IRR calculated from cf_net is 20.71%"
```

---

## Future Improvement

As this is a MVP (minimum viable product), there are some **improvements** that can be made in the future to improve the users experience. Such improvements are as followed:

1. Incorporate **transaction cost** such as legal fee, income tax, stamp duty and etc.
2. Incorporate **other expenses** such as maintenance fee, renovation fee and etc.
3. **More flexibility on cash flow input** to support multiple period cash flow
4. Provide **selling price prediction** of underlying property

---
