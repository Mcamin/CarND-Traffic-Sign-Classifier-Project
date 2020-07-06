## Project: Build a Traffic Sign Recognition Program
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

[//]: # (Image References)

[im01]: ./imgs/Training.png "Distribution of training data"
[im02]: ./imgs/Traffic_sign_examples.png "Traffic signs contrast and brightness"

The Project
---
The goals / steps of this project are the following:
* Load the data set
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report


Overview
---
In this project, i will apply what you've learned about deep neural networks and convolutional neural networks to 
classify traffic signs using TensorFlow (reaching 96.68% accuracy). The highlights of this solution would be data 
exploration, data preprocessing, training, testing and analyzing the performance of 2 models, testing the best model 
on some images from the web.

Dataset exploration
---
The [German Traffic Sign Dataset](http://benchmark.ini.rub.de/?section=gtsrb&subsection=dataset) consists of 34,799 
32×32 px color images that we are supposed to use for training, and 12,630 images that we will use for testing. 
Each image is a photo of a traffic sign belonging to one of 43 classes, e.g. traffic sign types.

Each image is a 32×32×3 array of pixel intensities, represented as [0, 255] integer values in RGB color space. 
Class of each image is encoded as an integer in a 0 to 42 range. Dataset is very unbalanced, and some classes are 
represented way better than the others. 

![alt text][im01]

The images also differ significantly in terms of contrast and brightness, so we will need to apply some kind of 
histogram equalization, this should noticeably improve feature extraction.

![alt text][im02]

Dataset preprocessing
---
The usual preprocessing in this case would include normalizing the images ( changing pixels values to [0, 1] as 
currently they are in [0, 255] range). Looking at the images, histogram equalization 
may be helpful as well. I will apply adaptive histogram equalization (CLAHE), as it seems to improve feature extraction 
even further in our case.

I will only use a single channel in my model, e.g. grayscale images instead of color ones. As Pierre Sermanet and Yann 
LeCun mentioned in their paper, using color channels didn't seem to improve things a lot.


Architecture 
---
I first tried with a standard LeNet architecture which when trained for 50 epochs, learning rate of 1e-3 and a batch size
of 128, the model achieved almost 96% accuracy. The only change that was made in the preprocessing phase, the use of 
Xavier initialization and the use of dropout. 
I then trained a VGG16 model which for the same parameters gave a better results with 96.6% accuracy. 

Results 
---
After a couple of fine-tuning training iterations this model scored 96.6% accuracy on the test set, which is fair 
enough. As there was a total of 12,630 images that we used for testing, apparently there are some examples that the 
model could not classify correctly like the Children crossing Sign download from the web which can be due to the fact 
that no augmentation was applied to the images, as the images used for the training were well cropped and centered 
whereas the last image used for testing had a background, and was inclined towards the right edge.
random crops, rotating images might be helpful in that case to enable the model to better identify the traffic signs. 

