# Car Plate Number Extraction System

A computer vision system for detecting and extracting license plate numbers from live camera feed using OpenCV and Tesseract OCR.

## Overview

This project implements a real-time license plate detection and recognition system with multiple processing stages:
- **Camera Input**: Captures live video from webcam
- **Plate Detection**: Identifies potential license plate regions using contour analysis
- **Plate Alignment**: Corrects perspective distortion for better OCR accuracy
- **OCR Recognition**: Extracts text from detected plates using Tesseract
- **Validation**: Validates plate format and implements temporal filtering
- **Logging**: Records detected plates with timestamps

## Features

- Real-time license plate detection from webcam feed
- Perspective correction for angled plates
- OCR text extraction with character whitelist
- Plate format validation (regex pattern matching)
- Temporal filtering to reduce false positives
- CSV logging of detected plates with timestamps
- Multiple processing stages for improved accuracy

## Project Structure

```
car-platenumber-extraction/
├── src/
│   ├── camera.py      # Basic camera test and feed display
│   ├── detect.py      # License plate detection using contours
│   ├── align.py       # Plate perspective correction and alignment
│   ├── ocr.py         # OCR text extraction from aligned plates
│   ├── validate.py    # Plate format validation
│   └── temporal.py    # Temporal filtering and logging
├── data/              # Data files (if any)
├── screenshots/       # Project screenshots
├── requirements.txt   # Python dependencies
└── README.md         # This file
```

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd car-platenumber-extraction
```

2. Install the required dependencies:
```bash
pip install -r requirements.txt
```

3. Install Tesseract OCR:
   - **Windows**: Download from [Tesseract at UB Mannheim](https://github.com/UB-Mannheim/tesseract/wiki)
   - **macOS**: `brew install tesseract`
   - **Ubuntu/Debian**: `sudo apt-get install tesseract-ocr`

## Usage

Each module can be run independently to test different stages:

### Camera Test
```bash
python src/camera.py
```
Tests basic camera functionality and displays live feed.

### Plate Detection
```bash
python src/detect.py
```
Detects potential license plate regions and draws bounding boxes.

### Plate Alignment
```bash
python src/align.py
```
Detects plates and shows perspective-corrected aligned versions.

### OCR Recognition
```bash
python src/ocr.py
```
Performs full detection, alignment, and OCR text extraction.

### Format Validation
```bash
python src/validate.py
```
Validates OCR results against license plate format patterns.

### Complete System with Logging
```bash
python src/temporal.py
```
Full pipeline with temporal filtering and CSV logging.

## Technical Details

### Detection Algorithm
- Converts frames to grayscale and applies Gaussian blur
- Uses Canny edge detection to find edges
- Applies contour detection to find rectangular regions
- Filters candidates based on area and aspect ratio (2.0-8.0)

### OCR Configuration
- Uses Tesseract with PSM 8 (single word) mode
- Character whitelist: A-Z, 0-9
- Otsu thresholding for binarization

### Validation Pattern
- Regex pattern: `[A-Z]{3}[0-9]{3}[A-Z]`
- Temporal filtering with 5-frame buffer
- 10-second cooldown between duplicate detections

### Output Format
Detected plates are logged to `plates_log.csv` with:
- Plate number
- Timestamp (YYYY-MM-DD HH:MM:SS format)

## Requirements

- Python 3.7+
- OpenCV 4.x
- NumPy
- Pytesseract
- SciPy
- Tesseract OCR engine

## Controls

- Press 'q' to quit any running module
- All modules display real-time processing with visual feedback

## Notes

- The system is optimized for standard license plate formats
- Performance depends on lighting conditions and camera quality
- Tesseract may need additional training for specific regional plate formats
- Minimum plate area threshold: 600 pixels

## Troubleshooting

1. **Camera not opening**: Check camera permissions and ensure no other applications are using the camera
2. **Poor OCR accuracy**: Ensure good lighting conditions and consider training Tesseract for specific plate formats
3. **Tesseract not found**: Make sure Tesseract is installed and in your system PATH
4. **False detections**: Adjust MIN_AREA and aspect ratio thresholds in the source code


## Author

Iradukunda Joyeuse