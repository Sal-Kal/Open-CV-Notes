#Advanced
Thresholding basically means binarization of an image. We define a threshold and based on the threshold the pixels are either `0` or `255`, resulting in a binarized image.
Two types
- Simple Thresholding
- Adaptive Thresholding
## Simple Thresholding
- `threshold(image_matrix, int:threshold_value, int:maxvalue, type)`: This function returns 2 values, the threshold value and an image matrix of the binarized image. The `image_matrix` is the image that we want to binarize, the `threshold_value` is the value of the pixel intensity which acts as a threshold to binarize the image, the `maxval` is the value that we want to set for the pixels that are above the specified threshold.
```python
gray = cv.cvtColor(image, cv.COLOR_BGR2GRAY)
threshold, thresh = cv.threshold(gray, 150, 255, cv.THRESH_BINARY)
cv.imshow('Simple Threshold', thresh)
```
Gray-scale Image:
![[Pasted image 20230129134816.png]]
Binarized Image:
![[Pasted image 20230213134510.png]]
Instead of `cv.THRESH_BINARY` we can set it to `cv.THRESH_BINARY_INV`, which means that the pixels values less than `150` will be set to `255`.
![[Pasted image 20230213134938.png]]
## Adaptive Thresholding
- `adaptiveThreshold(image_matrix, int:maxval, adaptive_method, threshold_type, kernel_size, int:c)`: This function creates a binary image by adaptively setting a threshold.
```python
gray = cv.cvtColor(image, cv.COLOR_BGR2GRAY)
adaptive_thresh = cv.adaptiveThreshold(gray, 255, cv.ADAPTIVE_THRESH_MEAN_C, cv.THRESH_BINARY, 11, 3)
cv.imshow('adaptive', adaptive_thresh)
```
For the `image_matrix` we provide the gray-scale image, the `maxval` is the value we want to set for the pixels that meet the threshold value, the `adaptive_method` is the kind of thresholding done. In this example we have used `cv.ADAPTIVE_THRESH_MEAN_C`, there are other methods such as `ADAPTIVE_THRESH_GAUSSIAN_C`. We then specify the `threshold_type` like in simple thresholding, the kernel size refers to the kernel block used to calculate the mean. The `c` is some mathematical value that is removed from the calculated threshold value.
![[Pasted image 20230213150347.png]]
