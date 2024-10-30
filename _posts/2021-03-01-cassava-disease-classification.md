---
layout: post
title: "Cassava disease classification"
---

Cassava is an important provider of carbohydrates in Africa and is therefore keyto the nutrition of a large part of the population of the continent. The plant can be affected by several diseases that result in lower yields.  Identifying them can be beneficial to food security. To help solve this problem, machine learning has been employed to identify diseases in pictures of cassava leaves. The data collected to make this possible was made available in the iCassava-2019 competition [^1]. During our computer vision class at AMMI we were required to work on this datset as part of an In-Class Kaggle competition which my team (Simon Bassey and I) won. In this blogpost I will describe our thought process and the simple methods we used.

# Data 

The dataset is made of cassava leaves images separated into 5 classes. Four of the class represents a disease and the last one is for healthy leaves. 
Below is a list of some observations we made on the data.
- The data is noisy. There were probably a few labeling mistakes.
- The dataset was not large. There was a total of 5656 labeled images.
- The dataset was highly imbalanced. The largest class had 2658 images and the smallest one had 316 images. 
- The data had low inter-class variance. The differences from one class to another were small and hard to notice.

# Experiments

## Dealing with the properties of the data

Here is a list of the ideas used to deal with the various properties of the data.
- To deal with the noisiness and the small dataset size of the data we used data augmentation. We kept it to a minimum since agressive augmentation can slow down the convergence rate.
- To deal with the imbalance we tried to use balanced sampling, however it became unclear how how to read the performance metrics so we dropped it.
- To deal with the low inter-class variance we used large image sizes in orderfor the model to be able to identify smaller patterns and details. Image sizes ranged from 400 to 600.

## First experiment

Our first try used the starter notebook provided to us. We used a pretrained SEResNext 50 trained on 80% of the data. The augmentations used were vertical and horizontal flips. The model was trained for 12 epochs. The optimizer used was an Adam optimizer with hypergradient descent [^2]. The learning rate was set to 1e-4 and the hypergrad learning rate was set to 1e-9. The optimizer was not changed. We used hypergradient descent in order to avoid tuning the learning rate. We replaced the average pooling layer by an adaptive pooling of 1 by 1. That was enough to reach 90.5% accuracy on the public leaderboard.

## Improvements

Here is a list of changes and the improvements they made.
- Change from SE ResNext 50 to Change from SE ResNext 101. Improvement to 0.909
- Add random erasing augmentation. No improvement
- Add test time augmentation.
- Reduce the number of epochs to 5. Improvement to 0.913
- Cross validation. No improvement, with both 5 fold and 6 fold crossvalidation.
- EfficientNets, ResNets did not provide any improvement
  
The final best model was a SE ResNext 101 trained for 5 epochs on 90% ofthe data. The image size was 500 with ten 448 sized crops taken from the image and its horizontal flip for augmentation.

# Conclusion

The dataset had multiple properties that made classification difficult, like class imbalance, small number of data samples, low inter-class variance. Our final model used a pretrained SE ResNext 101 trained for 5 epochs. Possible improvements include using better augmentation strategies. Center cropping was used during training instead of random cropping,  which was only noticed on the last day. Also using larger images could help.


...

[^1]: Ernest Mwebaze, Timnit Gebru, Andrea Frome, Solomon Nsumba, Jeremy Tusubira, [iCassava 2019 Fine-Grained Visual Categorization Challenge (2019)](https://arxiv.org/abs/1908.02900), arXiv:1908.02900
[^2]: Atilim Gunes Baydin, Robert Cornish, David Martinez Rubio, Mark Schmidt, Frank Wood, [Online Learning Rate Adaptation with Hypergradient Descent (2017)](https://arxiv.org/abs/1703.04782), arXiv:1703.04782
