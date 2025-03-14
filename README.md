# Predicting Stroke, Hypertension, and Heart Disease: Identifying Key Risk Factors
Data Science Institute - Cohort 5 - Team 1 Project

## Members
* Marta Zaiats ([mprezlyata](https://github.com/mprezlyata))
* Ranveer Kaur ([ranvikhalar](https://github.com/ranvikhalar))
* Vikram Katju ([vikramkatju](https://github.com/vikramkatju))
* Poulami Dey ([poulami249](https://github.com/poulami249))
* Lauren Mulders ([Mulders95](https://github.com/Mulders95))

## Business Case Question
Regression: What relevant predictors predict the occurence of stroke, hypertension and heart disease?

## Buisness Case

## Project Overview
This project aims to identify the key predictors that contribute to the occurrence of stroke, hypertension, and heart disease by leveraging data science techniques, particularly data visualization and machine learning models. Using this knowledge, our goal is to develop a predictive model that can predict whether a patient is likely to get stroke, hyper tension, and heart disease based on the input parameters like gender, age, avg_glucose_level, bmi, ever_married, smoking status etc., which could assist healthcare providers in identifying individuals at high risk and implementing preventive measures effectively.

### Requirements

This project uses the following Python libraries:

| **Library**          | **Use**                                    |
|----------------------|--------------------------------------------|
| `pandas`             | Data manipulation and analysis             |
| `numpy`              | Numerical computations                     |
| `seaborn`            | Statistical data visualization             |
| `plotly`             | Interactive visualizations                 |
| `scikit-learn`       | Machine learning models and evaluation     |
| `imbalanced-learn`   | Handling imbalanced datasets (e.g., SMOTE) |

## Data Overview
| **Column Name**        | **Description**                                                                                                               | **Datatype**   |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------|----------------|
| `id`                   | A unique identifier of each record.                                                                                           | `int64`        |
| `gender`               | The gender of the patient ("Male", "Female" or "Other").                                                                      | `object`       |
| `age`                  | The age of the patient.                                                                                                       | `float64`      |
| `hypertension`         | A binary indicator (0 or 1) representing whether the patient has hypertension.                                                | `int64`        |
| `heart_disease`        | A binary indicator (0 or 1) representing whether the patient has heart disease.                                               | `int64`        |
| `ever_married`         | The patient has ever been married (Yes or No).                                                                                | `object`       |
| `work_type`            | The type of work the patient is involved in ('Private', 'Self-employed', 'Govt_job', 'children', 'Never_worked').             | `object`       |
| `Residence_type`       | The type of residence (Urban or Rural).                                                                                       | `object`       |
| `avg_glucose_level`    | The average glucose level of the patient.                                                                                     | `float64`      |
| `bmi`                  | The Body Mass Index of the patient.                                                                                           | `float64`      |
| `stroke`               | A binary indicator (0 or 1) representing whether the patient has experienced a stroke.                                        | `int64`        |
| `smoking_status`       | The smoking status of the patient ('formerly smoked', 'never smoked', 'smokes', 'Unknown').                                   | `object`       |

## Data Cleaning and Handling Missing Values


## Exploratory Data Analysis



## Key Findings & Predictive Power of Features
For Stroke Prediction: Top influencing factors (e.g., age, hypertension, heart disease).
For Hypertension Prediction: Impact of bmi, smoking, and work type.
For Heart Disease Prediction: Role of age, hypertension, and glucose levels.

## Discussion & Interpretation
Insights on which groups are most at risk.
Potential bias or limitations in data.