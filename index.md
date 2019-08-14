---
layout: default
youtubeId: 0SFDhEOsj78
youtubeId2: 7F1HZAJaeSM
---
One of the more visible Artificial Intelligence explorations is in the area of Computer Vision.  In this area, the applications are aplenty including Automonous Vehile driving, X-ray analysis of tumors, etc.  Specifically in Computer Vision Analysis [**YOLOv3 You Only Look Once**](https://pjreddie.com/darknet/yolo) is about the fastest opensource with the use of tensorflow training. [**Tensorflow**](https://www.tensorflow.org) is by GOOGLE and openly available.  As of August 2019, it is in version 2.0B  The concept of using **tensorflow** is to use it to define the CNN model and train it against a set of labelled datasets so that subsequent programs can be used to predict with a certain amount of _accuracy_ Using tensorflow framework, one normally define the steps using [**python**](https://www.python.org/)

There is no way to dive into each topic as one can really go DEEPLY into deeplearning and some will even say you need to be good at mathematics, linear Algebra etc.  There is no end to all the learning one can do.  But as **Confucious** says 

> I hear and I forget. I see and I remember. I **do** and I understand

![Confucious](/assets/images/Confucious.jpg)

Additionally, IMHO, one should use [**UBUNTU**](https://ubuntu.com/) as the operating system to run these codes rather than WINDOWS 10 or a MAC.  And very soon, you will realise that you will need to know unix commands and learn about leveraging CUDAs and GPU from NVIDIA.  Each letter is yet another topic all by itself.  So, its actually very daunting to learn all these and at the same time, there are many **moving parts** such as version changes of the software packages.  Hence, [**GITHUB**](https://github.com/) is used as a repository of explorations by other like minded coders who willingly share their codes.  And one might end up BUILDING from SOURCE which might take an overnight run of the build if one wants a specific combination of OPENCV, CUDA and Tensorflow.  

The GITHUB makes sharing and learning one of the fastest as you can get to see how codes are written and how they are being used.  Learning to read codes is basic.  Then coding and debugging.  

# Basic VIDEO Analysis using YOLOv3 with Tensorflow v2.0

**Background**  

I chose the subject of Personal Mobile Devices PMDs as this is specific to Singapore. There are lots of PMDs causing accidents around Singapore and enforcement is bad.  MINISTER already keep saying LTA is exploring Video Analytics (AI) but it's still abit challenging.  Additional if ultimately any citizen can use their mobile phones to capture videos and the software correctly identify PMDs and if SPEED can be recorded etc, then it can come in very useful.  So in the decomposition of things to do, there are many elements of this "goal/project" -

* Recognise with acceptable processing speed (fps) and identify a PMD
* Calculate the SPEED of the PMD, perhaps to even analyse the picture to extract out the Registration NUMBER ( using OpenCV ?)
* Create and deploy the model onto a mobile phone ( Android and/or IPHONE )

In our real world, an EYE SURGEON, while he/she is a SURGEON, he/she will not be able to operate on the HEART effectively. Specialisation of any topic takes 10,000 hours.  So we don't have that long and the patience.  So, you have to have Andriod Studio MOBILE development (JAVA) skills, IPHONE XCODE (SWIFT) skills - Tried FLUTTER which allowed me to deploy a TF model on both IPHONE and ANDRIOD, UBUNTU Python and Tensorflow skills.  And move around these boxes without SPENDING A BOMB (tried VirtualBOX and installed MacOS Mojave and XCODE but cannot get my iPHONE detected as a device to deploy) and taking 10 years. 

A secondary objective is to stay mentally alert and on a learning mode.  As **internalisation** takes place only with trial and errors.

So **PART 1** must happen 1st - **RAW tensorflow YOLOv3 analysis ( before training )

Here's the video of the analysis of a Straits Times video that I captured

{% include youtubePlayer.html id=page.youtubeId %}

After a hard day's work of meddling around with TF records, I did a Transfer Training on YOLOv3 using Tensorflow 2.0 on my Ubuntu 19.04.

**PART 2 - after training, ran the video with the processing**

{% include youtubePlayer.html id=page.youtubeId2 %}

There are a few steps involved in training.  One is, of course, getting the images. Here, I went to the web and download as many images that I can search regarding PMDs.  Here's a list of them

![Dataset](/assets/images/DATA.jpg)

They come in various quality and sizes.  And I sourced for some 74 images.  The next step involved trial and error.  Initally, I used LabelImg on Ubuntu but then, it needed to generate TFrecords. The TFrecords program works from contrib in TF 1.3/1.4 and I am already on tf2.0.  Instead, I went to my Windows 10 enviroment and downloaded VOLT.

![Volt](/assets/images/VOIT.jpg)

VOLT has a nice option of exporting as TFrecords.  After the labelling and generating of tfrecords, the next step is to do the training.  The script for training has a few Quarks.  I nearly gave up.  This is when you start looking around the issues reported and I went in to change the train.py script.

![Training](/assets/images/TRAIN.jpg)

Training did not take TOO long.  And while this initial accuracy is not perfect, I think as an initial step and as a process, this looks promising.  I will then try generating a tflite version of the weights file for imbedding into FLUTTER (Andriod/IOS)  This step will be most challenging. 

### Stay Tuned for my next updates

![Octocat](https://github.githubassets.com/images/icons/emoji/octocat.png)

### Acronymns 

<dl>
<dt>YOLO</dt><dd>You Only Look(not live) Once</dd>
</dl>
