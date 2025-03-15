# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.

## Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## How to Use:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

## Program:
### Name: Samakash R S
### Reg No: 212223230182
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Read the input face image
img = cv2.imread('Akash (1).jpg')
# Display the face image with RGB channels (OpenCV uses BGR, Matplotlib uses RGB)
plt.imshow(img[:,:,::-1]);plt.title("Face")

# Read the sunglasses image with alpha channel (4 channels: BGR + Alpha)
glassPNG = cv2.imread('glass2.png', -1)
# Display the sunglasses image
plt.imshow(glassPNG[:,:,::-1]);plt.title("glass")

# Resize the sunglasses to fit on the face
glassPNG = cv2.resize(glassPNG, (200, 60))
print("image Dimension =", glassPNG.shape)

# Extract the BGR channels and the alpha channel separately from the sunglasses image
glassBGR = glassPNG[:, :, 0:3]  # BGR part
glassMask1 = glassPNG[:, :, 3]  # Alpha channel (transparency)

# Display the sunglasses' BGR channels and alpha channel
plt.figure(figsize=[15, 15])
plt.subplot(121); plt.imshow(glassBGR[:, :, ::-1]); plt.title('Sunglass Color channels')
plt.subplot(122); plt.imshow(glassMask1, cmap='gray'); plt.title('Sunglass Alpha channel')

# Copy the original face image to avoid altering it
faceWithGlasses = img.copy()
# Overlay the sunglasses BGR part onto the face image at the specified location
faceWithGlasses[160:220, 105:305] = glassBGR
# Display the face with sunglasses
plt.imshow(faceWithGlasses[..., ::-1])

# Create a mask using the alpha channel and normalize its values to 0 and 1
glassMask = cv2.merge((glassMask1, glassMask1, glassMask1))  # Merge alpha channel to 3-channel mask
glassMask = np.uint8(glassMask / 255)  # Normalize values to 0-1

# Copy the original face image for further processing
faceWithGlassesArithmetic = img.copy()
# Select the region of interest (ROI) where the glasses will be placed
eyeROI = faceWithGlassesArithmetic[160:220, 105:305]
# Mask the eye region by keeping only the background
maskedEye = cv2.multiply(eyeROI, (1 - glassMask))
# Mask the sunglasses image by keeping only the sunglasses part
maskedGlass = cv2.multiply(glassBGR, glassMask)
# Combine the masked eye region and masked sunglasses to create the final augmented ROI
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)

# Display the masked eye, masked sunglasses, and final augmented region
plt.figure(figsize=[20, 20])
plt.subplot(131); plt.imshow(maskedEye[..., ::-1]); plt.title("Masked Eye Region")
plt.subplot(132); plt.imshow(maskedGlass[..., ::-1]); plt.title("Masked Sunglass Region")
plt.subplot(133); plt.imshow(eyeRoiFinal[..., ::-1]); plt.title("Augmented Eye and Sunglass")

# Replace the original eye region in the face image with the augmented region
faceWithGlassesArithmetic[160:220, 105:305] = eyeRoiFinal

# Display the final output image
plt.figure(figsize=[10, 10])
plt.subplot(121); plt.imshow(img[:, :, ::-1]); plt.title("Original Image")
plt.subplot(122); plt.imshow(faceWithGlassesArithmetic[:, :, ::-1]); plt.title("With Sunglasses")

```
## Output:
### 1.Original image:
![alt text](<Akash (1).jpg>)

### 2.Glass:
![alt text](<Screenshot 2025-03-08 114525.png>)

### 3.Glass color channel:
![alt text](<Screenshot 2025-03-08 114616.png>)

### 4.Face With Glass:
![alt text](<Screenshot 2025-03-08 114640.png>)

### 5.Eye and glass region:
![alt text](<Screenshot 2025-03-08 114739.png>)

### 6.Final image with glass:
![alt text](<Screenshot 2025-03-08 114657.png>)

## Result:
Thus, the creative project designed to overlay sunglasses on individual passport size photo has been successfully executed.