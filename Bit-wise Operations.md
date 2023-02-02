#Advanced 
# Bitwise Operations
## Bitwise AND
A bitwise  operation of AND on two images  returns the intersection of the 2 images. We can use the `bitwise_and()` function for this.
- `bitwise_and(image_matrix_a, image_matrix_b)`: This function takes two image matrix and returns the intersection of the two images.
```python
blank = np.zeros((400,400), dtype="uint8")

rectangle = cv.rectangle(blank.copy(), (30,30), (370, 370), 255, -1)
circle = cv.circle(blank.copy(), (200,200), 200, 255, -1)

cv.imshow('Rectangle', rectangle)
cv.imshow('Circle', circle)

bitwise_and = cv.bitwise_and(rectangle, circle)
cv.imshow('bitwise and',bitwise_and)
```
Rectangle:
![[Pasted image 20230130193019.png]]
Circle:
![[Pasted image 20230130193102.png]]
Bitwise AND:
![[Pasted image 20230130193151.png]]
## Bitwise OR
A Bitwise operation of OR on two images returns the interesecting and none intersecting parts of the two images.
- `bitwise_or(image_matrix_a, image_matrix_b)`: This function is similar to `bitwise_and()` in function signature.
```python
bitwise_or = cv.bitwise_or(rectangle, circle)
cv.imshow('bitwise or',bitwise_or)
```
Bitwise OR:
![[Pasted image 20230130193505.png]]
## Bitwise XOR
The bitwise operation of XOR between 2 images is the non intersecting regions of the two images.
- `bitwise_xor(image_matrix_a, image_matrix_b)`: This function has the same function signature as `bitwise_and()` function.
```python
bitwise_xor = cv.bitwise_or(rectangle, circle)
cv.imshow('bitwise xor',bitwise_xor)
```
Bitwise XOR:
![[Pasted image 20230130194032.png]]
## Bitwise NOT
This function returns the not operation on each pixel of a given image.
`bitwise_not(image_matrix)`: The bitwise not operation is applied on  each pixel of the image.
```python
bitwise_not = cv.bitwise_not(rectangle)
cv.imshow('Bitwise not', bitwise_not) 
```
Bitwise NOT:
![[Pasted image 20230130194508.png]]
