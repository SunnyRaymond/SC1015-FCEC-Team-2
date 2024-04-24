# SC1015-FCEC-Team-2

# Question and Problem Definition
Given a training dataset listing passengers who either survived or didn't survive the Titanic disaster, can our model predict, using a test dataset that lacks survival information, whether these passengers survived?

## We decide to deploy the following workflow stages

1. **Define the question or problem.**
2. **Gather training and testing data.**
3. **Organize, prepare, and purify the data.**
4. **Analyze, recognize patterns, and explore the data.**
5. **Model, forecast, and address the problem.**
6. **Visualize, document, and present the steps of problem-solving and the ultimate solution.**
7. **Provide the results.**

## Workflow Goals

- **Classifying.** Our aim might be to classify or categorize our samples, and to understand the impact or correlation of various classes with our solution goal.

- **Correlating.** The approach could involve analyzing available features in the training dataset to determine which ones significantly contribute to our solution goal. It is important to evaluate whether there is a statistical correlation between a feature and the solution outcome and if changes in feature values alter the solution state and vice versa. This assessment is valid for both numerical and categorical features in the dataset. It also involves exploring correlations between features that go beyond survival to aid further goals and workflow stages.

- **Converting.** The modeling phase requires data preparation, where depending on the model algorithm, features might need to be converted to numerical equivalents, such as converting categorical text values to numbers.

- **Completing.** Preparing data may also involve estimating missing values within a feature since model algorithms typically perform best when no values are missing.

- **Correcting.** The training dataset might be scrutinized for errors or potentially inaccurate values within features, aiming to correct these values or exclude the samples that contain these errors. This could involve identifying outliers among our samples or features, or completely discarding a feature if it doesn't contribute to the analysis or might significantly skew the results.

- **Creating.** There may be opportunities to create new features based on an existing feature or a group of features, ensuring the new feature aligns with correlation, conversion, and completeness objectives.

- **Charting.** The selection of appropriate visualization plots and charts depends on the nature of the data and the solution goals.

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


