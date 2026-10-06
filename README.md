# Car Plate Detection System

[![Python 3.10+](https://img.shields.io/badge/python-3.10%2B-blue.svg)](https://www.python.org/downloads/)
[![OpenCV](https://img.shields.io/badge/OpenCV-4.5.3-5C3EE8.svg)](https://opencv.org/)
[![YOLO](https://img.shields.io/badge/YOLO-8.0.196-00FFFF.svg)](https://github.com/ultralytics/ultralytics)
[![EasyOCR](https://img.shields.io/badge/EasyOCR-1.7.0-FF6B35.svg)](https://github.com/JaidedAI/EasyOCR)

An intelligent computer vision system that detects license plates in uploaded videos and extracts their text. Built with YOLO for plate detection and EasyOCR for text recognition, PlateScope provides a local web interface with confidence scores, video timestamps, and CSV export.

## Features

- **Video Analysis** - Upload common video formats and sample frames for plate detection
- **Plate Detection** - YOLO model trained specifically for license plate detection
- **OCR Integration** - EasyOCR for text extraction
- **Reviewable Results** - Unique plates, OCR confidence, and video timestamps
- **CSV Export** - Download recognized plates for further analysis
- **MySQL Persistence** - Store videos, recognized plates, confidence, and timestamps

## Technology Stack

- **Python 3.10+** - Main programming language
- **Flask** - Local upload and results interface
- **OpenCV** - Computer vision processing
- **Ultralytics YOLO** - Object detection model
- **EasyOCR** - Text recognition
- **MySQL** - Persistent video and plate-result storage
- **NumPy** - Numerical operations
- **Jupyter** - Model training and analysis

## Demo

![Car Plate Detection Demo](video/video.gif)


## Project Structure

```
CarPlate/
├── main.py                    # Main entry point
├── requirements.txt           # Dependencies
├── api/
│   ├── app.py                # Flask routes and upload handling
│   ├── static/css/style.css  # Responsive interface styling
│   └── templates/index.html  # Upload and results page
├── config/
│   ├── settings.py           # Configuration
│   └── class_names.txt       # YOLO classes
├── database/
│   └── schema.sql            # MySQL database schema
├── models/
│   ├── best.pt               # Trained model
│   └── yolo11n.pt           # Base model
├── src/
│   └── plate_detector.py     # Headless detection and OCR pipeline
├── utils/
│   └── database_manager.py   # MySQL persistence and queries
├── .env.example              # MySQL configuration template
├── instance/uploads/         # Local uploaded videos (created at runtime)
├── data/videos/              # Test videos
└── notebooks/
    └── CarPlate.ipynb        # Training notebook
```

## Dataset

**Source**: [License Plate Recognition Dataset](https://universe.roboflow.com/roboflow-universe-projects/license-plate-recognition-rxg4e) from Roboflow Universe

### Training Your Own Model

```python
# Download dataset
from roboflow import Roboflow
rf = Roboflow(api_key="your_api_key")
project = rf.workspace("roboflow-universe-projects").project("license-plate-recognition-rxg4e")
version = project.version(11)
dataset = version.download("yolov11")

# Train model
!yolo task=detect mode=train model=yolo11n.pt data={dataset.location}/data.yaml epochs=50 imgsz=640
```

## Acknowledgments

- [Roboflow Universe](https://universe.roboflow.com/roboflow-universe-projects/license-plate-recognition-rxg4e) - Dataset
- [Ultralytics](https://github.com/ultralytics/ultralytics) - YOLOv11
- [EasyOCR](https://github.com/JaidedAI/EasyOCR) - OCR
  
