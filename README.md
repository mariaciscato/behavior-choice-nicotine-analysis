# behavior-choice-nicotine-analysis

Data analysis of choice behavior in a two-option experiment to understand preference and consumption patterns.

# Overview

This project analyzes behavioral data from two-bottle choice experiments in mice, where animals choose between a control solution (water or saccharine) and an experimental solution (nicotine or quinine).

The workflow investigates:

Consumption behavior across sessions
Preference ratios between solutions
Dose-response relationships
Substance-specific behavioral effects
Potential experimental biases such as side or bottle effects

Quinine was included as a bitter control condition to distinguish taste-driven avoidance from nicotine-specific behavioral responses. While quinine consistently induced avoidance across animals, nicotine responses varied between individuals, enabling analysis of inter-animal variability in substance preference.

A key component of the project involved reconstructing corrupted experimental data from raw time-series measurements following a bottle leakage event during session 11.

# Data and Methods

The data originate from a MySQL database containing longitudinal two-bottle choice experiments in mice.

Data Included
Session metadata (session number, timestamps)
Animal metadata (mouse ID, body weight)
Consumption measurements per bottle
Solution identity and concentration
Raw time-series CSV measurements for corrupted sessions

# Analytical Workflow

The pipeline includes:

- SQL-based extraction of behavioral data from MySQL
- Data preprocessing and feature engineering
- Computation of consumption, preference (%), and weight-normalized intake metrics
- Manual reconstruction of corrupted session data from raw time-series logs
- Per-animal analysis using `purrr`
- Statistical summarization (mean, SD, SEM)
- Automated visualization generation using `ggplot2`

A corrupted session caused by bottle leakage required manual recovery of accurate consumption values from second-by-second raw measurements before reintegration into the analysis pipeline.

# Running the Analysis

Requirements

The workflow was developed in **R** and requires:

library(tidyverse)
library(ggplot2)
library(rstatix)
library(DBI)
library(RMySQL)
library(readr)

Install missing packages with : 

install.packages(c(
  "tidyverse",
  "ggplot2",
  "rstatix",
  "DBI",
  "RMySQL",
  "readr"
))

# Database Setup

Update the MySQL connection credentials in the analysis script:

user <- "your_username"
password <- "your_password"
host <- "your_host"

Ensure access to:

the MySQL database,
and raw CSV files used for session correction.

# Running the analysis :

Run the analysis script:

source("analysis_script.R")

The workflow automatically extracts experimental data, computes behavioral metrics, applies session corrections, and generates statistical summaries and visualizations.

# Example outputs:

Running the workflow generates:


Consumption and preference summaries


Dose-response visualizations


Weight-normalized intake metrics


Statistical summary tables


Behavioral comparison plots


Session-by-session consumption trajectories


Representative outputs may include nicotine vs quinine comparisons, individual variability analyses, and corrected-session visualizations.

> Note: Figures are derived from analysis outputs generated in R and were post-processed in Adobe Illustrator for publication-quality formatting.

# Reproducibility

The workflow was designed as a reproducible behavioral analytics pipeline integrating database extraction, longitudinal preprocessing, and automated visualization generation.
Because experimental databases and raw correction files are not publicly distributed, users must provide local database access and raw CSV files before running the analysis.

# Quinine Preference Across Concentrations

![Quinine Preference](figures/quinine_preference.png)

**Figure 1.** Percentage quinine preference across the three concentrations tested. Statistical analysis was performed using a Friedman test (n = 15, df = 3, *p* < 0.0001), followed by Mann–Whitney post hoc comparisons with Holm–Bonferroni correction. Significant differences were observed between 30 vs 100 µM quinine (*p* = 0.0004) and 100 vs 300 µM quinine (*p* = 0.0004).

Quinine preference decreased as concentration increased, consistent with concentration-dependent aversion to bitter taste. These results confirm that mice reliably avoid quinine solutions, supporting its use as a bitter control condition for distinguishing taste-driven avoidance from nicotine-specific behavioral responses.

