# Secure Face Recognition Login System with Unauthorized Access Alerts

## Description
This project is a secure login system using face recognition. It authenticates the admin based on their face and alerts via SMS for unauthorized login attempts. The system captures snapshots of unauthorized attempts for review.

## Features
- **Face Detection**: Detects faces in real-time using a webcam.
- **Face Recognition**: Authenticates the admin based on a predefined image.
- **Unauthorized Access Alerts**: Sends an SMS notification using Twilio API if an unknown face is detected multiple times.
- **Snapshot Storage**: Saves snapshots of unauthorized login attempts.

## Prerequisites
1. Python 3.x
2. Required Python Libraries:
   - `cv2` (OpenCV)
   - `dlib`
   - `numpy`
   - `twilio`
3. Twilio Account SID, Auth Token, and Verified Phone Numbers.
4. Pre-trained `dlib` models:
   - `shape_predictor_68_face_landmarks.dat`
   - `dlib_face_recognition_resnet_model_v1.dat`

## Installation
1. Clone the repository:
   git clone https://github.com/kamalesh955/Secure-Face-Recognition-Login-System
2. Install dependencies:
   -`pip install opencv-python dlib numpy twilio`
3. Set environment variables:
   - `export TWILIO_ACCOUNT_SID='your_account_sid'`
   - `export TWILIO_AUTH_TOKEN='your_auth_token'`
   - `export TWILIO_PHONE_NUMBER='your_twilio_phone_number'`
4. Usage
   Update admin_image_path with the path to the admin's image.
5. Run the script:
   python face_recognition_login.py
   - `To exit, press 'q'.`
   
## Architecture
Architecture of the Project.
   - `Input: Live webcam feed.`
   - `Processing: Detects and recognizes faces using dlib and OpenCV.`
   - `Output: Displays real-time feedback and sends alerts for unauthorized attempts.`
