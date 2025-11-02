
# Food-101 Image Classification Project — Full Report

---

## Project Overview

This study aims to classify food categories using the popular **Food-101 image classification dataset** with different deep learning models.

The work consists of **two projects**:

* **5Category_ResNet18:** Classification on **5 selected categories** (pizza, hamburger, sushi, french fries, ice cream) from the Food-101 dataset using **ResNet-18** with transfer learning.
* **Project 2:** Classification on **20 selected categories** from the Food-101 dataset using **VGG16 and ResNet18** with transfer learning, freezing, and fine-tuning. Fine-tuning and hyperparameter adjustments were applied to improve model performance.

---

## 5Category_ResNet18: Classification with ResNet-18 on 5 Categories

### Categories Used

* pizza
* hamburger
* sushi
* french_fries
* ice_cream

### Dataset and Preprocessing

* Selected 750 training and 250 test images per category.
* Images were resized to **224x224**.
* Data augmentation applied: horizontal flip, random rotation, zoom, shift.
* Pixel values normalized.
* Split: 75% training, 10% validation, 15% test.

### Model Selection and Training

* **Model:** ResNet-18
* **Why ResNet-18?**
  Residual connections prevent gradient loss in deep networks and ImageNet pretrained weights are advantageous for transfer learning.
* **Transfer Learning:**
  Pretrained ImageNet weights used; last layers retrained for 5 categories.
* **Early Stopping:**
  Training stops if validation performance (especially F1 score) does not improve for 3 consecutive epochs.
  Although improvement could occur at epoch 10, training stopped early to save time and prevent overfitting. The best model weights were saved.

### Training Results (Epoch 10)

| Metric               | Value  |
| -------------------- | ------ |
| Train Loss           | 0.5447 |
| Train Accuracy       | 80.85% |
| Validation Loss      | 0.2765 |
| Validation Accuracy  | 90.60% |
| Validation Precision | 0.9071 |
| Validation Recall    | 0.9060 |
| Validation F1 Score  | 0.9059 |

* Best model saved as `best_model_resnet.pth`.

### Model Evaluation

* Accuracy, precision, recall, and F1 scores calculated on the test set.
* Confusion matrix visualized.

### Challenges

* Only 5 categories were selected due to the large size of the full dataset.

### Improvement Suggestions

* Work with more categories.
* Adjust learning rate scheduling and early stopping.
* Try different architectures or ensemble models.
* Hyperparameter optimization.

---

## Project 2: Transfer Learning and Fine-Tuning on 20 Categories with VGG16 and ResNet18

### Overview

* 20 different categories from Food-101 were selected.
* CNN architectures **VGG16** and **ResNet18** were used.
* Performance improved with transfer learning and fine-tuning.
* Additional layers and dropout rates improved model performance.
* Fine-tuning strategy: some models used feature extraction (layer freezing), others unfroze all layers.
* Early stopping and learning rate adjustments applied.

### Key Experiment Results

| Model & Modification                                | Validation/Test Accuracy (%) |
| --------------------------------------------------- | ---------------------------- |
| ResNet (fine-tuning all layers)                     | 71.98                        |
| ResNet (fine-tuning all layers, high learning rate) | 44.21                        |
| ResNet (fine-tuning only fully connected layers)    | 66.78                        |
| ResNet (1 or 2 residual blocks removed)             | 51.6 - 53.12                 |
| VGG (fine-tuning all layers, proper learning rate)  | 74.40                        |
| VGG (feature extraction, layers frozen)             | 68.62                        |

### Highlights

* Fine-tuning all layers significantly increased accuracy.
* Proper learning rate and early stopping influenced success.
* Weight maps and feature activations analyzed for improved model interpretability.

### Files Used

* `data.py`, `prepare_data`: Data preprocessing and loading.
* `model.py`: Model architectures and configurations.
* Jupyter Notebook files:

  * `resnet18_FineTuning.ipynb`
  * `resnet_frozen.ipynb`
  * `vgg_FineTuning.ipynb`
  * `vgg_Frozen.ipynb`

---

## General Conclusion and Recommendations

* **5Category_ResNet18** produced a fast and successful model with a limited set of categories.
* **Project 2** improved performance using a broader category set and detailed fine-tuning.
* Transfer learning and fine-tuning are critical and effective techniques in deep learning projects.
* Future work: comparing different models, hyperparameter optimization, ensemble methods, and advanced data augmentation techniques.

---

## Running Instructions

* Project code is in **Jupyter Notebook** format.
* Required Python libraries are listed in `requirements.txt`.
* Models are saved as `.pth` files.
* Can be run easily on **Google Colab** or locally.

---

## Additional Notes

* In Project 1, early stopping completed training at **epoch 10** instead of 30. This strategy saved time and prevented overfitting.

---
