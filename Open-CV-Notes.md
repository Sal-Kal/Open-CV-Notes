# Libraries:
-  OpenCV: `pip install opencv-python`
-  OpenCV with community plugins: `pip install opencv-contrib-python`
-  Caer: `pip install caer`
---
#Basics
# Reading Images & Videos
### Images
- `imread(str:path)`: This function is used to read an image. Takes the path of the image as input. Retruns an image matrix, so must be stored in a variable. This function reads the image in BGR format and not in RGB.
- `imshow(str:window_name, image_matrix)`: This function is used to print an image. The window name can be anything. The image matrix is the output of imread. This function assumes that the given image is in BGR formate and not in RGB. 
We can see more about color spaces [[#Color Spaces|here]].
### Videos
- `VideoCapture()`: This function takes an integer as an input or a string which can be the path of a video. Integers are used when you need to use system camera. The values starting from 0 identify the various cameras connected to your system.
- `read()`: Videos captured can't be read with `imshow()` so we use `read()` function to read each frame of the video captured using a loop and then use `imshow()` to show every frame.
```python
capture = cv.VideoCapture('./Videos/Beethoven - Moonlight Sonata (3rd Movement).mp4')

while True:
    isTrue, frame = capture.read()
    cv.imshow('Video', frame)
	# this is to make sure the videos doesn't display in an  infinite loop. It waits for 20 ms and then will quit the loop if letter d is pressed.
    if cv.waitKey(20) & 0xFF==ord('d'):
        break

capture.release()
cv.destroyAllWindows()
```
- `waitKey(int:milliseconds)`: This function is used to make sure that when an image is shown using `imshow()` it doesn't just close it immediately after opening the window. The function takes  the parameter in milliseconds. It waits for the specified time and then waits for an input from the keyboard. After the input from the keyboard, window closes and the program continues it's execution. Until the input from the keyboard is given the program waits. By passing a value of 0 in `waitKey()` the program immediately starts waiting for an input from the keyboard.
---
#Basics 
# Resizing and Rescaling
The height and width of a particular image frame can be accessed by using the `shape` array in the dot operator.
```python
height = frame.shape[0]
width = frame.shape[1]
```
- `resize(frame, tuple:(width, height), interpolation)`: This function can be used to resize a particular frame. It returns a resized frame. The first argument is the frame we want to resize, the second argument is a tuple containing the resized width and height that we desire. The Third argument is the type of interpolation. Interpolation refers to the way the extra pixels are calculated.
```python
# Rescaling function
def rescaleFrame(frame, scale = 0.75):
    width = int(frame.shape[1] * scale)
    height = int(frame.shape[0] * scale)
    dimensions = (width, height)

    return cv.resize(frame, dimensions, interpolation=cv.INTER_AREA)

# Playing a video in both original and rescaled form
while True:
    isTrue, frame = capture.read()

    frame_resized = rescaleFrame(frame)

    cv.imshow('Video', frame)
    cv.imshow('resized', frame_resized)

    if cv.waitKey(20) & 0xFF==ord('d'):
        break

capture.release()
cv.destroyAllWindows()
```
The capture object in the above example can be rescaled using the `set()` function.
```python
def changeRes(width, height):
	capture.set(3,width)
	capture.set(4,height)
```
Where 3 references the width of the capture frame, and 4 references the height of the captured frame. Hence new values of width and height can be set to a captured frame using the `set()` function.
It is important to note that the user defined `changeRes()` function only works for Live Videos and will not working with any stored video. For existing stored videos we can use the user define `rescaleFrame()` function.

---
#Basics 
# Drawing Shapes & Putting Text
The zeros function in numpy can be used to create a blank image
```python
blank = np.zeros((500,500,3), dtype='uint8')
```
We can later show this image using the `imshow()` function in opencv library. It will show a blank image with black background. The first and second values in `(500,500,3)` signifies the height and width, and the `3` means we can set color using rgb values as shown below.
```python
blank[:] = 0,255,0
```
The above code sets the color of each pixel in the blank image to green.
```python
blank[200:300,200:300] = 0,255,0
```
The above code sets particular pixels to green.
## Rectangle
- `rectangle(image_matrix, (int:x,int:y), (int:x,int:y), (rgb color values), int:thickness)`: This function is used to draw a rectangle on any image matrix. The first x and y values are the values from where the rectangle starts and the second x and y values are the values where the rectangle ends. The rgb values are for the border color of the rectangle. The thickness is the thickness of the rectangle border.
```python
cv.rectangle(blank, (0,0), (250,250), (0,255,0), thickness=2)
```
We can add `thickness = cv.FILLED` to fill the entire rectangle with the specified rgb value.
```python
cv.rectangle(blank, (0,0), (250,250), (0,255,0), thickness=cv.FILLED)
```
The above rectangle will be green in color. We can also set the thickness value as `-1` and we get the same result.
## Circle
- `circle(image_matrix, (int:x,int:y), int:radius, (rgb color values), int:thickness)`: This function is used to draw a circle on any image matrix, The x and y values used as parameters in this function is the coordinate for the center of the circle. Based on the given radius value, a circle is drawn from with this point as the center.
```python
cv.circle(blank, (blank.shape[1]//2, blank.shape[0]//2), 40, (0,0,255), thickness=-1)
```
In the above example we are taking the half of height and width of the image matrix, meaning the center of the image, which is where the circle will be drawn.
## Line
- `line(image_matrix, (int:x,int:y), (int:x,int:y), (rgb color values), int:thickness)`: The arguments are the same as the `rectangle()` function. The first x, y values are the starting coordinates of the line and the second x,y values are the ending coordinates. 
```python
cv.line(blank, (0,0), (blank.shape[1]//2, blank.shape[0]//2), (0,255,0), thickness=2)
```
## Text
- `putText(image_matrix, str:text, (int:x, int:y), font, float:font_scale, (rgb color values), int:thickness )`: This function is used to put some text on our image matrix. The text parameter specifies the text to be displayed. The x, y values are the coordinates where the start of our text will be placed on the image, the font family can be specified using the inbuilt `cv2` fonts. Then we specify the font scale.
```python
cv.putText(blank, 'Death is the only escape', (255,255), cv.FONT_HERSHEY_TRIPLEX, 1.0, (0,255,0), 2)
```
---
#Basics 
# Essential Functions
## Converting to Grayscale
- `cvtColor(image_matrix, cv.COLOR_BGR2GRAY)`: This function will convert any given image matrix to grayscale.
```python
img = cv.imread('./Photos/boodha.jpg')
gray = cv.cvtColor(img, cv.COLOR_BGR2GRAY)
cv.imshow('boodha_gray', gray)
```
The `cv.COLOR_BGR2GRAY` is specifically to convert to grayscale. There are other values which can also be used as shown [[#Color Spaces|here]].
## Blurring an image
- `GaussianBlur(image_matrix, (int:a, int:b), bordertype)`: This function will blur the given image according to the given kernel size. The a, b values represent the kernel values. The higher the kernel size more the blur.
```python
blur = cv.GaussianBlur(img, (9,9), cv.BORDER_DEFAULT)
```
## Edge Cascading
- `Canny(image_matrix, int:threshold1, int:threshold2)`: This function cascades the image based on the threshold values.
```python
canny = cv.Canny(image, 125, 175)
```
Before Edge Cascade:
![[Pasted image 20230128205114.png]]
After Edge Cascade:
![[Pasted image 20230128205143.png]]
## Dilating the Edges:
- `dilate(image_matrix, (int:a, int:b), int:iterations)`: This function is used to dilate the edges of an image. The dilation depends on the kernel size given by a, b. 
```python
dilated = cv.dilate(image, (3,3), iterations=1)
```
By increasing the iterations we can see more thicker edges.
## Eroding the Edges
- `erode(image_matrix, (int:a, int:b), int:iterations)`: This function is used to reverse the dilation done on an image.
 ```python
eroded = cv.erode(dilated, (3,3), iterations=1)
```
## Cropping an image
An image can be cropped by simply selecting the necessary range of the cropped matrix of an image.
```python
cropped = image[50:200, 200:400]
cv.imshow('cropped', cropped)
```
Basically array slicing.

---
#Basics 
# Image Transformations
## Translation and Rotation
Translation refers to shifting the image from it's original position along the x and y axis.
- `warpAffine(image_matrix, translated_matrix, (int:height, int:width))`: This function translates the given image matrix to the translated matrix. The tuple in the end represents the height and width of the image. We can write a user defined function as following:
```python
def translate(img, x, y):
    transMat = np.float32([[1,0,x],[0,1,y]])
    dimensions = (img.shape[1], img.shape[0])
    return cv.warpAffine(img, transMat, dimensions)

translated = translate(image, 100, 100)
cv.imshow('translated', translated)
```
The x value used in the user defined `translate()` function defines the translation along the x axis and the y value defines the translation along the y axis. It is similar to relative positioning in css.
The `warpAffine()` function can also be used for rotating the image in a very similar manner.
```python
def rotate(img, angle, rotPoint=None):
    (height, width) = img.shape[:2]
    if rotPoint is None:
        rotPoint = (width//2, height//2)
    rotMat = cv.getRotationMatrix2D(rotPoint, angle, 1.0)
    dimensions = (width, height)
    return cv.warpAffine(img, rotMat, dimensions)

rotated = rotate(image, 45)
cv.imshow('rotated', rotated)
```
The above example rotates the image along the center of the image. We can specify the point along which we want to rotate the image and the image will be rotated along that point. 
The above example rotates the image by 45<sup>o</sup> to the left. We can rotate it towards the right by giving negative values.
The `getRotationMatrix2D()` function is used to generated the rotated matrix. Similar to how we generate the translated matrix using numpy's `float32()`. 
## Flipping an Image
- `flip(image_matrix, int:flip_code)`: This function flips a given image based on the flip code. A flip code of `0` flips the image vertically, and a flip code of `1` flips the image horizontally.
```python
flip = cv.flip(image, 0)
cv.imshow('flipped', flip)
```
A flip code of `-1` flips the image both vertically and horizontally.

---
#Basics 
# Contour Detection
Contours can be defined as the boundaries of any object in an image. Contours and Edges are not the same. Contours are useful during shape analysis and object detection.
- `findContours(edge_dilated_image_matrix, mode, contour_approximation_method)`: This method is used to find the contours in any image. We first cascade the edges of an image and then give the edge cascaded image as the input for this function.
```python
canny = cv.Canny(image, 125,175)

contours, heirarchies = cv.findContours(canny, cv.RETR_LIST, cv.CHAIN_APPROX_NONE)
```
The function returns 2 things:
`contours`: This is a pythong list of all the coordinates of the contours found in the image.
`heirarchies`: This refers to an heirarchical representation of the contours. It represents the heirarchies of objects within an object.
The `cv.RETR_LIST` mode lists all the contours in the image. We have `cv.RETR_EXTERNAL` which retrieves only the external contours. We have `cv.RETR_TREE` which retrieves all heirarchical contours.
The `contour_approximation_method` used in the above example is `cv.CHAIN_APPROX_NONE`. This means there is no approximation method used. It returns all the contours.
We have `cv.CHAIN_APPROX_SIMPLE` which compresses all the contours of an image. Let's say we have a line in an image, using `cv.CHAIN_APPROX_NONE` will give us all the coordinates on that line. Whereas `cv.CHAIN_APPROX_SIMPLE` will give us only the start and end coordinates of the line.
We can gray scale and blur the image and then edge cascade to get better and more accurate contours. We can also use `threshold()` function to binarize the image to get better contours.
- `drawContours(image_matrix, contours_list, int:contourIndx, (rgb color values), int:thickness)`: We can draw the contours detected on a  blank image.
```python
blank = np.zeros(image.shape, dtype='uint8')
cv.drawContours(blank, contours, -1, (0,0,255), 1)
cv.imshow('contours', blank)
```
The `-1` specifies that we want all the contours to be drawn. The color represents the color the contours, and we have specified a thickness of `1`.
As mentioned above we can perform gray scale and blur effect for better results.

---
#Advanced
# Color Spaces
Color spaces are a system of representing an array of pixel colors. RGB is a color space, GrayScale is a color space.
Open CV by default uses BGR while reading an image.
Original BGR:
![[Pasted image 20230129134926.png]]
To convert BGR to Grayscale we use:
```python
gray = cv.cvtColor(image, cv.COLOR_BGR2GRAY)
```
![[Pasted image 20230129134816.png]]
To convert BGR to HSV we use:
```python
hsv = cv.cvtColor(image, cv.COLOR_BGR2HSV)
```
![[Pasted image 20230129135000.png]]
To convert BGR to LAB we use:
```python
lab = cv.cvtColor(image, cv.COLOR_BGR2LAB)
```
![[Pasted image 20230129135220.png]]
To convert BGR to RGB we use:
```python
rgb = cv.cvtColor(image, cv.COLOR_BGR2RGB)
```
![[Pasted image 20230129135837.png]]
Since opencv by default uses BGR when we convert it to RGB we see inversions like red in places of blue etc. Both `imshow()` and `imread()` read in BGR format by default.
We can convert RGB back to BGR, and HSV back to BGR, and Grayscale back to BGR. One of the examples are shown below.
```python
bgr = cv.cvtColor(hsv, cv.COLOR_HSV2BGR)
```
However we cannot convert Grayscale to HSV or LAB to Grayscale etc. We must first convert them to BGR and then convert them to other color spaces.

---
#Advanced 
# Color Channels
A color images consists of multiple color channels such as red, green and blue. We can split the color channels of a particular image using the `split()` function.
- `split(image_matrix)`: This function splits the blue, green and red channels of a particular image.
```python
b, g, r = cv.split(image)
cv.imshow('blue', b)
cv.imshow('green', g)
cv.imshow('red', r)
```
Blue:
![[Pasted image 20230129164043.png]]
Green:
![[Pasted image 20230129164124.png]]
Red:
![[Pasted image 20230129164154.png]]
We can see that these images are in grayscale because they show the distribution of the color intensities. By the split portion of red we can say that the red color channel of our image is the least intense and the blue color channel is the most intense.
Original:
![[Pasted image 20230129134926.png]]
We can merge these color channels using the `merge()` function.
- `merge([blue_channel,green_channel,red_channel])`: This function is used to merge the split color channels.
```python
merged = cv.merge([b,g,r])
```
We get the original image back.
We can also check the color channel intensities by using a blank image as shown below:
```python
b, g, r = cv.split(image)
blank = np.zeros(image.shape[:2],dtype='unit8')
blue = cv.merge([b,blank,blank])
green = cv.merge([blank,g,blank])
red = cv.merge([blank,blank,r])
cv.imshow('Blue', blue)
cv.imshow('Green', green)
cv.imshow('Red', red)
```
Blue:
![[Pasted image 20230129165353.png]]
Green:
![[Pasted image 20230129165446.png]]
Red:
![[Pasted image 20230129165529.png]]
We have essential just isolated the blue, green and red colors from this image. We see that there isn't a lot of red in this image by the output of the Red color channel. We see a lot of black patches. But the image does have a lot of Blue.

---
#Advanced 
# Blurring Techniques
Blurring is essentially done to remove the noise from a particular image.