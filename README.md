# TerrainSense AI 🌍
### CNN-Based Terrain Classification and Rover Traversal Intelligence

TerrainSense AI is a computer vision project that uses a **Convolutional Neural Network (CNN)** to classify terrain images and translate predictions into useful terrain characteristics for rover traversal decision support.

The system identifies terrain types such as grassy, marshy, rocky, sandy, and snowy, then maps the predicted class to attributes such as roughness, slipperiness, moisture, vegetation density, and treacherousness.

The goal is to help interpret visual terrain data and support safer, more informed rover navigation decisions.

## ✨ Features

- **CNN-Based Classification:** Classifies terrain images into five terrain categories.
- **Confidence Score:** Displays the model's confidence in its predicted class.
- **Terrain Intelligence:** Maps terrain classes to traversal-related characteristics.
- **Rover Telemetry Visualization:** Presents terrain attributes in a rover-oriented dashboard.
- **Image-Based Analysis:** Accepts a terrain image for inference.
- **Scan History:** Maintains a frontend session history of analyzed images.
- **REST API:** Uses a Flask backend to connect the frontend with the trained model.
- **Prototype Interface:** Includes a web/mobile-oriented interface and a separate Streamlit prototype.

## 🏞️ Supported Terrain Classes

| Terrain | Description |
|---|---|
| 🌿 Grassy | Vegetated ground |
| 💧 Marshy | Wet or waterlogged terrain |
| 🪨 Rocky | Rock-covered or uneven terrain |
| 🏜️ Sandy | Loose sand or sandy ground |
| ❄️ Snowy | Snow-covered terrain |

## 🧠 How It Works

The system follows this pipeline:

1. **Image Input:** Upload or select a terrain image.
2. **Preprocessing:** Resize and normalize the image according to the CNN's expected input format.
3. **CNN Inference:** Run the processed image through the trained TensorFlow/Keras model.
4. **Classification:** Predict one of the five terrain classes and obtain its confidence score.
5. **Terrain Mapping:** Map the predicted class to terrain characteristics.
6. **Visualization:** Display the classification, confidence, terrain attributes, and relevant rover-oriented telemetry.

```text
Terrain Image
     |
     v
Image Preprocessing
     |
     v
Trained CNN Model
(TensorFlow / Keras)
     |
     v
Terrain Class + Confidence
     |
     v
Terrain Attribute Mapping
     |
     v
Rover Traversal Dashboard
```

## 🛠️ Tech Stack

| Component | Technology |
|---|---|
| Machine Learning | Convolutional Neural Network (CNN) |
| Model Framework | TensorFlow / Keras |
| Model Format | H5 (`.h5`) |
| Backend | Python, Flask |
| API Integration | REST API, Flask-CORS |
| Frontend | React Native, Expo, React Native Web, Vite |
| Prototype | Streamlit |
| Data Processing | NumPy, image preprocessing utilities |

## 📊 Terrain Intelligence

In addition to predicting the terrain class, TerrainSense AI maps the result to characteristics relevant to rover traversal.

| Attribute | Purpose |
|---|---|
| Roughness | Represents expected surface unevenness |
| Slipperiness | Represents potential loss of traction |
| Treacherousness | Indicates a qualitative terrain difficulty estimate |
| Moisture | Represents expected wetness |
| Vegetation Density | Represents expected vegetation coverage |
| Rover Telemetry | Visualizes terrain-related indicators for decision support |

**Important:** These attributes are derived from terrain-class mappings unless independently measured or predicted by additional models. They should not be interpreted as calibrated physical measurements or verified real-world safety assessments.

## 📁 Project Structure

```text
TerrainSense-AI/
│
├── api_server.py
│
├── model/
│   └── terrain_recognition_model.h5
│
├── mobile_app/
│   ├── package.json
│   ├── src/
│   └── ...
│
├── streamlit_app.py
├── requirements.txt
└── README.md
```

*The structure above is illustrative. Adjust filenames and folders to match your actual repository.*

## 🚀 Getting Started

### Prerequisites

- Python 3.10 or another version compatible with your installed TensorFlow release
- Node.js and npm
- Git
- A trained CNN model saved in H5 format

### 1. Clone the Repository

```bash
git clone <YOUR_REPOSITORY_URL>
cd TerrainSense-AI
```

Replace `<YOUR_REPOSITORY_URL>` with your actual GitHub repository URL.

### 2. Set Up the Python Backend

Create and activate a virtual environment:

```bash
python -m venv venv
```

Windows:

```bash
venv\Scripts\activate
```

Install the dependencies:

```bash
pip install -r requirements.txt
```

Ensure that the trained model is available at:

```text
model/terrain_recognition_model.h5
```

Start the Flask API:

```bash
python api_server.py
```

The API address, port, and available endpoints depend on the configuration in `api_server.py`.

### 3. Run the Frontend

Open a separate terminal:

```bash
cd mobile_app
npm install
npm run dev
```

Use the command supported by your frontend's `package.json`. If the project uses Expo instead of a Vite development server, start it with the configured Expo command.

Configure the frontend API URL to point to the running Flask backend.

### 4. Run the Streamlit Prototype

If `streamlit_app.py` is present and configured:

```bash
streamlit run streamlit_app.py
```

The Streamlit interface is a separate prototype and may have its own configuration.

## 🔬 Model Inference

At a high level, the model inference pipeline is:

```python
# Conceptual example — adapt to your model's input shape.
import numpy as np
from tensorflow.keras.models import load_model

model = load_model(
    "model/terrain_recognition_model.h5"
)

# Preprocess the image using the same procedure
# used during model training.
# image_array = ...

# predictions = model.predict(image_array)
# predicted_class = np.argmax(predictions[0])
# confidence = float(np.max(predictions[0]))
```

The image dimensions, normalization method, class-index mapping, and output interpretation must match the original training pipeline.

## 🧪 Evaluation and Reliability

Model quality should be evaluated on a held-out dataset that was not used for training.

Useful evaluation metrics include:

- **Accuracy:** Overall proportion of correct classifications.
- **Precision:** Reliability of predictions for each terrain class.
- **Recall:** Ability to identify examples belonging to each terrain class.
- **F1-score:** Balance between precision and recall.
- **Confusion Matrix:** Identifies terrain categories the model frequently confuses.
- **Confidence Analysis:** Checks whether confidence scores correspond to actual prediction reliability.

Testing should also cover invalid images, unsupported file formats, corrupted inputs, and missing model files.

No performance metrics are reported here because validated evaluation results should come from the actual trained model.

## 🔭 Future Improvements

- Collect a larger and more diverse terrain dataset.
- Improve performance on visually similar terrain classes.
- Add probability calibration and uncertainty estimation.
- Evaluate performance across different lighting and weather conditions.
- Add image-level segmentation for identifying traversable regions.
- Integrate real sensor measurements for more reliable terrain attributes.
- Connect the perception system to a rover navigation simulator.
- Add automated testing, API monitoring, and model-version tracking.

## ⚠️ Limitations

TerrainSense AI is a prototype for terrain classification and rover traversal decision support.

- Predictions depend on the quality and distribution of the training data.
- A single image may not reveal hidden hazards or actual ground conditions.
- Class-based terrain attributes are estimates, not direct physical measurements.
- The system does not independently guarantee safe routes or control a physical rover.

Real-world deployment would require extensive validation, sensor integration, and safety testing.

## 🎯 Project Objective

The objective of TerrainSense AI is to demonstrate how computer vision and deep learning can transform terrain images into structured information that supports rover traversal analysis.

By combining CNN-based classification, backend inference, and terrain-oriented visualization, the project provides a foundation for further research in robotic perception and intelligent navigation.

## 👨‍💻 Author

**Vidhan Tripathi**

Computer Science and Engineering Student

Interests: Artificial Intelligence, Computer Vision, Deep Learning, and Robotics.

---

*TerrainSense AI — Turning terrain images into actionable traversal insights.*
