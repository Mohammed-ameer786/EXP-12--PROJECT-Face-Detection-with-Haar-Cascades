# EX. NO. 12

# FACE DETECTION USING HAAR CASCADES WITH OPENCV AND MATPLOTLIB

## AIM

To write a Python program using OpenCV to perform the following image manipulations:

i) Extract ROI from an image.  
ii) Perform face detection using Haar Cascades in static images.  
iii) Perform eye detection in images.  
iv) Perform face detection with label in real-time video from webcam.

## SOFTWARE REQUIRED

1. Anaconda – Python 3.7 or above
2. OpenCV library (`opencv-python`)
3. Matplotlib library (`matplotlib`)
4. Jupyter Notebook or VS Code

## ALGORITHM

### I) Load and Display Images

**Step 1:** Import the required packages: NumPy, OpenCV, and Matplotlib.

**Step 2:** Load the input image using `cv2.imread()`.

**Step 3:** Convert the image into grayscale using `cv2.cvtColor()`.

**Step 4:** Display the image using `plt.imshow()`.

### II) Extract ROI from an Image

**Step 1:** Select the required region from the image using array slicing.

**Step 2:** Extract the Region of Interest (ROI).

**Step 3:** Display the extracted ROI.

### III) Load Haar Cascade Classifiers

**Step 1:** Load the face and eye cascade XML files using `cv2.CascadeClassifier()`.

**Step 2:** Check whether the classifiers are loaded successfully.

### IV) Perform Face Detection in Images

**Step 1:** Define a function `detect_face()`.

**Step 2:** Copy the input image.

**Step 3:** Detect faces using `face_cascade.detectMultiScale()`.

**Step 4:** Draw rectangles around the detected faces.

**Step 5:** Return the processed image.

### V) Perform Eye Detection in Images

**Step 1:** Define a function `detect_eyes()`.

**Step 2:** Copy the input image.

**Step 3:** Detect eyes using `eye_cascade.detectMultiScale()`.

**Step 4:** Draw rectangles around the detected eyes.

**Step 5:** Return the processed image.

### VI) Perform Face Detection Using Webcam

**Step 1:** Capture video using `cv2.VideoCapture(0)`.

**Step 2:** Read video frames continuously.

**Step 3:** Detect faces in each frame.

**Step 4:** Draw rectangles and labels around detected faces.

**Step 5:** Display the processed video.

**Step 6:** Press ESC to exit and release the webcam.

## PROGRAM

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Load the image
img = cv2.imread("face.jpg")

if img is None:
    raise FileNotFoundError("Image not found!")

# Convert image to grayscale
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

# Display original image
plt.figure(figsize=(8, 6))
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis("off")
plt.show()

# Extract ROI
roi = img[50:250, 50:250]

plt.figure(figsize=(6, 4))
plt.imshow(cv2.cvtColor(roi, cv2.COLOR_BGR2RGB))
plt.title("Region of Interest (ROI)")
plt.axis("off")
plt.show()

# Load Haar Cascade classifiers
face_cascade = cv2.CascadeClassifier(
    cv2.data.haarcascades + "haarcascade_frontalface_default.xml"
)

eye_cascade = cv2.CascadeClassifier(
    cv2.data.haarcascades + "haarcascade_eye.xml"
)

# Check cascade files
if face_cascade.empty() or eye_cascade.empty():
    raise RuntimeError("Haar Cascade files could not be loaded!")

# Face detection function
def detect_face(image):
    result = image.copy()

    gray_img = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

    faces = face_cascade.detectMultiScale(
        gray_img,
        scaleFactor=1.1,
        minNeighbors=5
    )

    for (x, y, w, h) in faces:
        cv2.rectangle(result, (x, y), (x+w, y+h), (255, 255, 255), 3)

    return result

# Eye detection function
def detect_eyes(image):
    result = image.copy()

    gray_img = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

    eyes = eye_cascade.detectMultiScale(
        gray_img,
        scaleFactor=1.1,
        minNeighbors=5
    )

    for (x, y, w, h) in eyes:
        cv2.rectangle(result, (x, y), (x+w, y+h), (255, 255, 255), 3)

    return result

# Display face detection result
face_result = detect_face(img)

plt.figure(figsize=(8, 6))
plt.imshow(cv2.cvtColor(face_result, cv2.COLOR_BGR2RGB))
plt.title("Face Detection")
plt.axis("off")
plt.show()

# Display eye detection result
eye_result = detect_eyes(img)

plt.figure(figsize=(8, 6))
plt.imshow(cv2.cvtColor(eye_result, cv2.COLOR_BGR2RGB))
plt.title("Eye Detection")
plt.axis("off")
plt.show()

# Real-time face detection using webcam
cap = cv2.VideoCapture(0)

if not cap.isOpened():
    raise RuntimeError("Could not open webcam!")

while True:
    ret, frame = cap.read()

    if not ret:
        print("Failed to capture frame!")
        break

    gray_frame = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)

    faces = face_cascade.detectMultiScale(
        gray_frame,
        scaleFactor=1.1,
        minNeighbors=5
    )

    for (x, y, w, h) in faces:
        cv2.rectangle(frame, (x, y), (x+w, y+h), (0, 255, 0), 2)
        cv2.putText(
            frame,
            "Face Detected",
            (x, y-10),
            cv2.FONT_HERSHEY_SIMPLEX,
            0.7,
            (0, 255, 0),
            2
        )

    cv2.imshow("Real-Time Face Detection", frame)

    if cv2.waitKey(1) & 0xFF == 27:
        break

cap.release()
cv2.destroyAllWindows()
```

## DEVELOPED BY

**Name:** ___________________________________

**Register No:** _______________________________

## OUTPUT

### 1. Original Image

- The input image is loaded and displayed.
  <img width="1080" height="573" alt="image" src="https://github.com/user-attachments/assets/f0263534-08c5-4062-bf12-ddc221f0b101" />

- The original image is displayed in RGB format.

### 2. ROI Extraction

- A Region of Interest (ROI) is extracted from the input image.
  
- The selected region is displayed separately.
  <img width="975" height="506" alt="image" src="https://github.com/user-attachments/assets/25a5cc96-fc7d-4b8a-b8d8-4850a85f803e" />


### 3. Face Detection

- The input image is displayed.
- Detected faces are highlighted using rectangular boxes.

<img width="902" height="703" alt="image" src="https://github.com/user-attachments/assets/78c1b872-42b0-45d3-82cf-b09bfe5a8ea4" />


### 4. Eye Detection

- The input image is displayed.
- Detected eyes are highlighted using rectangular boxes.

<img width="1012" height="658" alt="image" src="https://github.com/user-attachments/assets/9d7f4ac1-b91f-45a4-839b-945119df7e3e" />


### 5. Real-Time Face Detection Using Webcam

- Webcam video is captured and displayed.
- Detected faces are highlighted using rectangles.
- A label is displayed above the detected face.
- Pressing ESC exits the video window.
  <img width="427" height="231" alt="image" src="https://github.com/user-attachments/assets/137038bf-d6dc-4de5-81d2-3e4586beccf3" />


## RESULT

Thus, ROI extraction, face detection, eye detection, and real-time face detection using Haar Cascades were implemented using OpenCV and Matplotlib.
