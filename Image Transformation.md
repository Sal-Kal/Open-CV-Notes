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
The `x` value used in the user defined `translate()` function defines the translation along the x axis and the y value defines the translation along the y axis. It is similar to relative positioning in CSS.
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
The `getRotationMatrix2D()` function is used to generated the rotated matrix. Similar to how we generate the translated matrix using the `float32()` function from the `numpy` library. 
## Flipping an Image
- `flip(image_matrix, int:flip_code)`: This function flips a given image based on the flip code. A flip code of `0` flips the image vertically, and a flip code of `1` flips the image horizontally.
```python
flip = cv.flip(image, 0)
cv.imshow('flipped', flip)
```
A flip code of `-1` flips the image both vertically and horizontally.