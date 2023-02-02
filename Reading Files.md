#Basics
# Reading Images & Videos
### Images
- `imread(str:path)`: This function is used to read an image. Takes the path of the image as input. Returns an image matrix, so must be stored in a variable. This function reads the image in BGR format and not in RGB.
- `imshow(str:window_name, image_matrix)`: This function is used to print an image. The window name can be anything. The image matrix is the output of `imread()` function. This function assumes that the given image is in BGR format and not in RGB. 
We can see more about color spaces [[Color Spaces|here]].
### Videos
- `VideoCapture()`: This function takes an integer as an input or a string which can be the path of a video. Integers are used when you need to use system camera. The values starting from 0 identify the various cameras connected to your system.
- `read()`: Videos captured can't be read with `imshow()` so we use `read()` function to read each frame of the video captured using a loop and then use `imshow()` to show every frame.
```python
capture = cv.VideoCapture('./Videos/Beethoven - Moonlight Sonata (3rd Movement).mp4')

while True:
    isTrue, frame = capture.read()
    cv.imshow('Video', frame)
	# this is to make sure the videos doesn't play in an infinite loop. It waits for 20 ms and then quits when the letter d is pressed.
    if cv.waitKey(20) & 0xFF==ord('d'):
        break

capture.release()
cv.destroyAllWindows()
```
- `waitKey(int:milliseconds)`: This function is used to make sure that when an image is shown using `imshow()` it doesn't just close it immediately after opening the window. The function takes  the parameter in milliseconds. It waits for the specified time and then waits for an input from the keyboard. After the input from the keyboard, window closes and the program continues it's execution. Until the input from the keyboard is given the program waits. By passing a value of 0 in `waitKey()` the program immediately starts waiting for an input from the keyboard.