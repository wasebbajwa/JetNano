# The Jetson Nano
![JetsonNano-DevKit_Front-Top_Right_trimmed](https://user-images.githubusercontent.com/70357685/143724062-3132ac08-b176-4f71-8278-bc2e4a628fe9.jpg)

The Jetson Nano is a lightweight, powerful, and easy to use edge device that can be used to both train and deploy a variety of machine learning models. It comes equipped with over 4 GB of ram, as well as the Jetpack SDK which is a comprehensive solution to building and deploying end to end AI models. Installing the Jetpack SDK to the Jetson Nano is relatively simple and comes with a variety of features such as built in technologies such as Nvidia Container Runtime which comes with Docker integration, specifically, with support for  GPU enabled  containerized applications.

![Capture](https://user-images.githubusercontent.com/70357685/143724059-0d6b1a41-4cf0-4176-9cce-1cc639d93218.JPG)

The Nano provides versatility by allowing you to connect a variety of accessories such as a mouse, keyboard, wi-fi adapter and technologies such as the Intel Neural Compute Stick all at once. This makes it very easy to set up and test various AI pipelines as there isn't a need to connect to an external machine via methods such as SSH.

## Getting Started
In order to build and deploy the objection detection model in this repository, you'll first need to setup and install the Jetpack SDK. You can find the latest release here: 
https://developer.nvidia.com/embedded/jetpack

It is recommended that you purchase an SD with over 128 GB of memory , the one I used for this project was purchased here: https://www.amazon.com/SanDisk-Memory-Standard-Packaging-SDSDUNC-128G-GN6IN/dp/B0143IISD0.

After inserting the SD card into your machine, you have to format the SD card. This can be done by a variety of applications ;however, I used the one found here: https://www.sdcard.org/downloads/formatter/. Formatting the SD card is important as it completely wipes the data on the SD card to ensure that you are working with a clean slate. For the first time formatting, a quick format will suffice ; however, I did run into issues while installing other Jetpack versions on the SD card which forced me to do a full format in order to ensure there was no remnants of the original Jetpack version on the SD card.

After formatting the card, install https://www.balena.io/etcher/ and transfer the installed Jetpack version onto the SD card from your machine. After a few steps, you are ready to start up the Jetson Nano and begin exploring! One of the first changes I made after booting up the Jetson Nano was to create SWAP. Jetpack uses the Zram module for configuring memory, which in short, allows you to essentially create more memory on the Jetson Nano. More information about Zram can be found here: https://en.wikipedia.org/wiki/Zram. To enable SWAP on the Jetson Nano, open up the command prompt and copy and paste the following commands: 

``` bash
sudo systemctl disable nvzramconfig
sudo fallocate -l 4G /mnt/4GB.swap
sudo mkswap /mnt/4GB.swap
sudo swapon /mnt/4GB.swap
```
## MobileNet V1
For this project, I used transfer learning in order to speed up the process of training. With the computing power and data I used for this project, it would be impossible to train an accurate object detection model. 

![Three-ways-in-which-transfer-might-improve-learning](https://user-images.githubusercontent.com/70357685/143785100-bc11bb61-c398-4917-bd33-701328bd81d8.png)

Transfer learning is so powerful because it allows you to have a much better start when training a model. It takes a pre trained model and freezes those layers in order to build on top of what the model already learned. CNN features in early stages are more general such as learning what edges or curves are , but they get more specific later on , which allows for a great use case for transfer learning. Especially in instances such as training on an edge device where you have low amounts of computing power and memory to work with.

## MobileNet V1
Mobilenet V1 is one of Google's models which is used for transfer learning. I chose Mobilenet as the architecture makes it very efficient for training and deploying on edge devices.

![alt text](https://user-images.githubusercontent.com/70357685/143724058-00dcfbd3-1077-43c4-815c-e9f843e2663f.JPG)

The bread and butter of Mobilenet is the Depthwise Seperable Convolution. In short, it allows for a huge reduction in computation power.  It also uses a variety of other neat tricks such as a Width Multiplier a to control the number of channels, Resolution Multiplier p for reduced representation, and it also has been tested on a variety of different datasets to show its efficacy. A general introduction to Mobilenet can be found here: https://towardsdatascience.com/review-mobilenetv1-depthwise-separable-convolution-light-weight-model-a382df364b69


