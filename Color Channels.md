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
