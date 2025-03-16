README
================

# Predicting Stroke, Hypertension, and Heart Disease: Identifying Key Risk Factors

Data Science Institute - Cohort 5 - Team 1 Project

# Members

- Marta Zaiats ([mprezlyata](https://github.com/mprezlyata))
- Ranveer Kaur ([ranvikhalar](https://github.com/ranvikhalar))
- Vikram Katju ([vikramkatju](https://github.com/vikramkatju))
- Poulami Dey ([poulami249](https://github.com/poulami249))
- Lauren Mulders ([Mulders95](https://github.com/Mulders95))

# Business Case Question

What relevant features explain the occurrence of stroke, hypertension
and heart disease?

# Business Case

# Project Overview

This project aims to identify the key features that influence the
occurrence of stroke, hypertension, and heart disease by leveraging data
science techniques, particularly data visualization and, if time
permits, machine learning models. Our goal is to create high quality
visualizations with appropriate complexity for each of the outcome
variables to depict their relationship with the features in this
dataset.

Using the visualizations we will create, time permitting, we will
attempt to to develop a predictive model that can predict whether a
patient is likely to get stroke, hypertension, and heart disease based
on the input parameters like gender, age, avg_glucose_level, bmi,
ever_married, smoking status etc., which could assist healthcare
providers in identifying individuals at high risk and implementing
preventive measures effectively.

# Requirements

This project uses the following Python libraries:

| *Library*          | *Use*                                      |
|--------------------|--------------------------------------------|
| `pandas`           | Data manipulation and analysis             |
| `numpy`            | Numerical computations                     |
| `seaborn`          | Statistical data visualization             |
| `plotly`           | Interactive visualizations                 |
| `scikit-learn`     | Machine learning models and evaluation     |
| `imbalanced-learn` | Handling imbalanced datasets (e.g., SMOTE) |

Although many of the data visualizations will be done in a Python
environment, some will also be done in an R environment using ggplot.

# Data Overview

*Dataset Source*: [Stroke Prediction
Dataset](https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset)

# Data Cleaning and Handling Missing Values

The ‘id’ column has no impact on any of the three outcome variables and
was consequently dropped from the datast. Summary statistics for the
three numerical variables (age, avg_glucose_level, and bmi) were
generated. The nominal variables in this dataset incude the three
outcome variables, stroke, heart_disease, and hypertension; and also the
predictors used to study the outcome variables (gender, ever_married,
work_type, Residence_type, and smoking_status). The three nominal
outcome variable are of int64 type with possible values 0 and 1 and were
left as is. The predictor nominal variables were all transformed to
category type variable. Frequency counts for each category was generated
for all the nominal variables,both the predictors as well as the
outcomes. All the predictor nominal variables were encoded appropriately
using the label encoder method.

The only variable with missing values in this dataset is bmi. Imputing
of missing values was done in the following way. First, two new
categorical variables corresponding to the age and avg_glucose variables
were created. These two newly created categorical variables were forced
to have only two levels or categories with their median value as the
cut-off. Next, the two newly created categorical variables (age
categorical and avg_glucose_level categorical) were combined with all
the nominal predictors (gender, ever_married, work_type, Residence_type,
and smoking_status together with the bmi variable itself to impute all
missing values of bmi with the grouped median values of the other
variables.

Several observations were discarded from the dataset. The rationale for
doing this is as follows:

All observations corresponding to work_type = children were removed from
the dataset. The rationale for doing this is that there are 687 such
observations whereas there are only 3 such observations representing
people with one of the three diseases (stroke, hypertension or heart
disease) under consideration. No model will be able to classify a binary
outcome variable with this kind of class disparity. One other thing to
keep in mind is that stroke, heart disease, and hypertension are
diseases typically affecting the elderly. Children, in particular, are
unlikely to get these diseases unless they have some abnormality, for
example, some genetic abnormality. Since we do not have any genetic
information in this dataset, and since the number of children with the
diseases of interest is very small it is best to remove of all such
observations.

The single observation corresponding to Gender = Other was removed from
the dataset. This observation is uninteresting because the person
corresponding to it does not have any of the three diseases under
consideration and because by being an ‘orphan observation’ no model will
be able to classify such a model correctly.

Finally, three different dataframes were created–one each for stroke,
hypertension, and heart disease. The dataframe for stroke comprised of
all observations in the original dataframe,once the work_type = children
observations have been removed, with the additional condition that only
those observations were retained where the age was equal to or greater
than the minimum age of anyone with stroke in the dataset. A similar
procedure was adopted in the creation of the hypertension and heart
disease dataframes. All three dataframes were then written to .csv files
(one .csv file per dataframe) to be used for further analysis.

# Exploratory Data Analysis

We have started creating visual depictions of the data for the outcome
variables and hope to weave the visuals together into a cohesive whole
by next week.

# Key Findings & Predictive Power of Features

For Stroke Prediction: To be determined (work in progress)

For Hypertension Prediction: To be determined (work in progress)

For Heart Disease Prediction: To be determined (work in progress)

# Discussion & Interpretation

Insights on which groups are most at risk: To be determined (work in
progress)

Potential bias or limitations in data: To be determined (work in
progress)
