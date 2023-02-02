#Basics 
# Resizing and Re-scaling
The height and width of a particular image frame can be accessed by using the `shape` array in the dot operator.
```python
height = frame.shape[0]
width = frame.shape[1]
```
- `resize(frame, (int:width, int:height), interpolation)`: This function can be used to resize a particular frame. It returns a resized frame. The first argument is the frame we want to resize, the second argument is a tuple containing the resized width and height that we desire. The Third argument is the type of interpolation. Interpolation refers to the way the extra pixels are calculated.
```python
# Rescaling function
def rescaleFrame(frame, scale = 0.75):
    width = int(frame.shape[1] * scale)
    height = int(frame.shape[0] * scale)
    dimensions = (width, height)

    return cv.resize(frame, dimensions, interpolation=cv.INTER_AREA)

# Playing a video in both original and rescaled form
while True:
    isTrue, frame = capture.read()

    frame_resized = rescaleFrame(frame)

    cv.imshow('Video', frame)
    cv.imshow('resized', frame_resized)

    if cv.waitKey(20) & 0xFF==ord('d'):
        break

capture.release()
cv.destroyAllWindows()
```
The capture object in the above example can be rescaled using the `set()` function.
```python
def changeRes(width, height):
	capture.set(3,width)
	capture.set(4,height)
```
Where 3 references the width of the capture frame, and 4 references the height of the captured frame. Hence new values of width and height can be set to a captured frame using the `set()` function.
It is important to note that the user defined `changeRes()` function only works for Live Videos and will not working with any stored video. For existing stored videos we can use the user define `rescaleFrame()` function.
