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
#str(df_stroke)
df_stroke <- df_stroke %>%
  mutate(heart_risk = as.integer(hypertension | heart_disease))
#str(df_stroke)


df_stroke <- df_stroke %>% select(stroke, age, avg_glucose_level, heart_risk )
#str(df_stroke)

df_stroke <- df_stroke %>%
  mutate(across(c(stroke, heart_risk), as.factor))
#str(df_stroke)
#head(df_stroke)

df_stroke <- df_stroke %>%
  mutate(
    stroke = recode(stroke, `0` = "no stroke", `1` = "stroke")
  )

df_stroke <- df_stroke %>%
  mutate(
    heart_risk = recode(heart_risk, `0` = "no heart risk", `1` = "heart risk")
  )
#str(df_stroke)

#head(df_stroke)


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
  facet_wrap(~ stroke) +
  labs(
    x = "Age",
    y = "Average glucose level",
    color = "heart risk"
  ) +
  palette +
  labs (caption = "Scatterplot of Average glucose level by Age facetted by stroke status and color coded by heart risk.\n(heart risk implies the risk of stroke given either heart disease or hypertension)") +
  theme(plot.caption = element_text(hjust = 0.5))
```

![](Vikram-DSI-Project-plots_files/figure-gfm/unnamed-chunk-2-2.png)<!-- -->

### Heart disease plots

``` r
df_heart_disease <- read.csv("heart_disease_full.csv", header = TRUE, 
                      stringsAsFactors = TRUE)

#str(df_heart_disease)
df_heart_disease <- df_heart_disease %>%
  mutate(stroke_risk = as.integer(hypertension | stroke))
#str(df_heart_disease)


df_heart_disease <- df_heart_disease %>% select(heart_disease, age, 
                                        avg_glucose_level, stroke_risk,
                                        gender, work_type, smoking_status)
#str(df_heart_disease)

df_heart_disease <- df_heart_disease %>%
  mutate(across(c(heart_disease, stroke_risk, gender, 
                  work_type, smoking_status), as.factor))
#str(df_heart_disease)
#head(df_heart_disease)

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
#str(df_heart_disease)
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
#str(df_heart_disease)


#risk in stroke risk means risk of heart disease (due to stroke)

#head(df_heart_disease)

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
  palette +
  labs (caption = "Scatterplot of Average glucose level by Age facetted by work type and heart disease,  color coded by gender and shaped by stroke risk.\n(Stroke risk implies the risk of heart disease given either stroke or hypertension)") +
  theme(plot.caption = element_text(hjust = 0.5)) 
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
  palette +
  labs (caption = "Scatterplot of Average glucose level by Age facetted by smoking status and heart disease,\ncolor coded by gender and shaped by stroke risk.\n(Stroke risk implies the risk of heart disease given either stroke or hypertension)") +
  theme(plot.caption = element_text(hjust = 0.0)) 
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
  palette +
  labs (caption = "Scatterplot of Average glucose level by Age facetted by smoking status and heart disease,\ncolor coded by work type and shaped by stroke risk.\n(Stroke risk implies the risk of heart disease given either stroke or hypertension)") +
  theme(plot.caption = element_text(hjust = 0.0)) 
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
  palette +
  labs (caption = "Scatterplot of Average glucose level by Age facetted by heart disease and smoking status,\ncolor coded by heart risk and shaped by work type") +
  theme(plot.caption = element_text(hjust = 0.5))
```

![](Vikram-DSI-Project-plots_files/figure-gfm/unnamed-chunk-3-11.png)<!-- -->
