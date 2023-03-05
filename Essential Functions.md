#Basics 
# Essential Functions
## Converting to Gray-scale
- `cvtColor(image_matrix, cv.COLOR_BGR2GRAY)`: This function will convert any given image matrix to gray-scale.
```python
img = cv.imread('./Photos/boodha.jpg')
gray = cv.cvtColor(img, cv.COLOR_BGR2GRAY)
cv.imshow('boodha_gray', gray)
```
The `cv.COLOR_BGR2GRAY` is specifically to convert to gray-scale. There are other values which can also be used as shown [[Color Spaces|here]].
## Blurring an image
#Blurring
- `GaussianBlur(image_matrix, (int:a, int:b), bordertype)`: This function will blur the given image according to the given kernel size. The a, b values represent the kernel values. The higher the kernel size more the blur.
```python
blur = cv.GaussianBlur(img, (9,9), cv.BORDER_DEFAULT)
```
You can read more about blurring [[Blurring Techniques|here]]
## Edge Cascading
#Edge_Detection 
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