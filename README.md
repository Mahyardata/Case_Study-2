# Case_Study-2
How-can-a-wellness-technology-company-play-it-smart


### Installing and loading common packages and libraries ###

install.packages("tidyverse")

library(tidyverse)

install.packages("dplyr")

library(dplyr)

install.packages("ggplot2")

library(ggplot2)


### Load the CSV files and make a data frame ###


daily_activity <- read.csv("dailyActivity_merged.csv")

sleep_day <- read.csv("sleepDay_merged.csv")

# Take a look at the daily_activity data.
head(daily_activity)

# Identify all the columns in the daily_activity data.
colnames(daily_activity)

# Take a look at the sleep_day data.
head(sleep_day)

# Identify all the columns in the sleep_day data.
colnames(sleep_day)


# Understanding some summary statistics #


# How many unique participants are there in each data frame? 
n_distinct(daily_activity$Id)

n_distinct(sleep_day$Id)

# How many observations are there in each data frame?
nrow(daily_activity)

nrow(sleep_day)

# What are some quick summary statistics we want to know about each data frame?

# For the daily activity data frame:
daily_activity %>%  
  select(TotalSteps,
         TotalDistance,
         SedentaryMinutes) %>%
  summary()

# For the sleep day data frame:

sleep_day %>%  
  select(TotalSleepRecords,
         TotalMinutesAsleep,
         TotalTimeInBed) %>%
  summary()


# Plotting a few explorations to get more information and more easily to understand #


# What's the relationship between steps taken in a day and sedentary minutes? 
# How could this help inform the customer segments that we can market to? 

ggplot(data=daily_activity, aes(x=TotalSteps, y=SedentaryMinutes)) + geom_point()

# What's the relationship between minutes asleep and time in bed? 

ggplot(data=sleep_day, aes(x=TotalMinutesAsleep, y=TotalTimeInBed)) + geom_point()

# Merging these two datasets #

combined_data <- merge(sleep_day, daily_activity, by="Id")

View(combined_data)

# Take a look at how many participants are in this data set.
n_distinct(combined_data$Id)



[Visualization 1 ] [TotalSteps_SedentaryMinutes.pdf](https://github.com/user-attachments/files/18893350/TotalSteps_SedentaryMinutes.pdf)

[Visualization 2 ] [TotMinAsleep_TotTimeInBed.pdf](https://github.com/user-attachments/files/18893371/TotMinAsleep_TotTimeInBed.pdf)
