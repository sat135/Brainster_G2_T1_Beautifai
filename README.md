# Brainster Final Project: 

## Group 2 - Team 1
Team Members:
* Jasmina Lavchanska - Nikolovska ( Team Leader )
* Dimitri Kjososki
* Ivica Todorovski
* Tina Stefanovska
* Polad Emin

# Project Title: Beautif.ai

 * Description
 * How does it work?
 * The project implementation
   * Phase 1 : Dataset creation
   * Phase 2 : Training the model
   * Phase 3 : Validation
 * Summary of results

## Description

Beautif.ai is an ios mobile application designed to edit and enhance pictures on a mobile device meant for personal and business usage. The goal of the project is to create a robust classifier which will be able to detect whether an image consists of Daylight Sky, Night sky or No sky at all. Furthermore, during the dataset collection phase, the team decided that one more class should be added in order to identify whether the sky in the night photos is well separated or not. The final set of classes is:
 * Daylight Sky
 * Night sky which can be separated
 * Night Sky without well defined separation points
 * Images without sky (indoor or outdoor). 

The model will be integrated in the application for further use.

## How does it work? 

This model will find a use in recognizing and separating the sky from the rest of the objects on the photo. Once a picture is taken, the application by itself will recognize if there is a sky at all, and then to recognize if it is a day or night in order to identify if sky-algorithm shoud be offered as an option to the user to edit the sky.

## The process

The project implementation was divided in 3 phases:

Phase 1 : Dataset Generation
  * Dataset Collection
  * Dataset Preparation

Phase 2 : Training and Deployment
  * Compose neural network architectures
  * Ping Pong phase with Dataset labelers
  * Fine tunning of the model

Phase 3 : Validation
  * Analysis and benchmark Precision/Recall
  * Predictions of random images

### Phase 1: Dataset Generation

In order to train a deep-learning model regarding requests, we needed an appropriate dataset with balanced distribution of images for the four above stated classes. 
One of the challenges we met during this project was collecting the data. We decided to combine images from existing dataset previously used in similar MIT project and private photos from the team members. This approach was selected in oreder to have high diversity in the dataset since the time and resources of the team members were limited. 
Data preparation consisted of labeling, renaming and resizing the collected dataset.
The final dataset cosists of **8640** images with train - validation split of 85% - 15%:

Class Name | Number of images | Example 1 | Example 2 | Example 3 | Example 4 | Example 5
------------ | ------------- | ------------- | ------------- | ------------- | ------------- | -------------
Daylight Sky | 3304 | ![GitHub image](Images/Primer/Day/day_134.jpg) | ![GitHub image](Images/Primer/Day/day_108.jpg) | ![GitHub image](Images/Primer/Day/day_17.jpg) | ![GitHub image](Images/Primer/Day/day_19.jpg) | ![GitHub image](Images/Primer/Day/day_37.jpg)
Night sky separated | 658 | ![GitHub image](Images/Primer/night_separeted/night_separated_100.jpg) | ![GitHub image](Images/Primer/night_separeted/night_separated_108.jpg)| ![GitHub image](Images/Primer/night_separeted/night_separated_188.jpg) | ![GitHub image](Images/Primer/night_separeted/night_separated_241.jpg) | ![GitHub image](Images/Primer/night_separeted/night_separated_7.jpg)
Night sky not separated | 887 | ![GitHub image](Images/Primer/night_not_separated/night_not_separated_11.jpg) | ![GitHub image](Images/Primer/night_not_separated/night_not_separated_133.jpg) | ![GitHub image](Images/Primer/night_not_separated/night_not_separated_42.jpg) | ![GitHub image](Images/Primer/night_not_separated/night_not_separated_140.jpg) | ![GitHub image](Images/Primer/night_not_separated/night_not_separated_87.jpg)
No sky | 3791 | ![GitHub image](Images/Primer/no_sky/no_sky_201.jpg) | ![GitHub image](Images/Primer/no_sky/no_sky_21.jpg) | ![GitHub image](Images/Primer/no_sky/no_sky_258.jpg) | ![GitHub image](Images/Primer/no_sky/no_sky_296.jpg) | ![GitHub image](Images/Primer/no_sky/no_sky_6.jpg)

Distribution by class:

![GitHub graph](/Images/Graphs/image%20(5).png)


### Phase 2: Training and Deployment

To solve this problem, we have tried several image classifiers that classify one of four categories. To construct this classifier, we used pre-trained CNN:
 * ResNet50
 * ResNet101
 * ResNet152
 * Xception
 * VGG16
 * VGG19
 * InceptionV3
 * InceptionResNetV2
 * DenseNet201
 * DenseNet169


Eventhough most of the validation accuracy were over 80%, the best performing model were ResNet models, particulary ResNet101. The top results are as follows:
Model | Validation Accuracy
------------ | -------------
ResNet101 | 0.90902
ResNet101 | 0.90825

Best overall results were achieved with transfer-learning using pre-trained ResNet101 an re-train it on our data in ImageNet - 50 epoch, Batch size - 15; Accuracy 90,9%.

### Phase 3: Validation

Validation of the model results was done on Valiadtion set and on about 30 new images. 

Evaluation matix:

Class Name | Precision | Recall | f1-score
------------ | ------------- | ------------- | ------------- 
Daylight Sky | 0.91 | 0.93 | 0.92
Night sky separated | 0.76 | 0.66 | 0.70
Night sky not separated | 0.79 | 0.80 | 0.80
No sky | 0.93 | 0.93 | 0.93

Confusion matrix:

![GitHub graph](/Images/Graphs/Confusion_matrix.png)

Missclasified examples:

Class Name | Number of missed classified | Predicted Sky | Predicted Night sky | Predicted Night No_sky | Predicted No_sky  
------------ | ------------- | ------------- | ------------- | ------------- | ------------- 
Daylight Sky | 35 | | ![GitHub image](Images/Missed/Day/day_2983.jpg)| ![GitHub image](Images/Missed/Day/day_458.jpg) | ![GitHub image](Images/Missed/Day/day_463.jpg) 
Night sky separated | 34 | ![GitHub image](Images/Missed/N_sep/night_separated_123.jpg) | | ![GitHub image](Images/Missed/N_sep/night_separated_230.jpg) | ![GitHub image](Images/Missed/N_sep/night_separated_331.jpg) 
Night sky not separated | 26 | ![GitHub image](Images/Missed/N_not_sep/night_not_separated_532.jpg) | ![GitHub image](Images/Missed/N_not_sep/night_not_separated_2.jpg) | | ![GitHub image](Images/Missed/N_not_sep/night_not_separated_452.jpg) 
No sky | 40 | ![GitHub image](Images/Missed/No_sky/no_sky_736.jpg) | ![GitHub image](Images/Missed/No_sky/no_sky_1623.jpg) | ![GitHub image](Images/Missed/No_sky/no_sky_1448.jpg)  | 



## Summary of results
