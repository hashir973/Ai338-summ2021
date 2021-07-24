Code:

import numpy as np
from sklearn import cross_validation
from sklearn import datasets
from sklearn import svm

setwd("D:/Kaggle Datasets/titanic")
training_set = read.csv("Train.csv")
test_set = read.csv("test.csv")
 
test_setSurvived = NA
 
complete_data = rbind(training_set, test_set)
 
library(Amelia)
missmap(complete_data, main = "Missing value map")
 
complete_dataAge[is.na(complete_dataAge)] <- median(complete_dataAge, na.rm=T)
complete_dataEmbarked[complete_dataEmbarked==""] <- "S"
 
drop <- c("Ticket","Name","Cabin")
df = complete_data[,!(names(complete_data) %in% drop)]
 
for (i in c("Survived","Pclass","Sex","Embarked")){
  df[,i]=as.factor(df[,i])
} 
# Create dummy variables for categorical variables
# install.packages("dummies")
library(dummies)
df <- dummy.data.frame(df, names=c("Pclass","Sex","Embarked"), sep="_")
training_set = df[1:669, ]
test_set = df[670:891, ] 
# install.packages("tidyverse")
library(tidyverse)
training_set_sub = training_set %>% select(Pclass_1, Pclass_2, Age, Sex_female, SibSp)
test_set_sub = test_set %>% select(Pclass_1, Pclass_2, Age, Sex_female, SibSp)
library(e1071)
classifier = svm(x = training_set_sub
                 , y = training_setSurvived
                 , kernel = 'linear'
                 , type = 'C-classification')
 
y_pred = predict(classifier, newdata = test_set_sub)
library(caret)
confusionMatrix(table(y_pred, test_set[, 2])) 
output = pd.DataFrame({'PassengerId': titanic_test.index,'Survived': y_test_pred})
output.to_csv('SVM-TitanicSurvival.csv',index=False)

"Support Vector Machine (SVM) is a supervised machine learning algorithm capable of performing classification, regression and even outlier detection. The linear SVM classifier works by drawing a straight line between two classes."


import numpy as np # linear algebra
import pandas as pd # data processing, CSV file I/O (e.g. pd.read_csv)
import matplotlib.pyplot as plt
%matplotlib inline
import seaborn as sns

# Input data files are available in the read-only "../input/" directory
# For example, running this (by clicking run or pressing Shift+Enter) will list all files under the input directory
import os
for dirname, _, filenames in os.walk('/kaggle/input'):
    for filename in filenames:
        print(os.path.join(dirname, filename))
titanic_train = pd.read_csv(r'/kaggle/input/titanic/train.csv',index_col='PassengerId')
titanic_test=pd.read_csv(r'/kaggle/input/titanic/test.csv',index_col='PassengerId')
titanic_train.head()
titanic_test.head()
titanic_train.loc[:,'Survived'].sum()/len(titanic_train.loc[:,'Survived'])*100
titanic_train.isna().sum()
vars = ['Pclass','Sex','SibSp','Parch','Embarked']

i=1
fig=plt.figure()

for var in vars:
    sns.countplot(data=titanic_train,x=var,hue='Survived')
    plt.show()
sns.displot(data=titanic_train,x='Age',hue='Survived',multiple='stack',bins=8)

sns.displot(data=titanic_train,x='Fare',hue='Survived',multiple='stack',bins=10)
plt.show()
titanic_train.Cabin.fillna('NA',inplace=True)
titanic_test.Cabin.fillna('NA',inplace=True)
titanic_train["Title"] = ([i.split(",")[1].split(".")[0].strip() for i in titanic_train.Name])
titanic_test["Title"] = ([i.split(",")[1].split(".")[0].strip() for i in titanic_test.Name])
print(titanic_train.Title.unique())
print(titanic_test.Title.unique())
print(titanic_train.loc[titanic_train.Title=='Master',:].Age.describe([]))
print(' ')
print(titanic_train.loc[titanic_train.Title=='Mr',:].Age.describe([]))
train_dummy = pd.get_dummies(titanic_train[['Sex','Title']],drop_first=True)
test_dummy = pd.get_dummies(titanic_test[['Sex','Title']],drop_first=True)
output = pd.DataFrame({'PassengerId': titanic_test.index,'Survived': y_test_pred})
output.to_csv('Submission-KNN-Muneeb.csv',index=False)

" It is the learning where the value or result that we want to predict is within the training data (labeled data) and the value which is in data that we want to study is known as Target or Dependent Variable or Response Variable."

import numpy as np # linear algebra
import pandas as pd # data processing, CSV file I/O (e.g. pd.read_csv)
import tensorflow as tf
import os
for dirname, _, filenames in os.walk('/kaggle/input'):
    for filename in filenames:
        print(os.path.join(dirname, filename))
dftrain = pd.read_csv("/kaggle/input/titanic/train.csv", index_col=0, dtype={"Cabin":"string", "Embarked": "string"})
dftrain = dftrain.drop(columns=["Cabin", "Embarked"]).dropna()
y_train = dftrain.pop("Survived")
dftest = pd.read_csv("/kaggle/input/titanic/test.csv", index_col=0)
dfsubm = pd.read_csv("/kaggle/input/titanic/gender_submission.csv", index_col=0)
dfeval = dftest.join(dfsubm)
dfeval = dfeval.drop(columns=["Cabin", "Embarked"]).dropna()
y_eval = dfeval.pop("Survived")
CATEGORY_COLUMNS = ["Sex"]
NUMERIC_CULUMNS = ["Pclass", "Age", "SibSp", "Parch", "Fare"]
feature_columns = []
for feature_name in CATEGORY_COLUMNS:
    vocabulary = dftrain[column].unique()
    feature_columns.append(tf.feature_column.categorical_column_with_vocabulary_list(feature_name, vocabulary))
for feature_name in NUMERIC_CULUMNS:
    feature_columns.append(tf.feature_column.numeric_column(feature_name, dtype=tf.floa
ds = make_input_fn(dftrain, y_train, batch_size=10)()
for feature_batch, label_batch in ds.take(1):
  print('Some feature keys:', list(feature_batch.keys()))
  print()
  print('A batch of class:', feature_batch['Fare'])
  print()
  print('A batch of Labels:', label_batch)                                                            
linear_est = tf.estimator.LinearClassifier(feature_columns=feature_columns)
linear_est.train(train_input_fn)
result = linear_est.evaluate(eval_input_fn)
print(result)
output = pd.DataFrame({'PassengerId': titanic_test.index,'Survived': y_test_pred})
output.to_csv('Linear-Submission.csv',index=False)


"Linear classifiers classify data into labels based on a linear combination of input features. Therefore, these classifiers separate data using a line or plane or a hyperplane (a plane in more than 2 dimensions). They can only be used to classify data that is linearly separable."



![WhatsApp Image 2021-07-24 at 5 03 08 AM](https://user-images.githubusercontent.com/65955079/126867874-831d4799-a4f8-4a3e-b5b8-e6c93d365ee7.jpeg)



![svm](https://user-images.githubusercontent.com/53654229/126365125-d60e6725-94a1-4625-b03c-f5746da76d9b.jpeg)


![linear](https://user-images.githubusercontent.com/82328789/126365453-49b628ad-08b4-4e28-9010-cc0fa56b75f5.jpeg)
