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
![image](https://user-images.githubusercontent.com/77570308/167725962-8e7c479c-a2e9-45ed-bccd-203c5ca9fae6.png)

```bash
str(equip)
```
![image](https://user-images.githubusercontent.com/77570308/167725028-23d98fb6-f24f-4296-9a04-7908b714c357.png)

```bash
summary(equip)
```
![image](https://user-images.githubusercontent.com/77570308/167725844-a6ca0c80-ee37-41a4-953c-f715c84c9507.png)

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
Losses are reported as stocks variables. In order to plot new daily losses, I create new data frames containing the first difference of losses.

```bash
# compute new losses by day
equip_diff <- data.frame(Date=equip$date[1:(nrow(equip)-1)], Day=equip$day[1:(nrow(equip)-1)],
                   Aircrafts=diff(equip$aircraft), Helicopters=diff(equip$helicopter), Tanks=diff(equip$tank),
                   APCs=diff(equip$APC), FieldArtillery=diff(equip$field.artillery), MRLs=diff(equip$MRL),
                   MilitaryAuto=diff(equip$military.auto), FuelTanks=diff(equip$fuel.tank), Drones=diff(equip$drone),
                   NavalShips=diff(equip$naval.ship), AntiAircraft=diff(equip$anti.aircraft.warfare),
                   SpecialEquipment=diff(equip$special.equipment), MobileSRBMSystems=diff(equip$mobile.SRBM.system))
person_diff <- data.frame(Date=person$date[1:(nrow(person)-1)], Day=person$day[1:(nrow(person)-1)],
                          Killed=diff(person$personnel), POW=diff(person$POW))
``` 
Plot new daily losses for each type of equipment. Combine all the plots in one figure. 

```bash
# new equipment losses by date
n1 <- ggplot(data = equip_diff, aes(x=Date, y=Aircrafts)) + geom_line(color = "darkred") + xlab("") +
  geom_point(aes(alpha=Aircrafts), size=I(1), color="darkred") + theme(legend.position="none")
n2 <- ggplot(data = equip_diff, aes(x=Date, y=Helicopters)) + geom_line(color = "darkred") + xlab("") +
  geom_point(aes(alpha=Helicopters), size=I(1), color="darkred") + theme(legend.position="none")
n3 <- ggplot(data = equip_diff, aes(x=Date, y=Tanks)) + geom_line(color = "darkred") + xlab("") +
  geom_point(aes(alpha=Tanks), size=I(1), color="darkred") + theme(legend.position="none")
n4 <- ggplot(data = equip_diff, aes(x=Date, y=APCs)) + geom_line(color = "darkred")  + xlab("") +
  geom_point(aes(alpha=APCs), size=I(1), color="darkred") + theme(legend.position="none")
n5 <- ggplot(data = equip_diff, aes(x=Date, y=FieldArtillery)) + geom_line(color = "darkred") + xlab("") +
  geom_point(aes(alpha=FieldArtillery), size=I(1), color="darkred") + theme(legend.position="none")
n6 <- ggplot(data = equip_diff, aes(x=Date, y=MRLs)) + geom_line(color = "darkred") + xlab("") +
  geom_point(aes(alpha=MRLs), size=I(1), color="darkred") + theme(legend.position="none")
n7 <- ggplot(data = equip_diff, aes(x=Date, y=MilitaryAuto)) + geom_line(color = "darkred") + xlab("") +
  geom_point(aes(alpha=MilitaryAuto), size=I(1), color="darkred") + theme(legend.position="none")
n8 <- ggplot(data = equip_diff, aes(x=Date, y=FuelTanks)) + geom_line(color = "darkred") + xlab("") +
  geom_point(aes(alpha=FuelTanks), size=I(1), color="darkred") + theme(legend.position="none")
n9 <- ggplot(data = equip_diff, aes(x=Date, y=Drones)) + geom_line(color = "darkred") + xlab("") +
  geom_point(aes(alpha=Drones), size=I(1), color="darkred") + theme(legend.position="none")
n10 <- ggplot(data = equip_diff, aes(x=Date, y=NavalShips)) + geom_line(color = "darkred") + xlab("") +
  geom_point(aes(alpha=NavalShips), size=I(1), color="darkred") + theme(legend.position="none")
n11 <- ggplot(data = equip_diff, aes(x=Date, y=AntiAircraft)) + geom_line(color = "darkred") + xlab("") +
  geom_point(aes(alpha=AntiAircraft), size=I(1), color="darkred") + theme(legend.position="none")
n12 <- ggplot(data = equip_diff, aes(x=Date, y=SpecialEquipment)) + geom_line(color = "darkred") + xlab("") +
  geom_point(aes(alpha=SpecialEquipment), size=I(1), color="darkred") + theme(legend.position="none")
n13 <- ggplot(data = equip_diff, aes(x=Date, y=MobileSRBMSystems)) + geom_line(color = "darkred") + xlab("") +
  geom_point(aes(alpha=MobileSRBMSystems), size=I(1), color="darkred") + theme(legend.position="none")

grid.arrange(n1, n2, n3, n4, n5, n6, n7, n8, n9, n10, n11, n12, n13, nrow = 5, ncol = 3,
             top = textGrob("Daily Equipment Losses by Type (since 24.02.2022)", gp=gpar(fontsize=16)))
```
![daily_equip_line2](https://user-images.githubusercontent.com/77570308/167730120-5d7d226a-8a7e-4d7d-be7d-786833c9b044.png)

Plot total equipment losses by type on 22.04.2022.

```bash
# graph of final losses
group <- colnames(equip_diff)
group <- group[3:length(group)]
value <- as.numeric(equip[nrow(equip),3:ncol(equip)])
data <- data.frame(group,value)
data %>%
  mutate(group = fct_reorder(group, value)) %>%
  ggplot( aes(x=group, y=value)) +
  geom_bar(stat="identity", fill="darkred", width=.4) +
  coord_flip() + xlab("") +
  ylab("# of units") + ggtitle("Total Equipment losses on 22.04.2022") + 
  theme(text=element_text(size=16), plot.title = element_text(hjust = 0.35))
```
![total_equip_bars](https://user-images.githubusercontent.com/77570308/167730155-51df0c74-1d27-4cd4-af81-e0f12084a0a5.png)

Next, I visualize the losses of personnel (including POWs). 

```bash
# new personnel losses by date
p1 <- ggplot(data = person_diff, aes(x=Date, y=Killed)) + geom_line(color = "darkred") +
  xlab("") +  ggtitle("Daily Personnel losses (since 24.02.2022)") +
  theme( plot.title = element_text(hjust = 0.35, size=16), 
        legend.position="none") + 
  geom_point(aes(alpha=Killed), size=I(2), color="darkred") 


p2 <- ggplot(data = person_diff, aes(x=Date, y=POW)) + geom_line(color = "darkred") +
  xlab("") + geom_point(aes(alpha=POW), size=I(2), color="darkred") +
  theme(legend.position="none")

group <- colnames(person_diff)
group <- group[3:length(group)]
value <- as.numeric(person[nrow(person), c(3,5)])
data <- data.frame(group,value)

#total personnel losses
ploss <- data %>%
  mutate(group = fct_reorder(group, value)) %>%
  ggplot( aes(x=group, y=value)) +
  geom_bar(stat="identity", fill="darkred", width=.4) +
  coord_flip() + xlab("") +
  ylab("") + ggtitle("Total Personnel losses on 22.04.2022") + 
  theme(text=element_text(size=14), plot.title = element_text(hjust = 0.35))

grid.arrange(p1, p2, ploss, ncol = 1)
```

![person_all](https://user-images.githubusercontent.com/77570308/167730577-4f7384a2-6401-4590-a89e-8e20f0355e0f.png)

## Conclusions:

* The pattern of losses changed after March 15 th , which suggests the
breaking point for the Northern direction around that time.
* Further losses shift to surveillance operations (drones) and logistics
(fuel tanks).
* More insights can be drawn with information on the geographical
distribution of losses, as well as comparing losses with the total forces
used in the region.
