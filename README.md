# Automated PCB Defect Detection via Image Processing

## Dataset Acknowledgement

The algorithm was developed, tested, and validated using the publicly available **PCB Defect Dataset**. This dataset provides a wide variety of reference and faulty PCB image pairs with varying conditions, making it an ideal benchmark for evaluating structural comparison algorithms.
* **Source:** [Kaggle - PCB Defect Dataset by Norbert Elter](https://www.kaggle.com/datasets/norbertelter/pcb-defect-dataset)

---

## Phase 1: Computer Vision Pipeline & Defect Extraction

The primary objective of this project is to create a robust and automated quality inspection system that compares newly manufactured PCBs against a verified "Golden Reference" board. The pipeline is designed to strictly isolate missing drilled holes by overcoming lighting variances and environmental noise.

The algorithm executes the following core image processing stages in sequence:

1. **Illumination Normalization:** To prevent false positives caused by regional lighting differences, both the reference and test images are converted to grayscale and normalized using a large-kernel Gaussian filter to estimate and subtract background illumination.
2. **Noise Reduction:** A 5x5 Gaussian blur is applied to smooth out minor pixel variations and sensor noise without losing critical structural edges.
3. **Otsu Thresholding:** The optimal threshold values are dynamically calculated using Otsu's method, converting the normalized grayscale boards into precise binary images for structural comparison.
4. **Absolute Difference & Morphological Cleaning:** The absolute difference between the binary reference and test image is extracted. Any resulting high-frequency noise artifacts are surgically removed using morphological opening and closing operations.
5. **Contour Analysis & Detection:** Finally, structural contours are calculated. By applying strict geometric filters (evaluating contour area, bounding box aspect ratio, and board margins), the algorithm successfully isolates and highlights the exact coordinates of the missing holes.

<p align="center">
  <img src="Figure1_IP%20Project.png" alt="Defect Detection Output">
  <br>
  <em><b>Figure 1:</b> The final output of the computer vision pipeline, successfully isolating and highlighting the missing holes on a faulty PCB.</em>
</p>
