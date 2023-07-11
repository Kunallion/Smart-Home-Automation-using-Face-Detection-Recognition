# FaceRecognition-Attendance

## Recommended Python Interpreter Version : Python 3.7.6

1) Get the required packages
2) Add training images in "ImagesAttendance" Folder for the machine to encode and save its embeddings.
3) When launched, the code triggers the system camera to open and recognise trained faces.
4) Attendace is marked with timestamp in "Attendance.csv" file.

### Code Functionality/Breakdown
This (main.py) Python script utilizes the OpenCV and face_recognition libraries to perform face recognition and attendance marking using a webcam.

1. The necessary libraries are imported: cv2 (OpenCV), numpy, face_recognition, os, and datetime.

2. The script assumes that there is a folder named "ImagesAttendance" containing images of individuals whose attendance needs to be marked. The list of files in the folder is obtained using `os.listdir(path)` and stored in the `myList` variable.

3. The images are loaded from the folder, and their corresponding class names (file names without the extension) are stored in the `classNames` list.

4. The function `findEncodings(images)` takes the loaded images and converts them to RGB format before using face_recognition library's `face_encodings` function to compute the face encodings for each image. The resulting encodings are stored in the `encodeList` and returned.

5. The function `markAttendance(name)` is responsible for marking the attendance of a recognized face. It opens the "Attendance.csv" file in read and write mode (`'r+'`), reads the existing lines, and checks if the given name already exists in the attendance file. If not, it appends a new entry with the name and the current timestamp.

6. The known face encodings are obtained by calling `findEncodings(images)` and stored in the `encodeListKnown` variable.

7. The script captures video from the webcam using `cv2.VideoCapture(0)`.

8. A loop is started to continuously read frames from the webcam. Each frame is resized, converted to RGB format, and then processed for face recognition.

9. The `face_recognition` library's `face_locations` function is used to detect faces in the frame, and the corresponding face encodings are computed using `face_encodings`.

10. For each detected face, the script compares the computed face encoding with the known encodings using `compare_faces` and calculates the face distance using `face_distance`.

11. The index of the closest match is obtained using `np.argmin(faceDis)`.

12. If a match is found (i.e., `matches[matchIndex]` is True), the recognized person's name is obtained from `classNames`. The bounding box and text are drawn on the frame using OpenCV's `rectangle` and `putText` functions.

13. The `markAttendance` function is called with the recognized name to mark the attendance in the "Attendance.csv" file.

14. The processed frame with bounding boxes and text is displayed in a window using `imshow`.

15. The loop continues until the user presses a key.
