README
================
2025-03-23

# Predicting Stroke, and Heart Disease: Identifying Key Risk Factors

Data Science Institute - Cohort 5 - Team 1 Project

## Members

- Marta Zaiats ([mprezlyata](https://github.com/mprezlyata))
- Ranveer Kaur ([ranvikhalar](https://github.com/ranvikhalar))
- Vikram Katju ([vikramkatju](https://github.com/vikramkatju))
- Poulami Dey ([poulami249](https://github.com/poulami249))
- Lauren Mulders ([Mulders95](https://github.com/Mulders95))

## Introduction

Stroke and heart disease remain leading causes of death and disability
worldwide. According to the World Health Organization, 15 million people
suffer a stroke annually, with 5 million resulting in death and another
5 million facing permanent disability. Traditional healthcare approaches
often react to diseases rather than predict and prevent them. This
project takes a proactive, data-driven approach to understanding the
primary predictors of stroke, hypertension, and heart disease. By
leveraging data science techniques, we aim to enable personalized risk
assessment and early intervention to reduce hospitalizations, treatment
costs, and mortality rates.

## Business Question

How can data-driven techniques, including machine learning and data
visualization, be utilized to identify key predictors of stroke,
hypertension, and heart disease, and how can this knowledge be applied
to improve early detection and preventive healthcare measures?

## Project Overview

This project aims to identify the key features that influence the
occurrence of stroke, hypertension, and heart disease by leveraging data
science techniques, particularly data visualization. Our goal is to
create high quality visualizations with appropriate complexity for each
of the outcome variables to depict their relationship with the features
in this dataset.

Using the visualizations we will create, time permitting, we will
attempt to develop a predictive model that can predict whether a patient
is likely to get stroke, and heart disease based on the input parameters
like gender, age, avg_glucose_level, bmi, ever_married, smoking status
etc., which could assist the target audience in identifying individuals
at high risk and implementing preventive measures effectively. The
target audience for this project includes:

1.  Healthcare Providers – Doctors, cardiologists, and medical
    professionals who can use the predictive model to assess patient
    risk and implement early interventions.

2.  Public Health Officials – Organizations focused on disease
    prevention and healthcare policy can use insights from the model to
    develop targeted awareness and prevention programs.

3.  Patients & At-Risk Individuals – People looking to understand their
    personal risk factors and take proactive steps toward prevention and
    lifestyle changes.

# Requirements

This project uses the following Python libraries:

| **Library**        | **Use**                                    |
|--------------------|--------------------------------------------|
| `pandas`           | Data manipulation and analysis             |
| `numpy`            | Numerical computations                     |
| `seaborn`          | Statistical data visualization             |
| `plotly`           | Interactive visualizations                 |
| `scikit-learn`     | Machine learning models and evaluation     |
| `matplotlib`       | Data visualization                         |
| `statsmodels`      | Statistical models                         |
| `scipy`            | Scientific computation                     |
| `imbalanced-learn` | Handling imbalanced datasets (e.g., SMOTE) |

Although many of the data visualizations will be done in a Python
environment, some will also be done in an R environment using ggplot and
other libraries on an as-needed basis.

# Data Overview

*Dataset Source*: [Stroke Prediction
Dataset](https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset)

| **Column Name**     | **Description**                                                                                                   | **Datatype** |
|---------------------|-------------------------------------------------------------------------------------------------------------------|--------------|
| `id`                | A unique identifier of each record.                                                                               | `int64`      |
| `gender`            | The gender of the patient (“Male”, “Female” or “Other”).                                                          | `object`     |
| `age`               | The age of the patient.                                                                                           | `float64`    |
| `hypertension`      | A binary indicator (0 or 1) representing whether the patient has hypertension.                                    | `int64`      |
| `heart_disease`     | A binary indicator (0 or 1) representing whether the patient has heart disease.                                   | `int64`      |
| `ever_married`      | The patient has ever been married (Yes or No).                                                                    | `object`     |
| `work_type`         | The type of work the patient is involved in (‘Private’, ‘Self-employed’, ‘Govt_job’, ‘children’, ‘Never_worked’). | `object`     |
| `Residence_type`    | The type of residence (Urban or Rural).                                                                           | `object`     |
| `avg_glucose_level` | The average glucose level of the patient.                                                                         | `float64`    |
| `bmi`               | The Body Mass Index of the patient.                                                                               | `float64`    |
| `stroke`            | A binary indicator (0 or 1) representing whether the patient has experienced a stroke.                            | `int64`      |
| `smoking_status`    | The smoking status of the patient (‘formerly smoked’, ‘never smoked’, ‘smokes’, ‘Unknown’).                       | `object`     |

Additional columns that we have created for the analysis are heart risk
and stroke risk.

**Heart Risk** - It implies the risk of stroke given either heart
disease or hypertension.

**Stroke Risk** - It implies the risk of heart disease given either
stroke or hypertension.

| **Column Name** | **Description**                                                                                 | **Datatype** |
|-----------------|-------------------------------------------------------------------------------------------------|--------------|
| `heart_risk`    | A binary indicator (0 or 1) representing whether the patient has hypertension or heart disease. | `int64`      |
| `stroke_risk`   | A binary indicator (0 or 1) representing whether the patient has stroke or hypertension.        | `int64`      |

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
the nominal predictors gender, ever_married, work_type, Residence_type,
and smoking_status together with the bmi variable itself to impute all
missing values of bmi with the grouped median values of the other
variables.

Several observations were discarded from the dataset. The rationale for
doing this is as follows:

1.  All observations corresponding to work_type = children were removed
    from the dataset. The rationale for doing this is that there are 687
    such observations whereas there are only 3 such observations
    representing people with one of the three diseases (stroke,
    hypertension or heart disease) under consideration. No model will be
    able to classify a binary outcome variable with this kind of class
    disparity. One other thing to keep in mind is that stroke, heart
    disease, and hypertension are diseases typically affecting the
    elderly. Children, in particular, are unlikely to get these diseases
    unless they have some abnormality, for example, some genetic
    abnormality. Since we do not have any genetic information in this
    dataset, and since the number of children with the diseases of
    interest is very small it is best to remove of all such
    observations.

2.  The single observation corresponding to Gender = Other was removed
    from the dataset. This observation is uninteresting because the
    person corresponding to it does not have any of the three diseases
    under consideration and because by being an ‘orphan observation’ no
    model will be able to classify such a model correctly.

3.  Finally, three different dataframes were created–one each for
    stroke, hypertension, and heart disease. The dataframe for stroke
    comprised of all observations in the original dataframe,once the
    work_type = children observations have been removed, with the
    additional condition that only those observations were retained
    where the age was equal to or greater than the minimum age of anyone
    with stroke in the dataset. A similar procedure was adopted in the
    creation of the hypertension and heart disease dataframes. All three
    dataframes were then written to .csv files (one .csv file per
    dataframe) to be used for further analysis.

# Exploratory Data Analysis

[Click here: Stroke Data
Visualization](https://mulders95.github.io/Predicting_Stroke_and_Heart_Disease/Plots_Used/stroke_data.html)

The figure above compares the stroke dataset before and after the
cleaning process. Prior to cleaning, 4.8% of the population in the
dataset had experienced a stroke. After cleaning, this percentage
increased to 7.2%, indicating that the data cleaning process made the
target variable (stroke occurrence) more prevalent.

In the cleaned dataset, heart risk is defined as a composite variable
that includes a positive marker for hypertension or heart disease. If an
individual had either condition, they were classified as having heart
risk. Among those in the cleaned dataset, 20% of individuals with heart
risk had experienced a stroke.

By improving data quality, the cleaned dataset more accurately
represents the relationship between key health factors and stroke
occurrence. This refinement enhances the reliability of predictive
modeling and statistical analysis, supporting more precise insights into
stroke risk factors.

[Click here: Stroke Normalized Data
Visulization](https://mulders95.github.io/Predicting_Stroke_and_Heart_Disease/Plots_Used/stroke_analysis_normalized.html)

The figure above is a normalized analysis comparing populations relative
to each other highlights heart risk, age, and glucose levels as
significant stroke predictors. - Heart Risk: Individuals with heart risk
have a higher relative stroke occurrence, with 14.56% experiencing a
stroke, compared to 5.39% among those without heart risk.  
- Age: The 60+ population shows a sixfold higher stroke occurrence
(12.06%) than those aged 40-59 (2.11%).  
- Glucose Levels: Individuals with higher glucose levels (190+ mg/dL)
have a greater relative risk of stroke (8.84%) compared to those with
lower glucose levels (5.67%).

[Click here: Heart Disease Data
Visulization](https://mulders95.github.io/Predicting_Stroke_and_Heart_Disease/Plots_Used/heart_disease_data.html)

The figure above compares the heart disease dataset before and after the
data cleaning process. In the cleaned dataset, stroke risk is defined as
a composite variable that includes a positive marker for hypertension or
had a stroke. If an individual had either condition, they were
classified as having stroke risk. Prior to cleaning, the predictor
variables were distributed as follows:

Before Cleaning  
- **Smoking Status:**  
- Never smoked = 37%  
- Unknown = 30%  
- Formerly smoked = 17%  
- Smokes = 15%

- **Gender:**
  - Male = 41%  
  - Female = 59%
- **Work Type:**
  - Government job = 13%  
  - Self-employed = 16%  
  - Private = 57%  
  - Children = 13%  
  - Never worked = 0.4%

After Cleaning  
- **Smoking Status:**  
- Never smoked = 40%  
- Unknown = 19%  
- Formerly smoked = 22%  
- Smokes = 18%

- **Heart Disease (Composite Variable of Hypertension and Stroke,
  Similar to Heart Risk)** = 8%

- **Gender:**

  - Male = 60%  
  - Female = 40%

- **Work Type:**

  - Government job = 16%  
  - Self-employed = 21%  
  - Private = 62%

The cleaning process led to notable shifts in variable distributions,
particularly in smoking status, gender, and work type. The percentage of
individuals with unknown smoking status decreased significantly from 30%
to 19%, improving the dataset’s reliability. The reclassification of
heart disease as a composite variable incorporating hypertension and
stroke resulted in 8% of the population being categorized under this
metric.

Additionally, gender distribution shifted, with males increasing from
41% to 60% and females decreasing to 40%. The work type distribution saw
a rise in self-employed individuals (from 16% to 21%) and government
workers (from 13% to 16%), while private-sector representation remained
dominant at 62%.

These refinements ensure a more accurate and representative dataset for
further analysis, reducing missing data and improving the integrity of
statistical modeling.

![](README_files/figure-gfm/facet_plot-1.png)<!-- --> ![Facet
plot](https://github.com/Mulders95/Predicting_Stroke_and_Heart_Disease/blob/main/Plots_Used/heart_disease_facet_plot_6vars_p1.png)

The above plot compares six different variables. The plot indicates that
certain job types may have a higher average risk of heart disease than
others. Moreover, the plots continue to show that there is a correlation
between age and heart disease.

# Key Findings in Datasets

### Key Findings in Stroke Dataset

The analysis provides several key insights regarding stroke factors:

1.  Heart Risk (Heart Disease or Hypertension) is associated with Stroke

    - A Chi-square test of independence (p = 0.000) confirms an
      association between stroke and heart risk at the 5% significance
      level. The Cramer’s V for this test is 0.14 implying a weak
      association exists between these two variables.

2.  Age and Glucose Levels Are Significant Predictors

    - Mann-Whitney U tests inform that age and average glucose levels
      differ significantly between stroke and non-stroke groups (p =
      0.000 for both age and stroke status as well as for average
      glucose levels and stroke status). Further, no significant
      relationship exists between BMI and stroke status (p = 0.359).

3.  No Significant Association Between Stroke and Gender, Marital
    Status, Work Type, Residence Type, and Smoking Status

    - The Chi-square test of independence results show no statistically
      significant relationship at the 5% significance level, between
      stroke and:
      - Gender (p = 0.338, Cramer’s V = 0.016)
      - Marital status (p = 0.9483, Cramer’s V = 0.001)
      - Work type (p = 0.1354, Cramer’s V = 0.034)
      - Residence type (p = 0.2686, Cramer’s V = 0.019)
      - Smoking status (p = 0.2400, Cramer’s V = 0.038)

![](README_files/figure-gfm/stroke_venn-1.png)<!-- --> ![Stroke Venn
plot](https://github.com/Mulders95/Predicting_Stroke_and_Heart_Disease/blob/main/Plots_Used/stroke_venn.png)

### Venn Diagram Findings:

There are 247 patients with a history of stroke, regardless of whether
they also have heart risk factors (hypertension or heart disease).
Additionally, there are 647 patients with heart risk.The hear risk
patients include individuals with hypertension or heart disease,
regardless of whether they have experienced a stroke.

The 100 patients in the intersection section of the Venn diagram
highlights the co-occurrence of stroke and heart risk. These represent
patients who have a history of both stroke and either heart disease or
hypertension, implying they may be at a greater risk of further
complications. These patients may require targeted interventions or
preventive measures due to the compounded health risks.

### Association Between Stroke and Smoking Status

A key question in the analysis is whether there is any association
between stroke and smoking status. The Chi-Square test of independence
indicates no significant association based on the current smoking status
categories:

- Never smoked  
- Formerly smoked  
- Unknown  
- Smokes

To explore this further, smoking status categories were restructured and
retested:

#### First Reclassification

- Formerly smoked and smokes were combined into a single category: Ever
  Smoked.  
- The Chi-Square test of independence still yielded an insignificant
  p-value (p= 0.2628) at the 5% significance level, indicating no
  association.

#### Second Reclassification

- Formerly smoked, smokes, and unknown were combined into Ever Smoked
  (assuming that some former smokers might not disclose their smoking
  history).  
- Again, the Chi-Square test of independence produced an insignificant
  p-value (p= 0.2400) at the 5% significance level, reinforcing the lack
  of association.

Regardless of how smoking status is categorized, the dataset
consistently shows no statistically significant relationship between
stroke and smoking status at the 5% significance level.

------------------------------------------------------------------------

### Key Findings in Heart Disease Dataset

The analysis provides several key insights regarding heart disease
factors:

1.  Gender Is Significantly Associated with Heart Disease

    - A Chi-square test of independence (p = 0.0000) indicates an
      association between gender and heart disease at the 5%
      significance level. The corresponding Cramer’s V value of 0.108
      indicates a weak relationship between gender and heart disease.

2.  Stroke Risk (Stroke or Hypertension) is Significantly Associatied
    with Heart Disease

    - A Chi-square test of independence (p = 0.000) indicates a
      significant relationship between stroke risk and heart disease at
      the 5% significance level. The corresponding Cramer’s V value of
      0.129 indicates a weak relationship between heart disease and
      stroke risk.

3.  Work Type is Associatied with Heart Disease A Chi square test of
    independence (p = 0.002) indicates a significant relationship
    between work type and heart disease. That is, individuals with
    specific work types may be at higher risk of heart disease. The
    corresponding Cramer’s V value of 0.059 suggests a weak relationship
    exists between work type and heart disease.

4.  Smoking Status is Associatied with Heart Disease

    - A Chi-square test of independence (p = 0.0065) indicates a
      relationship between Smoking Status and heart disease at the 5%
      significance level.The corresponding Cramer’s V value of 0.058
      suggests a weak relationship exists between smoking status and
      heart disease status.

5.  No Significant Association Between Heart Disease and Other
    Categorical Variables

    - The Chi-square test of independence results indicate no
      statistically significant relationship between heart disease and:
      - Marital status (p = 0.5902, Cramer’s V = 0.009)
      - Residence type (p = 1.0, Cramer’s V = 0.0)

6.  Age and Glucose Levels Are Significant Predictors

    - Mann-Whitney U tests inform that age and average glucose levels
      differ significantly between heart disease and non-heart disease
      groups (p = 0.000 for both age and heart disease status as well as
      for average glucose levels and heart disease status). Further, no
      significant relationship exists between BMI and heart disease
      status (p = 0.729).

![](README_files/figure-gfm/heart_disease_venn-1.png)<!-- --> ![Heart
Disease
plot](https://github.com/Mulders95/Predicting_Stroke_and_Heart_Disease/blob/main/Plots_Used/heart_disease_venn.png)

### Venn Diagram Findings:

There are 275 patients in this dataset who have a history of heart
disease, regardless of whether they also have stroke risk factors
(hypertension or heart disease). There are also 656 patients with heart
risk, who include individuals with hypertension or stroke, regardless of
whether they have experienced heart disease.

The 98 patients in the intersection section of the Venn diagram
highlights the co-occurrence of heart disease and stroke risk. These are
patients who have a history of both heart disease and (stroke or
hypertension), which may place them at an elevated risk for additional
complications. These patients may require targeted interventions or
preventive measures due to the compounded health risks.

# Biases and Limitations of Predictive Data

#### Sampling Bias

The dataset comes from a confidential source and is intended only for
educational purposes. Since the data collection methods are unknown, we
cannot verify whether the dataset was randomly sampled from a diverse
and representative population. If the sample is biased or not reflective
of an appropriate target population, the results will not generalize
beyond this dataset.

Additionally, the team made a decision to remove all children from the
data since of the 670 children in this dataset only 3 had occurence of
either of stroke, heart disease or hypertension. Further, only those
observations were included that fell between a lower cut-off and upper
cut-off of the 3 numerical variables, age, avg_glucose_level and BMI.
The lower cut-off for each of the 3 numerical variables (age,
avg_glucose_level and BMI) was the smallest value for that variable with
a positive occurence of stroke when studying the stroke dataset and the
smallest value for that variable with a positive occurence of heart
disease when studying the heart disease dataset. Likewise for the upper
cut-off values for stroke and heart disease for each of the numerical
predictors. The rationale for only selecting observations within the
cut-off values was that we wanted to build a predictive model for stroke
and heart disease. Our understand was that such a model would not be an
effective model if we did not follow the approach we did.

#### Correlation vs. Causation

A key limitation of this dataset is the risk of misinterpreting
correlation as causation. While the analysis may reveal associations
between variables, it does not prove that one factor directly causes
another.

For example, the dataset might show an association between high glucose
levels and stroke risk, but this does not necessarily mean that high
glucose levels cause strokes. Other factors, such as diabetes, lifestyle
choices, or genetic predisposition, could be influencing both variables.

#### Feature Selection Bias

The dataset does not include certain critical stroke and heart disease
risk factors such as:

- Genetics  
- Dietary habits  
- Medication use  
- Environmental factors

These missing variables could significantly impact disease risk, meaning
the analysis might be incomplete or misleading. Hidden confounding
factors may drive risk in ways that this dataset does not capture,
potentially leading to biased conclusions. By recognizing these biases
and limitations, we can interpret the findings with caution and
acknowledge the need for more comprehensive studies to fully understand
risk factors.
