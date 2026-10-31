# Ex.No.6---Record-edge-detection

## Aim

To perform edge detection using Sobel, Roberts, Prewitt, Laplacian, and Canny edge detectors.

## Software Required

- Anaconda – Python 3.7  
- Jupyter Notebook / VS Code  
- OpenCV (cv2)  
- NumPy  
- Matplotlib 

## Algorithm

### Step 1:
Import all the necessary modules for the program.

### Step 2:
Load an image using `cv2.imread()`.

### Step 3:
Convert the image to grayscale.

### Step 4:
Apply **Sobel operator** using OpenCV to detect edges.

### Step 5:
Apply **Prewitt operator** using custom kernels.

### Step 6:
Apply **Roberts operator** using custom kernels.

### Step 7:
Apply **Laplacian operator** using OpenCV.

### Step 8:
Apply **Canny edge detector** using OpenCV.

### Step 9:
Display all edge-detected images for comparison.

## Developed By

# Name: Vijiyalakshmi A 
# Register No: 212225240185

```
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Step 1: Load the image
img = cv2.imread("tom_jerry.jpg")

if img is None:
    print("Image not found! Check the filename.")
else:
    # Step 2: Convert the image to grayscale
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

    # Step 3: Sobel operator
    sobel_x = cv2.Sobel(gray, cv2.CV_64F, 1, 0, ksize=3)
    sobel_y = cv2.Sobel(gray, cv2.CV_64F, 0, 1, ksize=3)
    sobel = cv2.magnitude(sobel_x, sobel_y)
    sobel = cv2.convertScaleAbs(sobel)

    # Step 4: Prewitt operator using custom kernels
    prewitt_x = np.array([[-1, 0, 1],
                          [-1, 0, 1],
                          [-1, 0, 1]], dtype=np.float32)

    prewitt_y = np.array([[-1, -1, -1],
                          [ 0,  0,  0],
                          [ 1,  1,  1]], dtype=np.float32)

    px = cv2.filter2D(gray, cv2.CV_32F, prewitt_x)
    py = cv2.filter2D(gray, cv2.CV_32F, prewitt_y)
    prewitt = cv2.magnitude(px, py)
    prewitt = cv2.convertScaleAbs(prewitt)

    # Step 5: Roberts operator using custom kernels
    roberts_x = np.array([[1, 0],
                          [0, -1]], dtype=np.float32)

    roberts_y = np.array([[0, 1],
                          [-1, 0]], dtype=np.float32)

    rx = cv2.filter2D(gray, cv2.CV_32F, roberts_x)
    ry = cv2.filter2D(gray, cv2.CV_32F, roberts_y)
    roberts = cv2.magnitude(rx, ry)
    roberts = cv2.convertScaleAbs(roberts)

    # Step 6: Laplacian operator
    laplacian = cv2.Laplacian(gray, cv2.CV_64F, ksize=3)
    laplacian = cv2.convertScaleAbs(laplacian)

    # Step 7: Canny edge detector
    canny = cv2.Canny(gray, 50, 150)

    # Step 8: Display all images for comparison
    titles = ["Original Image", "Grayscale", "Sobel",
              "Prewitt", "Roberts", "Laplacian", "Canny"]

    images = [cv2.cvtColor(img, cv2.COLOR_BGR2RGB),
              gray, sobel, prewitt, roberts, laplacian, canny]

    plt.figure(figsize=(14, 10))

    for i in range(len(images)):
        plt.subplot(3, 3, i + 1)
        plt.imshow(images[i], cmap="gray" if i != 0 else None)
        plt.title(titles[i])
        plt.axis("off")

    plt.tight_layout()
    plt.show()
```
# Output

### Original Image
<img width="202" height="305" alt="image" src="https://github.com/user-attachments/assets/77576eab-008e-418f-8e57-8496512a5ba5" />

## Grayscale Image
<img width="212" height="312" alt="image" src="https://github.com/user-attachments/assets/58442f44-ef7b-4965-b218-a25fab84918b" />

###  Sobel Edge Detector
- Detects edges in horizontal and vertical directions  
- Produces gradient-based edge map
<img width="203" height="305" alt="image" src="https://github.com/user-attachments/assets/081f9a37-5817-4c95-b1bb-3695144da186" />

###  Prewitt Edge Detector
- Similar to Sobel but simpler kernel  
- Detects directional edges
<img width="201" height="296" alt="image" src="https://github.com/user-attachments/assets/1a3016b0-e568-4e57-a41a-1f044f1ecfb2" />

###  Roberts Edge Detector
- Detects edges using diagonal gradients  
- Sensitive to noise  
<img width="201" height="303" alt="image" src="https://github.com/user-attachments/assets/c64370af-0fcb-48f0-aa67-196b88fc1abe" />

###  Laplacian Edge Detector
- Detects edges using second-order derivatives  
- Highlights rapid intensity changes  
<img width="197" height="310" alt="image" src="https://github.com/user-attachments/assets/c867be56-ef9f-4710-95db-d6a5028add45" />

###  Canny Edge Detector
- Multi-stage edge detection  
- Produces clean and thin edges
<img width="192" height="303" alt="image" src="https://github.com/user-attachments/assets/aebc208d-34d2-45dd-94b3-dc438c5a3a08" />

## Result

Thus, edges are successfully detected using Sobel, Prewitt, Roberts, Laplacian, and Canny edge detection techniques. Each method highlights edges differently based on gradient and intensity variations, improving feature extraction and analysis.
