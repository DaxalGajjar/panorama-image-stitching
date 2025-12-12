# Panorama-Image-Stitching-
 **Manuelle und automatische Bildverarbeitung**

The process you have performed, according to the steps in the `image_stitch_manual.ipynb` file, is as follows:

1.  **Mount Google Drive:** The first step was to mount your Google Drive to access the image files.
    * `from google.colab import drive`
    * `drive.mount('/content/drive')`
2.  **Import Libraries:** Essential libraries for computer vision and numerical operations were imported.
    * `import cv2` (OpenCV)
    * `import numpy as np`
    * `import matplotlib.pyplot as plt`
3.  **Load Images:** Four specific JPEG images were loaded from a directory in your Google Drive using `cv2.imread()`.
    * `image1 = cv2.imread(...)` (loading '3.2.jpg')
    * `image2 = cv2.imread(...)` (loading '3.1.jpg')
    * `image3 = cv2.imread(...)` (loading '3.3.jpg')
    * `image4 = cv2.imread(...)` (loading '3.4.jpg')
4.  **Convert Color Space:** The loaded images were converted from OpenCV's default BGR format to RGB format.
    * `image1 = cv2.cvtColor(image1, cv2.COLOR_BGR2RGB)`
    * `image2 = cv2.cvtColor(image2, cv2.COLOR_BGR2RGB)`
    * `image3 = cv2.cvtColor(image2, cv2.COLOR_BGR2RGB)`
    * `image4 = cv2.cvtColor(image2, cv2.COLOR_BGR2RGB)`
5.  **Detect Keypoints and Descriptors:** The ORB (Oriented FAST and Rotated BRIEF) algorithm was used to detect distinctive keypoints and compute their descriptors on the first two images (`image1` and `image2`).
    * `orb = cv2.ORB_create()`
    * `keypoints1, descriptors1 = orb.detectAndCompute(image1, None)`
    * `keypoints2, descriptors2 = orb.detectAndCompute(image2, None)`
6.  **Visualize Keypoints:** The detected keypoints were drawn onto `image1` and `image2` and then displayed using `cv2_imshow`.
    * `image1_keypoints = cv2.drawKeypoints(...)`
    * `image2_keypoints = cv2.drawKeypoints(...)`
    * `cv2_imshow(image1_keypoints)`
    * `cv2_imshow(image2_keypoints)`
  

The process outlined in the `image_stitch_auto.ipynb` file automates the creation of a panoramic image using OpenCV's built-in stitching functionality.

The steps performed are:

1.  **Mount Google Drive**: The process begins by mounting Google Drive to ensure the image files are accessible within the Colab environment.
    * `from google.colab import drive`
    * `drive.mount('/content/drive')`
2.  **Import Libraries**: Essential libraries for computer vision and array manipulation are imported.
    * `import cv2` (OpenCV)
    * `import numpy as np`
    * `import matplotlib.pyplot as plt`
3.  **Image Import and Read**: Four individual images are loaded from a specified path in Google Drive.
    * `image1 = cv2.imread(...)`, `image2 = cv2.imread(...)`, etc., loading files like `3.1.jpg` through `3.4.jpg`.
4.  **Image Color Conversion**: The loaded images are converted from OpenCV's default BGR color space to the RGB format for correct display and processing.
5.  **Initialize Stitcher:** A Stitcher object is created using OpenCV's `cv2.Stitcher_create()` function, which is designed to handle the entire stitching pipeline automatically.
6.  **Stitch Images:** The core stitching operation is performed by passing the list of loaded images to the `stitcher.stitch()` method. This function attempts to find matching features, estimate transformations (homographies), warp, and blend the images into a single panorama .
7.  **Output and Save Result:** The script checks the status of the stitching operation:
    * **Success:** If successful (`cv2.Stitcher_OK`), the stitched panorama is displayed using `matplotlib.pyplot` and saved as `panorama_result.jpg`.
    * **Failure:** If the stitching fails, an error status is reported, with specific error details provided (e.g., `ERR_NEED_MORE_IMGS`, `ERR_NO_FEATURES`, or `ERR_HOMOGRAPHY_EST_FAIL`).
