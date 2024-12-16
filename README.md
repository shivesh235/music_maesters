# Music Maesters

---

## **Project Overview**

This project is a Flask-based web application that generates music based on a user's detected facial expression, gender, dominant color in the captured video feed, and age. It leverages OpenCV for video processing, the FER (Facial Expression Recognition) library for emotion detection, and an **AudioLDM** pipeline to synthesize music based on generated prompts.

---

## **Features**

- **Live Video Feed**: Captures video frames from the webcam.
- **Facial Detection**: Detects faces in the frame using a DNN-based model from OpenCV.
- **Emotion Recognition**: Identifies the dominant emotion using the FER library.
- **Age and Gender Detection**: Predicts the user’s age and gender using pre-trained DNN models.
- **Dominant Color Extraction**: Determines the most dominant color in the frame for additional mood classification.
- **Music Prompt Generation**: Generates descriptive prompts for music synthesis based on:
  - Gender
  - Detected emotion
  - Dominant color tone (bright/dull)
  - Age group
- **Audio Generation**: Uses the **AudioLDM2 pipeline** to create music based on the generated prompts.
- **Web Interface**: A Flask-based UI for displaying the live video feed, the generated prompts, and downloading the synthesized audio file.

---

<img src="https://github.com/shivesh235/sound_scene_synthesis/blob/master/Web-UI/frosthack_muzic-main/assests/images/6.png" height=500px>

## **Prerequisites**

### **Hardware Requirements**
- Webcam for capturing live video feed.
- GPU (optional but recommended for faster audio generation with **AudioLDM2**).

### **Software Requirements**
- Python 3.8 or higher
- Libraries:
  - Flask
  - OpenCV
  - FER
  - Diffusers
  - PyTorch
  - NumPy
  - SciPy
  - Random
  - Collections

---

## **Setup Instructions**

1. **Clone the Repository**
   ```bash
   git clone <repository_url>
   cd <repository_directory>
   ```

2. **Install Dependencies**
   Create a virtual environment and install the required libraries.
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
   pip install -r requirements.txt
   ```

3. **Download Pre-Trained Models**
   Ensure the following pre-trained models are present in the working directory:
   - `opencv_face_detector_uint8.pb` and `opencv_face_detector.pbtxt` for face detection.
   - `age_net.caffemodel` and `age_deploy.prototxt` for age prediction.
   - `gender_net.caffemodel` and `gender_deploy.prototxt` for gender prediction.
   - The **AudioLDM2** model:
     ```bash
     pip install diffusers
     ```

4. **Static Directory**
   Place the audio files in the `static/audio/` directory for serving.

5. **Run the Application**
   Launch the Flask application:
   ```bash
   python app.py
   ```
   The application will be available at `http://127.0.0.1:5000`.


---

## **Usage Instructions**

1. **Access the Web App**
   Open the application in a web browser.

2. **Live Video Feed**
   - The webcam feed will automatically display in the browser.
   - Detected faces, gender, age, and emotions will appear as overlays on the video.

3. **Generate Music**
   - Once the application identifies a face, emotion, and other parameters, a music prompt will be generated.
   - Click the "Generate Music" button to create a custom audio track.

4. **Download the Audio**
   - After the audio is generated, a link will appear to download the MP3 file.

---

## **Core Functions**

### **Video Processing**
- `gen_frames()`: Captures webcam frames, detects faces, and overlays emotion, age, and gender predictions.

### **Prompt Generation**
- `generate_prompt(frame, gender, mood, age)`: Combines image, facial, and demographic data to create a text prompt for the AudioLDM2 model.

### **Music Synthesis**
- `get_mp3_file(prompt)`: Generates audio using the AudioLDM2 pipeline based on the generated text prompt.

### **Dominant Color Detection**
- `find_dominant_color(image, k=3)`: Uses K-Means clustering to detect the most dominant color in the image.

### **Brightness Detection**
- `is_bright(image, threshold=100)`: Determines whether the image is bright or dull based on average pixel intensity.

---


---

## **Future Improvements**

- Add more robust age classification using a fine-tuned deep learning model.
- Support additional audio styles or genres based on specific moods or demographics.
- Optimize performance for large-scale deployment.

---
