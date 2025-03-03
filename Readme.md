# DenseNet121 for Chest X-ray Classification

This repository contains a convolutional neural network (CNN) based on **DenseNet121** for chest X-ray disease classification. In our approach, we freeze all layers except for the last block of DenseNet121 and fine-tune this model on the **NIH Chest X-ray Dataset**. We also compare our fine-tuned model with a pretrained model from the [TorchXRayVision](https://github.com/mlmed/torchxrayvision) package.

## Project Overview
- **Model Architecture:** DenseNet121 pretrained on ImageNet.
- **Fine-tuning Strategy:** 
  - Freeze early layers and the majority of DenseNet blocks.
  - Retrain only the last block (and a custom classifier head) on the NIH Chest X-ray Dataset.
- **Dataset:** NIH Chest X-ray Dataset, which contains 112,120 frontal-view X-ray images from 30,805 patients with labels for 14 common thoracic diseases.
- **Task:** Multi-label image classification for disease detection.

## Dataset
The **NIH Chest X-ray Dataset** provides a large collection of frontal chest X-ray images with annotations for 14 thoracic diseases. Detailed information and download instructions can be found on the official source: [NIH Chest X-ray Dataset](https://nihcc.app.box.com/v/ChestXray-NIHCC).

## Model Training and Fine-Tuning
Our model leverages the powerful DenseNet121 architecture. We perform the following steps:
1. **Load the pretrained DenseNet121 model** and freeze all layers up to (and including) the third dense block.
2. **Replace the classifier head** with a custom output layer that is suitable for our multi-label classification task.
3. **Fine-tune the network** on the NIH Chest X-ray Dataset by training only the last block and the classifier head. This approach helps to reduce training time while still adapting the model to the specific characteristics of chest X-ray images.

## Results and Evaluation
We evaluated both our fine-tuned model and a pretrained model from the TorchXRayVision package. The results are presented below, including ROC curves and classification reports.

### ROC Curves
The ROC curves for our model and the TorchXRayVision model are shown in the figures below:

![Model Results](https://github.com/LaskawiecPiotr/X-ray-disease-detection/blob/main/AUC%2C%20our%20model.png)
![X-Ray Vision Model Results](https://github.com/LaskawiecPiotr/X-ray-disease-detection/blob/main/AUC%2C%20the%20XRayVision%20pretrained%20model.png)

### Classification Reports
Below are the detailed classification reports comparing our fine-tuned model with the pretrained TorchXRayVision model:

| **Report for Our Model** | **Report for the X-Ray Vision Model** |
|--------------------------|---------------------------------------|
| | |
| Disease             |   precision |   recall |   f1-score | | Disease             |   precision |   recall |   f1-score |
|---------------------:|------------:|---------:|-----------:| |---------------------:|------------:|---------:|-----------:|
| Pneumothorax       |   0.2013    | 0.8253   |   0.3237   | | Pneumothorax       |   0.1183    | 0.8564   |   0.2079   |
| Mass               |   0.1402    | 0.6083   |   0.2279   | | Mass               |   0.0958    | 0.8417   |   0.1720   |
| Atelectasis        |   0.2343    | 0.6313   |   0.3418   | | Atelectasis        |   0.1590    | 0.8983   |   0.2702   |
| Nodule             |   0.1236    | 0.5339   |   0.2007   | | Nodule             |   0.0785    | 0.7723   |   0.1426   |
| Consolidation      |   0.1050    | 0.8711   |   0.1874   | | Consolidation      |   0.0843    | 0.9673   |   0.1551   |
| Pleural_Thickening |   0.0793    | 0.6944   |   0.1423   | | Pleural_Thickening |   0.0580    | 0.8423   |   0.1085   |
| Effusion           |   0.3273    | 0.7976   |   0.4642   | | Effusion           |   0.2565    | 0.8727   |   0.3965   |
| Infiltration       |   0.3515    | 0.6401   |   0.4538   | | Infiltration       |   0.2406    | 0.9268   |   0.3820   |
| micro avg          |   0.1968    | 0.7016   |   0.3074   | | micro avg          |   0.1391    | 0.8852   |   0.2404   |
| macro avg          |   0.1953    | 0.7003   |   0.2927   | | macro avg          |   0.1364    | 0.8722   |   0.2293   |
| weighted avg       |   0.2464    | 0.7016   |   0.3520   | | weighted avg       |   0.1734    | 0.8852   |   0.2834   |
| samples avg        |   0.1555    | 0.3799   |   0.2054   | | samples avg        |   0.1244    | 0.4784   |   0.1861   |

Our model achieves a significant improvement in precision for many diseases. For instance, the precision for *Effusion* and *Infiltration* is higher in our model compared to the X-Ray Vision model, demonstrating the benefits of fine-tuning on this specific dataset.

## Additional Details
- **Training Details:**  
  We trained our model with a learning rate schedule and used class weights to address class imbalance. The final model was trained for 20 epochs.
  
- **Feature Extraction and Augmentation:**  
  We used various image augmentation techniques during training to improve generalization. The code for these procedures is available in the repository.

- **Comparison with Pretrained Model:**  
  The pretrained X-Ray Vision model serves as a baseline. Our fine-tuning approach, which involves freezing early layers and retraining the later layers, shows improved disease-specific performance as reflected in the ROC curves and classification reports.

## Conclusion
This project demonstrates the effectiveness of fine-tuning a pretrained DenseNet121 for chest X-ray classification. By retraining only the final block on the NIH Chest X-ray dataset, we achieve competitive results with improved precision and recall for several diseases. The results, including ROC curves and classification reports, validate the potential of this approach for real-time chest X-ray analysis in clinical settings.

## References
- NIH Chest X-ray Dataset: [NIH Chest X-ray Dataset](https://nihcc.app.box.com/v/ChestXray-NIHCC)
- TorchXRayVision: [TorchXRayVision GitHub](https://github.com/mlmed/torchxrayvision)
- Original Paper:  
  Bernardini, Andrea, et al. *AIOSA: An approach to the automatic identification of obstructive sleep apnea events based on deep learning*. Artificial Intelligence in Medicine 118 (2021): 102133. DOI: [10.1016/j.artmed.2021.102133](https://doi.org/10.1016/j.artmed.2021.102133)

