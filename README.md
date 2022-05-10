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

## Conclusions:
