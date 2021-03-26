# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 5: COVID-19's Impact on the U.S. Prison System

by Marta Ghiglioni, Sheena Cook, and Edward Mendoza 

### Executive Summary

On January 2020, the United States first reported its first case of C0VID-19 in the state of Washington. Little was known about this novel coronavirus, but as time progressed, we have seen cases increase sporadically, death growing at an unbelievable rate, and life as we know it has drastically changed the way we interact with our fellow citizens. 

In this Executive Summary, we will take a deep dive into one segment of the population that is often times overlook in the discusson of COVID-19 -- prisoners of the United States. Regardless of one's beliefs about prisoners (whether justice was served fairly or not), we will take a look at the impact it has taken on the prison system as a whole. 

Furthermore, we wanted to gain meaningful insights from prisoners and staff members affected by COVID-19, and suggest recommendations to the Federal Bureau of Prisons to decrease the rate of COVID-19 cases

The analysis we used involved several models which will be discussed further within this summary, where the best models produced an accuracy score ranging between 75% and 80%

---

### Data Sources
Data were pulled from the following sites:
- [Marshall Project](https://www.themarshallproject.org/2020/05/01/a-state-by-state-look-at-coronavirus-in-prisons)
- [John Hopkins University and Medicine](https://coronavirus.jhu.edu/us-map)
- [Bureau of Justice](www.bjs.gov)

---

### Notebook Index

- [01 | Data Cleaning](https://git.generalassemb.ly/edwardmendoza89/Project_5_shared/blob/master/Marta/01_Data_Cleaning.ipynb)
- [02 | Feature Data](https://git.generalassemb.ly/edwardmendoza89/Project_5_shared/blob/master/Marta/02_Feature_Data.ipynb)
- [03 | EDA Visualization](https://git.generalassemb.ly/edwardmendoza89/Project_5_shared/blob/master/Edward/Revised%20EDA%20for%20Covid-19%20Prison-Civilian%20Data.ipynb)
- [04 | Model Prisoners COVID](https://git.generalassemb.ly/edwardmendoza89/Project_5_shared/blob/master/Sheena/Final/04.1%20Modeling_prisoners_w_deaths.ipynb)
- [05 | Model Staff COVID](https://git.generalassemb.ly/edwardmendoza89/Project_5_shared/blob/master/Sheena/Final/05.1%20Modeling_staff_w_deaths.ipynb)
- [06 | Model Prisoners - FacilityFeatures](https://git.generalassemb.ly/edwardmendoza89/Project_5_shared/blob/master/Marta/06_Model_Prisoners_FacilityFeatures.ipynb)
- [07 | Model Staff - FacilityFeatures](https://git.generalassemb.ly/edwardmendoza89/Project_5_shared/blob/master/Marta/07_Model_Staff_FacilityFeatures.ipynb)

---

### EDA and Cleaning

We performed basic exploratory data analysis and consequential data cleaning. More importantly, we either dropped imputed null values, generated monthly COVID-19 cases per state (since data was produced per date, we wanted to ensure that we were pulling the unique cases rather than a cumulative figure in our data that might skew the results), and combined Facility Features with Covid-19 data related to prisoners and staff members. 

We also generated a "State Heat Map" that visualized the number of prisoner/covid-19 cases per capita to accurately display the rate of prisoner cases by the prisoner population. The result is shown below:

![covid-19](https://git.generalassemb.ly/edwardmendoza89/Project_5_shared/blob/master/Edward/images/covid_19_heatmap.png)

---

### Models

#### Modeling Features

For the COVID-19 model, the features that were passed in the model were the following: 
- cases per month
- cases per state
- Data related to staff, prisoners, and civilians, measuring cases, tests, and deaths

For the COVID-19 model with Feature Engineering, the features that were passed in the model were the following: 
- Every feature that was aforementioned above as well as:
  - Design Capacity
  - Prison Work Programs

#### Testing

We customized our train-test-split into chronological order by date.
This change allowed our model to predict the number of cases for the following month

#### Modeling Prisoner COVID-19 Cases Based on COVID-19 Data

|Model|Train Score|Test Score|
| --- | --- | --- |
|Ridge| .713 | .786 |
|Lasso| .834 | .758 | 
|Linear Regression| .841 | .647 | 
|Random Forest| .932 | .656 | 
|Bagged Decision Tree| .927 | .783 |
|KNN| .555 | .561 | 

#### Modeling Staff COVID-19 Cases Based on COVID-19 Data

|Model|Train Score|Test Score|
| --- | --- | --- |
|Random Forest GridSearch| .747 | .792 |
|Ridge| .835 | .786 |
|Lasso| .95 | .715 | 
|Random Forest| .945 | .869 | 
|Bagged Decision Tree| .938 | .820 |
|KNN| .629 | .662 | 

#### Modeling Prisoner COVID-19 Cases with Facility Features

|Model|Train Score|Test Score|
| --- | --- | --- |
|Random Forest| .718 | .759 |
|Lasso| .761 | .698 | 
|Ridge| .635 | .751 | 
|Bagged Decision Tree| .821 | .68 | 
|KNN| .559 | .517 | 

#### Modeling Staff COVID-19 Cases with Facility Features

|Model|Train Score|Test Score|
| --- | --- | --- |
|Random Forest| .779 | .80 |
|Lasso| .95 | .704 | 
|Ridge| .947 | .772 | 
|Bagged Decision Tree| .772 | .747 | 
|KNN| .633 | .635 | 

These results show that we had to test a variety of models to ensure that our ideal model would generalize well on data that it hasn't seen, thus ensuring the model wouldn't be deemed as overfit. 

---

### Conclusion

#### Is there a correlation between number of COVID-19 cases among civilians and inmates? 

Our results point that civilian cases are good predictors for inmate cases; however, staff predictions are better. The reason for this phenomenon is that they can be classified as potential vectors to carrying this disease, since they can possibly contract the virus amongst fellow staff workers, family members as well as certain retail businesses such as grocery stores. Furthermore, with the advent of cases where people can be asymptomatic -- that is, that they display no common symptoms of having COVID-19 -- the possibility of outbreaks within prisons can be inevitable at best. 

#### Can prison features predict the number of cases of COVID-19 among inmates and staff?

Based on our models, they can improve model predictions of about 10%

---

### Further Analysis

#### To improve our analysis, we would:
- Include analysis of intersectionality amongst the prison population (protected classes such as age, race, gender identity, etc)
- Train a time series model to better explain the infection rates
- Research and request update data on facilities 


