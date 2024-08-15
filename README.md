#Eye Tracking with Mouse Control

This Python code demonstrates eye tracking with mouse control using OpenCV and PyAutoGUI libraries. It utilizes the webcam to capture frames and detect the user's eyes using Haar cascades for face and eye detection. The position of the eye is then mapped to the screen coordinates, essentially controlling the mouse cursor with eye movements.

Code Breakdown

Imports:

OpenCV (cv2) for image processing and computer vision tasks.
NumPy (np) for numerical operations.
PyAutoGUI for interacting with the desktop environment (moving the mouse cursor).
Haar Cascade Loading:

Loads pre-trained Haar cascade classifiers for face and eye detection from OpenCV's data directory.
Webcam Initialization:

Initializes the webcam to capture video frames.
Screen Dimensions:

Retrieves the screen width and height using PyAutoGUI to map eye positions to screen coordinates.
move_mouse function:

This function takes the x and y coordinates as arguments and moves the mouse cursor to that position on the screen using PyAutoGUI.
get_eye_center function:

This function takes the detected eyes (eyes), frame width (frame_width), and frame height (frame_height) as arguments.
It assumes the first detected eye is used for cursor control.
It calculates the center coordinates (x and y) of the eye and returns them. If no eyes are detected, it returns None.
Smoothing Variables:

previous_x and previous_y store the previous smoothed coordinates of the eye center.
smoothing_factor is a value between 0 and 1 that determines the weight given to the new eye position compared to the previous one. Higher values result in smoother cursor movement but may introduce lag.
Main Loop:

Captures a frame from the webcam using cap.read().
Converts the frame to grayscale for better face and eye detection.
Detects faces in the grayscale frame using the face_cascade classifier.
Iterates through each detected face:
Extracts the region of interest (ROI) for the face from the grayscale and color frames.
Detects eyes within the facial ROI using the eye_cascade classifier.
Calls get_eye_center to get the center coordinates of the first eye (assuming it's the one being used for control).
Maps the eye center coordinates to screen coordinates using the frame dimensions and screen width/height.
Applies smoothing to the mapped coordinates using the previous coordinates and smoothing_factor.
Calls move_mouse to move the cursor to the smoothed screen coordinates.
Updates the previous_x and previous_y with the newly smoothed values.
Draws rectangles around the detected eyes on the color frame for debugging purposes.
Displays the frame with detected eyes using cv2.imshow.
Listens for the 'q' key press to quit the program.
Cleanup:

Releases the webcam capture.
Closes all OpenCV windows.
This code provides a basic implementation of eye tracking for mouse control. You can experiment with different parameters like smoothing_factor to fine-tune the control behavior. Note that the accuracy of eye detection and cursor control can be influenced by lighting conditions and the user's posture relative to the webcam.
