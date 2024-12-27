---
layout: post
title:  "Beginning a new project - live bird species detection"
date:   2024-12-23 16:00:00 +0000
categories: docker machine learning
---
Recently I have been searching for a winter project to and have recently settled on a camera to detect birds visiting a bird feeder. I plan on loosely following this great guide from a youtuber called [Jeffs Pi in the Sky][jeff-yt] ([click here for his GitHub account][jeff-github]). Jeff's series was extremely useful and I'm excited to work on a project using data from close to home that can have ongoing benefits once finished. This project will involve:

- Getting a Rasberry Pi (either 3 or 4) up and running.
- Testing an object detection model on images of birds online. 
     - I want to consider multiple different models and compare them under different datasets to expand on Jeff's model. I am curious as to whether there is more recent software that could be a good alternative to Jeff's model.
     - In particular, I will try YOLOv8 - YOLOv11.
- Training a bird detection model on images of birds around our bird feeder.
- Setting up the model to detect birds live on a rasberry pi with this live stream locally available.
- Adding a log of bird arrivals to a database with new arrivals automatically put on a website.
- Running all of this with docker in a self-contained manner where we can slowly make improvements to the setup.
- In the long-run I would like to create some visualisations on the frequencies of visits of different birds at our feeders.

Software I am currently considering using (likely subject to change):

- Docker
- Conda/pyenv virtual environments for different parts of the project. Jeff uses pyenv but I normally use conda so if would like to stick with it if possible.
- Python 3.9 (or perhaps more recent)
    - ffmpeg
    - open cv
- Some kind of object detection algorithm from Tensorflow/PyTorch/Keras
    - I want to compare these methods and see if I can use a more recent model than  
- A labelling application (labellmg, Label Studio, Roboflow, Datatorch)
- Github pages to host a website with some pictures of the birds visiting the feeder. 

This will be my first major project using Docker - I have been reading up on the documentation and recently was looking into making a Dockerfile. I'm hoping after this project I will become a more proficient with the software.

[jeff-yt]: https://www.youtube.com/@jeffs_piinthesky/videos
[jeff-github]: https://github.com/jeffspiinthesky
