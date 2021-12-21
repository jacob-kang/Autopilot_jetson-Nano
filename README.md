# Autopilot_jetson-Nano  
This repository is about team project in 'Deep learning class' in Hanbat National University _(tought by KyunTae Lim)_.  
And I was a **team leader** and whole period was 4 weeks project.

# Introduction
**Autopilot**'s interest is increasing without interupt.  
Lots of big company such as Amazon, Tesla, Uber etc. research Autopilot area these day and They are looking for great developer and the popularity may look likely to go further.  
But It is not easy to pracitce or test your model with real car. (hard to hack your car (is it possible?) or too danger)  

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

