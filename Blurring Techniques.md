#Advanced 
#Blurring
# Blurring Techniques
Blurring is essentially done to remove the noise from a particular image.
## Average Blur
In this technique all the pixels of a given image are given the average values of their surrounding pixels. The surround radius is based on the kernel size given. We can do this by the `blur()` method.
- `blur(image_matrix, (int:a, int:b))`: This function applies average blur on the given image matrix. The tuple argument specifies the kernel size.
```python
average = cv.blur(image, (3,3))
```
The higher the kernel size the more blurry the image.
## Gaussian Blur
Instead of substituting the average value of the surrounding pixels, in Gaussian blur each surrounding pixel is given a particular weight. The average of the products of those weights are substituted. The surround radius is based on the kernel size given. We get less blur compared to average method but the Gaussian blur is more natural compared to the average method.
```python
gauss = cv.GaussianBlur(image, (3,3), 0)
```
## Median Blur
Instead of using average as in average method it uses the median of the surrounding pixels. This method is more effective in reducing noise from an image compared to average method. It is used in advanced computer vision projects. Median blur can be applied using the `medianBlur()` function.
Median blurs look much more like smooth smudges rather than blurs. Binarizing a median blurred image can be done for better object detection.
- `medianBlur(image_matrix, int:kernel_size)`: It doesn't require a tuple for kernel size of same height and width.
```python
median = cv.medianBlur(image, 7)
```
## Bilateral Blur
This is the most effective out of all bluring techniques and is used in the most advanced computing projects. Other blurring techniques do not check if you are reducing the edges in the image or not. But Bilateral Blur blurs the image and retains the edges of the image at the same time.
- `bilateralBlur(image_matrix, int:diameter, int:sigma_color, int:sigma_space)`
We specify a `diamter` instead of a kernel size because the kernel used is a circle. A larger value of the `sigma_color` means that more colors from the surrounding pixels will be considered when calculating the blur. A larger value of the `sigma_space` means that farther more pixels from the center of the kernel will influence the blur.
```python
bilateral = cv.bilateralFilter(image, 20, 35, 35)
```
The blur seems to be very minimal.
