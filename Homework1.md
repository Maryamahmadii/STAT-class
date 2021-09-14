A Two-Stage Machine Learning Approach to Predict Heart Transplantation
Survival Probabilities over Time with a Monotonic Probability Constraint
================
Maryam Ahmadi [1]
September 14, 2021

-   [Section: Loading Data & Data Clearning and
    Preparation](#section-loading-data-data-clearning-and-preparation)
    -   [Section:Loading Data and Assigning IDs for each
        case](#sectionloading-data-and-assigning-ids-for-each-case)
-   [Interactive App](#interactive-app)

This page documents the data cleaning and preparation procedure,
variable selection, statistical modeling, and survival probability
calibration procedures used in these research articles: 1) A Design of
Experiement Approach for Improving Performance of Machine Learning
Algorithms in predicting Survival of Transplant Surgeries. & 2) A
Two-Stage Machine Learning Approach to Predict Heart Transplantation
Survival Probabilities over Time with a Monotonic Probability
Constraint.

Details of the codes and the functions are available over Github of the
study: <https://github.com/transplantation/unos-ht>

Data was provided from the **UNOS** registry by staff at the US, United
Network for Organ Sharing.

The reader can **show** any code chunk by clicking on the *code* button.
We chose to make the default for the code hidden since we: (a) wanted to
improve the readability of this document; and (b) assumed that the
readers will not be interested in reading every code chunk.

Figure 1 provides an overview of our two-stage framework for obtaining
monotonic survival probabilities over time.

![Figure 1: The proposed two-stage framework for obtaining monotonically
decreasing heart transplantation survival
probabilities.](https://raw.githubusercontent.com/transplantation/unos-ht/master/data/rmarkdown/two_stage/figures/figure-1-methodology.JPG)

# Section: Loading Data & Data Clearning and Preparation

The snippet below documents the list of **R** packages and functions
that were used in this research. For convenience, we used the
<tt>pacman</tt> package since it allows for installing/loading the
needed packages in one step.

``` r
rm(list = ls()) # clear global environment
graphics.off() # close all graphics
library(pacman) # needs to be installed first
# p_load is equivalent to combining both install.packages() and library()
p_load(haven,dplyr,caret,foreign,glmnet,
       lubridate,dataPreparation,httr, DT, stringr, AUC, snow, testit,caretEnsemble,
       C50, Biocomb, varImp, party,
       randomForest,
       kernlab,gower,
       e1071,Boruta,ROSE,DMwR,
       unmarked) # unmarked is for downloading and reading an .rds file.
# UNOS data are loaded from this local drive, data could be obtained from www.unos.org
data.path <- "C:\\Users\\hza0020\\OneDrive - Auburn University\\Transplant\\BUAL-LAB\\DoE_10years\\"

source("https://raw.githubusercontent.com/transplantation/unos-ht/master/data/functions.R")
```

## Section:Loading Data and Assigning IDs for each case

In this snippet below, we load the data file and the form that records
the information regarding variables in the data. Both files are provided
by UNOS but we added one column: **INTERPRETATION\_TYPE** to the
information form. It records the variable type for each variable in the
data. This is a varaible we created based on the code book provided by
UNOS. The information can be found
[here](https://raw.githubusercontent.com/transplantation/DoE/Hamid/Interpretation_type.csv).
The data dictionary can be found
[here](https://www.srtr.org/requesting-srtr-data/saf-data-dictionary/).

``` r
# load data set
heart.df <- read_sas(paste0(data.path,"thoracic_data.sas7bdat"))

# add ids for each row
heart.df$ID <- row.names(heart.df)
# heart.form contains the variable definitions of each variable in data
heart.form <- read.csv("C:/Users/hza0020/OneDrive - Auburn University/Transplant/BUAL-LAB/DoE_10years/Interpretation_type.csv")  
```

Here is the information included in the form.

# Interactive App

We have created an interactive app that presents two modules for
performing the analysis:

1.  Manual Entry, where users can insert the values of predictor
    variables using several text boxes.

2.  CSV Entry, where users can upload the values of predictor variables
    using a comma seperated variable (CSV) file.

Visit the app:
[here](http://dataviz.miamioh.edu/Heart-Transplant/monotonic/).

[1] Aubrun University, <hamid@auburn.edu>
