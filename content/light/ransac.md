---
title: Ransac
date: 2024-03-17
enableToc: false
---

The RANSAC (Random Sample Consensus) algorithm is a robust estimation method used to fit a mathematical model to a dataset that contains outliers. It is widely used in computer vision for tasks such as estimating the fundamental matrix in stereo vision, finding homographies between image pairs in panorama stitching, and fitting geometric shapes to sets of points. RANSAC works by repeatedly selecting a random subset of the original data to estimate model parameters, then validating this model against the entire dataset to find the best-fitting model that has the highest number of inliers.

The general steps of RANSAC are :

1. Select a Random Subset: Randomly select a minimal subset of points necessary to estimate the model parameters.
2. Estimate the Model: Estimate the model parameters using this subset.
3. Identify Inliers: Determine which points from the entire dataset fit this model within a certain threshold (these points are considered inliers).
4. Repeat: Repeat steps 1-3 for a predefined number of iterations, each time updating the best-fitting model if the current iteration has more inliers.
5. Best Model: After all iterations, choose the model with the highest number of inliers.
RANSAC is particularly useful because it is capable of providing a good estimation even when the data contains a significant number of outliers.

## Example in OpenCV: Estimating a Homography with RANSAC

Below is an example of using RANSAC in OpenCV to estimate a homography between two images. This is commonly used in applications like image stitching or when you want to understand the transformation between two scenes.

```
import cv2
import numpy as np

# Load your images
image1 = cv2.imread('image1.jpg')
image2 = cv2.imread('image2.jpg')

# Convert images to grayscale
gray1 = cv2.cvtColor(image1, cv2.COLOR_BGR2GRAY)
gray2 = cv2.cvtColor(image2, cv2.COLOR_BGR2GRAY)

# Initialize SIFT detector
sift = cv2.SIFT_create()

# Find keypoints and descriptors with SIFT
keypoints1, descriptors1 = sift.detectAndCompute(gray1, None)
keypoints2, descriptors2 = sift.detectAndCompute(gray2, None)

# Create a BFMatcher object
bf = cv2.BFMatcher(cv2.NORM_L2, crossCheck=True)

# Match descriptors
matches = bf.match(descriptors1, descriptors2)

# Sort them in the order of their distance
matches = sorted(matches, key=lambda x:x.distance)

# Draw first 10 matches
img_matches = cv2.drawMatches(image1, keypoints1, image2, keypoints2, matches[:10], None, flags=cv2.DrawMatchesFlags_NOT_DRAW_SINGLE_POINTS)

# Extract location of good matches
points1 = np.zeros((len(matches), 2), dtype=np.float32)
points2 = np.zeros_like(points1)

for i, match in enumerate(matches):
    points1[i, :] = keypoints1[match.queryIdx].pt
    points2[i, :] = keypoints2[match.trainIdx].pt

# Find Homography
H, status = cv2.findHomography(points1, points2, cv2.RANSAC)

# Use the Homography Matrix to warp the images
result = cv2.warpPerspective(image1, H, (image1.shape[1] + image2.shape[1], image1.shape[0]))
result[0:image2.shape[0], 0:image2.shape[1]] = image2

# Display the stitched image
cv2.imshow('Result', result)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

This code performs the following steps:

* Loads two images and converts them to grayscale.
* Detects SIFT keypoints and computes descriptors for both images.
* Uses a Brute-Force Matcher to match the descriptors between the two images.
* Uses RANSAC to estimate a homography matrix that best aligns the two images.
* Warps one image onto the other using the estimated homography to demonstrate how they align.
