# Lane Detection in Video Frames

This project uses OpenCV to detect and visualize road lane markings in video footage. The program processes each frame through a pipeline of color filtering, edge detection, and line detection to identify left and right lane boundaries. It then computes and draws a center line between the two lanes. Processed frames are displayed in real time.

## Features

- **Lane Boundary Detection**: Identifies left and right lane lines using the Hough Line Transform with slope-based classification.
- **Center Line Calculation**: Computes a midline between detected lanes using slope interpolation, extended to the bottom of the frame.
- **Real-Time Processing**: Processes and displays each video frame as lanes are detected.
- **Color and Edge Filtering**: Isolates lane markings by removing light-colored regions and detecting dark edges via Canny edge detection.

## Project Structure

- `main.py`: Contains all lane detection logic — video capture, image processing, line detection, lane classification, center line computation, and display.

## How It Works

1. **Read Frame**: The program reads the video file frame by frame.
2. **Color Filtering**: Light-colored regions are masked out to isolate darker lane features.
3. **Grayscale + Blur**: The filtered frame is converted to grayscale and blurred with a Gaussian kernel to reduce noise.
4. **Dark Area Isolation**: Pixels within a specific intensity range (50–100) are isolated, then Canny edge detection is applied.
5. **Region of Interest**: A trapezoid mask limits detection to the lower portion of the frame where lanes typically appear.
6. **Line Detection**: The Hough Line Transform detects line segments within the masked region.
7. **Lane Classification**: Lines are separated into left and right lanes based on slope (positive slope = right, negative = left). Near-horizontal lines are discarded.
8. **Center Line**: The midpoint between the two lane boundaries is calculated and extended to the bottom of the frame.
9. **Display**: The original frame is overlaid with pink lane lines and a blue center line, then displayed.

## Usage

**Prepare the Video File:**

Place the video file in the same directory as the script. The default filename is `IMG_8204.MOV`. Update the `cv2.VideoCapture("IMG_8204.MOV")` line in `main.py` to use a different file if needed.

**Run the Program:**

```bash
python main.py
```

**Controls:**

- The video plays in a window titled `"E"`.
- Press `i` to stop processing and exit.

## Functions

### `apply_color_mask(image, lower, upper)`

Applies a BGR color range mask to an image and returns only the pixels within that range.

- **Parameters:**
  - `image`: Input BGR image.
  - `lower`: Lower bound BGR tuple.
  - `upper`: Upper bound BGR tuple.
- **Returns:** Masked image.

### `apply_filtering(image)`

Removes light-colored regions from the image to isolate potential lane edges.

- **Parameters:**
  - `image`: Input BGR image.
- **Returns:** Filtered image with light areas subtracted.

### Main Loop

- Reads each frame and applies the full detection pipeline.
- Classifies detected lines into left/right lanes by slope.
- Computes lane boundary endpoints from min/max coordinates.
- Calculates center line endpoints via slope interpolation between left and right boundaries.
- Draws left lane (pink), right lane (pink), and center line (blue) on the frame.

## Requirements

- Python 3.x
- OpenCV (`cv2`)
- NumPy

Install dependencies:

```bash
pip install opencv-python numpy
```
