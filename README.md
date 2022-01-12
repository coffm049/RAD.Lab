# RAD.Lab
Common scripts to aid in calculations for the RAD lab (Dr. Kathryn Cullen)

The two scripts so far included are for calculating summary statistics from Attention Network (ANT) and Iowa Gambling (IGT) tasks. 

# Example for ANT data
# NOTE: you need to have tidyverse, rprime, rstudioapi, and wrapr installed.
# Install these in R with the following command <install.packages(c("tidyverse", "rprime", "wrapr", "rstudioapi")) >

library(rstudioapi)
######################
# User input

# Enter the file path for the ANT .txt data
ANT_folder <- selectDirectory()

# End User input
######################
# Source the script with ANT functions
source("Scripts/ANT-functions.R")


# Extract the files in that folder 
files <- list.files(ANT_folder, full.names = TRUE)

# select only the .txt files
files <- files[str_ends(files, ".txt")]

# Seed empty df to save attention network results
results <- data.frame()


# compute attention network metrics for each experiment
for (i in 1:20) {
  print(paste("Processing experiment", i))
  results <- rbind(results, Attention_systems_calculator(files[i], thirds = FALSE))
  results <- rbind(results, Attention_systems_calculator(files[i], thirds = TRUE))
}

r1 <- results
r2 <- results
r3 <- results
#### This is for storing and combining results from multiple years.
# 
results <- rbind(r1, r2, r3)

# save results as a csv if you want.
write.csv(results, "ANT_results.csv")
