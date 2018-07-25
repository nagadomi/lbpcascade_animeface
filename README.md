# lbpcascade_animeface

The face detector for anime/manga using OpenCV.

Original release since 2011 at [OpenCVによるアニメ顔検出ならlbpcascade_animeface.xml](http://ultraist.hatenablog.com/entry/20110718/1310965532) (in Japanese)

## Usage

Download and place the cascade file into your project directory.

    wget https://raw.githubusercontent.com/nagadomi/lbpcascade_animeface/master/lbpcascade_animeface.xml

### Python Example

```python
import cv2
import sys
import os.path

def detect(filename, cascade_file = "../lbpcascade_animeface.xml"):
    if not os.path.isfile(cascade_file):
        raise RuntimeError("%s: not found" % cascade_file)

    cascade = cv2.CascadeClassifier(cascade_file)
    image = cv2.imread(filename, cv2.IMREAD_COLOR)
    gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    gray = cv2.equalizeHist(gray)
    
    faces = cascade.detectMultiScale(gray,
                                     # detector options
                                     scaleFactor = 1.1,
                                     minNeighbors = 5,
                                     minSize = (24, 24))
    for (x, y, w, h) in faces:
        cv2.rectangle(image, (x, y), (x + w, y + h), (0, 0, 255), 2)

    cv2.imshow("AnimeFaceDetect", image)
    cv2.waitKey(0)
    cv2.imwrite("out.png", image)

if len(sys.argv) != 2:
    sys.stderr.write("usage: detect.py <filename>\n")
    sys.exit(-1)
    
detect(sys.argv[1])
```
Run

    python detect.py imas.jpg

![result](https://user-images.githubusercontent.com/287255/43184241-ed3f1af8-9022-11e8-8800-468b002c73d9.png)

## Note
I am providing similar project at https://github.com/nagadomi/animeface-2009. animeface-2009 is my original work that was made before libcascade_animeface. The detection accuracy is higher than this project. However, installation of that is a bit complicated. Also I am providing a face cropping script using animeface-2009.
