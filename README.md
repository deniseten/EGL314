# EGL314 TEAM D (PHOTO BOOTH)
![Alt text](<images/grp photo.jpeg>)

# Introduction of our project
(UPDATE!!!)

# Storyboard
![Alt text](images/storyboard.jpeg)

# System Diagrams
## Control Diagram
![Alt text](<images/control diagram.png>)

## Video Diagram
![Alt text](images/Video%20Diagram.png)

## Lighting Diagram
![Alt text](images/lighting%20diagram.png)

## Audio Diagram
![Alt text](images/audio%20diagram.jpg)

# Floor Plan and Layout
(UPDATE!!!)

# Equipment List
(UPDATE!!!)

# Server Rack Setup
![Alt text](images/rack%20layout.jpg)
![Alt text](images/Srever-rack.jpeg)

# Projector Setup
![Alt text](images/Projector.jpg)

# Video Setup
![Alt text](images/Pandora%20Box%20Sequence%20for%20314.jpg)
Sequence setup inside pandora box.
![Alt text](images/Connection%20manager%20for%20314.jpg)
Tcp connection setup in the widget designer for the raspberry pi to communicate with the pandora box.

# Audio Setup
![Alt text](images/audio%20setup.jpg)
This the type of cable used
![Alt text](images/type%20of%20cable.jpg)

# Lighting Setup
![Alt text](images/artnet_dmx_node.jpg)
![Alt text](images/dmx_driver.jpg)
This is the dmx driver that we connect to the artnet-dmx node.

# Cameras Setup
![Alt text](images/Screen2.jpeg)
Two Cameras-> Video Cam and Webcam

# Final Setup
![Alt text](images/final1.jpeg)
![Alt text](images/final2.jpeg)
![Alt text](images/final3.jpeg)

# Socket Configuration
```
TCP_IP = '192.168.1.50'
TCP_PORT = 5020
BUFFER_SIZE = 1024

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect((TCP_IP, TCP_PORT))
```
This section configures the socket connection's TCP/IP address, port number, and buffer size. It generates a socket object, 's', with the supplied IP address and port number, and connects to the specified server.

# Video Capture Initialization
```
cap = cv2.VideoCapture(0)
```
The code creates a 'cap' video capture object to collect frames from the default camera (index 0). This object will be used later to get video frames.

