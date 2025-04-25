# Histopathologic-Cancer-Detection

In this exercise I'm going to build a model for Histopathologic Cancer Detection, using the data from Kaggle competition.

https://www.kaggle.com/competitions/histopathologic-cancer-detection/overview

The available data is organized in two folders; train and test, with images patches of patology scans. In addition there is a file called "train_labels.csv", which contains the labels for the images of the training set, with values of 1 in cases when cancer is possitive and 0 when is negative.


## Exploratory Data Analysis (EDA)
The first step is to combine the labels with the names of the files inside the train folder, to use the data later.

After, I'm going to verify this points:

* Duplicated Id's
* Labels with missing data
* Imbalance of the labels

![image](https://github.com/user-attachments/assets/3d530394-6590-4c17-9249-d1825f9d3bb5)

After analyze the data we can conclude there are not duplicated data or empty labels, in addtion there is an imbalance in the labels, but I'm not going to modify current data.

## Processing
The processing has the next steps:

The first step it to split the training data in training and validation, for this I use 20% of the data.
Next is a real-time data augmentation pipeline that will randomly transform your images, this step helps the model to generalize better
Define the target height & width for every image (IMG_SIZE).
Number of images passed through the network in each training or validation step (BATCH_SIZE).
Finally I create two Keras data generators that read image file paths and labels from DataFrames.


## Model Architecture
For this project I'm going to use a CNN model, to accelerate the training process I use transfer learning using as base model the EfficientNet model. The feature-extraction layers are frozen, and then I add a trainable head for binary classification.

For tune the hyperparameters, I tested different learning rates, and obtained the best results with the selected one.

![image](https://github.com/user-attachments/assets/4934e514-19f4-4724-83b6-bc9cfe5212f3)

## Results and Analysis Hyperparameter tunning
These initial plots are from a different model using different EPOCHS = 10 and Learning Rate = 0.001, the results are worst compared with the model used in the project

For Learning Rate = 0.001:

![image](https://github.com/user-attachments/assets/81d33090-cc9b-436b-92fb-37949e2720df)

Learning Rate = 1e-4:
![image](https://github.com/user-attachments/assets/b5e23e1d-60a9-4b28-9175-d96d5989714e)

Next I'm going to calculate and plot the ROC curve for trhe best model:

![image](https://github.com/user-attachments/assets/74357783-4c02-4a77-a6b6-cda5fc7099a8)

## Conclusions
The CNN model using EfficientNet as base model, has a good performance, however the result still can be improved trying differente hyperparameters or a different base model. The main problem is the time required to train the model with different parameters, I try a couple of scenarios, but probably there are better options that I didn't test because of this compunting time requirements.

One of the strategies I try for different hyperparameter was using an small dataset, however the performance was poor because of the overfiting generated because of this large number of parameters of the model against the small number of samples.

At the end I train a few model with different parameters, but the limitation is that I only could consider a few scenarios
