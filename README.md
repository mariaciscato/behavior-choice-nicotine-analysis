# behavior-choice-nicotine-analysis
Data analysis of choice behavior in a two-option experiment to understand preference and consumption patterns.

# Problem statement
This project analyzes behavioral data from a two-bottle choice experiment in mice, where animals choose between a control solution (water or saccharine) and an experimental solution (nicotine or quinine).

The goal is to quantify consumption patterns, preference (%), and dose-response relationships, while accounting for potential experimental biases (e.g., side or bottle effects).

A key challenge is the presence of corrupted data (session 11) due to a bottle leakage event, requiring manual reconstruction of consumption values from raw time-series logs.

Importantly, quinine serves as a bitter control to distinguish taste-driven avoidance from true behavioral responses. While all mice avoid quinine, nicotine elicits variable responses across individuals, allowing us to assess substance-specific effects beyond simple bitterness aversion.

# Data description

The data come from a MySQL database containing two-bottle choice experiments in mice.

It includes:

Session data (session number, timestamps)
Animal metadata (mouse ID, body weight)
Consumption data (volume per bottle, solution type, concentration)

Sampling resolution:

Consumption was recorded every second
Body weight was measured approximately every 4 days

To address a corrupted session (due to bottle leakage), raw CSV files with time-resolved measurements were used to manually reconstruct accurate consumption values.

# Key techniques used

SQL data extraction (MySQL → R)
Data cleaning & preprocessing (filtering, missing values, type conversion)
Feature engineering (consumption volumes, preference %, weight-normalized intake)
Manual data correction from raw time-series logs (corrupted session recovery)
Functional programming (purrr) to automate per-animal analysis
Statistical summarization (mean, SD, SEM)
Data visualization with ggplot2

# How to run the code

1) Install required R packages:

install.packages(c("tidyverse", "ggplot2", "rstatix", "DBI", "RMySQL", "readr"))

2) Update the MySQL database credentials in the script (user, password, host).

Ensure access to the database and place required CSV files (for session correction) in the correct directory.

3) Run the script:

source("analysis_script.R")
The script will extract data, compute consumption and preference metrics, apply corrections, and generate summary outputs and plots.

# Example outputs:
