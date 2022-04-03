---
author: bergercookie
tags:
  - "Machine Learning"
  - Programming
categories:
  - Scratchpad
comments: true
date: "2019-10-14T00:00:00Z"
draft: false
title: 🛠️  Scratchpad - CV Applications II Course by OpenCV
showtoc: true
---

# Computer Vision Applications using OpenCV

## Facial Landmark Detection

### Improve the speed of Facial Landmark Detection:

1. Use face detection that comes with OS - if possible (e.g., Android, iOS)
2. Skip frames - e.g,. run every 3 frames
3. Downscale image, detect faces there ... then propagate bboxes to original image
   (dividing the coordinates by the scale used for resizing the original frame.). Then just do landmark detection on
   original image and computed bounding box

### Improve landmark stabilisation

1. **Weighted Moving Average** - Average the landmark point location over a small time window
2. Kalman Filtering
3. Optical Flow

## Code snippets

### OpenCV - Rescale an image - keep ratio

{{< highlight python >}}
import cv2

# Load image

img = cv2.imread("<path-to-img>")

# Scale down - keep ratio

dims = img.shape[0:2]
ratio = dims[0] / dims[1]

target_x = 960 # resolution - x
target_y = int(960 / ratio)
imgS = cv2.resize(img, (target_x, target_y))

cv2.namedWindow('windowname', cv2.WINDOW_NORMAL) # Create window with freedom of dimensions
cv2.imshow('windowname', imgS)
cv2.waitKey(0) # Display the image infinitely until any keypress

# in case you want to kill the window

cv2.destroyAllWindows()
{{< / highlight >}}

### OpenCV - imshow but keep it until <ESC> pressed

{{< highlight python >}}
import cv2
import time

def imshow\_(winname: str, img):
cv2.imshow(winname, img)

    while True:
        k = cv2.waitKey()
        if k == 27:
            break
        time.sleep(0.2)

    cv2.destroyWindow(winname)()

{{< / highlight >}}

## Hints & Tricks

- `dlib::faceDetector` is trained on 80x80 faces. If the faces in your images
  are less than that then you need to upscale before running the detection.
- `dlib::landmarkDetector`: Paper says it runs in 1ms
- dlib -> RGB, OpenCV -> BGR. Thus for OpenCV -> dlib: `cv2.cvtColor(img, cv2.COLOR_BGR2RGB)`

## Useful Links

- [dlib]( http://dlib.net/ )
- [OpenFace](https://github.com/cmusatyalab/openface)
- [Demystifying Face Recognition: Face Alignment](https://melgor.github.io/blcv.github.io/static/2017/12/28/demystifying-face-recognition-iii-face-preprocessing)
  - So we were not able to confirm that using aligned images for model learned on cropped faces boost the accuracy.
- [OpenCV - Python filtering operations](https://docs.opencv.org/master/d4/d13/tutorial_py_filtering.html)
