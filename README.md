# war-losses
Data visualization of russian military losses in Ukraine since 24.02.2022

## Goal:
Illustrate the dynamics of equipment and personel losses in the first 2 months of full-scale russian invasion, make conclusions about the changes in character of warfare. 

## Data description:

### russia_losses_equipment.csv

* date - current date
* day - number of days since the start of the full scale invasion (24.02.2022)
* aircraft - # of units destroyed since the start of the full scale invasion (24.02.2022)
* helicopter
* tank
* APC - armoured personnel carrier
* field artillery
* MRL - multiple rocket launcher
* military auto
* fuel tank
* drone
* naval ship
* anti-aircraft warfare
* speacial equipment
* mobile SRBM system - mobile short-range ballistic missile system


### russia_losses_personnel.csv

* date - current date
* day - number of days since the start of the full scale invasion (24.02.2022)
* personnel - # of killed personnel since the start of the full scale invasion (24.02.2022)
* POW - # of prisoners of war since the start of the full scale invasion (24.02.2022)


## Data visualization:

Firstly, I load the packages needed for the analysis. The most common for exploratory data analysis are: *dplyr* and *ggplot2*.

```bash
# packages
library(ggplot2)
#install.packages("dplyr")
library(dplyr)
library(tidyr)
#install.packages("gridExtra")
library(gridExtra)
library(grid)
library(forcats)
```

Then, I set the directory and upload the data.

```bash
# working directory
getwd()
setwd("C:\\Users\\hrabo\\Dropbox\\Portfolio\\R\\UkraineData")

# load the data
equip <- read.csv("russia_losses_equipment.csv")
person <- read.csv("russia_losses_personnel.csv")
```
Explore the data by looking at the first few rows, data type and summary of each column. I find that the records for some types of equipment are missing in the beginning of the dataset, so I change the NAs with zeros. Moreover, I transform *date* variable from **chr** into **date** format. 

```bash
# explore
head(equip)
```
```bash
str(equip)
```
![image](https://user-images.githubusercontent.com/77570308/167725028-23d98fb6-f24f-4296-9a04-7908b714c357.png)

```bash
summary(equip)
```

# format variables

#replace NA with zeros
equip[is.na(equip)] <- 0
person[is.na(person)] <- 0
#make dates
equip$date <- as.Date(equip$date,
                       format = "%Y-%m-%d")
str(equip)
person$date <- as.Date(person$date,
                      format = "%Y-%m-%d")
str(person)
```


## Conclusions:
