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



![alt text](https://user-images.githubusercontent.com/70357685/143724058-00dcfbd3-1077-43c4-815c-e9f843e2663f.JPG)

![Capture](https://user-images.githubusercontent.com/70357685/143724059-0d6b1a41-4cf0-4176-9cce-1cc639d93218.JPG)

![JetsonNano-DevKit_Front-Top_Right_trimmed](https://user-images.githubusercontent.com/70357685/143724062-3132ac08-b176-4f71-8278-bc2e4a628fe9.jpg)



Special thanks to Dusty-NV and his Jetson-Inference repository which made learning the Jetson Nano so much easier!
