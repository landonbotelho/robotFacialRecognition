# TurtleBot 4 Face Explorer

A ROS 2 robotics project developed for the TurtleBot 4 that combines autonomous exploration, computer vision, facial recognition, and real-time motion control.

The robot explores its environment until it detects a specific target face. Once the target is recognized, the robot switches from autonomous exploration to face-following behavior and tracks the person for a fixed period before stopping.

## Overview

This project was developed using Python and ROS 2 for a TurtleBot 4 equipped with an OAK-D camera.

The system subscribes to the robot's live camera feed, processes each frame using OpenCV and the `face_recognition` library, and compares detected faces against a previously encoded target image.

Before the target is found, the robot performs autonomous exploration using randomized forward and rotational movement.

When the target face is detected, the robot transitions into a tracking state and uses the horizontal position of the face within the camera frame to steer toward and follow the target.

After following the target for approximately 20 seconds, the robot stops permanently.

## Features

- Autonomous environmental exploration
- Real-time camera processing
- Face detection and recognition
- Target-specific facial matching
- Dynamic transition between exploration and tracking states
- Proportional steering based on face position
- ROS 2 velocity command publishing
- OAK-D camera integration
- Basic backup and avoidance behavior
- Live OpenCV visualization of detected faces

## Technologies

- Python
- ROS 2
- TurtleBot 4
- OpenCV
- `face_recognition`
- NumPy
- CvBridge
- OAK-D Camera
- ROS 2 `sensor_msgs`
- ROS 2 `geometry_msgs`

## How It Works

### 1. Target Face Encoding

At startup, the program loads a reference image of the target individual and generates a facial encoding using the `face_recognition` library.

```python
self.target_face = face_recognition.load_image_file("landon.jpg")
self.target_encoding = face_recognition.face_encodings(self.target_face)[0]
