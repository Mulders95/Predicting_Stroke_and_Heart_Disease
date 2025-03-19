# Predicting Stroke, Hypertension, and Heart Disease: Identifying Key Risk Factors

Data Science Institute - Cohort 5 - Team 1 Project

# Members

- Marta Zaiats ([mprezlyata](https://github.com/mprezlyata))
- Ranveer Kaur ([ranvikhalar](https://github.com/ranvikhalar))
- Vikram Katju ([vikramkatju](https://github.com/vikramkatju))
- Poulami Dey ([poulami249](https://github.com/poulami249))
- Lauren Mulders ([Mulders95](https://github.com/Mulders95))

## Introduction
Stroke and heart disease remain leading causes of death and disability worldwide. According to the World Health Organization, 15 million people suffer a stroke annually, with 5 million resulting in death and another 5 million facing permanent disability. Traditional healthcare approaches often react to diseases rather than predict and prevent them. This project takes a proactive, data-driven approach to understanding the primary predictors of stroke, hypertension, and heart disease. By leveraging data science techniques, we aim to enable personalized risk assessment and early intervention to reduce hospitalizations, treatment costs, and mortality rates.

## Business Question
How can data-driven techniques, including machine learning and data visualization, be utilized to identify key predictors of stroke, hypertension, and heart disease, and how can this knowledge be applied to improve early detection and preventive healthcare measures?

### Project Overview

This project aims to identify the key features that influence the occurrence of stroke, hypertension, and heart disease by leveraging data science techniques, particularly data visualization. Our goal is to create high quality visualizations with appropriate complexity for each of the outcome variables to depict their relationship with the features in this dataset.

Using the visualizations we will create, time permitting, we will attempt to develop a predictive model that can predict whether a patient is likely to get stroke, and heart disease based on the input parameters like gender, age, avg_glucose_level, bmi, ever_married, smoking status etc., which could assist the target audience in identifying individuals at high risk and implementing preventive measures effectively. The target audience for this project includes:

1. Healthcare Providers – Doctors, cardiologists, and medical professionals who can use the predictive model to assess patient risk and implement early interventions.

2. Public Health Officials – Organizations focused on disease prevention and healthcare policy can use insights from the model to develop targeted awareness and prevention programs.

3. Patients & At-Risk Individuals – People looking to understand their personal risk factors and take proactive steps toward prevention and lifestyle changes.



# Requirements

This project uses the following Python libraries:

| **Library**        | **Use**                                    |
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

1. All observations corresponding to work_type = children were removed from
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

2. The single observation corresponding to Gender = Other was removed from
the dataset. This observation is uninteresting because the person
corresponding to it does not have any of the three diseases under
consideration and because by being an ‘orphan observation’ no model will
be able to classify such a model correctly.

3. Finally, three different dataframes were created–one each for stroke,
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

## Key Findings & Predictive Power of Features

### Key Findings in Stroke Dataset
The analysis provides several key insights regarding stroke risk factors:

1. Heart Risk (Heart Disease and/or Hypertension) Are Strongly Associated with Stroke
   - Individuals with heart risk have a significantly higher likelihood of experiencing a stroke.
   - A Chi-square test (p = 0.000) confirms a strong association between stroke and heart risk using the 5% significance.

2. Age and Glucose Levels Are Significant Predictors
   - Stroke patients tend to be older and have higher average glucose levels.
   - A Mann-Whitney U test indicates that age and glucose levels differ significantly between stroke and non-stroke groups.

3. No Significant Association Between Stroke and Gender, Marital Status, Work Type, Residence Type, and Smoking Status
   - The Chi-square test results show no statistically significant relationship using the 5% significance, between stroke risk and:
     - Gender (p = 0.338)
     - Marital status (p = 0.9483)
     - Work type (p = 0.1354)
     - Residence type (p = 0.2686)
     - Smoking status (p = 0.2400)

### Association Between Stroke and Smoking Status
A key question in the analysis is whether there is any association between stroke and smoking status. The Chi-Square test of independence indicates no significant association based on the current smoking status categories:

- Never smoked  
- Formerly smoked  
- Unknown  
- Smokes  

To explore this further, smoking status categories were restructured and retested:

#### First Reclassification  
- Formerly smoked and smokes were combined into a single category: Ever Smoked.  
- The Chi-Square test still yielded an insignificant p-value (p= 0.2628) at the 5% significance level, indicating no association.

#### Second Reclassification  
- Formerly smoked, smokes, and unknown were combined into Ever Smoked (assuming that some former smokers might not disclose their smoking history).  
- Again, the Chi-Square test produced an insignificant p-value (p= 0.2400) at the 5% significance level, reinforcing the lack of association.  

Regardless of how smoking status is categorized, the dataset consistently shows no statistically significant relationship between stroke and smoking status at the 5% significance level.

---
### Key Findings in Heart Disease Dataset  
The analysis provides several key insights regarding heart disease risk factors:  

1. Gender Is Significantly Associated with Heart Disease   
    - The dataset suggests that men have a higher likelihood of developing heart disease compared to women.  
    - A Chi-square test (p = 0.0000) indicates a strong association between gender and heart disease using the 5% significance.

2. Stroke Risk (Stroke and/or Hypertension) is Significantly Associatied with Heart Disease 
    - Individuals with stoke risk (had a stroke and/or have hypertension) are more likely to have experienced heart disease.  
    - A Chi-square test (p = 0.000) confirms a significant relationship between stroke risk and heart disease using the 5% significance.  

3. Work Type is Associatied with Heart Disease 
    - Individuals with specific work types are at higher risk to have experienced heart disease.  
    - A Chi-square test (p = 0.0019) confirms a relationship between Smoking Status and heart disease using the 5% significance. 

4. Smoking Status is Associatied with Heart Disease 
    - Individuals who formerly or currently smoke are at higher risk to have experienced heart disease.  
    - A Chi-square test (p = 0.0065) confirms a relationship between Smoking Status and heart disease using the 5% significance.  

5. No Significant Association Between Heart Disease and Other Categorical Variables  
    - The Chi-square test results indicate no statistically significant relationship between heart disease and:  
        - Marital status (p = 0.5902)
        - Residence type (p = 1.0)  

6. Age and Glucose Levels Are Significant Predictors
   - Stroke patients tend to be older and have higher average glucose levels.
   - A Mann-Whitney U test indicates that age and glucose levels differ significantly between heart disease and without heart disease groups.

# Discussion & Interpretation

Insights on which groups are most at risk: To be determined (work in
progress)

### Biases and Limitations of Predictive Data  

#### Sampling Bias  
The dataset comes from a confidential source and is intended only for educational purposes. Since the data collection methods are unknown, we cannot verify whether the dataset was randomly sampled from a diverse and representative population. If the sample is biased or not reflective of the general public, the results may not generalize beyond this dataset.  

Additionally, the team made a decision to removed children from the data, meaning the findings apply only to adults. 

#### Correlation vs. Causation  
A key limitation of this dataset is the risk of misinterpreting correlation as causation. While the analysis may reveal associations between variables, it does not prove that one factor directly causes another.  

For example, the dataset might show a correlation between high glucose levels and stroke risk, but this does not necessarily mean that high glucose levels cause strokes. Other factors, such as diabetes, lifestyle choices, or genetic predisposition, could be influencing both variables.  

#### Feature Selection Bias  
The dataset does not include certain critical stroke and heart disease risk factors such as:  

- Genetics  
- Dietary habits  
- Medication use  
- Environmental factors  

These missing variables could significantly impact disease risk, meaning the analysis might be incomplete or misleading. Hidden confounding factors may drive risk in ways that this dataset does not capture, potentially leading to biased conclusions.  

By recognizing these biases and limitations, we can interpret the findings with caution and acknowledge the need for more comprehensive studies to fully understand risk factors.


