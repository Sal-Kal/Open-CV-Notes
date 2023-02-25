#Advanced 
# Computing Histogram
Histograms allow you to visualize the distribution of pixel intensities in a particular image.
We can calculate the histogram of a gray-scale image using the `calcHist()` function
- `calcHist([list_of_images], [channel_list], mask_matrix, [hist_size], [range])`:
This function calculates the histogram for a list of images. We can send these images in a list as argument to this function. The `channel_list` specifies the index of the the color channel list for which we want to compute the histogram for. The `mask_matrix` specifies the masked area of the image upon which we want to compute the histogram. The number of bins for which the histogram is to be calculated is given in `hist_size`. The `range` specifies the range of pixel intensity values for which we want to calculate the histogram.
```python
import matplotlib.pyplot as plt

gray = cv.cvtColor(image, cv.COLOR_BGR2GRAY)

gray_hist = cv.calcHist([gray], [0], None, [256], [0,256])

plt.figure()
plt.title('Grayscale Histogram')
plt.xlabel('Bins')
plt.ylabel('# of pixels')
plt.plot(gray_hist)
plt.xlim([0,256])
plt.show()
```
The above example works only for calculating the histogram for gray scale images.
The `channel_list` is `0` because we are computing it for a gray-scale image.
![[Pasted image 20230130201507.png]]
We can see that that around 30000 pixels are of the intensity 25 - 30.
We can see a peak in 30000.
We can compute the histogram on a mask on the image.
We can do this by setting the `mask` parameter in the `calcHist()` function to a masked image matrix as shown in the previous examples of Masking.
In the above example we have set the `mask` value to `None`.
The below code snippet can be used to calculate the histogram of a color image:
```python
colors = ('b','g', 'r')

for i,col in enumerate(colors):
    hist = cv.calcHist([image], [i], None, [256], [0,256])
    plt.plot(hist, color = col)
    plt.xlim([0,256])

plt.show()
```
![[Pasted image 20230213130035.png]]
We can see the histograms computed for all the 3 color channels.
We see a peak of red pixels with the intensity of around 5.