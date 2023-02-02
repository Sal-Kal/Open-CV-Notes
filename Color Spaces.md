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
