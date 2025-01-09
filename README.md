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
