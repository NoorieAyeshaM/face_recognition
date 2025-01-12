1.DESCRIPTION:

This face recognitioin code uses a pre-trained Keras model to perform real-time image classification from a live video feed. It captures frames from the camera, resizes and normalizes them, and then predicts the class and confidence score for each frame. The results are displayed on the video feed with the predicted class and score overlayed. The program runs continuously until the user presses 'q' to quit.

2.FEATURES:

Live video feed with predictions displayed in real-time.

Confidence scores for each prediction.

Easy-to-adapt code for custom models and datasets.

3.PREREQUISITES:

PYTHON 3.9(interpreter)

Pycharm Community Version

A pre-trained face model from Google Teachable Machine

4. FILE STRUCTURE:

keras_model.h5: Pre-trained Keras model file.

labels.txt: Text file with class names for the model.

face_recognition.py: Main Python script for running the program.

5. HOW IT WORKS:
   
Workflow:

The script loads the model and labels.

Opens the default camera and captures video frames.

Each frame is resized and normalized before being passed to the model for prediction.

The predicted class and confidence score are displayed on the video feed.

5. CUSTOMIZATION:
    
How users can adapt the code:

Replace keras_model.h5 with a custom model trained for their use case.

Update labels.txt with corresponding class names.

Change the video source (e.g., use a video file instead of a camera).

6.STEP BY STEP PROCEDURE TO MAKE THE PROJECT RUN SUCCESSFULLY:

Step 1: Install Python and PyCharm :

Download Python from python.org/downloads and install it on your system. During installation, ensure you check the box to add Python to your PATH.

Install PyCharm:

STEP 1:Download PyCharm from jetbrains.com/pycharm/download and install it. PyCharm will serve as your development environment to write and execute Python programs. 

STEP 2: Create a New Python Project in PyCharm Launch PyCharm and select New Project. Choose a project directory and ensure Python is selected as the interpreter.

STEP 3: Create a Python File In the project folder, right-click and select New > Python File. Name the file face_recognition_py. 

STEP 4: Import Required Libraries Open the main_.py file.

1.Install TensorFlow 2.10.0:
pip install tensorflow==2.10.0

2.Install Numpy (compatible version):
pip install numpy==1.21.6
set CUDA_VISIBLE_DEVICES=-1

3.Install OpenCV with  GUI suport
pip install opencv-python==4.5.5.64

STEP 5: Load a Pre-Trained Face Detection Model use google teacheable Machines to create pre trained model using the steps

7.STEPS TO BE FOLLOWED TO TRAIN THE MODEL:

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

8.COMPLETE CODE:

from keras.models import load_model
import cv2
import numpy as np
import os

# Disable scientific notation for clarity
np.set_printoptions(suppress=True)

# Verify model and labels file paths
model_path = r"C:\Users\noori\PycharmProjects\face_recognition\keras_model.h5"
labels_path = "labels.txt"

if not os.path.exists(model_path):
    print("Error: keras_model.h5 not found.")
    exit(1)

if not os.path.exists(labels_path):
    print("Error: labels.txt not found.")
    exit(1)

# Load the model
model = load_model(model_path, compile=False)

# Load the labels
class_names = [line.strip() for line in open(labels_path, "r").readlines()]

# Open video source (0 for default camera, or specify file path for video file)
cap = cv2.VideoCapture(0, cv2.CAP_DSHOW)

# Check if the video source is opened successfully
if not cap.isOpened():
    print("Error: Unable to access the camera.")
    exit(1)

print("Press 'q' to exit.")

while True:
    ret, frame = cap.read()  # Capture a frame
    if not ret or frame is None:
        print("Error: Failed to capture a frame. Exiting...")
        break

    # Resize the frame
    try:
        resized_frame = cv2.resize(frame, (224, 224), interpolation=cv2.INTER_AREA)
    except cv2.error as e:
        print(f"OpenCV error during resizing: {e}")
        break

    # Normalize the image for the model
    image = np.array(resized_frame, dtype=np.float32)
    image = np.expand_dims(image, axis=0)  # Add batch dimension
    image = image / 255.0  # Normalize pixel values to [0, 1]

    # Predict using the model
    prediction = model.predict(image)
    index = np.argmax(prediction)
    class_name = class_names[index]
    confidence_score = prediction[0][index]

    # Print prediction and confidence score
    print(f"Class: {class_name} | Confidence Score: {np.round(confidence_score * 100, 2)}%")

    # Overlay the prediction text on the frame
    cv2.putText(frame, f"{class_name}: {np.round(confidence_score * 100, 2)}%", (10, 30), cv2.FONT_HERSHEY_SIMPLEX, 1, (255, 0, 0), 2)

    # Display the frame
    cv2.imshow("Live Feed", frame)

    # Break the loop on pressing 'q'
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

# Release resources
cap.release()
cv2.destroyAllWindows()

9.TROUBLESHOOTING:

Camera Not Accessible: Ensure no other application is using the camera.

Model/Labels Not Found: Verify the paths to keras_model.h5 and labels.txt.

OpenCV Errors: Check if the camera is functioning properly.

