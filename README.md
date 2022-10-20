# Neural_Network_Charity_Analysis

## Overview

The purpose of this analysis is to create a binary classifier model that is capable of predicting whether applicants will be successful if they are funded by Alphabet Soup, a philanthropic foundation dedicated to helping organizations that protect the environment, improve people’s well-being, and unify the world.

## Results

#### Data Preprocessing

- Target variable for the model:
- The IS_SUCCESSFUL column, which answers: “Was the money used effectively?”

- Feature variables for the model:
	- Columns:
		- APPLICATION_TYPE - Alphabet Soup application type
		- AFFILIATION - Affiliated sector of industry
		- CLASSIFICATION - Government organization classification
		- USE_CASE - Use case for funding
		- ORGANIZATION - Organization type
		- INCOME_AMT - Income classification
		- SPECIAL_CONSIDERATIONS - Special consideration for application
		- ASK_AMT - Funding amount requested

- Variables which are neither targets nor features, and were removed from the input data
	- Columns:
		- EIN - Identification column
		- NAME - Identification column
		- STATUS - Active status
			- Full column removed after first removing the 5 rows with non-active status

#### Compiling, Training, and Evaluating the Model

- Number of layers, neurons, and activation functions that were selected for the neural network model:
	- Layers: There were 3 hidden layers in addition to the input and output layers
	- Neurons: 180 neurons in total, split between the 3 hidden layers accordingly: 80, 60, 40
	- Activation Functions: RELU

- Why the above numbers and functions were chosen:
	- Layers: There were originally only 2 layers in a model that would not achieve more than 72% accuracy. A Third was added to help increase this accuracy number. The data set is not particularly complex or humongous, so 3 layers were enough to provide the desired results.
	- Neurons: The first layer was approximately twice that of the input neurons, with additional layers decreasing to help lower run time and increase accuracy.
	- Activation Functions: RELU was chosen for the main layers due to its ability to simplify the output. Originally, Sigmoid was chosen as the output function so it would give the result between 0 and 1, which is aligns with the IS_SUCCESSFUL target column and gives the model 100% accuracy, however I changed it to RELU to decrease the amount of loss experienced without sacrificing much accuracy.
		- Sigmoid Output Activation Function Loss/Accuracy
		- ![sigmoid_output_stats](https://user-images.githubusercontent.com/105808695/197036791-b5887ee5-b49f-4cae-9d5a-2dd17fc98c69.png)
		- RELU Output Activation Function Loss/Accuracy
		- ![RELU_output_stats](https://user-images.githubusercontent.com/105808695/197036756-dd7c6d9a-4180-4697-973e-f77cf185940f.png)

- Target model performance was able to be achieved, as seen above with the use of the RELU Output Activation Function
	- Loss: 2%
	- Accuracy: 99.8%

- Steps taken to increase/optimize model performance:
	- Removed the 5 STATUS 0 rows, then removed STATUS column
      - The results with an “inactive status” were not important to this model, and due to removing them, the STATUS column was no longer providing necessary insight into the final model.
	- For "ASK_AMT" Column: removed outlier issue by binning those other than 5000
      - The majority of the results had their requested funding amount as 5000, which skewed the data too much:
      - ![ask_amt_counts](https://user-images.githubusercontent.com/105808695/197036846-bfeb0fc3-2b72-495f-a930-7c5ce1056361.png)
      - After binning the other numbers together to remove the data-skewing outliers, this column was able to provide more accurate information for the model
      - ![ask_amt_binned](https://user-images.githubusercontent.com/105808695/197036864-12bf79a1-6891-46f4-8001-6a30445c85ad.png)
	- Added 20 more nodes to hidden nodes layer 2
      - This was done to help increase model accuracy
	- Added third hidden layer, with 40 hidden nodes
      - This was done to help increase model accuracy
	- Output layer activation function changed from "Sigmoid" to "RELU"
      - As explained above, this helped to decrease the amount of loss seen in the model 
	- Reduced epochs from 100 to 50
      - The model achieved this result fairly quickly, with little loss, so the epochs were reduced to save time and space.

## Summary

This model can be useful to predict whether or not applicants will be successful if they receive funding from Alphabet Soup, as it runs with 99.8% accuracy and only 2% loss.

#### Recommendation

Another model that could be useful is the Random Forest Classifier, as it’s often used to solve classification problems. Random Forest Classifiers can typically handle large data with outliers better than Neural Network Deep Learning Models and will provide a buffer against overfitting the data. Additionally, they require less experience going into creating the model, so it could be a better fit for more analysts and companies.
