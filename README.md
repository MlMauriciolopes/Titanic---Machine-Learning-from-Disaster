# Titanic Dataset

## Dataset Description

### The Challenge

The sinking of the Titanic is one of the most infamous shipwrecks in history. On April 15, 1912, during her maiden voyage, the widely considered “unsinkable” RMS Titanic sank after colliding with an iceberg. Unfortunately, there weren't enough lifeboats for everyone onboard, resulting in the death of 1502 out of 2224 passengers and crew.

While there was some element of luck involved in surviving, it seems some groups of people were more likely to survive than others. In this challenge, we ask you to build a predictive model that answers the question: "what sorts of people were more likely to survive?" using passenger data (i.e., name, age, gender, socio-economic class, etc).

The data has been split into two groups:

- Training set (train.csv)
- Test set (test.csv)

The training set should be used to build your machine learning models. For the training set, we provide the outcome (also known as the “ground truth”) for each passenger. Your model will be based on "features" like passengers' gender and class. You can also use feature engineering to create new features.

The test set should be used to see how well your model performs on unseen data. For the test set, we do not provide the ground truth for each passenger. It is your job to predict these outcomes. For each passenger in the test set, use the model you trained to predict whether or not they survived the sinking of the Titanic.

We also include gender_submission.csv, a set of predictions that assume all and only female passengers survive, as an example of what a submission file should look like.

### Data Columns

- 'PassengerId'
- 'Survived'
- 'Pclass'
- 'Name'
- 'Sex'
- 'Age'
- 'SibSp'
- 'Parch'
- 'Ticket'
- 'Fare'
- 'Cabin'
- 'Embarked'

### Data Dictionary

- **survival**: Survival (0 = No, 1 = Yes)
- **pclass**: Ticket class (1 = 1st, 2 = 2nd, 3 = 3rd)
- **sex**: Sex
- **age**: Age in years
- **sibsp**: # of siblings / spouses aboard the Titanic
- **parch**: # of parents / children aboard the Titanic
- **ticket**: Ticket number
- **fare**: Passenger fare
- **cabin**: Cabin number
- **embarked**: Port of Embarkation (C = Cherbourg, Q = Queenstown, S = Southampton)

### Variable Notes

- **pclass**: A proxy for socio-economic status (SES) (1st = Upper, 2nd = Middle, 3rd = Lower)
- **age**: Age is fractional if less than 1. If the age is estimated, it is in the form of xx.5
- **sibsp**: The dataset defines family relations (Sibling = brother, sister, stepbrother, stepsister; Spouse = husband, wife)
- **parch**: The dataset defines family relations (Parent = mother, father; Child = daughter, son, stepdaughter, stepson). Some children traveled only with a nanny, therefore parch=0 for them.

## Initial Insights

During the initial analysis:

- The dataset indicates that more women survived than men, with 100% survival for females in the original data.
- People in the 3rd class experienced the highest casualties.
- The 'Age' column appeared to be the most correlated with the passenger's class.
- In the 'Fare' column, there was only one missing value, and this passenger, according to the data, belonged to the 3rd class.
- Analyzing the 'Embarked' column, most people who boarded at 'S' did not survive, with only 33.69% of them surviving.
- In the 'Embarked' column, there are only two missing values, and these two passengers are from the same cabin, B28.

## Solution

- One of the chosen solutions for this challenge was to preprocess the data together by creating a separate test column, 'PassengerId,' and merging the datasets.
- In the 'Age' column, there were many 'NaN' values, so it was necessary to transform these missing values. When a specific age was missing, it was replaced by the mean age of the passenger's class from the 'Pclass' column.
- The 'SibSp' and 'Parch' columns represent family members. Therefore, one analysis solution was to create a new column called 'FamilySize' to combine the total number of people in a single column, including the passenger and their companions from the two columns.
- The 'Ticket' column was not added to the new dataframe due to its lack of a consistent pattern.
- The 'Cabin' column was not added to the new dataframe because it had many missing values, even though there were numbering patterns for cabins, with only 0.007% valid values.
- In the 'Name' column, a new column called 'Title' was created to categorize names by titles (e.g., Mr, Miss, Master, etc.).
- For modeling, eight models were tested: 'Random Forest Classifier,' 'Logistic Regression,' 'K-Nearest Neighbors,' 'Gaussian Naive Bayes,' 'Linear Support Vector Machine (SVC),' 'Stochastic Gradient Descent,' 'Decision Tree Classifier,' and 'Gradient Boost Trees.' While some models did not yield apparent results, they were tested as a practice for learning purposes.
- The 'GridSearchCV' method was used in the 'Get Params' section for hyperparameter tuning.

## References

- [Great Learning](https://www.mygreatlearning.com/blog/gridsearchcv/)
- [Kaggle](https://www.kaggle.com/competitions/titanic/data)
- Kaggle Challenge: Titanic - Machine Learning - [Part 1](https://www.youtube.com/watch?v=8Fu-jBoPci0) & [Part 2](https://www.youtube.com/watch?v=4ryDV7EUtlU&list=PLTrMTWH_kmG_sapE9vb57IzsqAsUV7Xtz&index=2)
