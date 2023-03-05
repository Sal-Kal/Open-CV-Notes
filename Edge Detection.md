#Advanced
#Edge_Detection
## Laplacian
- `Laplacian(image_matrix, ddepth)`: This function can be used to detect the edges using the Laplacian method. The below code snippet shows an example.
```python
gray = cv.cvtColor(image, cv.COLOR_BGR2GRAY)
lap = cv.Laplacian(gray, cv.CV_64F)
lap = np.uint8(np.absolute(lap))
cv.imshow('Laplacian', lap)
```
Original Gray-scale
![[Pasted image 20230129134816.png]]
After Edge Detection
![[Pasted image 20230216111122.png]]
## Sobel
- `Sobel(image_matrix, ddepth, int:dx, int:dy)`: This function can be used to detect the edges using the Sobel method.
```python
gray = cv.cvtColor(image, cv.COLOR_BGR2GRAY)

sobelx = cv.Sobel(gray, cv.CV_64F, 1, 0)
sobely = cv.Sobel(gray, cv.CV_64F, 0, 1)

cv.imshow("Sobel x", sobelx)
cv.imshow("Sobel y", sobely)
```
Sobel X:
![[Pasted image 20230305140001.png]]
We can see the X axis specific gradients.
Sobel Y:
![[Pasted image 20230305140030.png]]
We can see the Y axis specific gradients.
We can also get the Combined Sobel image by combining these two using the `bitwise_or()` function.
```python
gray = cv.cvtColor(image, cv.COLOR_BGR2GRAY)

sobelx = cv.Sobel(gray, cv.CV_64F, 1, 0)
sobely = cv.Sobel(gray, cv.CV_64F, 0, 1)

combined_sobel = cv.bitwise_or(sobelx, sobely)
cv.imshow("Combined Sobel", combined_sobel)
```
Combined Sobel:
![[Pasted image 20230305140432.png]]
The Canny Edge detection mentioned [[Essential Functions#Edge Cascading|here]] is a bit advanced edge detection algorithm which uses the Sobel method in one of it's steps. 