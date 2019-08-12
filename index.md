---
layout: default
youtubeId: 0SFDhEOsj78
---
One of the more visible Artificial Intelligence explorations is in the area of Computer Vision.  In this area, the applications are aplenty including Automonous Vehile driving, X-ray analysis of tumors, etc.  Specifically in Computer Vision Analysis [**YOLOv3 You Only Look Once**](https://pjreddie.com/darknet/yolo) is about the fastest opensource with the use of tensorflow training.  [Tensorflow] (https://www.tensorflow.org/) is by GOOGLE and openly available.  As of August 2019, it is in version 2.0B  The concept of using **tensorflow** is to use it to define the CNN model and train it against a set of labelled datasets so that subsequent programs can be used to predict with a certain amount of _accuracy_ Using tensorflow framework, one normally define the steps using [**python**](https://www.python.org/)

There is no way to dive into each topic as one can really go DEEPLY into deeplearning and some will even say you need to be good at mathematics, linear Algebra etc.  There is no end to all the learning one can do.  But as **Confucious** says 

> I hear and I forget. I see and I remember. I do and I understand

Additionally, one should use [**UBUNTU**](https://ubuntu.com/) as the operating system to run these codes.  And very soon, you will realise that you will need to know unix commands and learn about leveraging CUDAs and GPU from NVIDIA.  Each letter is yet another topic all by itself.  So, its actually very daunting to learn all these and at the same time, there are **moving parts** such as version changes of the softwares.  Hence, [**GITHUB**](https://github.com/) is used as a repository of explorations by other like minded coders who willingly share their codes.

The GITHUB makes sharing and learning one of the fastest as you can get to see how codes are written and how they are being used.  Learning to read codes is basic.  Then coding and debugging.  

# Basic VIDEO Analysis using YOLOv3 with Tensorflow v2.0

**Background**  I chose Personal Mobile Devices PMDs as this is specific to Singapore. There are lots of situation where PMDs are causing accidents around Singapore and enforcement is bad.  So, if anyone can use their mobile phones to capture videos and PMDs are recognised, and if SPEED can be recorded etc, then it can come in very useful.  So in the decomposition of things to do, there are many elements of this "goal/project" -

Recognise with acceptable processing speed (fps) and identify a PMD
Calculate the SPEED of the PMD, perhaps to even analyse the picture to extract out the Registration NUMBER ( using OpenCV ?)
Create this mobile APP ( Android and IPHONE ) to take the model and use it on the phone.

In the real world, the EYE SURGEON while he/she is a SURGEON, he/she will not be able to operate on the HEART.  So, you have to have Andriod Studio MOBILE development (JAVA) skills, IPHONE XCODE (SWIFT) skills, UBUNTU Python and Tensorflow skills.  And move around these boxes without SPENDING A BOMB and taking 10 years. 

So PART 1 must happen 1st - RAW tensorflow YOLOv3 analysis ( before training )

Here's the video of the analysis of a Straits Times video that I captured

{% include youtubePlayer.html id=page.youtubeId %}

### Small image

![Octocat](https://github.githubassets.com/images/icons/emoji/octocat.png)

### Large image

![Branching](https://guides.github.com/activities/hello-world/branching.png)


### Acronymns 

<dl>
<dt>YOLO</dt><dd>You Only Look(not live) Once</dd>
</dl>
