# Module 21 Report - David Girma

## Overview of the analysis

A Neural Network Model will be used for predicting if an applicant for funding will succeed or not in their venture, as we assume the role of a nonprofit foundation . Using the features in the dataset provided, a binary classifier will predict whether applicants will be successful. This model will be trained with a CSV file containing more than 34,000 records of companies that have already received funding. This CSV file of course has a dedicated column that determine if the current project is considered successful or not.


## Results

The procedure on building this model can be split into two major parts: Data preprocessing & the model itself (compilation, training and evaluation). We aim to achieve 75% of accuracy with this Deep Learning model.

### Data Preprocessing

The target variables of this model is the 'IS_SUCCESSFUL' column, as this determines wether an applicant has been successful in the data source or not, hence it will help us predict for future reference. This was also determined by the fact that this variable is binary (0=fail, 1= successful). In the other hand, the features are all the other variables, except for the EIN and NAME columns, which was believed they were not contibuting to the model. 

As already mentioned, the variables removed from the data source (CSV) were the EIN (ID column) and NAME, as the number of incidencies did not repeat that often, with the case of EIN being fundamentally the ID of each applicant, so it made sense to get rid of that column. 

Finally, the variables application type and classification were scrutinized so the Others category was added in order to eliminate potential outliers for this analysis. 

### Compilation, training & evaluation 

In regards to the second part of the analysis (compiling, training & evaluation of the model), the number of neurons, layers and activation functions were the following:

####
number_input_features = len(X_train_scaled[0])
hidden_nodes_layer1 = 7
hidden_nodes_layer2 = 14
hidden_nodes_layer3 = 21
####

The reasoning behind these 3 layers was that the number of input features is determined by len( X_train_scaled[0]), which equals to 274. Then for the hidden layers (intermediate layers) the numbers 7, 14 and 21 were chosen, as these gave us a total of 2,052 parameters (optimization version), which made the model robust and able to predict without so many resources consumption.

### Objective achieved

The target of 75% accuracy was met once the NAME column was kept from the data source, but all the instances were the NAME did not repeat at least 5 times were then categorized as 'Others.' Once this change was made, the accuracy went from 73% to 77%, which met the goal proposed for this analysis:

1) Original accuracy:
268/268 - 0s - 218us/step - accuracy: 0.7340 - loss: 0.5504
Loss: 0.5503745079040527, Accuracy: 0.73399418592453

2) Optimization accuracy:
268/268 - 0s - 240us/step - accuracy: 0.7743 - loss: 0.4725
Loss: 0.47254258394241333, Accuracy: 0.7743440270423889

This increase in the model performance was achieved by ONLY eliminating the EIN ID variable, and keeping the NAME, although he had to also categorize into Others some values that were not that frequent. This led to the observation that for a given company, they could apply many time for the funding opportunity, so their history of whether their other attempts for fundings leading to success can be taken into account. 


## Summary
With >2,000 parameters for this model, we achieved >75% accuracy for the prediction of funding projects, determining if these are likely to succeed, or not. 


Model: "sequential"
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━┓
┃ Layer (type)                    ┃ Output Shape           ┃       Param # ┃
┡━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━┩
│ dense (Dense)                   │ (None, 7)              │         1,925 │
├─────────────────────────────────┼────────────────────────┼───────────────┤
│ dense_1 (Dense)                 │ (None, 14)             │           112 │
├─────────────────────────────────┼────────────────────────┼───────────────┤
│ dense_2 (Dense)                 │ (None, 1)              │            15 │
└─────────────────────────────────┴────────────────────────┴───────────────┘
 Total params: 2,052 (8.02 KB)
 Trainable params: 2,052 (8.02 KB)
 Non-trainable params: 0 (0.00 B)

As all the params were trainable, and with a 0% loss, the accuracy % suits our needs adequately. One recommendation would be to try with different combinations of numbers of hidden layers and neurons, as the only variables that were corrected for boosting this accuracy were the NAME column and the application type and classification.
