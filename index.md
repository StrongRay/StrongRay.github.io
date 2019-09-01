# Custom Object Detection

Object detection is the ability for the computer to recognize the image as if it’s recognized by the human eye.  This is Computer Vision 101 and the basis for Autonomous Vehicles and other detection like X-Rays, production line, Security Monitoring, etc.  However, a 4 frame per second is totally useless in the real world.  I wanted to see if I can do some custom deep learning to “program” a model to recognize objects.  Obviously, there is no thrill in doing the “Cats and Dogs” thing or “Types of Flowers” 
Having just attended [SGINNOVATE](https://sginnovate.com/events/AI) Red Dragon’s Advanced Computer Vision course at BASH last week, I thought (in a Singapore context) Personal Mobile Devices (PMD) might be a nice challenge given that the COCO dataset or IMAGENET doesn’t have PMDs in their dataset. 
So, would l need a couple of hundreds or at least a thousand images for custom training ? So the key questions for the exploration are as follows

1.	Can a custom object be detected using 74 labelled images ?
2.	How many training batches is sufficient ?
3.	What model can one use to train ?
4.	Where can this be best trained ?

## The Image Dataset

I selected images from google search and selected clear in perspective PMDs.  However, my scope did not include e-scooters nor MONO-wheel type of PMDs.  I realized after the training, some scenes are detected with PMD but as they fade further away, the bounding boxes disappear.  This implies that the collection of images could be further enhanced by perhaps taking a video and extracting out zooming out frames of a PMD in motion.  

Labelling is a simple but tedious job, but there are many tools available to help.  The one I chose was [VOTT](https://github.com/microsoft/VoTT).  

![Image File](/assets/images/VOIT.jpg)

Perhaps in future, such a tool can take a video and try to auto generate bounding boxes if we predefine the object on one frame.  Still, the idea is not about being perfect, but to take this through end to end.  

By sheer randomness, I decided on 74 images after discarding some.  By reading up on some posts, some say they need 400 images or even a thousand.  So the hypothesis is “Can a custom object model be created based on 74 images ?” And how accurate is enough ?  From a zero detection to possibly some detection is a good start. 
 
![Image File](/assets/images/DATA.jpg)

## Yolo-ing around

You only Look Once [YOLO](https://pjreddie.com/media/files/papers/YOLOv3.pdf) is a nice and fast model for detecting images and developed by Joseph Redmon and Ali Frahadi of University of Washington.  Mathematics aside, there are many implementations from C to Python (Tensorflow) and Pytorch.  I chose [AlexyAB Darknet fork](https://github.com/AlexeyAB/darknet) which provided an upgraded version from PKREDDIE.   

So, the GIST is the concept of Transfer Learning.  Select a trained weights from one of the model and then use it to train your dataset.  So, this is supposedly better and faster than training from scratch.  The codes FREEZE up the earlier Convoluted Neural Networks (CNN) layers and let the later layers open for data propogation and back propogation.  

After starting with darknet 53 weights and then moved to Yolov3 Tiny. Reason being, the footprint of a Yolov3 Tiny is the smallest and hence, it should technically be training faster but perhaps less accurate as it is less complex than the full Yolov3.  

## It’s all about Hyper parameters tuning 

“Setting up” the data directory, ie. Where to place the config files and data images and labels require a one time definition.  The fastest way is to get one model right and then you can build on the same model.  For me, it’s finding a ONE CLASS object detection layout.

“Programming” is nothing more than fine tuning the “parameters” of the CFG file.  These files layout the different layers and in particular, it offers a lot of detailed complex stuff that would otherwise be tedious to code.  In particular, DATA AUGMENTATION is one where the image dataset is being randomly treated with HUE, etc to bring about a slightly different image for training.  Hence, the total number of images increases from the base set of 74 that I have collected and labelled.  

It would be great to have ZOOM in and OUT as another such **data augmentation**, but this is not provided for. Either we go into the C codes to modify and add on this feature or expand the data collection part so that we expand the datasets.  

Defining BATCHes is like the number of "loops" the training will run through x number of images.  In the past, given the time in class or at home, I would think 100 is more than sufficient.  But there is NO detection =)  This leads to a very important concept of “ART vs SCIENCE” in Machine Learning.  Those who don’t see GRAPHs, will tell you it’s ART and a trial and error.  But machines and computers are not emotional or sensitive objects.  They work based on an algorithm.  Here after reading, you will see Average LOSS for each batch,  

I originally tried only 200 batches.  I later moved to 2000.  So, how does one interpret this graph ? If you do somewhere less than 25 batches, the loss is in the 2-3000s.  Ie. If you take the weights and predict an image, chances are you predict nothing =)
Now this graph makes a lot more importance as you hit < 1 loss in the 0.xxx as low we possible.  You can see the results of training here.  When I run only 1000 batches, the PMD on the left is not detected.  But when I ran at 2000 batches, the same PMD is seen.  

![Graph-1](/assets/images/BatchNo-Loss-2.jpg) 

So, you can see in the above graph, the average loss at 270 batches is still really quite BAD.  You need to bring the average loss down to < 1 at least.

![Graph-2](/assets/images/BatchNo-Loss-3.jpg) 

Here's the difference between the 2 weights file, one trained till 1000 batches and the other till 2000 batches
There are slight differences, but note the one with 2000 will detect abit more images.  Those not detected will still be true for both as the dataset doesn't include PMDs of those models.

{% include youtubePlayer.html id="DcA5VkTIP4s" %}

Before you go about training endlessly, there is a Deep Learning concept called **UNDERFITTING** and **OVERFITTING** during training.  

**Underfitting** happens when after you trained your model, your model still **CANNOT** detect anything that you want to detect, ie. The weights are not adjusted in each CNN layer such that they can identify any the features.  Likely, the training batches is too little and/or the selected images are not varied enough.   **Overfitting** is the other extreme - the model can **ONLY** detect those from the training and validation dataset and no detection for any other images that the model has never seen before.  Both models are quite useless.  The best model is to train until underfitting is the least and at the inflexion point before it becomes overfitted.  

Below is an image from a VIDEO (mp4) that I sourced from Straits Times as a source of frames that I did not expose the model to train for.  This is where the **MAGIC of Deep Learning** begins.  

The ability of Machine Learning model to predict something other than what it is trained for.  This is also termed as **SUPERVISED** Learning.  The Supervision comes from a human (me) associating images with bounding boxes and labelling them to TELL the computer to recognize the item as in this case, a PMD.    Without this “supervision”, how will the computer ever know what you mean by a PMD.  There is also UNSUPERVISED learning which is another story all together.  But unlike pure programming, where you do matching of images, the automatic weights adjustment is done for you back and forth.  Which also means that DEBUGGING process is quite difficult.  You have to play around and understand the basis of how such programs work and learn to tune it such that it picks the best strategy to give you the greatest accuracy.  The transportable skills here is in knowing why certain images are not recognised and being able to explain.  Only when one can explain, can only tune the model or collect more data images to compliment the model.  With ONE BIG ASSUMPTION - that the people in GOOGLE tensorflow or any model got their internal codes correct, much like if 1+1 is not = 2 at the Microsoft OS level, surely no amount of Application software can get this right.

![Graph](/assets/images/Batch.jpg)

So my TEST strategy before processing through the ST video is to capture certain frames and do a single IMAGE prediction based on sample images extracted from the videos that are not part of the dataset.  For if these are not predicted, there is a likely chance that the VIDEO fed through the trained model will not predict.  

So **WHERE** DO YOU WANT this training to happen?

To recap, Training is letting the software adjust the weights of the CNN model through batches of passing through labelled images so that after many rounds, the CNN model has a nicely setup weights on each layer such that if you feed it a new image, it can tell if it detects the object or not.  In my last training, I ran off my 4 CPU laptop, started at 9 pm and it ended at 2 am.  So, if the system crashed, you come back and restart the training cycle.  The moment of truth comes only when you pass this “pre-trained” weights with predicting a new image.

This brings to the next IMPORTANT topic called [**GOOGLE COLAB**][https://colab.research.google.com/] and your GOOGLE DRIVE.  Google has graciously given “free” CPU/GPU/TPU for training, provided you know how to use them.  The lowest speed is Computer Processing Unit (CPU), followed by Graphical Processing Unit (GPU) and finally the top in class is the Tensor Processing Unit (TPU).  GPU are the likes of Graphics cards that are mainly used by NVIDIA to speed up image processing and they in turn found a use in the AI world.  

Engineers who love software, but can’t typically do hardware and vice versa.  The gist of this is this – Training of these models require alot of Processing power and the more you have ( that you need not pay for ) the quicker it is to have the work (training) done.  So, learning how to use GOOGLE COLAB is very useful.  BUT, **NOT** everything of AI is PYTHON. It's like an UBUNTU environment on the cloud.  Actually a Mac is a unix box underneath too, that is another story altogether.  

A skillset of moving around COLAB is important and mounting your drive for storage of codes.  Otherwise, everything is lost in the session after you log off.  The quick summary is that I set up the codes on my laptop UBUNTU 19.4 environment, ZIP the files and upload to my GOOGLE drive, then start a COLAB session and mount my google drive to “!unzip” the file in a jupyter Notebook. 

Attending the SGINNOVATE course forced me to learn how to do this effectively.  And doing the exercise helps me to focus on the whims of this environment.  

## Everything in life is about the results ( while you are tricked into thinking it’s the process that matters )

Repeatable success can only be achieved through disciplined approach. Whether its coding or Data Science.  The keeping of a LOGbook and “Documenting your code” in a jupyter notebook helps remind yourself 3 months after you come back.  Here’s a code sniplet of the notebook showing an image predict on s25.jpg.  A high level of confidence shows that the recognition is perhaps more sure.  Adding a THRESH variable can make the system ignore any prediction less than 0.x% 

![Prediction](/assets/images/s1.png)

The following is the processed video
{% include youtubePlayer.html id="UXStERpkuQo" %}
