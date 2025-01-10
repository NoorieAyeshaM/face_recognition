1.DESCRIPTION:

This face recognitioin code uses a pre-trained Keras model to perform real-time image classification from a live video feed. It captures frames from the camera, resizes and normalizes them, and then predicts the class and confidence score for each frame. The results are displayed on the video feed with the predicted class and score overlayed. The program runs continuously until the user presses 'q' to quit.

2.INSTALLATION:

python 3.9

Pycharm Community Edition

3.FEATURES:

Highlights of the project:

Live video feed with predictions displayed in real-time.

Confidence scores for each prediction.

Easy-to-adapt code for custom models and datasets.

4.REQUIREMENTS:
PYTHON 3.9(interpreter)

The required dependencies and libraries:(THIS HAS TO BE DONE IN THE TERMINAL OF PYCHARM)

1.Install TensorFlow 2.10.0:
pip install tensorflow==2.10.0

2.Install Numpy (compatible version):
pip install numpy==1.21.6
set CUDA_VISIBLE_DEVICES=-1

3.Install OpenCV with  GUI suport
pip install opencv-python==4.5.5.64

5. FILE STRUCTURE:
   
Purpose of key files:

keras_model.h5: Pre-trained Keras model file.

labels.txt: Text file with class names for the model.

face_recognition.py: Main Python script for running the program.

6. HOW IT WORKS:
   
Workflow:

The script loads the model and labels.

Opens the default camera and captures video frames.

Each frame is resized and normalized before being passed to the model for prediction.

The predicted class and confidence score are displayed on the video feed.


7. CUSTOMIZATION:
    
How users can adapt the code:

Replace keras_model.h5 with a custom model trained for their use case.

Update labels.txt with corresponding class names.

Change the video source (e.g., use a video file instead of a camera).

8. TROUBLESHOOTING:
   
Common issues and their solutions:

Camera Not Accessible: Ensure no other application is using the camera.

Model/Labels Not Found: Verify the paths to keras_model.h5 and labels.txt.

OpenCV Errors: Check if the camera is functioning properly.

9.STEPS TO BE FOLLOWED TO TRAIN THE MODEL:

1.Search for google teachable machine

![pic-1](https://github.com/user-attachments/assets/0bc2094c-8aaa-4e51-82d3-3476b2a0a6a8)

2.Select get started

![oic-2](https://github.com/user-attachments/assets/5c34d813-eed1-4b91-b4e5-d759b812edc8)



3.Select image project

![pic-3](https://github.com/user-attachments/assets/c232140d-5840-4d6f-8c6d-a3441ee5ea1e)



4.Select standard image model

![pic-4](https://github.com/user-attachments/assets/6b1c9f6f-aa0a-47f0-aada-8829c62e3ef1)

5.add class name (eg.yourname) click on web cam and record your face with 3-4 angles,train the model and then check the output then export the model

![pic-5](https://github.com/user-attachments/assets/0abe8da3-783f-4e2e-904f-d3434e6b8e4b)

6.Select Tensorflow----OpenCVKeras----Download my model

![pic-6](https://github.com/user-attachments/assets/d1bc8541-c3db-4de9-8e5e-d281d7baeffd)

