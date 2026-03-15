# Image Segmentation using U-Net

## Project Overview

This project implements a **semantic image segmentation model using a modified U-Net architecture** to detect and segment objects in images. The model is trained on a curated subset of the **COCO 2017 dataset** to segment four classes:

* Cake
* Car
* Dog
* Person

Semantic segmentation assigns a **class label to each pixel** in an image, allowing precise object boundary detection. This technique is widely used in applications such as **autonomous driving, medical imaging, and scene understanding**.

The project demonstrates the **complete deep learning pipeline**, including data preprocessing, exploratory data analysis, model training, evaluation, and visualization of segmentation results.

---

## Dataset

The dataset is a **curated subset of the COCO 2017 dataset**.

**Total images:** 630

Dataset split:

* Training: 300 images
* Validation: 300 images
* Testing: 30 images

### Target Classes

* Cake
* Car
* Dog
* Person

### Dataset Characteristics

* Images have **varying resolutions**
* **Class imbalance exists** in the dataset
* Pixel-level annotations are provided in **COCO format**

### Preprocessing Steps

* Images resized to **128 × 128**
* Multi-class segmentation masks generated
* Pixel labels assigned:

  * 0 → Background
  * 1 → Cake
  * 2 → Car
  * 3 → Dog
  * 4 → Person

### Data Augmentation

To improve generalization, the following augmentations were applied:

* Horizontal flipping
* Vertical flipping
* Rotation (90°, 180°, 270°)

---

## Model Architecture

This project uses a **modified U-Net architecture**, a popular deep learning model for semantic segmentation.

### Key Components

* Encoder–decoder structure
* Skip connections between encoder and decoder layers
* Convolutional layers with **ReLU activation**
* **Batch normalization** after convolution layers
* Final **softmax layer** for multi-class segmentation

### Architecture Structure

Encoder:

* Conv → BatchNorm → Conv → BatchNorm → MaxPooling

Decoder:

* Upsampling
* Skip connections
* Convolution layers

Output:

* **5-class prediction**

  * Background
  * Cake
  * Car
  * Dog
  * Person

---

## Training Configuration

| Parameter     | Value                                     |
| ------------- | ----------------------------------------- |
| Optimizer     | Adam                                      |
| Loss Function | Weighted Sparse Categorical Cross-Entropy |
| Metric        | Mean Intersection over Union (mIoU)       |
| Epochs        | 10                                        |
| Batch Size    | 8                                         |
| Image Size    | 128 × 128                                 |

### Class Weighting

Class weights are applied to handle **dataset imbalance**.

---

## Evaluation Metrics

### Mean Intersection over Union (mIoU)

mIoU measures the overlap between **predicted segmentation and ground truth masks**.

### Per-Class IoU Scores

| Class      | IoU    |
| ---------- | ------ |
| Background | 0.8367 |
| Cake       | 1.0000 |
| Car        | 0.0344 |
| Dog        | 0.9661 |
| Person     | 0.0639 |

### Additional Evaluation

* Confusion matrix analysis
* Visual comparison of predictions vs ground truth

---

## Results

### Training Performance

* Loss decreased steadily during training
* Validation IoU stabilized after several epochs
* Data augmentation improved generalization

### Model Observations

* Strong performance for **Cake and Dog**
* Lower performance for **Car and Person** due to:

  * class imbalance
  * visual complexity
  * overlapping features

---

## Visual Outputs

The model generates:

* Predicted segmentation masks
* Color-coded ground truth masks
* Comparison plots of:

  * Input image
  * Ground truth mask
  * Predicted mask

---

## Project Workflow

1. Load COCO dataset annotations
2. Filter images containing target classes
3. Generate segmentation masks
4. Perform exploratory data analysis
5. Apply data augmentation
6. Train U-Net model
7. Evaluate segmentation results
8. Visualize predictions and confusion matrices

---

## Technologies Used

Programming Language:

* Python

Libraries:

* TensorFlow / Keras
* NumPy
* Matplotlib
* Scikit-learn
* pycocotools
* scikit-image

---

## Future Improvements

Possible improvements for future work include:

* Using **larger datasets** to reduce class imbalance
* Testing advanced segmentation models:

  * DeepLabv3+
  * SegFormer
  * Mask R-CNN
* Hyperparameter tuning
* Applying **post-processing techniques** such as Conditional Random Fields (CRFs)
* Optimizing models for **real-time applications**




