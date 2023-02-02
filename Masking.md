#Advanced 
# Masking
Masking allows us to focus or work on particular regions or objects of an image.
The dimensions of a mask has to be the same as that of an image.
Original Image:
![[Pasted image 20230130195701.png]]
We can apply a mask in the following manner:
```python
blank = np.zeros(image.shape[:2], dtype='uint8')

mask = cv.circle(blank, (image.shape[1]//2, image.shape[0]//2), 100, 255, -1)

cv.imshow('Mask', mask)

masked = cv.bitwise_and(image, image, mask = mask)
cv.imshow('Masked', masked)
```
We first create a blank image and then create a masked region, a cirlcle in the center in this case.
Then we use `bitwise_and()` function to apply this mask on our image.
Masked:
![[Pasted image 20230130195917.png]]
We can see that a circular region in the center is only visible from the original image. The rest is masked.
We can move the center of circle around or use other shapes like rectangles.
