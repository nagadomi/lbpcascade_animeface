# lbpcascade_animeface

The face detector for anime/manga using OpenCV.

Original release since 2011 at [OpenCVによるアニメ顔検出ならlbpcascade_animeface.xml](http://ultraist.hatenablog.com/entry/20110718/1310965532) (in Japanese)

## Usage

Download and place the cascade file into your project directory.

    wget https://raw.githubusercontent.com/nagadomi/lbpcascade_animeface/master/lbpcascade_animeface.xml

### Python Example

```python
import cv2
import cv  
import sys

def detect(filename):
    cascade = cv2.CascadeClassifier("../lbpcascade_animeface.xml")
    image = cv2.imread(filename)
    gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    gray = cv2.equalizeHist(gray)
    
    faces = cascade.detectMultiScale(gray,
                                     # detector options
                                     scaleFactor = 1.1,
                                     minNeighbors = 5,
                                     minSize = (24, 24),
                                     flags = cv.CV_HAAR_SCALE_IMAGE)
    for (x, y, w, h) in faces:
        cv2.rectangle(image, (x, y), (x + w, y + h), (0, 0, 255), 2)

    cv2.imshow("AnimeFaceDetect", image)
    cv2.waitKey(0)
    cv2.imwrite("out.png", image)
    
if __name__ == "__main__":
    detect(sys.argv[1])
```
Run

    python detect.py imas.jpg

![result](https://raw.githubusercontent.com/nagadomi/lbpcascade_animeface/master/figure/imas.png)
