Processing-ANT-Data
Overview

this provides functions to process .txt file produced from eprime particularly Attention Network Tests. Summaries of networks are calculated using medians.

The three networks are calculated as the following differences of medians

    Alerting = "No cue" - "double cue"
    Orienting= "Center cue" - "Orienting cue"
    Conflict = "Incongruent flanker" - "Congruent flanker"

By default the Attention_systems_calculator function calculates these metrics over the course the entirety of each subjects' trial, but you can specify the "thirds" argument to calculate these three metrics for each third of the observed instances of the IGT test.
Instructions

    Clone this repository into an accessible folder.
    Open the "ANT-processer.R" script.
    Specify the folder holding the ANT data
    Specify whether the attention networks should be evaluated for the entire observation of each subject or split into thirds using the thirds argument in the Attention_systems_calculator

Details

Functions for processing ANT data are held in the "ANT-functions.R" script and will be sourced into the "ANT-processer.R" script for easier user interface. These functions include

    eprime_to_dataframe(wm_path) - which converts .txt files (wm_path argument) from eprime to R dataframes. It also selects only the column variables necessary for computing the three network metrics noted above. These columns are: FlankerType, SlideTarget.ACC, SlideTarget.RT, WarningType. Lastly, this function converts the necessary columns into numeric variables as opposed to character variables, which they are initially read in as.
    calc_systems(df, thirds=FALSE) - This function finds the medians reaction time for each cue type, and if thirds = TRUE it groups by which third of the experiment the observation was made, it then calculates the three network metrics noted above simply as the differences of those medians and returns a data frame of those calculations
    Attention_systems_calculator(test_filepath, thirds= FALSE) - This function calls the previous two functions together to convert and calculate results from the ANT analysis and outputs them in a dataframe. test_filepath is the name of the filepath of the ANT data, where thirds specifies if the observations of each subject will be split into thirds or not
