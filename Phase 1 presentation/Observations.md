Changes:
- Use negative camber for landing gear, parallel to the longer side of the board.
- Suspension in drone's "legs(?)"
- Flaps?
- A lesser MP camera would not be as bad, if we convert the target board to a lower bit image, like to bit.

Observation on body:
- Lemon 3s 5500mAh 45C/90C: 45c is continuous, 90 is burst
	- 5500mAh Battery
	- 5500mAh / 1000 = 5.5Ah 
	- 45C x 5.5Ah = 247.5 Amps available 
		- 60 / 247.5C = 0.2424 minutes


## GPS navigation
- The final report states: "Using RTK (Real Time Kinematic) GPS module was considered, which offer extremely high accuracy in the centimeter range, they are expensive, and their availability is not guaranteed". 
	- Consider using the base station as data retrieval for more accurate location, and then moving drone relative to it.

## Target recognition

### Object Detection
[Object detection](https://www.mathworks.com/discovery/object-detection.html) is the process of finding instances of objects in images. In this instance, The model will take one image from the input stream, and process it to find instances of object, targets in this case, we want to detect. The Drone will cover the area and get location of all targets that it can find.

At this point, we will have a pre-programmed point in the system, that will be the coordinates (or a rough estimate) in the image of where our payload will drop to in real life if the drone is at a stand still at the selected height.

Now, The drone with the payload will go to the Target's coordination. Once it has reached what it believes is the dropzone, It will take a picture and run object detection again, and find the coordination of target in that pic. The program will calculate how far the Drone is from the pre-programmed point, by comparing coordinates A with the pre programmed point. Then the drone will move to that position. After it has moved, It'll move again ensure that it is at an acceptable point, then drop the payload.

>Note: Object Recognition was also considered, but dropped because it would require tighter constraints.

### Performance
Raspberry Pi performs pretty badly at Object Detection. Depending on the speed of drone, it can at best process 2 frames per second on OpenCV.

> For embedded devices such as the Raspberry Pi, I typically always recommend Single Shot Detectors (SSDs) with a MobileNet base. These models are challenging to train (i.e. optimizing hyperparameters), but once you have a solid model, the speed and accuracy tradeoffs are well worth it.
> https://pyimagesearch.com/2020/01/27/yolo-and-tiny-yolo-object-detection-on-the-raspberry-pi-and-movidius-ncs/


### PATH mapping
Last implementation covered the whole area(?) in order to map the field. If it is allowed, It would be better to instead divide the field into two parts. 
- The Drone will take flight and move along the first path, checking the area for any hotspots.
- If it finds n hotspots out of x hotspots, it will capture their data. Then it will find x-n hotspots in the rest of the area. 
- Best case it finds all hotspots in path 1, saving nearly half our time. Else in worst case, it'll take the normal amount of time it would have taken.



