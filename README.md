## Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look
Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

# Features:
Detects the face in an image.
Places a stylish sunglass overlay perfectly on the face.
Works seamlessly with individual passport-size photos.
Customizable for different sunglasses styles or photo types.
# Technologies Used:
Python
OpenCV for image processing
Numpy for array manipulations
# How to Use:
Clone this repository.
Add your passport-sized photo to the images folder.
Run the script to see your "cool" transformation!
# Applications:
Learning basic image processing techniques.
Adding flair to your photos for fun.
Practicing computer vision workflows.
Feel free to fork, contribute, or customize this project for your creative needs!

# Program:
```
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Read images
image = cv2.imread("MY PICTURE.jpeg")
glass = cv2.imread("1.png", cv2.IMREAD_UNCHANGED)

# Convert face image to RGB
image = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

# Position and size
x = 310
y = 325
width = 500


# Resize glasses
height = int(glass.shape[0] * width / glass.shape[1])
glass = cv2.resize(glass, (width, height))

# ROI
roi = image[y:y+height, x:x+width]

# Alpha channel
alpha = glass[:, :, 3] / 255.0
alpha = np.dstack((alpha, alpha, alpha))

# RGB channels of glasses
glass_rgb = cv2.cvtColor(glass[:, :, :3], cv2.COLOR_BGR2RGB)

# Blend
blended = glass_rgb * alpha + roi * (1 - alpha)

# Place result
result = image.copy()
result[y:y+height, x:x+width] = blended.astype(np.uint8)

# Save
cv2.imwrite(
    "output_sunglasses.jpg",
    cv2.cvtColor(result, cv2.COLOR_RGB2BGR)
)

# Show
plt.figure(figsize=(8,10))
plt.imshow(result)

plt.show()
```
# Output:
<img width="1217" height="806" alt="image" src="https://github.com/user-attachments/assets/28556724-fdf6-4db4-b2fd-ab40fd3c934e" />

# Result:
The sunglasses were successfully placed over the eye region of the given image using image masking and alpha blending. The final processed image was displayed successfully in the Jupyter Notebook.
