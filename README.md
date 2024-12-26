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
  In this task, I analyzed a grayscale image by extracting details such as its dimensions, intensity distribution, and intensity range. Additionally, I displayed the image and plotted a histogram to visualize the frequency distribution of pixel intensities.
- **Approach**: 
  I processed the image by loading it as grayscale, extracted intensity distributions, and visualized the frequency of pixel intensities using NumPy and Matplotlib.

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


## Task 2
- **Description**: 
   In this task, I extracted and visualized a sub-region of a provided RGB image and its corresponding grayscale representation. Additionally, the original images and the sub-region values were displayed.
- **Approach**: 
   I used skimage to load the image and convert it to grayscale. A specific sub-region was extracted from both the RGB and grayscale images, and the pixel values were visualized.

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

### 2.  Load the RGB Image

```bash
  image_path = r'C:\Users\user\Downloads\DIP_Lab_task_02.jpg'
  image_rgb = io.imread(image_path)

```
- io.imread: Reads the image from the given path.

### 3. Convert to Grayscale

```bash
  image_gray = color.rgb2gray(image_rgb)
  image_gray = (image_gray * 255).astype(np.uint8)

```
- color.rgb2gray: Converts the RGB image to grayscale (pixel values normalized to the range 0–1).
- (image_gray * 255).astype(np.uint8): Scales the pixel values to 8-bit integers (range 0–255).

### 4. Extract a Sub-region (5x5)

```bash
  start_x, start_y = 50, 50
  sub_region_rgb = image_rgb[start_y:start_y + 5, start_x:start_x + 5]
  sub_region_gray = image_gray[start_y:start_y + 5, start_x:start_x + 5]

```
- Extracts a 5x5 pixel sub-region starting at the coordinates (50, 50) from both the RGB and grayscale images.

### 5. 5. Display the Original RGB and Grayscale Images

```bash
  plt.figure(figsize=(12, 6))
  plt.subplot(1, 2, 1)
  plt.imshow(image_rgb)
  plt.title("Original RGB Image")
  plt.axis('off')

  plt.subplot(1, 2, 2)
  plt.imshow(image_gray, cmap='gray', vmin=0, vmax=255)
  plt.title("Grayscale Image")
  plt.axis('off')
  plt.show()

```
- plt.imshow: Displays the images.
- cmap='gray': Ensures the grayscale image is displayed correctly.
- plt.axis('off'): Hides the axes for cleaner visualization.

### 6.  Display Sub-region Values

```bash
  print("Sub-region (5x5) from RGB Image:")
  print(sub_region_rgb)

  print("\nSub-region (5x5) from Grayscale Image:")
  print(sub_region_gray)

```
- Prints the pixel values of the 5x5 sub-region for both RGB and grayscale images.

### 7. Visualize the 5x5 Grayscale Sub-region

```bash
  plt.figure(figsize=(4, 4))
  plt.imshow(sub_region_gray, cmap='gray', vmin=0, vmax=255)
  plt.title("5x5 Sub-region of Grayscale Image")
  plt.axis('on')
  plt.show()

```
- plt.imshow: Displays the grayscale sub-region.
- plt.axis('on'): Shows the axes for precise location information.


## Task 3
- **Description**: 
  In this task, I applied a median filter to reduce noise in a grayscale image using both 3x3 and 5x5 kernel sizes. The original image with noise was displayed, followed by the images after filtering to visualize the noise reduction effect.
- **Approach**: 
  I applied a median filter manually to smooth the image and reduce noise. A smaller kernel size (3x3) was used first, followed by a larger kernel size (5x5) to observe the impact of filter size on noise reduction.
  
### Code Walkthrough

### 1. Import Libraries



```bash
  from PIL import Image
  import numpy as np
  import matplotlib.pyplot as plt

```
- PIL: Used for loading and processing images.
- numpy: Provides tools for working with numerical data, including images as arrays.
- matplotlib.pyplot: Used to display images and plots.

### 2.  Load the Image

```bash
  image_path = r'C:\Users\user\Downloads\DIP_Lab_task_03.png'
  image = Image.open(image_path).convert('L')
  image_array = np.array(image)

```
- Image.open: Opens the image from the specified path.
- convert('L'): Converts the image to grayscale.
- np.array: Converts the image to a NumPy array for easier processing.

### 3. Display the Original Image

```bash
  plt.figure(figsize=(8, 6))
  plt.title("Original Image with Noise")
  plt.imshow(image_array, cmap='gray', vmin=0, vmax=255)
  plt.axis('off')
  plt.show()

```
- plt.imshow: Displays the image in grayscale.
- vmin=0, vmax=255: Ensures pixel values are displayed in the 0-255 range.
- plt.axis('off'): Hides axis for cleaner visualization.

### 4. Apply Median Filter (3x3 Kernel)

```bash
  def apply_median_filter(image, kernel_size=3):
      padded_image = np.pad(image, kernel_size // 2, mode='constant', constant_values=0)
      filtered_image = np.zeros_like(image)
      for i in range(image.shape[0]):
          for j in range(image.shape[1]):
              region = padded_image[i:i + kernel_size, j:j + kernel_size]
              filtered_image[i, j] = np.median(region)
      return filtered_image

  smoothed_image = apply_median_filter(image_array, kernel_size=3)


```
- apply_median_filter: A custom function to apply the median filter to smooth the image.
- padded_image: Adds padding around the image to handle border pixels.
- np.median: Computes the median of the pixel values in the kernel region.
- smoothed_image: The filtered image using a 3x3 kernel.

### 5. Display Smoothed Image (3x3 Kernel)

```bash
  plt.figure(figsize=(8, 6))
  plt.title("Smoothed Image (Median Filter Applied)")
  plt.imshow(smoothed_image, cmap='gray', vmin=0, vmax=255)
  plt.axis('off')
  plt.show()

```

### 6.  Apply Median Filter (5x5 Kernel)

```bash
  smoothed_image_5x5 = apply_median_filter(image_array, kernel_size=5)


```
- Applies the median filter using a 5x5 kernel to observe the effect of increased kernel size.

### 7. Display Smoothed Image (5x5 Kernel)

```bash
  plt.figure(figsize=(8, 6))
  plt.title("Smoothed Image (Median Filter with 5x5 Kernel)")
  plt.imshow(smoothed_image_5x5, cmap='gray', vmin=0, vmax=255)
  plt.axis('off')
  plt.show()

```





