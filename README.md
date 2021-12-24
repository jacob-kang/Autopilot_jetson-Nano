# Autopilot_jetson-Nano  
This repository is about team project in 'Deep learning class' in Hanbat National University _(advisor : prof.KyunTae Lim)_.  
And I was a **team leader** and whole period was 4 weeks project.  
![entire](https://user-images.githubusercontent.com/88817336/146987758-1b7884a5-79c5-464d-a4e1-1c091abf32c1.gif)



# Introduction
**Autopilot**'s interest is increasing without interupt.  
Lots of big company such as Amazon, Tesla, Uber etc. research Autopilot area these day and They are looking for great developer and the popularity may look likely to go further.  
But It is not easy to pracitce or test your model with real car. (hard to hack your car (Is it even possible?) or too danger)  

With Nvidia Jetson Nano and Jetbot AI kid, You can practice Autopilot technology and it is really helpful to get a sense how The Autopilot works.  
  
In this reposityry, We are introducing about our Autopilot project.  
And If you are studying Autopilot with Jetson Nano and Jetson robot or not, It might be helpful.  
  
# Preparation
  
## Jetson Nano
> NVIDIA® Jetson Nano™ Developer Kit is a small, powerful computer that lets you run multiple neural networks in parallel for applications like image classification, object detection, segmentation, and speech processing. All in an easy-to-use platform that runs in as little as 5 watts.

As you can see the above quatation, You can practice some AI models with [Jetso nano](https://developer.nvidia.com/embedded/jetson-nano-developer-kit).  
Jetson nano is just small grphic card so you are able to train models (but only light weight model).  

## Jetson robot
In jetson nano, Models can be trained and inference.  
With inferenced information, Jetson robot can move what you trained. (We used '[Waveshare Jetbot AI kid](https://www.nvidia.com/en-us/autonomous-machines/embedded-systems/jetbot-ai-robot-kit)'.)  

# Project detail
Our Autopilot is configured **Road following, Collision Avoidance, Object detection**. (You can see the details lower part)

The flow chart is like below image.  
![Algorithm flow chart](https://user-images.githubusercontent.com/88817336/146943975-d4aa3aa6-675b-426c-bf05-90442dd13bac.JPG)
  
Green is Regression model, Red is Classification model.

## Model
There are 3 models for this project and 1 xml file for face recognition of OpenCV.
* LR_best_model_trt.pth
* block_free_model_trt.pth
* road_following_model_trt.pth

* haarcascade_frontalface_default.xml

### 1. LR_best_model_trt.pth
This bases on resnet18 and is converted as [TensorRT](https://developer.nvidia.com/tensorrt).  
And this model is for Left / Right decision. We are trained this model with more than 400 images.
  
We took pictures included these images.  
#### Left
Left road sign / Car toy  
<img src="https://user-images.githubusercontent.com/88817336/146966539-caeddd62-fc05-4515-8611-ee4cfd12d391.JPG" width="15%" height="15%"/></center>
<img src="https://user-images.githubusercontent.com/88817336/146966542-38971a56-5274-4c14-8ca9-156750a0c9b3.png" width="20%" height="20%"/></center>  

![left](https://user-images.githubusercontent.com/88817336/146988903-10f6d049-b05e-487a-bfd4-9e501df37063.gif)  



#### Right
Right road sign  
<img src="https://user-images.githubusercontent.com/88817336/146966728-3d459ab9-e613-4212-9966-755e9152b3c8.JPG" width="15%" height="15%"/></center>  
![right](https://user-images.githubusercontent.com/88817336/146988907-705e5eef-a224-4cfb-9914-ba1d40c4d95d.gif)  
### 2. block_free_model_trt.pth
This bases on resnet18 and is converted as [TensorRT](https://developer.nvidia.com/tensorrt) too.  
And this model is used like object detection.  
This model detects object in front of jetbot. If it detects something, It inferences as Block.  

### 3. road_following_model_trt.pth
This bases on resnet18 and is converted as [TensorRT](https://developer.nvidia.com/tensorrt).  
This model trained the track which is served when We buy jetbot.  
Our jetbot settings are these.  

* speed_gain_slider = 0.20  
* steering_gain_slider = 0.05  
* sttering_dgain_slider = 0.0  
* sttering_bias_slider = 0.0  
(These parameter must differ every jetbot. So You need to find your fit parameters.)  

![road following](https://user-images.githubusercontent.com/88817336/146989056-1c702036-9620-4c2e-aeb2-d02cbe94482e.gif)  
  
### 4. haarcascade_frontalface_default.xml  
This is from openCV face detection model named [haarcascade](https://docs.opencv.org/3.4/db/d28/tutorial_cascade_classifier.html).  
We used this model to mosaic person's face during recording when the jetbot is running.  
In this project, We consered about personal privacy policy.  
Many company gathers autopilot data without caring people's privacy. That's why we use cascade model.  

## Function
#### avoidance()  
After left or right decision, Our jetbot calls avoidance().  
You can find these in Main.ipynb.  
```
def left_avoidance():
  ...
  
def right_avoidance():
  ...
```
If LR_best_model decides left, It calls left_avoidnace() and It decides the other sides, It calls right_avoidance().  
So our jetbot can avoid obstructions on the road.  


#### preprocess()  
This method makes ndarray to tensor array then normalize the tensor with mean, standard.  
and return the tensor **half**.  
