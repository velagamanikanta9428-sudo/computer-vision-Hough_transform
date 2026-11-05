# Line and Circle Detection Using Hough Transform

## Aim
To detect straight lines and circular shapes in an input image using the Hough Transform techniques in OpenCV.

## Overview
This notebook performs line detection and circle detection on an input image.

### Part A: Line Detection
1. Loads the input image.
2. Checks whether the image was loaded successfully.
3. Creates a copy of the original image for drawing detected shapes.
4. Converts the image to grayscale.
5. Applies Canny edge detection.
6. Uses the Probabilistic Hough Line Transform (`cv2.HoughLinesP()`) to detect line segments.
7. Draws detected lines in green.

### Part B: Circle Detection
1. Applies a 5 × 5 median blur to the grayscale image to reduce noise.
2. Uses the Hough Circle Transform (`cv2.HoughCircles()`) to detect circles.
3. Draws detected circle boundaries in red.
4. Marks the center of each detected circle in blue.

### Part C: Display Result
Displays the final image with detected lines and circles.

## Technologies Used
- Python
- OpenCV (`cv2`)
- NumPy
- Matplotlib
- Jupyter Notebook / Google Colab

## Project Structure
```text
CV-Lab-11/
├── CVLAB11.ipynb
├── images013.jpg       
└── README.md
```

## Requirements
Install the required Python packages:

```bash
pip install opencv-python numpy matplotlib
```

## How to Run

### Option 1: Jupyter Notebook

1. Download or clone this repository.
2. Open a terminal in the project folder.
3. Install the dependencies:
   ```bash
   pip install opencv-python numpy matplotlib
   ```
4. Place `images013.jpg` in the project folder.
5. Open the notebook:
   ```bash
   jupyter notebook CVLAB11.ipynb
   ```
6. Update the image path in the notebook if necessary.
7. Run the notebook cell.

### Option 2: Google Colab

1. Upload `CVLAB11.ipynb` to Google Colab.
2. Upload `images013.jpg` to your Google Drive under the `COMPUTER VISION` folder.
3. Mount Google Drive if it is not already mounted:
   ```python
   from google.colab import drive
   drive.mount('/content/drive')
   ```
4. Run the notebook cell.

## Important Code

### Load and Convert the Image

```python
img = cv2.imread('/content/drive/MyDrive/COMPUTER VISION/images013.jpg')
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
```

### Canny Edge Detection

```python
edges = cv2.Canny(gray, 50, 150, apertureSize=3)
```

Canny edge detection identifies image edges before line detection.

### Probabilistic Hough Line Transform

```python
lines = cv2.HoughLinesP(
    edges, 1, np.pi / 180, 100,
    minLineLength=100, maxLineGap=10
)
```

Detected line segments are drawn in **green**.

### Hough Circle Transform

```python
gray_blurred = cv2.medianBlur(gray, 5)

circles = cv2.HoughCircles(
    gray_blurred,
    cv2.HOUGH_GRADIENT,
    1,
    20,
    param1=50,
    param2=30,
    minRadius=0,
    maxRadius=0
)
```

Detected circle boundaries are drawn in **red**, and their centers are marked in **blue**.

## Expected Output
The notebook displays the input image with:
- **Green lines** representing detected line segments.
- **Red circles** representing detected circular boundaries.
- **Blue points** representing the centers of detected circles.

If no lines or circles are detected, the output will show only the shapes that the algorithm successfully identifies.

## Troubleshooting
- **Image not found:** Confirm that `images013.jpg` exists at the path used by `cv2.imread()`.
- **No lines detected:** The result depends on the image and the Canny/Hough parameters.
- **No circles detected:** Try adjusting the Hough Circle parameters, especially `param2`, based on the input image.
- **Missing module:** Install the required packages using the commands in the Requirements section.

## Notes
- The notebook uses Canny thresholds of `50` and `150`.
- The Hough Line Transform uses a threshold of `100`, minimum line length of `100`, and maximum line gap of `10`.
- The circle detector uses `cv2.HOUGH_GRADIENT` with `param1=50` and `param2=30`.
- The notebook expects the input image `images013.jpg`; add it to the repository so others can reproduce the experiment.

## Author
Velaga Manikanta Sai.

241FA23016.

III-Data Science.
