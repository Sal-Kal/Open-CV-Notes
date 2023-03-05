#Faces
Face Detection refers to detecting faces in an image, whereas Face Recognition refers to identifying whose face it is. 
OpenCV has many inbuilt classifiers that uses something known as Haarcascades. These include detecting full body, or face, or smile on a face in an image, etc.
Download the respective Haarcascade classifier xml file from OpenCV's official github [repo](https://github.com/opencv/opencv/tree/4.x/data).
- First we convert the image to gray-scale.
- We then use the downloaded xml file using the `CascadeClassifier()` function as shown below.
- Once that is done we then detect the face from the image. This is done by the `detectMultiScale()` function as shown below.
- We use the `rectangle()` function mentioned [[Shapes and Texts#Drawing Shapes & Putting Text#Rectangle|here]] to draw a rectangle around the face which has been detected.
```python
import cv2 as cv

def rescaleFrame(frame, scale = 0.75):
    width = int(frame.shape[1] * scale)
    height = int(frame.shape[0] * scale)
    dimensions = (width, height)
    return cv.resize(frame, dimensions, interpolation=cv.INTER_AREA)

img = cv.imread('./Photos/hank_happy.jpg')
image = rescaleFrame(img)
gray = cv.cvtColor(image, cv.COLOR_BGR2GRAY)

# Reading the xml file
haar_cascade = cv.CascadeClassifier('./FrontalFace.xml')

#Detecting the image
faces_rect = haar_cascade.detectMultiScale(gray, scaleFactor = 1.1, minNeighbors = 3)

#Printing the numbef of faces detected
print("The number of faces found are: ", len(faces_rect))

cv.imshow('Hank', image)

#Drawing a rectangle around the detected face
for (x,y,w,h) in faces_rect:
    cv.rectangle(image, (x,y), (x+w, y+h), (0,0,0), thickness=2)


#Showing the detected face
cv.imshow('Faces Detected', image)

cv.waitKey(0)
```
Provided Image:
![[Pasted image 20230305151236.png]]
Detected Faces:
![[Pasted image 20230305151256.png]]
This technique is very sensitive to noise in the image. When we want to detect multiple faces OpenCV might detect objects that remotely resemble a face.
Eg:
![[Pasted image 20230305151849.png]]
In such cases we can either increase or decrease the `minNeighbors` parameter in the `detectMultiScale()` function.
![[Pasted image 20230305152300.png]]
If we want to increase the number of faces detected then we decrease the value of `minNeighbors` otherwise we increase it.
Sometimes accessories worn on a person's face or freckles can affected the way faces are detected.