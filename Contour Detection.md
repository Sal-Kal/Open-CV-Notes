#Basics 
# Contour Detection
Contours can be defined as the boundaries of any object in an image. Contours and Edges are not the same. Contours are useful during shape analysis and object detection.
- `findContours(edge_dilated_image_matrix, mode, contour_approximation_method)`: This method is used to find the contours in any image. We first cascade the edges of an image and then give the edge cascaded image as the input for this function.
```python
canny = cv.Canny(image, 125,175)

contours, heirarchies = cv.findContours(canny, cv.RETR_LIST, cv.CHAIN_APPROX_NONE)
```
The function returns 2 things:
`contours`: This is a python list of all the coordinates of the contours found in the image.
`heirarchies`: This refers to an hierarchical representation of the contours. It represents the hierarchies of objects within an object.
The `cv.RETR_LIST` mode lists all the contours in the image. We have `cv.RETR_EXTERNAL` which retrieves only the external contours. We have `cv.RETR_TREE` which retrieves all hierarchical contours.
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
