# MSDS_462
A repository for MSDS 462 - Computer Vision at Northwestern University

The goal of the project is to train an image classification model and deploy that model to an iOS app.  

## Attempt 1 - Melanoma Classification Using EfficientNet
Skin cancer is the most prevalent type of cancer. Melanoma, specifically, is responsible for 75% of skin cancer deaths, despite being the least common skin cancer. The American Cancer Society estimates over 100,000 new melanoma cases will be diagnosed in 2020. It's also expected that almost 7,000 people will die from the disease. As with other cancers, early and accurate detection—potentially aided by data science—can make treatment more effective.

In this competition, you’ll identify melanoma in images of skin lesions. In particular, you’ll use images within the same patient and determine which are likely to represent a melanoma. Using patient-level contextual information may help the development of image analysis tools, which could better support clinical dermatologists.

This notebook performs and exploratory data analysis of the Kaggle SIIM-ISIC Melanoma Classification competition (https://www.kaggle.com/c/siim-isic-melanoma-classification/overview) as explained above.  After the EDA was performed a model utilizing EfficientNet B6 was trained and evaluated.  The model with very little tweaking performed well and achieved an AUC of .8164 on the validation dataset.  An attempt was then made to use coremltools to convert the model to .mlmodel for integration into an iOS app.  This did not work as coremltools expects an older version of tensorflow and keras underwhich EfficientNet is not available (or at least I couldn't figure out).  Next a CNN without EfficentNet was built and the same process as above was attempted.  Despite messing around with tensorflow and keras versions I was not able to get coremltools to work.  I then decided to try Google AutoML.

## Attempt 2 - Melanoma Classification Using Google AutoML and Integration into an iOS App
This notebook explains the process of training a model on Google Vision AutoML.  First a storage bucket must be utilized, second your data should be balanced, third Googld Cloud SDK Shell helps tremendously to upload your images, fourth it was very simple to build and train a model, and fifth that model is easily downloaded to .mlmodel.  The issue then arose of integrating that model into the Apple Vision Classification Sample Project.  I haven't learned Swift, yet, and the output from the mlmodel created by Google AutoML were different than what the project was expecting.  I wasn't able to figure out how to fix this.  Next, I decided to try Apple Create ML.

## Attempt 3 - Melanoma Classification Using Create ML and Integration into an iOS APP
Create ML was extremely easy to use.  The longest part of the process was waiting for the model to train.  It was very easy to export the model to Xcode and integrate that model into the Apple Vision Classificaiton Sample Project.  This notebook shows how to train a model in Create ML and integrate that model into a working iOS app that can classify images as other, benign moles, and malignant moles.   