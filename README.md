# CUHK-STAT1013: Project Assignment - **Part 1** Dataset Analysis

## **Background**
Dataset from a 2019 survey of Starbucks customers.
### **Description**
The survey was divided into four broad areas:
- basic personal information of customers
- spending（time/money) at Starbucks
- rating of Starbucks indicators
- recommendation index

**Github:** [basic-dataset/Starbucks satisfactory survey.csv at master · prasertcbs/basic-dataset · GitHub](https://github.com/prasertcbs/basic-dataset/blob/master/Starbucks%20satisfactory%20survey.csv)



**Sample size:** 122

**Feature documentation:**   

| Feature    | Class | Shape | Dtype|
| ----------- | ----------- | --- |---|
|Sex | ClassLabel |  |object|
|Average spend (per visit) | Tensor | |object|


# **Hypothesis**
1. I want to investigate the difference in spending levels at Starbucks by gender because I am curious about whether customers' preferences for Starbucks products differed by gender.


2. *1.* I am comparing two groups of customers, male and female.
       (G1：Average consumption per visit for male; G2:Average consumption per visit for female)
       
      *2.* The response variable I have chosen is the average amout they spend per visit to Starbucks.
  
      *3.* Yes, because the average level of customer spending per visit can be counted, they all fall into the realm of consumption and can be compatible.


3. I would expect one group to consume at a higher level than the other, as there may be differences in tastes between the two gender groups and therefore in the amount of money consumed.


4. I found the data from the website (https://github.com/prasertcbs/basic-dataset), which is provided by my teacher.


5. I will give the same questionnaire to Starbucks consumers worldwide to greatly improve the accuracy of the statistics (according to **Central Limit Theorem**).

# Perpare your dataset

- Tell us what groups you want to compare in the dataset
  - **G1** (Average spend (per visit) | Sex = Male) vs. **G2** (Average spend (per visit)| Sex = Female)


```python
import pandas as pd
import seaborn as sns
```


```python
df=pd.read_csv('https://raw.githubusercontent.com/prasertcbs/basic-dataset/master/Starbucks%20satisfactory%20survey.csv')
df.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Timestamp</th>
      <th>1. Your Gender</th>
      <th>2. Your Age</th>
      <th>3. Are you currently....?</th>
      <th>4. What is your annual income?</th>
      <th>5. How often do you visit Starbucks?</th>
      <th>6. How do you usually enjoy Starbucks?</th>
      <th>7. How much time do you normally  spend during your visit?</th>
      <th>8. The nearest Starbucks's outlet to you is...?</th>
      <th>9. Do you have Starbucks membership card?</th>
      <th>...</th>
      <th>11. On average, how much would you spend at Starbucks per visit?</th>
      <th>12. How would you rate the quality of Starbucks compared to other brands (Coffee Bean, Old Town White Coffee..) to be:</th>
      <th>13. How would you rate the price range at Starbucks?</th>
      <th>14. How important are sales and promotions in your purchase decision?</th>
      <th>15. How would you rate the ambiance at Starbucks? (lighting, music, etc...)</th>
      <th>16. You rate the WiFi quality at Starbucks as..</th>
      <th>17. How would you rate the service at Starbucks? (Promptness, friendliness, etc..)</th>
      <th>18. How likely you will choose Starbucks for doing business meetings or hangout with friends?</th>
      <th>19. How do you come to hear of promotions at Starbucks? Check all that apply.</th>
      <th>20. Will you continue buying at Starbucks?</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2019/10/01 12:38:43 PM GMT+8</td>
      <td>Female</td>
      <td>From 20 to 29</td>
      <td>Student</td>
      <td>Less than RM25,000</td>
      <td>Rarely</td>
      <td>Dine in</td>
      <td>Between 30 minutes to 1 hour</td>
      <td>within 1km</td>
      <td>Yes</td>
      <td>...</td>
      <td>Less than RM20</td>
      <td>4</td>
      <td>3</td>
      <td>5</td>
      <td>5</td>
      <td>4</td>
      <td>4</td>
      <td>3</td>
      <td>Starbucks Website/Apps;Social Media;Emails;Dea...</td>
      <td>Yes</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2019/10/01 12:38:54 PM GMT+8</td>
      <td>Female</td>
      <td>From 20 to 29</td>
      <td>Student</td>
      <td>Less than RM25,000</td>
      <td>Rarely</td>
      <td>Take away</td>
      <td>Below 30 minutes</td>
      <td>1km - 3km</td>
      <td>Yes</td>
      <td>...</td>
      <td>Less than RM20</td>
      <td>4</td>
      <td>3</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>5</td>
      <td>2</td>
      <td>Social Media;In Store displays</td>
      <td>Yes</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2019/10/01 12:38:56 PM GMT+8</td>
      <td>Male</td>
      <td>From 20 to 29</td>
      <td>Employed</td>
      <td>Less than RM25,000</td>
      <td>Monthly</td>
      <td>Dine in</td>
      <td>Between 30 minutes to 1 hour</td>
      <td>more than 3km</td>
      <td>Yes</td>
      <td>...</td>
      <td>Less than RM20</td>
      <td>4</td>
      <td>3</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>3</td>
      <td>In Store displays;Billboards</td>
      <td>Yes</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2019/10/01 12:39:08 PM GMT+8</td>
      <td>Female</td>
      <td>From 20 to 29</td>
      <td>Student</td>
      <td>Less than RM25,000</td>
      <td>Rarely</td>
      <td>Take away</td>
      <td>Below 30 minutes</td>
      <td>more than 3km</td>
      <td>No</td>
      <td>...</td>
      <td>Less than RM20</td>
      <td>2</td>
      <td>1</td>
      <td>4</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>Through friends and word of mouth</td>
      <td>No</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2019/10/01 12:39:20 PM GMT+8</td>
      <td>Male</td>
      <td>From 20 to 29</td>
      <td>Student</td>
      <td>Less than RM25,000</td>
      <td>Monthly</td>
      <td>Take away</td>
      <td>Between 30 minutes to 1 hour</td>
      <td>1km - 3km</td>
      <td>No</td>
      <td>...</td>
      <td>Around RM20 - RM40</td>
      <td>3</td>
      <td>3</td>
      <td>4</td>
      <td>2</td>
      <td>2</td>
      <td>3</td>
      <td>3</td>
      <td>Starbucks Website/Apps;Social Media</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 21 columns</p>
</div>




```python
df.rename(columns={'1. Your Gender':'Sex', '11. On average, how much would you spend at Starbucks per visit?':'Average spend (per visit)'},inplace=True)
```


```python
(df[df['Sex']=='Male']['Average spend (per visit)']).head(5)
```




    2         Less than RM20
    4     Around RM20 - RM40
    7         Less than RM20
    9     Around RM20 - RM40
    16    Around RM20 - RM40
    Name: Average spend (per visit), dtype: object




```python
(df[df['Sex']=='Female']['Average spend (per visit)']).head(5)
```




    0        Less than RM20
    1        Less than RM20
    3        Less than RM20
    5        Less than RM20
    6    Around RM20 - RM40
    Name: Average spend (per visit), dtype: object




```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 122 entries, 0 to 121
    Data columns (total 21 columns):
     #   Column                                                                                                                  Non-Null Count  Dtype 
    ---  ------                                                                                                                  --------------  ----- 
     0   Timestamp                                                                                                               122 non-null    object
     1   Sex                                                                                                                     122 non-null    object
     2   2. Your Age                                                                                                             122 non-null    object
     3   3. Are you currently....?                                                                                               122 non-null    object
     4   4. What is your annual income?                                                                                          122 non-null    object
     5   5. How often do you visit Starbucks?                                                                                    122 non-null    object
     6   6. How do you usually enjoy Starbucks?                                                                                  121 non-null    object
     7   7. How much time do you normally  spend during your visit?                                                              122 non-null    object
     8   8. The nearest Starbucks's outlet to you is...?                                                                         122 non-null    object
     9   9. Do you have Starbucks membership card?                                                                               122 non-null    object
     10  10. What do you most frequently purchase at Starbucks?                                                                  122 non-null    object
     11  Average spend(per visit)                                                                                                122 non-null    object
     12  12. How would you rate the quality of Starbucks compared to other brands (Coffee Bean, Old Town White Coffee..) to be:  122 non-null    int64 
     13  13. How would you rate the price range at Starbucks?                                                                    122 non-null    int64 
     14  14. How important are sales and promotions in your purchase decision?                                                   122 non-null    int64 
     15  15. How would you rate the ambiance at Starbucks? (lighting, music, etc...)                                             122 non-null    int64 
     16  16. You rate the WiFi quality at Starbucks as..                                                                         122 non-null    int64 
     17  17. How would you rate the service at Starbucks? (Promptness, friendliness, etc..)                                      122 non-null    int64 
     18  18. How likely you will choose Starbucks for doing business meetings or hangout with friends?                           122 non-null    int64 
     19  19. How do you come to hear of promotions at Starbucks? Check all that apply.                                           121 non-null    object
     20  20. Will you continue buying at Starbucks?                                                                              122 non-null    object
    dtypes: int64(7), object(14)
    memory usage: 20.1+ KB



```python
import matplotlib.pyplot as plt

plt.rcParams['figure.figsize']
sns.set()
```


```python
sns.histplot(data=df,x='Average spend (per visit)',hue='Sex')
plt.show()
```


    
![png](output_12_0.png)
    



```python

```
