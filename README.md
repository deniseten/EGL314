# EGL314 TEAM D

# Storyboard
![Alt text](images/storyboard.jpeg)
# System Diagram
## Control Diagram
![Alt text](images/control%20diagram.png)

## Video Diagram
![Alt text](images/Video%20Diagram.png)

## Lighting Diagram
![Alt text](images/lighting%20diagram.png)

## Audio Diagram
![Alt text](images/audio%20diagram.jpg)

# Floor Plan
![Alt text](images/floor%20plan.png)

# Rack Layout
![Alt text](images/rack%20layout%20diagram.png)

# Equipment List
![Alt text](images/euipment%20list.png)

# Projector Setup
![Alt text](images/Projector.jpg)


# Server Rack Setup
![Alt text](images/rack%20layout.jpg)

[def]: images/audio%20diagram.png

# Video Setup
![Alt text](images/Pandora%20Box%20Sequence%20for%20314.jpg)
Sequence setup inside pandora box.
![Alt text](images/Connection%20manager%20for%20314.jpg)
Tcp connection setup in the widget designer for the raspberry pi to communicate with the pandora box.

# Audio Setup
[label](images/audio%20setup.jpg)
This the type of cable used
![label](images/type%20of%20cable.jpg)

### Socket Configuration:
```
TCP_IP = '192.168.1.50'
TCP_PORT = 5020
BUFFER_SIZE = 1024

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect((TCP_IP, TCP_PORT))
```
This section configures the socket connection's TCP/IP address, port number, and buffer size. It generates a socket object, 's', with the supplied IP address and port number, and connects to the specified server.

### Video Capture Initialization:
```
cap = cv2.VideoCapture(0)
```
The code creates a 'cap' video capture object to collect frames from the default camera (index 0). This object will be used later to get video frames.

### Hand Movement Detection:
```
previous_frame = None
gesture = None

while True:
    ret, frame = cap.read()
    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
    gray = cv2.GaussianBlur(gray, (9, 9), 0)
    
    if previous_frame is None:
        previous_frame = gray
        continue
    
    frame_diff = cv2.absdiff(previous_frame, gray)
    _, thresh = cv2.threshold(frame_diff, 30, 255, cv2.THRESH_BINARY)
    dilated = cv2.dilate(thresh, None, iterations=3)
    
    contours, _ = cv2.findContours(dilated, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
    
    left_swipe = False
    right_swipe = False

    for contour in contours:
        if cv2.contourArea(contour) < 1000:
            continue
        
        x, y, w, h = cv2.boundingRect(contour)
        
        if x < frame.shape[1] // 2:
            right_swipe = True
            cv2.putText(frame, "Right Swipe", (x, y - 10), cv2.FONT_HERSHEY_SIMPLEX, 0.9, (0, 255, 0), 2)
        else:
            left_swipe = True
            cv2.putText(frame, "Left Swipe", (x, y - 10), cv2.FONT_HERSHEY_SIMPLEX, 0.9, (0, 255, 0), 2)
        
        cv2.rectangle(frame, (x, y), (x + w, y + h), (0, 255, 0), 2)

    if left_swipe and not right_swipe:
        gesture = "Left Swipe"
        MESSAGE = b"left"
        s.send(MESSAGE)
    elif right_swipe and not left_swipe:
        gesture = "Right Swipe"
        MESSAGE = b"right"
        s.send(MESSAGE)
    else:
        gesture = "No Swipe"
        MESSAGE = b"no swipe"
        s.send(MESSAGE)
    
    cv2.imshow('Hand Movement Detection', frame)
    
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

    previous_frame = gray

cap.release()
cv2.destroyAllWindows()

```
This programme gathers camera frames, detects hand motions, determines swipe direction (left or right), transmits matching messages over a socket connection, and displays processed frames with swipe labels.