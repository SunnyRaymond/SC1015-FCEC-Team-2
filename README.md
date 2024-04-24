# SC1015-FCEC-Team-2

# Question and Problem Definition
Given a training dataset listing passengers who either survived or didn't survive the Titanic disaster, can our model predict, using a test dataset that lacks survival information, whether these passengers survived?

## We decide to deploy the following workflow stages

1. **Define the question or problem.SHI QILUN**
2. **Gather training and testing data.GUO YICHEN**
3. **Organize, prepare, and purify the data.GUO YICHEN**
4. **Analyze, recognize patterns, and explore the data.GUO YICHEN**
5. **Model, forecast, and address the problem.TAO QIANKUAN GUO YICHEN SHI QILUN**
6. **Visualize, document, and present the steps of problem-solving and the ultimate solution.TAO QIANKUAN**
7. **Provide the results.**

# We first acquire data and analyze by describing data

# Then we made assumptions Based on Data Analysis
## Correlating

We aim to assess how closely each feature is associated with survival at the project's onset, intending to compare these preliminary findings with correlations derived from more detailed models later in the projec### 

## Completing

- The **Age** feature might be completed as it appears to have a significant correlation with survival.
- Completing the **Embarked** feature could also be crucial, as it might relate to survival or another critical fea#ture.

## Correcting

- The **Ticket** feature might be excluded from our analysis due to a high duplication rate (22%) and a possible lack of correlation with survival.
- **Cabin** could be omitted because it is highly incomplete or mostly null in both the training and test datasets.
- **PassengerId** should be removed from the training dataset as it does not impact survival.
- The **Name** feature, which is relatively non-standard, might also be dropped as it likely does not directly influen#ce survival.

## Creating

- Consider creating a **Family** feature derived from **Parch** and **SibSp** to count family members on board.
- Engineer a new feature from the **Name** field to extract **Title** as a distinct attribute.
- Transform the continuous numerical **Age** feature into an ordinal categorical feature by introducing **Age bands**.
- A **Fare range** feature might also be created to assist our anal#ysis if beneficial.

## Classifying

Further assumptions can be added based on initial problem descriptions:
- Women (Sex=female) had a higher survival rate.
- Children (Age<?) were more likely to survive.
- Upper-class passengers (Pclass=1) had a higher likelihood of survival.

# After that we Analyze Data by Visualizing

## Correlating Numerical Features

Utilizing a histogram chart proves valuable for examining continuous numerical variables such as **Age**, where establishing bands or ranges can reveal significant patterns. Histograms show the distribution of samples across automatically determined bins or consistent ranges, aiding in addressing queries about specific age groups (e.g., Did infants have a higher survival rate?).

### Observations

- Infants (Age <=4) exhibited a high survival rate.
- The oldest passengers (Age = 80) survived.
- A significant number of individuals aged 15-25 did not survive.
- The majority of passengers fell within the 15-35 age group.

### Decisions

- Age should be incorporated into our model training, as it is crucial.
- Address missing values in the Age data.
- Segment age into distinct groups.

## Correlating Numerical and Ordinal Features

Utilize a single plot to identify correlations by combining multiple features, both numerical and categorical that have numeric values.

### Observations

- **Pclass=3** had the highest number of passengers, yet the majority did not survive. This observation supports our classifying assumption #2.
- Infant passengers in **Pclass=2** and **Pclass=3** mostly survived, adding further support to our classifying assumption #2.
- The majority of passengers in **Pclass=1** survived, confirming our classifying assumption #3.
- There is variation in the **Age** distribution of passengers across different **Pclass** groups.

### Decisions

- **Pclass** should be considered in our model training.

## Correlating Categorical Features

Correlate categorical features with our solution goal to identify significant relationships.

### Observations

- Female passengers exhibited a significantly higher survival rate compared to males, supporting our classifying assumption (#1).
- An exception was noted at **Embarked=C**, where males displayed a higher survival rate. This suggests a potential correlation between **Pclass** and **Embarked**, and subsequently between **Pclass** and **Survived**, rather than a direct correlation between **Embarked** and **Survived**.
- Males had a better survival rate in **Pclass=3** compared to **Pclass=2** at **Embarked=C** and **Embarked=Q**, underscoring our need to complete information on embarkation (completing #2).
- Survival rates varied among male passengers at different ports of embarkation within **Pclass=3**, aligning with correlating assumption (#1).

### Decisions

- Include the **Sex** feature in model training.
- Complete and incorporate the **Embarked** feature in model training.

## Correlating Categorical and Numerical Features

Explore the relationships between categorical features (with non-numeric values) and numeric features. Focus on correlating **Embarked** (categorical non-numeric), **Sex** (categorical non-numeric), **Fare** (numeric continuous), with **Survived** (categorical numeric).

### Observations

- Passengers who paid higher fares had a better survival rate, supporting the idea of creating fare ranges as mentioned in our assumption for creating (#4).
- The port of embarkation shows a correlation with survival rates, confirming our correlating assumption (#1) and the need to complete this information (completing #2).

### Decisions

- Consider implementing fare bands for the **Fare** feature.

# Next step is clean data

## Correcting by dropping features

Based on our previous analysis we want to drop the Cabin and Ticket features.

Note that where applicable we perform operations on both training and testing datasets together to stay consistent.

## Creating new feature extracting from existing

**Observations.**


- Most titles band Age groups accurately. For example: Master title has Age mean of 5 years.
- Survival among Title Age bands varies slightly.
- Certain titles mostly survived (Mme, Lady, Sir) or did not (Don, Rev, Jonkheer).

**Decision.**

- We decide to retain the new Title feature for model training.

## Converting a categorical feature

Now we can convert features which contain strings to numerical values. This is required by most model algorithms. Doing so will also help us in achieving the feature completing goal.

converting Sex feature to a new feature called Gender where female=1 and male=0.

## Completing a numerical continuous feature

Note correlation among Age, Gender, and Pclass. Guess Age values using median values for Age across sets of Pclass and Gender feature combinations. So, median Age for Pclass=1 and Gender=0, Pclass=1 and Gender=1, ...

## Create new feature combining existing features

We can create a new feature for FamilySize which combines Parch and SibSp. This will enable us to drop Parch and SibSp from our datasets.

## Completing a categorical feature

Embarked feature takes S, Q, C values based on port of embarkation. Our training dataset has two missing values. We simply fill these with the most common occurance.

## Converting categorical feature to numeric

We can now convert the EmbarkedFill feature by creating a new numeric Port feature.

## Quick completing and converting a numeric feature

complete the Fare feature for single missing value in test dataset using mode to get the value that occurs most frequently for this feature. 

round off the fare to two decimals

# Nearly final step---Model, predict and solve

Our problem is a classification and regression problem. We want to identify relationship between output (Survived or not) with other variables or features (Gender, Age, Port...). We are also perfoming a category of machine learning which is called supervised learning as we are training our model with a given dataset. With these two criteria - Supervised Learning plus Classification and Regression, Choices include:

- Logistic Regression
- Decision Tree
- Random Forrest

## Validating Assumptions with Logistic Regression

Logistic Regression can be employed to validate our assumptions and decisions related to feature creation and completion by examining the coefficients of the features in the decision function.

### Key Insights from Logistic Regression

- **Positive Coefficients**: These increase the log-odds of the response, enhancing the probability of the outcome. A significant observation is the **Sex** feature, which has the highest positive coefficient, indicating that as the Sex value increases (from male: 0 to female: 1), the probability of Survived=1 also increases significantly.

- **Negative Coefficients**: These decrease the log-odds of the response, reducing the probability of the outcome. For instance, as **Pclass** increases, the probability of Survived=1 decreases the most. This highlights the inverse relationship between Pclass and survival.

- **Artificial Feature Inclusion**: The interaction term **Age\*Class** emerges as a good artificial feature for modeling, as it exhibits the second-highest negative correlation with survival. Similarly, **Title** stands out with the second-highest positive correlation with survival.

### Decisions

Based on these findings:
- Prioritize features with strong positive or negative coefficients in the logistic regression model to refine the predictive accuracy.
- Consider creating and using artificial interaction features like **Age\*Class** and **Title** that have shown significant correlations with the outcome.

## Decision Tree Model Overview

The decision tree model is a predictive modeling technique used for both classification and regression tasks:

- **Classification Trees**: In these tree structures, the target variable takes a finite set of values. The leaves of the tree represent class labels, while the branches represent conjunctions of features that lead to these labels.

- **Regression Trees**: These trees are used when the target variable can take continuous values, typically real numbers. In regression trees, the path from the root to the leaf represents decision rules applicable to the input features.

### Model Confidence

- The model confidence score for the decision tree is the highest among all models evaluated so far, indicating its strong predictive performance.

This clear distinction between classification and regression trees helps in understanding the specific application and utility of decision trees depending on the nature of the target variable and the dataset at hand.

## Random Forest Model Overview

Random Forests are one of the most popular machine learning methods used today. They are an ensemble learning method applicable to both classification and regression tasks. Here’s how they work:

- **Ensemble Learning Method**: Random Forests operate by constructing multiple decision trees during training. For a classification task, the final prediction is the mode of the classes predicted by individual trees; for a regression task, it is the mean prediction of the trees.

- **Parameter: n_estimators**: Typically, Random Forests consist of multiple trees (e.g., `n_estimators=100`), which means 100 decision trees are constructed.

### Model Confidence

- The confidence score of the Random Forest model is the highest among all models evaluated, highlighting its robustness and reliability in predictive accuracy.

### Decision for final output

- Based on the superior performance of the Random Forest model, we have decided to use its output (`Y_pred`) for our output of results. This decision underscores our confidence in the model's predictive capabilities and its suitability for handling the task at hand.


# Final Model evaluation
Our submission to the competition site Kaggle , achieving a 77.00 score.

# References
- [Getting Started with Pandas: Kaggle's Titanic Competition](https://www.kaggle.com/c/titanic/details/getting-started-with-random-forests)
