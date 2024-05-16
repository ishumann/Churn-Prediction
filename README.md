# Churn Prediction

## What is Churn?

Churn refers to customers who are likely to disengage or become inactive over time. This can be indicated by a lack of account activity, reduced usage compared to previous levels, or a decline in services or purchases.

## Objective

The objective of this project is to:

1. Identify and visualize factors contributing to customer churn.
2. Build a prediction model to classify if a customer is likely to churn.
3. Choose a model that provides a probability of churn, allowing customer service to target potentially churned customers more effectively with minimal effort.

## How?

We will approach this using the following methods:

1. **Deep Learning (Sequential Model):** Construct a neural network by stacking layers on top of each other to analyze complex patterns in the data.
2. **H2O AutoML:**
   - Open-sourced and in-memory machine learning platform.
   - Offers linear scalability and utilizes algorithms like gradient boosting, generalized linear models, and deep learning.

## Project Timeline

1. **Data Analysis:**
   - Explore data to identify relationships and patterns.
2. **Feature Engineering:**
   - Preprocess data to prepare it for modeling.
3. **Model Building:**
   - Implement machine learning and deep learning algorithms.
4. **Model Building with AutoML:**
   - Utilize H2O AutoML to automate model selection and tuning for improved performance and efficiency.

## Data Analysis

check how data is distributed and how diff feature are responsible for the outcome.

tenure - how old the customer been with the bank
no. of products - no. of services cust is using.
isactivemember - using account fequantly i.e widrowing

dependent variable - exited(chruning)



## Steps for data analysis
### Data Visualization
* Extited ratio
    * Pie chart
        * how many customer chruned or not in persantage.
        * observation -
            * 20.4% customer churned

* Relation of  categories againest exited features (Count Plot)
    * obeservation -
        * Geography vs Exited
            * majority customer are from france followed by spain and germany(almost equal)
            * france and germany has maximum churn rate but the ratio between churned and retained in germany rate people exiting is high. (retained ~ 1700-1800, exited ~ 700-800) , france -> (retained ~ 4000, exited ~ 700-800)

        * Gender  vs Exited
            * male are more in numbers
            * although female count is less but churn count is more then male
        * HasCrCard  vs Exited
            * cust with card > no card
            * surprisingly cust with card exited > no card
        * IsActiveMember  vs Exited
            * ~(almost) = proportion
            * less active chruned more

* Relation of  Continues againest exited features (box Plot)
    * creditscore vs Exited -> not much diffrence b/w retained and exited cust.'s credit score not valuble for prediction
    * vs age -> cust. with churning is old than retained. median > 40, less likely 30~40.
    * vs tenure -> newer (2 - years and older cust. 8) likely to churn, 4-6 yrs cust. most likly stay.
    * vs balance -> median is same, 25 %ile is 0 for cust. who stayed, 25% people have who stayed 0 balance
    * vs servies -> can't tell from this, same, not good predictor
    * salay -> is same, not to tell from it.

### Good Predictors are:
* Tenure
* Balance
* Age
* Geography
* Gender
* HasCrCard
* IsActiveMember


## Feature Engineering

*  making a new column BalanceSalaryRatio
    * bal. and salary alone were not impacful so, combined and  check is it effactiing on exited
    * obervation - not that imacful but cust. > 2 -> likly to leave.

*  making a new column TenureByAge
    * Ten. and age were were  impacful so, combined and  check is it effactiing on exited
    * obervation - not that imacful

### For Categorical Data
* Encoding
    * Gender - labelEncoding
    * location - OneHotEncoding

### For  Numarical Data
* Feature Scaling
    * MinMaxScaler - scaled by min, max -> turn into [0,1], scale data in between 0 and 1. affect by outliars, use distribution != Gaussian
    * StandardScaler: centered around zero, remove mean -> scale to unit variance -> scale by std(), less effected by outliars, prefferd by algo that assumes zero- centered data - regression models.


#### Final data

## Model Training
* ANN - stack of neural layers one tensor intput -> ANN -> one Tensor Output    

* When not to use?
 * model have muliple i/p or multi o/p,
    * if any:
        * do layer sharing
 * you want non-linear topology
 (i.e. a residual connectionm a multi-branch model)

 ## Model Evaluation
 * Confusion matrix (tp,fn,fp,tn)
 * Classification Report(presision, recall, f1-score, support, accuracy, specifity, macro avg, weigh avg)
  * presision -> true spam pred out of total spam prediction
    * if not concern with ham being classi. as spam
    * if person  is frustrast with spam he will be ok with ham classi. as spam. than he look for precision
  * recall -> true spam pred out of true spam.
    * If wanna make sure that only spam is being prdicted as spam, and imp. mail not going in spam mail. than emphisis on this.
    * recall = balanced approch(harmonic mean) b/w precision and recall
