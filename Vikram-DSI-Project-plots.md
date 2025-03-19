Vikram DSI Project Plots
================
Vikram Katju
2025-03-19

``` r
library(tidyverse)
```

### Stroke Plots

``` r
df_stroke <- read.csv("stroke_full.csv", header = TRUE, 
                      stringsAsFactors = TRUE)
str(df_stroke)
```

    ## 'data.frame':    3413 obs. of  18 variables:
    ##  $ gender                : Factor w/ 2 levels "Female","Male": 2 1 2 1 1 2 2 1 1 1 ...
    ##  $ age                   : num  67 61 80 49 79 81 74 69 59 78 ...
    ##  $ hypertension          : int  0 0 0 0 1 0 1 0 0 0 ...
    ##  $ heart_disease         : int  1 0 1 0 0 0 1 0 0 0 ...
    ##  $ ever_married          : Factor w/ 2 levels "No","Yes": 2 2 2 2 2 2 2 1 2 2 ...
    ##  $ work_type             : Factor w/ 3 levels "Govt_job","Private",..: 2 3 2 2 3 2 2 2 2 2 ...
    ##  $ Residence_type        : Factor w/ 2 levels "Rural","Urban": 2 1 1 2 1 2 1 2 1 2 ...
    ##  $ avg_glucose_level     : num  229 202 106 171 174 ...
    ##  $ bmi                   : num  36.6 28.8 32.5 34.4 24 29 27.4 22.8 28.2 24.2 ...
    ##  $ smoking_status        : Factor w/ 4 levels "formerly smoked",..: 1 2 2 3 2 1 2 2 4 4 ...
    ##  $ stroke                : int  1 1 1 1 1 1 1 1 1 1 ...
    ##  $ gender_encoded        : int  1 0 1 0 0 1 1 0 0 0 ...
    ##  $ ever_married_encoded  : int  1 1 1 1 1 1 1 0 1 1 ...
    ##  $ work_type_encoded     : int  2 3 2 2 3 2 2 2 2 2 ...
    ##  $ Residence_type_encoded: int  1 0 0 1 0 1 0 1 0 1 ...
    ##  $ smoking_status_encoded: int  1 2 2 3 2 1 2 2 0 0 ...
    ##  $ Age_temp              : int  1 1 1 0 1 1 1 1 1 1 ...
    ##  $ avg_glucose_level_temp: int  2 2 2 2 2 2 1 2 1 1 ...

``` r
df_stroke <- df_stroke %>%
  mutate(heart_risk = as.integer(hypertension | heart_disease))
str(df_stroke)
```

    ## 'data.frame':    3413 obs. of  19 variables:
    ##  $ gender                : Factor w/ 2 levels "Female","Male": 2 1 2 1 1 2 2 1 1 1 ...
    ##  $ age                   : num  67 61 80 49 79 81 74 69 59 78 ...
    ##  $ hypertension          : int  0 0 0 0 1 0 1 0 0 0 ...
    ##  $ heart_disease         : int  1 0 1 0 0 0 1 0 0 0 ...
    ##  $ ever_married          : Factor w/ 2 levels "No","Yes": 2 2 2 2 2 2 2 1 2 2 ...
    ##  $ work_type             : Factor w/ 3 levels "Govt_job","Private",..: 2 3 2 2 3 2 2 2 2 2 ...
    ##  $ Residence_type        : Factor w/ 2 levels "Rural","Urban": 2 1 1 2 1 2 1 2 1 2 ...
    ##  $ avg_glucose_level     : num  229 202 106 171 174 ...
    ##  $ bmi                   : num  36.6 28.8 32.5 34.4 24 29 27.4 22.8 28.2 24.2 ...
    ##  $ smoking_status        : Factor w/ 4 levels "formerly smoked",..: 1 2 2 3 2 1 2 2 4 4 ...
    ##  $ stroke                : int  1 1 1 1 1 1 1 1 1 1 ...
    ##  $ gender_encoded        : int  1 0 1 0 0 1 1 0 0 0 ...
    ##  $ ever_married_encoded  : int  1 1 1 1 1 1 1 0 1 1 ...
    ##  $ work_type_encoded     : int  2 3 2 2 3 2 2 2 2 2 ...
    ##  $ Residence_type_encoded: int  1 0 0 1 0 1 0 1 0 1 ...
    ##  $ smoking_status_encoded: int  1 2 2 3 2 1 2 2 0 0 ...
    ##  $ Age_temp              : int  1 1 1 0 1 1 1 1 1 1 ...
    ##  $ avg_glucose_level_temp: int  2 2 2 2 2 2 1 2 1 1 ...
    ##  $ heart_risk            : int  1 0 1 0 1 0 1 0 0 0 ...

``` r
df_stroke <- df_stroke %>% select(stroke, age, avg_glucose_level, heart_risk )
str(df_stroke)
```

    ## 'data.frame':    3413 obs. of  4 variables:
    ##  $ stroke           : int  1 1 1 1 1 1 1 1 1 1 ...
    ##  $ age              : num  67 61 80 49 79 81 74 69 59 78 ...
    ##  $ avg_glucose_level: num  229 202 106 171 174 ...
    ##  $ heart_risk       : int  1 0 1 0 1 0 1 0 0 0 ...

``` r
df_stroke <- df_stroke %>%
  mutate(across(c(stroke, heart_risk), as.factor))
str(df_stroke)
```

    ## 'data.frame':    3413 obs. of  4 variables:
    ##  $ stroke           : Factor w/ 2 levels "0","1": 2 2 2 2 2 2 2 2 2 2 ...
    ##  $ age              : num  67 61 80 49 79 81 74 69 59 78 ...
    ##  $ avg_glucose_level: num  229 202 106 171 174 ...
    ##  $ heart_risk       : Factor w/ 2 levels "0","1": 2 1 2 1 2 1 2 1 1 1 ...

``` r
head(df_stroke)
```

    ##   stroke age avg_glucose_level heart_risk
    ## 1      1  67            228.69          1
    ## 2      1  61            202.21          0
    ## 3      1  80            105.92          1
    ## 4      1  49            171.23          0
    ## 5      1  79            174.12          1
    ## 6      1  81            186.21          0

``` r
df_stroke <- df_stroke %>%
  mutate(
    stroke = recode(stroke, `0` = "no stroke", `1` = "stroke")
  )

df_stroke <- df_stroke %>%
  mutate(
    heart_risk = recode(heart_risk, `0` = "no heart risk", `1` = "heart risk")
  )
str(df_stroke)
```

    ## 'data.frame':    3413 obs. of  4 variables:
    ##  $ stroke           : Factor w/ 2 levels "no stroke","stroke": 2 2 2 2 2 2 2 2 2 2 ...
    ##  $ age              : num  67 61 80 49 79 81 74 69 59 78 ...
    ##  $ avg_glucose_level: num  229 202 106 171 174 ...
    ##  $ heart_risk       : Factor w/ 2 levels "no heart risk",..: 2 1 2 1 2 1 2 1 1 1 ...

``` r
head(df_stroke)
```

    ##   stroke age avg_glucose_level    heart_risk
    ## 1 stroke  67            228.69    heart risk
    ## 2 stroke  61            202.21 no heart risk
    ## 3 stroke  80            105.92    heart risk
    ## 4 stroke  49            171.23 no heart risk
    ## 5 stroke  79            174.12    heart risk
    ## 6 stroke  81            186.21 no heart risk

``` r
################
#####Stroke plots:
################
palette <- scale_color_brewer(palette = "Dark2")

#3 variables in a plot: Average Glucose level, Age, and stroke(Stroke status)
ggplot(df_stroke, aes(x = age, y = avg_glucose_level, color = stroke)) +
  geom_point() +
  facet_wrap(~ stroke) +
  labs(
    x = "Age",
    y = "Average Glucose Level",
    color = "Stroke status"
  ) +
  palette
```

![](Vikram-DSI-Project-plots_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

``` r
#4 variables in a plot: Average Glucose level, Age, stroke(Stroke status),
# and heart_risk (heart risk status)
ggplot(df_stroke, aes(x = age, y = avg_glucose_level, color = heart_risk)) +
  geom_point() +
  facet_grid(heart_risk ~ stroke) +
  labs(
    x = "Age",
    y = "Average Glucose Level",
    color = "heart risk"
  ) +
  palette
```

![](Vikram-DSI-Project-plots_files/figure-gfm/unnamed-chunk-2-2.png)<!-- -->

### Heart disease plots

``` r
df_heart_disease <- read.csv("heart_disease_full.csv", header = TRUE, 
                      stringsAsFactors = TRUE)

str(df_heart_disease)
```

    ## 'data.frame':    3604 obs. of  18 variables:
    ##  $ gender                : Factor w/ 2 levels "Female","Male": 2 1 2 1 1 2 2 1 1 1 ...
    ##  $ age                   : num  67 61 80 49 79 81 74 69 59 78 ...
    ##  $ hypertension          : int  0 0 0 0 1 0 1 0 0 0 ...
    ##  $ heart_disease         : int  1 0 1 0 0 0 1 0 0 0 ...
    ##  $ ever_married          : Factor w/ 2 levels "No","Yes": 2 2 2 2 2 2 2 1 2 2 ...
    ##  $ work_type             : Factor w/ 3 levels "Govt_job","Private",..: 2 3 2 2 3 2 2 2 2 2 ...
    ##  $ Residence_type        : Factor w/ 2 levels "Rural","Urban": 2 1 1 2 1 2 1 2 1 2 ...
    ##  $ avg_glucose_level     : num  229 202 106 171 174 ...
    ##  $ bmi                   : num  36.6 28.8 32.5 34.4 24 ...
    ##  $ smoking_status        : Factor w/ 4 levels "formerly smoked",..: 1 2 2 3 2 1 2 2 4 4 ...
    ##  $ stroke                : int  1 1 1 1 1 1 1 1 1 1 ...
    ##  $ gender_encoded        : int  1 0 1 0 0 1 1 0 0 0 ...
    ##  $ ever_married_encoded  : int  1 1 1 1 1 1 1 0 1 1 ...
    ##  $ work_type_encoded     : int  2 3 2 2 3 2 2 2 2 2 ...
    ##  $ Residence_type_encoded: int  1 0 0 1 0 1 0 1 0 1 ...
    ##  $ smoking_status_encoded: int  1 2 2 3 2 1 2 2 0 0 ...
    ##  $ Age_temp              : int  1 1 1 0 1 1 1 1 1 1 ...
    ##  $ avg_glucose_level_temp: int  2 2 2 2 2 2 1 2 1 1 ...

``` r
df_heart_disease <- df_heart_disease %>%
  mutate(stroke_risk = as.integer(hypertension | stroke))
str(df_heart_disease)
```

    ## 'data.frame':    3604 obs. of  19 variables:
    ##  $ gender                : Factor w/ 2 levels "Female","Male": 2 1 2 1 1 2 2 1 1 1 ...
    ##  $ age                   : num  67 61 80 49 79 81 74 69 59 78 ...
    ##  $ hypertension          : int  0 0 0 0 1 0 1 0 0 0 ...
    ##  $ heart_disease         : int  1 0 1 0 0 0 1 0 0 0 ...
    ##  $ ever_married          : Factor w/ 2 levels "No","Yes": 2 2 2 2 2 2 2 1 2 2 ...
    ##  $ work_type             : Factor w/ 3 levels "Govt_job","Private",..: 2 3 2 2 3 2 2 2 2 2 ...
    ##  $ Residence_type        : Factor w/ 2 levels "Rural","Urban": 2 1 1 2 1 2 1 2 1 2 ...
    ##  $ avg_glucose_level     : num  229 202 106 171 174 ...
    ##  $ bmi                   : num  36.6 28.8 32.5 34.4 24 ...
    ##  $ smoking_status        : Factor w/ 4 levels "formerly smoked",..: 1 2 2 3 2 1 2 2 4 4 ...
    ##  $ stroke                : int  1 1 1 1 1 1 1 1 1 1 ...
    ##  $ gender_encoded        : int  1 0 1 0 0 1 1 0 0 0 ...
    ##  $ ever_married_encoded  : int  1 1 1 1 1 1 1 0 1 1 ...
    ##  $ work_type_encoded     : int  2 3 2 2 3 2 2 2 2 2 ...
    ##  $ Residence_type_encoded: int  1 0 0 1 0 1 0 1 0 1 ...
    ##  $ smoking_status_encoded: int  1 2 2 3 2 1 2 2 0 0 ...
    ##  $ Age_temp              : int  1 1 1 0 1 1 1 1 1 1 ...
    ##  $ avg_glucose_level_temp: int  2 2 2 2 2 2 1 2 1 1 ...
    ##  $ stroke_risk           : int  1 1 1 1 1 1 1 1 1 1 ...

``` r
df_heart_disease <- df_heart_disease %>% select(heart_disease, age, 
                                        avg_glucose_level, stroke_risk,
                                        gender, work_type, smoking_status)
str(df_heart_disease)
```

    ## 'data.frame':    3604 obs. of  7 variables:
    ##  $ heart_disease    : int  1 0 1 0 0 0 1 0 0 0 ...
    ##  $ age              : num  67 61 80 49 79 81 74 69 59 78 ...
    ##  $ avg_glucose_level: num  229 202 106 171 174 ...
    ##  $ stroke_risk      : int  1 1 1 1 1 1 1 1 1 1 ...
    ##  $ gender           : Factor w/ 2 levels "Female","Male": 2 1 2 1 1 2 2 1 1 1 ...
    ##  $ work_type        : Factor w/ 3 levels "Govt_job","Private",..: 2 3 2 2 3 2 2 2 2 2 ...
    ##  $ smoking_status   : Factor w/ 4 levels "formerly smoked",..: 1 2 2 3 2 1 2 2 4 4 ...

``` r
df_heart_disease <- df_heart_disease %>%
  mutate(across(c(heart_disease, stroke_risk, gender, 
                  work_type, smoking_status), as.factor))
str(df_heart_disease)
```

    ## 'data.frame':    3604 obs. of  7 variables:
    ##  $ heart_disease    : Factor w/ 2 levels "0","1": 2 1 2 1 1 1 2 1 1 1 ...
    ##  $ age              : num  67 61 80 49 79 81 74 69 59 78 ...
    ##  $ avg_glucose_level: num  229 202 106 171 174 ...
    ##  $ stroke_risk      : Factor w/ 2 levels "0","1": 2 2 2 2 2 2 2 2 2 2 ...
    ##  $ gender           : Factor w/ 2 levels "Female","Male": 2 1 2 1 1 2 2 1 1 1 ...
    ##  $ work_type        : Factor w/ 3 levels "Govt_job","Private",..: 2 3 2 2 3 2 2 2 2 2 ...
    ##  $ smoking_status   : Factor w/ 4 levels "formerly smoked",..: 1 2 2 3 2 1 2 2 4 4 ...

``` r
head(df_heart_disease)
```

    ##   heart_disease age avg_glucose_level stroke_risk gender     work_type
    ## 1             1  67            228.69           1   Male       Private
    ## 2             0  61            202.21           1 Female Self-employed
    ## 3             1  80            105.92           1   Male       Private
    ## 4             0  49            171.23           1 Female       Private
    ## 5             0  79            174.12           1 Female Self-employed
    ## 6             0  81            186.21           1   Male       Private
    ##    smoking_status
    ## 1 formerly smoked
    ## 2    never smoked
    ## 3    never smoked
    ## 4          smokes
    ## 5    never smoked
    ## 6 formerly smoked

``` r
df_heart_disease <- df_heart_disease %>%
  mutate(
    heart_disease = recode(heart_disease, `0` = "no heart disease", 
                           `1` = "heart disease")
  )

df_heart_disease <- df_heart_disease %>%
  mutate(
    stroke_risk = recode(stroke_risk, `0` = "no stroke risk", 
                         `1` = "stroke risk")
  )
str(df_heart_disease)
```

    ## 'data.frame':    3604 obs. of  7 variables:
    ##  $ heart_disease    : Factor w/ 2 levels "no heart disease",..: 2 1 2 1 1 1 2 1 1 1 ...
    ##  $ age              : num  67 61 80 49 79 81 74 69 59 78 ...
    ##  $ avg_glucose_level: num  229 202 106 171 174 ...
    ##  $ stroke_risk      : Factor w/ 2 levels "no stroke risk",..: 2 2 2 2 2 2 2 2 2 2 ...
    ##  $ gender           : Factor w/ 2 levels "Female","Male": 2 1 2 1 1 2 2 1 1 1 ...
    ##  $ work_type        : Factor w/ 3 levels "Govt_job","Private",..: 2 3 2 2 3 2 2 2 2 2 ...
    ##  $ smoking_status   : Factor w/ 4 levels "formerly smoked",..: 1 2 2 3 2 1 2 2 4 4 ...

``` r
levels(df_heart_disease$heart_disease)
```

    ## [1] "no heart disease" "heart disease"

``` r
levels(df_heart_disease$stroke_risk)
```

    ## [1] "no stroke risk" "stroke risk"

``` r
levels(df_heart_disease$gender)
```

    ## [1] "Female" "Male"

``` r
levels(df_heart_disease$work_type)
```

    ## [1] "Govt_job"      "Private"       "Self-employed"

``` r
levels(df_heart_disease$smoking_status)
```

    ## [1] "formerly smoked" "never smoked"    "smokes"          "Unknown"

``` r
df_heart_disease <- df_heart_disease %>%
  mutate(
    work_type = recode(work_type, 'Govt_job' = 'Govt job', 
                         'Private' = 'Private', 
                       'Self-employed' = 'Self-employed')
  )
levels(df_heart_disease$work_type)
```

    ## [1] "Govt job"      "Private"       "Self-employed"

``` r
str(df_heart_disease)
```

    ## 'data.frame':    3604 obs. of  7 variables:
    ##  $ heart_disease    : Factor w/ 2 levels "no heart disease",..: 2 1 2 1 1 1 2 1 1 1 ...
    ##  $ age              : num  67 61 80 49 79 81 74 69 59 78 ...
    ##  $ avg_glucose_level: num  229 202 106 171 174 ...
    ##  $ stroke_risk      : Factor w/ 2 levels "no stroke risk",..: 2 2 2 2 2 2 2 2 2 2 ...
    ##  $ gender           : Factor w/ 2 levels "Female","Male": 2 1 2 1 1 2 2 1 1 1 ...
    ##  $ work_type        : Factor w/ 3 levels "Govt job","Private",..: 2 3 2 2 3 2 2 2 2 2 ...
    ##  $ smoking_status   : Factor w/ 4 levels "formerly smoked",..: 1 2 2 3 2 1 2 2 4 4 ...

``` r
#risk in stroke risk means risk of heart disease (due to stroke)

head(df_heart_disease)
```

    ##      heart_disease age avg_glucose_level stroke_risk gender     work_type
    ## 1    heart disease  67            228.69 stroke risk   Male       Private
    ## 2 no heart disease  61            202.21 stroke risk Female Self-employed
    ## 3    heart disease  80            105.92 stroke risk   Male       Private
    ## 4 no heart disease  49            171.23 stroke risk Female       Private
    ## 5 no heart disease  79            174.12 stroke risk Female Self-employed
    ## 6 no heart disease  81            186.21 stroke risk   Male       Private
    ##    smoking_status
    ## 1 formerly smoked
    ## 2    never smoked
    ## 3    never smoked
    ## 4          smokes
    ## 5    never smoked
    ## 6 formerly smoked

``` r
palette <- scale_color_brewer(palette = "Dark2")

#Three variables in a plot:age, avg_glucose_level, and heart_disease
ggplot(df_heart_disease, aes(x = age, y = avg_glucose_level, color = 
                               heart_disease)) +
  geom_point() +
  facet_wrap(~ heart_disease) +
  labs(
    x = "Age",
    y = "Average Glucose Level",
    color = "Heart disease status"
  ) +
  palette
```

![](Vikram-DSI-Project-plots_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

``` r
#Four variables in a plot:age, avg_glucose_level,heart_disease, and gender
ggplot(df_heart_disease, aes(x = age, y = avg_glucose_level, 
                             color = heart_disease)) +
  geom_point() +
  facet_grid(gender ~ heart_disease) +
  labs(
    x = "Age",
    y = "Average Glucose Level",
    color = "Heart disease status"
  ) +
  palette
```

![](Vikram-DSI-Project-plots_files/figure-gfm/unnamed-chunk-3-2.png)<!-- -->

``` r
##Four variables in a plot:age, avg_glucose_level,heart_disease, and work_type
ggplot(df_heart_disease, aes(x = age, y = avg_glucose_level, 
                             color = heart_disease)) +
  geom_point() +
  facet_grid(work_type~heart_disease) +
  labs(
    x = "Age",
    y = "Average Glucose Level",
    color = "Heart disease status"
  ) +
  palette
```

![](Vikram-DSI-Project-plots_files/figure-gfm/unnamed-chunk-3-3.png)<!-- -->

``` r
###Four variables in a plot:age, avg_glucose_level,heart_disease, and
###                         smoking_status
ggplot(df_heart_disease, aes(x = age, y = avg_glucose_level, 
                             color = heart_disease)) +
  geom_point() +
  facet_grid(smoking_status~heart_disease) +
  labs(
    x = "Age",
    y = "Average Glucose Level",
    color = "Heart disease status"
  ) +
  palette
```

![](Vikram-DSI-Project-plots_files/figure-gfm/unnamed-chunk-3-4.png)<!-- -->

``` r
#-----------------------
#Five variables in a plot: Age, avg_glucose_level, heart_disease,
#                          smoking status, and Gender
ggplot(df_heart_disease, aes(x = age, y = avg_glucose_level, 
                             color = gender)) +
  geom_point() +
  facet_grid(smoking_status~heart_disease) +
  labs(
    x = "Age",
    y = "Average Glucose Level",
    color = "Gender"
  ) +
  palette
```

![](Vikram-DSI-Project-plots_files/figure-gfm/unnamed-chunk-3-5.png)<!-- -->

``` r
#Five variables in a plot: Age, avg_glucose_level, heart_disease,
#                          smoking status, and Gender
ggplot(df_heart_disease, aes(x = age, y = avg_glucose_level, 
                             color = gender)) +
  geom_point() +
  facet_grid(work_type~heart_disease) +
  labs(
    x = "Age",
    y = "Average Glucose Level",
    color = "Gender"
  ) +
  palette
```

![](Vikram-DSI-Project-plots_files/figure-gfm/unnamed-chunk-3-6.png)<!-- -->

``` r
#Five variables in a plot: Age, avg_glucose_level, heart_disease,
#                          work_type, and stroke_risk
ggplot(df_heart_disease, aes(x = age, y = avg_glucose_level, 
                             color = stroke_risk)) +
  geom_point() +
  facet_grid(work_type~heart_disease) +
  labs(
    x = "Age",
    y = "Average Glucose Level",
    color = "Stroke risk status"
  ) +
  palette
```

![](Vikram-DSI-Project-plots_files/figure-gfm/unnamed-chunk-3-7.png)<!-- -->

``` r
#--------

#Note that Age is fixed on x axis, avg_glucose_level is fixed on y axis and
#heart_disease is doing the column-wise faceting and is also fixed. We can
#therefore only have four possible plots with six variables in a plot from
#all the variables under consideration which are:
#Numerical variables: age and avg_glucose_level (2)
#Nominal variables: gender, stroke risk, heart disease, work_type, 
#                   smoking_status (5)

#We can obtain the four plots by dropping one at a time smoking_status,
#work_type, stroke_risk, and gender

#Six variables in a plot:Age, avg_glucose_level, heart_disease, gender,
#                         work_type, stroke_risk (dropping smoking status)

ggplot(df_heart_disease, aes(x = age, y = avg_glucose_level, 
                             color = gender, shape = stroke_risk)) +
  geom_point() +
  facet_grid(work_type~heart_disease) +
  labs(
    x = "Age",
    y = "Average Glucose Level",
    color = "Gender",
    shape = "Stroke risk"
  ) +
  palette
```

![](Vikram-DSI-Project-plots_files/figure-gfm/unnamed-chunk-3-8.png)<!-- -->

``` r
#Six variables in a plot:Age, avg_glucose_level, heart_disease, gender,
#                         smoking_status, stroke_risk (dropping work type)

ggplot(df_heart_disease, aes(x = age, y = avg_glucose_level, 
                             color = gender, shape = stroke_risk)) +
  geom_point() +
  facet_grid(smoking_status~heart_disease) +
  labs(
    x = "Age",
    y = "Average Glucose Level",
    color = "Gender",
    shape = "Stroke risk"
  ) +
  palette
```

![](Vikram-DSI-Project-plots_files/figure-gfm/unnamed-chunk-3-9.png)<!-- -->

``` r
#Six variables in a plot:Age, avg_glucose_level, heart_disease, 
#                         smoking_status, stroke_risk (dropping gender)

ggplot(df_heart_disease, aes(x = age, y = avg_glucose_level, 
                             color = work_type, shape = stroke_risk)) +
  geom_point() +
  facet_grid(smoking_status~heart_disease) +
  labs(
    x = "Age",
    y = "Average Glucose Level",
    color = "Work type",
    shape = "Stroke risk"
  ) +
  palette
```

![](Vikram-DSI-Project-plots_files/figure-gfm/unnamed-chunk-3-10.png)<!-- -->

``` r
#Six variables in a plot:Age, avg_glucose_level, heart_disease, 
#                         smoking_status, gender (dropping stroke_risk)

ggplot(df_heart_disease, aes(x = age, y = avg_glucose_level, 
                             color = gender, shape = work_type)) +
  geom_point() +
  facet_grid(smoking_status~heart_disease) +
  labs(
    x = "Age",
    y = "Average Glucose Level",
    color = "Gender",
    shape = "Work type"
  ) +
  palette
```

![](Vikram-DSI-Project-plots_files/figure-gfm/unnamed-chunk-3-11.png)<!-- -->
