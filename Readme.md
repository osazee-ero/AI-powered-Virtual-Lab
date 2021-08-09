## HAND-CONTROLLED VIRTUAL LABORATORY USING OAK-D CAMERA, TENSORFLOW AND UNITY GAME ENGINE.

This repo contains the current progress in attempting to create a virtual laboratory environment, where lab equipments can be controlled by hand gestures. The first attempt is to control the position of the mouse cursor with hand positioning.

This repo documents contains the workflow adopted in training the object detector, and linking with unity 3d game engine.

The goal of this repo/post was for submission to the [OpenCV Spatial AI competition 2021](https://opencv.org/opencv-ai-competition-2021/)


Here is the current progress in action.

<img src="images/hand1.gif" width="33.3%"><img src="images/hand2.gif" width="33.3%"><img src="images/hand3.gif" width="33.3%">
Realtime detection on video stream from a webcam .

<img src="images/chess1.gif" width="33.3%"><img src="images/chess2.gif" width="33.3%"><img src="images/chess3.gif" width="33.3%">
Detection on a Youtube video.


**Content of this document**
- Motivation - Why AI controlled Virtual Lab.
- Training the hand detection Model and Converting the trained tensorflow model to blob file format to be used in OAK-D CAMERA.
- Linking the predicted detections to unity game engine.
- How to use the files.
- Thoughts on future work.


## Motivation - Why AI powered Virtual Laboratory?

Virtual laboratory are simulated learning environments that offers the possibility of conducting otherwise physical laboratory experiments online. This could be very useful especially during these challenging times. These digital laboratories would allow students still participate in laboratory components of their studies from their homes, stay motivated while learning, as well as allow them learn complex and high-risk experiments risk-free, before using this sometimes very expensive equipment’s.  Also, schools in developing countries where there is no access to these equipment’s could benefit from this technology, as students in such schools could still utilize these expensive equipment’s.
Solution
The overall objective of the project would entail designing a working prototype of a digital 3D laboratory manipulated using visual and hand gestures. A working solution would allow a user:
- Orbit and zoom around the digital laboratory using facial expression such as eye-ball tracking for scene-view, or facial expression for zooming.
- Move and manipulate laboratory equipment’s using hand-gestures.
 To implement this, we intend to first design a realistic 3D simulator using Unity game engine and SolidWorks CAD software, then train a custom deep-learning model for translating facial expression and hand gestures captured by the OAK-D camera into commands for navigation and control of the digital equipment’s in the simulated laboratory. The depth information from the OAK camera would be very useful in the human-machine interaction for navigation and control in the system. 
 
 For this stage of the project, we are trying to implement basic hand-controlled motion.

## Training the hand detection Model

**The Egohands Dataset**

The hand detector model is built using data from the [Egohands Dataset](http://vision.soic.indiana.edu/projects/egohands/) dataset. This dataset works well for several reasons. It contains high quality, pixel level annotations (>15000 ground truth labels) where hands are located across 4800 images. All images are captured from an egocentric view (Google glass) across 48 different environments (indoor, outdoor) and activities (playing cards, chess, jenga, solving puzzles etc).


If you will be using the Egohands dataset, you can cite them as follows:

> Bambach, Sven, et al. "Lending a hand: Detecting hands and recognizing activities in complex egocentric interactions." Proceedings of the IEEE International Conference on Computer Vision. 2015.


**Tensorflow Model** 

Tensorflow offers a variety of object detection models (in the tensorflow [model zoo](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md#coco-trained-models-coco-models)) and we used the `ssd_mobilenet_v1_coco` model as the base model. 

Once training is completed, the trained inference graph (`frozen_inference_graph.pb`) is then exported, and converted to a blob file that can be deployed and saved in the examples folder in `depthai-python\models` folder. 

In order to convert your trained tensorflow model to blob file format representation, you can use this notebook (https://colab.research.google.com/drive/1Xip9MiWOJyemxyjMDURLXbeJgCzaYR1t)


## Linking the predicted detections to unity game engine.


For linking the predicted dectections with unity game engine, a TCP connection was established, the codes are located in the scripts folder of unity project and the examples folder in the python project.

## How to use the files.
**Requirements**
- Unity game engine Version 2019
- Depth AI python module


**Instructions**

- clone the repo or download the zip file.
- Place the 'ssd_mobilenet_v2_converted_from_tf.blob' model in your model folder in the depthAI python module.
- Open Unity Game engine and navigate to the VirtualLab2 directory as project directory, then launch.
- Plug in your OAK-D camera, then Run the python file modified_rgb_mobilenet.py to listen for connection from Unity.
- Play the Unity game simulation, and click "Connect", wait for connection to be established.
- Test hand control gestures.

Here is how to use it.

<img src="images/hand1.gif" width="33.3%"><img src="images/hand2.gif" width="33.3%"><img src="images/hand3.gif" width="33.3%">
Realtime detection on video stream from a webcam .

<img src="images/chess1.gif" width="33.3%"><img src="images/chess2.gif" width="33.3%"><img src="images/chess3.gif" width="33.3%">
Detection on a Youtube video.


## Thoughts on future work
This work is still very much in progress, the hand controlled gestures is far from perfect. We are implementing several solutions for seamlessly controlling the unity game characeter with the detected hand gestures,
You can use this work as a start to test your projects.


Osazee Ero, Osezua Ibhadode:  HAND-CONTROLLED VIRTUAL LABORATORY USING OAK-D CAMERA, TENSORFLOW AND UNITY GAME ENGINE  https://github.com/osazee-ero/AI-powered-Virtual-Lab

