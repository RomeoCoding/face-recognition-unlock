# Face Unlock System with ESP32 Integration

## Overview
This project implements a face recognition-based access control system using Python and an ESP32 microcontroller. The system detects and recognizes faces using OpenCV and the `face_recognition` library, then sends an HTTP request to the ESP32 to unlock a connected device.

## Features
- Face detection and recognition using OpenCV
- Storage of employee face encodings in a SQLite database
- Efficient event-based triggering to reduce unnecessary processing
- HTTP communication between the laptop and ESP32 for unlocking
- Modular structure for easy expansion and integration

## Project Structure
```
face_unlock_project/
│── database/
│   ├── faces.db               # SQLite database storing face encodings
│   ├── manage_db.py           # Script to add/remove faces from the database
│── models/
│   ├── encode_faces.py        # Converts images to face encodings and stores them in DB
│── scripts/
│   ├── face_detect.py         # Captures faces from webcam and compares with database
│   ├── trigger.py             # Waits for a face detection event, then activates recognition
│── utils/
│   ├── camera.py              # Camera-related helper functions
│   ├── network.py             # HTTP request handling functions (to ESP32)
│── main.py                    # Runs the full face unlock system
│── requirements.txt           # Dependencies
│── README.md                  # Project documentation
```

## Installation
### Prerequisites
Ensure you have Python installed (version 3.8+ recommended). Install dependencies using:
```sh
pip install -r requirements.txt
```

### Setting Up the Database
1. Add employee face images to a directory (e.g., `faces/`).
2. Run the encoding script to process and store the faces:
```sh
python models/encode_faces.py
```

## Usage
### Running the Face Recognition System
To start face detection and recognition:
```sh
python scripts/face_detect.py
```

### Running the Trigger System
To activate event-based face detection:
```sh
python scripts/trigger.py
```

### Managing the Database
To add or remove employee face data:
```sh
python database/manage_db.py
```

## Communication with ESP32
The laptop sends an HTTP request when an authorized face is detected. The ESP32 listens for requests and unlocks the connected device when triggered. The request format:
```
GET http://<ESP32-IP>/unlock
```

## Future Enhancements
- Implement encryption for HTTP requests to enhance security
- Add multi-device support for access control across different locations
- Develop a mobile application for remote access management

