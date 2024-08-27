# Face Recognition System Using OpenCV and Caffe

## Project Overview

This project implements a face recognition attendance system using OpenCV's DNN module with a Caffe-based face detection model and OpenFace for face embeddings. The system identifies users based on their facial features and marks attendance accordingly. It includes two primary scripts:
- **`main.py`**: Follows a Kaggle notebook implementation for face recognition.
- **`test.py`**: Tests the model on a custom dataset.

#### Introduction to Model Integration
In this project, three key models work together to perform face detection and recognition:

1. Caffe-Based Face Detector (ResNet-10 SSD): This model identifies and localizes faces within images by generating bounding boxes around potential face regions. It’s efficient and suitable for real-time applications.
2. OpenFace Model: OpenFace extracts distinctive facial features by mapping images to a compact embedding space. This allows for accurate face recognition based on these unique embeddings.
3.	Face Embeddings and Recognition: The embeddings generated by OpenFace are compared with pre-stored embeddings. The system identifies faces by matching these embeddings with labeled data.

This integration enables the system to detect faces, extract their features, and predict identities with high accuracy.

## Features
- Accurate face detection and recognition.
- Supports single image per user for quick deployment.
- Custom dataset testing for accuracy evaluation.

## Folder Structure

```
Face Recognition using Caffe/
│
├── dataset/               # Contains images for training
│   └── <name>.jpg/png     # One image per user, named as their label
├── models/                # Pre-trained models
│   ├── deploy.prototxt
│   ├── res10_300x300_ssd_iter_140000.caffemodel
│   └── openface_nn4.small2.v1.t7
├── code/
│   ├── main.py            # Main script following Kaggle implementation
│   ├── test.py            # Script for testing on a custom dataset
│   └── embeddings.pkl     # Serialized embeddings and labels
└── README.md              # Project documentation
```

## Dataset

### Training Dataset

The model is trained and evaluated using a custom dataset. Each image should be named in the format <name>.extension, where <name> represents the label of the person in the image.
To test the main.py file, you can use the LFW (Labeled Faces in the Wild) dataset. 

This dataset contains labeled images of celebrities and can be used to evaluate the face recognition model. Access the LFW dataset on Kaggle [here](https://www.kaggle.com/datasets/jessicali9530/lfw-dataset/data).

### Notes

- Use high-quality images for training to improve model performance.
- PNG is recommended for high-quality images, but JPEG can be used for efficient storage.

## Setup Instructions

1. **Clone the repository:**
    ```bash
    git clone https://github.com/yourusername/face-recognition-attendance.git
    cd face-recognition-attendance
    ```

2. **Set up a virtual environment:**
    ```bash
    python3 -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    ```

3. **Install the required dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

4. **Download the Pre-trained Models:**
   - [Caffe-based Face Detector](https://github.com/opencv/opencv/blob/master/samples/dnn/face_detector/deploy.prototxt)
   - [OpenFace Model](https://github.com/cmusatyalab/openface/blob/master/models/openface/nn4.small2.v1.t7)
   - [Caffe Model](https://github.com/keyurr2/face-detection/blob/master/res10_300x300_ssd_iter_140000.caffemodel)

   Place them in the `models/` directory as shown above.

## Training

- **To generate embeddings:**
    ```bash
    python code/main.py
    ```
    This script reads images from the `dataset/` folder, extracts face embeddings using the OpenFace model, and stores them in `embeddings.pkl`.

## Testing

To test the face recognition system, follow these steps in **tests.py**:

1. **Set Up Paths**: Update the paths for the face detection model, face recognition model, test image, and embeddings file with your local directory paths. Replace the placeholder paths with the appropriate paths for your environment.

   ```python
   face_detector = cv2.dnn.readNetFromCaffe(
       'your/path/to/deploy.prototxt',
       'your/path/to/res10_300x300_ssd_iter_140000.caffemodel'
   )
   face_recognizer = cv2.dnn.readNetFromTorch(
       'your/path/to/openface_nn4.small2.v1.t7'
   )
   image_path = 'your/path/to/test_image.jpg'
   embeddings_file = 'your/path/to/embeddings.pkl'
   ```

2. **Run Prediction**: Execute the script to obtain the predicted name for the face in the specified image. Ensure that the `predict_name` function and `embeddings.pkl` file are correctly set up as described in the code.

   ```python
   predicted_name = predict_name(image_path, embeddings_file, face_detector, face_recognizer)
   print(f"Predicted Name: {predicted_name}")
   ```

This will give you the predicted name based on the test image provided. Ensure all paths and file names are updated according to your directory structure.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---
