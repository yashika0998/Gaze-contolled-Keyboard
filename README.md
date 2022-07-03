# Gaze-contolled-Keyboard
## Situation:
I came across a blog how Computer Vision can help people affected by quadriplegia who completely lost the control of their limbs. 

The zeal to work in Computer Vision with opencv made me to do some real world project that could be helpful for such people. In this project the idea to create the automatic virtual keyboard which could be controlled by our gaze without using the hands.

## Task:
The “Gaze controlled keyboard” is a application in which we are going to control the keyboard through our eyes. Here Python with OpenCV will be used completely from scratch. The goal of such app is to write without using our hands.

## Action/Approach
This project is built in two main parts:

* **Eye detection**: Detection of the eyes (with or without glasses), their movement and most important their blinking.

* **Virtual keyboard**: A keyboard on the screen where we’re going to select the letters by just using/blinking our eyes.

### 1.1 Eye detection
Here real time video detction from the webcam will be applied to detect the frames. To detect the eyes we will use face landmark detection approach. We will be able to find 68 specific landmarks of the face usinf dlib library. To each point there is a specific index assigned. Hence, we will use the following landmark points to detect the eye.

* Left eye points: (36, 37, 38, 39, 40, 41)

* Right eye points: (42, 43, 44, 45, 46, 47)

![](Images/face_landmarks.JPG)

### 1.2 Detecting the blinking
After we detect the eye. we detect the 2 lines: an horizontal line and a vertical line crossing the eye.

Visual of eye when the it is open.

![](Images/eye_open.jpg)

Visual of eye when it is closed.

![](Images/eye_closed.jpg)

ratio = hor_line_lenght / ver_line_lenght
By calculating the ratio of length of horizontal line to vertical line. We observed if the ratio is more than 6.0, the eye are closed. Hence after improving this parameter to near 5.5-5.7 gives more accuracy of blinking the eye.

### 1.3 Gaze Detection
The idea is to divide the keyboard into two parts. The part of keyboard either left or right focused by eye, gets activated and light up.

Here is how virtual keyboard is divided
![](Images/keyboard.png)

Hence for that we need to detect the gaze of our eyes. The possible direction of gaze are shown in image below.

![](Images/different_direction_of_eye.png)

The idea is to split the eye in two parts and to find out in which of the two parts there is more sclera (white part of eye) visible.

![](Images/2_division_eye.png)

If the sclera is more visible on the right part, so the eye is looking at the left (our left) like in picture attached above. Moreover to detect the sclera we convert the eye into grayscale, then finding a **threshold** helps us to count the white pixels.

We divide the white pixels of the left part and those of the right part to achieve the gaze ratio. 

* If the gaze ratio < 1: looking to the right. 

* If gaze ratio > 1.7 the eyes are looking to the left side.

### 2.1 Virtual Keyboard
The idea is to choose the left or right keyboard that we already divided and display the Keys on the screen. Light up the key one at time according to the pace of your blink. The key you want to choose should be lighted up, and then blink your eyes for longer than 1 second. This will allow the letter to be typed on white board along with a beep sound.

Using mathematical logic in numpy and cv2 libraries, we create the keyboard.

![](Images/virtual_keyboard.png)

This is a left side keyboard.

### 2.2 Light up letters each 10 frames
Letterswill lght up after every 10 frames to reach the letter we want to press. Blinking eye for longer will type the key.

## Final result

I have tried of typing the word WELL

![](Images/output.png)



#### Inspiration From
Pyscource blogs by Sergio Canu

#### Author

Yashika Mittal (yashika0998)

https://www.linkedin.com/in/yashika-mittal/






