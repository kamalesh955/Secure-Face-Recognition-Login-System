import cv2
import dlib
import numpy as np
import os
from twilio.rest import Client
import time
import os

count2 = 0
count = 0
folder_path = r"C:\Path\to store\unauthorized logins"

def send_sms(to_number, body):
    account_sid = os.getenv('TWILIO_ACCOUNT_SID')
    auth_token = os.getenv('TWILIO_AUTH_TOKEN')

    client = Client(account_sid, auth_token)

    from_number = os.getenv('TWILIO_PHONE_NUMBER')

    try:
        message = client.messages.create(
            body=body,
            from_=from_number,
            to=to_number
        )
        print(f"Message sent successfully! SID: {message.sid}")

    except Exception as e:
        print(f"Failed to send message: {e}")


detector = dlib.get_frontal_face_detector()

predictor = dlib.shape_predictor(r'C:\Path\to\shape_predictor_68_face_landmarks.dat')

admin_image_path = 'admin.jpg'
admin_image = cv2.imread(admin_image_path)

face_rec = dlib.face_recognition_model_v1(r'C:Path\to\dlib_face_recognition_resnet_model_v1.dat')

def get_face_encoding(image):
    gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    faces = detector(gray)

    if len(faces) == 0:
        return None

    face = faces[0]
    shape = predictor(gray, face)
    encoding = np.array(face_rec.compute_face_descriptor(image, shape))

    return encoding

admin_encoding = get_face_encoding(admin_image)

cap = cv2.VideoCapture(0)

while True:
    ret, frame = cap.read()
    if not ret:
        break

    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
    faces = detector(gray)

    for face in faces:
        x1, y1, x2, y2 = face.left(), face.top(), face.right(), face.bottom()

        cv2.rectangle(frame, (x1, y1), (x2, y2), (0, 255, 0), 2)

        face_shape = predictor(gray, face)
        face_encoding = np.array(face_rec.compute_face_descriptor(frame, face_shape))

        if np.linalg.norm(admin_encoding - face_encoding) < 0.55:
            cv2.putText(frame, 'Admin', (x1, y1 - 10), cv2.FONT_HERSHEY_SIMPLEX, 0.9, (0, 255, 0), 2)
            count2 += 1
            if count2 == 6:
                print("It's a picture of me!")

        else:
            cv2.putText(frame, 'Unknown', (x1, y1 - 10), cv2.FONT_HERSHEY_SIMPLEX, 0.9, (0, 0, 255), 2)
            count += 1
            if count == 5:
                print("It's not a picture of me!")
                time.sleep(0.5)
                cap.release()
                cv2.destroyAllWindows()
                cv2.waitKey(1)
                snapshot_path = os.path.join(folder_path, f"unauthorized_{int(time.time())}.jpg")
                cv2.imwrite(snapshot_path, frame)
                print(f"Snapshot saved: {snapshot_path}")
                send_sms('+918754211211', 'UNAUTHORIZED LOGIN ATTEMPT!')
                break

    cv2.imshow('Face Detection', frame)

    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()
