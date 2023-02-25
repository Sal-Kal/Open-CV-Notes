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


