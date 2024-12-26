# DIP Lab Final Assignment

## Overview
This repository contains solutions to image processing tasks from the DIP lab final assignment. It covers tasks like: 
- [Task 1: Upload the image(DIP_Lab_task_01.png) from drive with extracting details like: image dimension, frequency distribution of intensities, range. [5]](#task-1)
- [Task 2: Convert the RGB image(DIP_Lab_task_02.jpg) to a gray scale image and compare a sub-region of the image by intensity values(5*5 dimension would be enough for comparison). [10]](#task-2)
- [Task 3: Apply Image(DIP_Lab_task_03.png) smoothing with appropriate kernel applied. Identify the noise(if any) before processing. [35]](#task-3)
- [Task 4: Implement an appropriate technique to reduce the brightness of the provided image (DIP_Lab_task_04.jpg) effectively. [20]](#task-4)
- [Task 5: Solve the segmentation problem for the given image: 'DIP_Lab_task_05.jpg' [30]](#task-5)

## Task 1
- **Description**: 
  In this task, I extructed details of the provided image like: image dimension, frequency distribution of intensities, range.
- **Approach**: 
  I used a simple intensity subtraction method to decrease brightness while ensuring the pixel values remain in valid range.

### Code Walkthrough

### 1. Import Libraries



```bash
  from skimage import io, color
  import numpy as np
  import matplotlib.pyplot as plt

```
- skimage: Used for loading and processing images.
- numpy: Provides tools for working with numerical data, including images as arrays.
- matplotlib.pyplot: Used to display images and plots.

### 2.  Load the Image

```bash
  image_path = r'C:\Users\user\Downloads\DIP_Lab_task_01.png'
  image_array = io.imread(image_path, as_gray=True) 

```
- io.imread: Reads the image from the given path.
- as_gray=True: Converts the image to grayscale (pixel values normalized to the range 0–1).

### 3. Extract Image Dimensions

```bash
  height, width = image_array.shape
  print(f"Image Dimensions: {height}x{width}")

```
- The shape property gives the number of rows (height) and columns (width) in the image.
- Prints the dimensions of the image (e.g., 225x225 pixels).

### 4. Compute Frequency Distribution of Intensities

```bash
  frequency_distribution = {}
  for pixel in image_array.ravel():  # Flatten the 2D array
      frequency_distribution[pixel] = frequency_distribution.get(pixel, 0) + 1

```
- image_array.ravel(): Converts the 2D array of pixel values into a 1D list for easy processing.
- frequency_distribution: A dictionary that keeps track of how often each pixel intensity appears in the image.

### 5. Print the Frequency Distribution

```bash
  print("Frequency Distribution of Intensities:")
  for intensity, frequency in sorted(frequency_distribution.items()):
      print(f"Intensity {intensity}: {frequency}")
```
- Loops through the intensity values and their frequencies, printing them in ascending order.

### 6.  Compute Intensity Range

```bash
  min_intensity = np.min(image_array)
  max_intensity = np.max(image_array)
  print(f"Intensity Range: {min_intensity} to {max_intensity}")

```
- np.min: Finds the smallest pixel intensity in the image.
- np.max: Finds the largest pixel intensity in the image.
- Prints the range of pixel intensities (e.g., 0.0 to 1.0).

### 7. Display the Grayscale Image

```bash
  plt.figure(figsize=(6, 6))
  plt.imshow(image_array, cmap='gray', vmin=0, vmax=255)
  plt.title("Grayscale Image")
  plt.axis('off')
  plt.show()

```
- plt.imshow: Displays the image.
- cmap='gray': Ensures the image is displayed in grayscale.
- vmin=0, vmax=255: Maps the intensity values from the normalized range (0–1) to 8-bit (0–255).
- plt.axis('off'): Hides the axes for cleaner visualization.

### 8. Plot the Histogram
```bash
  plt.figure(figsize=(8, 6))
  plt.hist(image_array.ravel(), bins=256, range=(0, 255), color='gray', alpha=0.7)
  plt.title("Frequency Distribution of Intensities")
  plt.xlabel("Intensity Value")
  plt.ylabel("Frequency")
  plt.grid(True)
  plt.show()


```
- plt.hist: Creates a histogram showing the frequency of each pixel intensity.
- bins=256: Divides the range of intensities into 256 bins (one for each possible grayscale value).
- range=(0, 255): Maps normalized values to the 0–255 range.
- color='gray': Uses a gray color for the histogram bars.
- plt.grid: Adds a grid for easier interpretation.
