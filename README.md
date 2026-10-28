# Geometric-Transformations-Using-OpenCV


## Aim

To write a Python program using OpenCV to perform various geometric transformations on an image, including translation, scaling, shearing, reflection, and rotation.

## Software Requirements

- Python 3
- Anaconda / Jupyter Notebook / VS Code
- OpenCV (`cv2`)
- NumPy
- Matplotlib

## Algorithm

1. Import the required libraries: OpenCV, NumPy, and Matplotlib.
2. Read the input image in color mode.
3. **Image Translation:** Create a translation matrix and shift the image 50 pixels right and 80 pixels down using `cv2.warpAffine()`.
4. **Image Scaling:** Resize the image to 0.5× and 2× using `cv2.resize()`.
5. **Image Shearing:** Create horizontal and vertical shearing matrices and apply them using `cv2.warpAffine()`.
6. **Image Reflection:** Perform horizontal, vertical, and both-axis flipping using `cv2.flip()`.
7. **Image Rotation:** Rotate the image by 45° and 90° using `cv2.getRotationMatrix2D()` and `cv2.warpAffine()`.
8. Display the original and transformed images using Matplotlib.

## Program

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

img = cv2.imread("parrot.jpg")

if img is None:
    print("Error: parrot.jpg not found!")
    raise SystemExit

img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
height, width = img.shape[:2]

# Image Translation
translation_matrix = np.float32([
    [1, 0, 50],
    [0, 1, 80]
])

translated = cv2.warpAffine(
    img, translation_matrix, (width, height)
)

# Image Scaling
downscaled = cv2.resize(img, None, fx=0.5, fy=0.5)
upscaled = cv2.resize(img, None, fx=2, fy=2)

# Image Shearing
horizontal_matrix = np.float32([
    [1, 0.5, 0],
    [0, 1, 0]
])

vertical_matrix = np.float32([
    [1, 0, 0],
    [0.5, 1, 0]
])

horizontal_shear = cv2.warpAffine(
    img, horizontal_matrix,
    (int(width * 1.5), height)
)

vertical_shear = cv2.warpAffine(
    img, vertical_matrix,
    (width, int(height * 1.5))
)

# Image Reflection
horizontal_flip = cv2.flip(img, 1)
vertical_flip = cv2.flip(img, 0)
both_flip = cv2.flip(img, -1)

# Image Rotation
center = (width // 2, height // 2)

rotation_45_matrix = cv2.getRotationMatrix2D(
    center, 45, 1.0
)

rotation_90_matrix = cv2.getRotationMatrix2D(
    center, 90, 1.0
)

rotated_45 = cv2.warpAffine(
    img, rotation_45_matrix, (width, height)
)

rotated_90 = cv2.warpAffine(
    img, rotation_90_matrix, (width, height)
)

# Function to display images
def show_images(title, images):
    count = len(images)
    fig, axes = plt.subplots(
        1, count, figsize=(5 * count, 5)
    )

    fig.suptitle(title, fontsize=16)

    if count == 1:
        axes = [axes]

    for ax, (image, label) in zip(axes, images):
        ax.imshow(image)
        ax.set_title(label)
        ax.axis("off")

    plt.tight_layout()
    plt.show()

# Display Original Image
show_images("Original Image", [
    (img, "Original")
])

# Display Translation
show_images("Image Translation", [
    (img, "Original"),
    (translated, "Translated")
])

# Display Scaling
show_images("Image Scaling", [
    (img, "Original"),
    (downscaled, "Downscaled 0.5x"),
    (upscaled, "Upscaled 2x")
])

# Display Shearing
show_images("Image Shearing", [
    (img, "Original"),
    (horizontal_shear, "Horizontal Shear"),
    (vertical_shear, "Vertical Shear")
])

# Display Reflection
show_images("Image Reflection", [
    (img, "Original"),
    (horizontal_flip, "Horizontal Flip"),
    (vertical_flip, "Vertical Flip"),
    (both_flip, "Both Axes Flip")
])

# Display Rotation
show_images("Image Rotation", [
    (img, "Original"),
    (rotated_45, "Rotation 45 Degrees"),
    (rotated_90, "Rotation 90 Degrees")
])
```

## Output

### 1. Image Translation
<img width="422" height="313" alt="image" src="https://github.com/user-attachments/assets/d4038cd0-9009-4ca9-b95e-6c186c5a7e98" />

### 2. Image Scaling

<img width="437" height="152" alt="image" src="https://github.com/user-attachments/assets/7c9187c5-8d79-4da0-8b72-155bb204faa7" />


### 3. Image Shearing
<img width="422" height="305" alt="image" src="https://github.com/user-attachments/assets/caabf60a-0026-4f34-a09d-60f56ccdac90" />

### 4. Image Reflection

<img width="427" height="311" alt="image" src="https://github.com/user-attachments/assets/5e04ae4d-da29-4463-9145-027eae50e193" />


### 5. Image Rotation

<img width="417" height="311" alt="image" src="https://github.com/user-attachments/assets/de08ac00-44eb-405c-8861-a362d20f2a38" />


## Result

Thus, geometric transformations including translation, scaling, shearing, reflection, and rotation were successfully performed on an image using OpenCV.


