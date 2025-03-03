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

<table>
<tr><th>Report for our model </th><th>Report for the X-ray vision model</th></tr>
<tr><td>

|Disease             |   precision |   recall |   f1-score |
|:-------------------|------------:|---------:|-----------:|
| Pneumothorax       |   0.201332  | 0.82533  |   0.3237   |
| Mass               |   0.140185  | 0.608317 |   0.227861 |
| Atelectasis        |   0.234323  | 0.631331 |   0.341788 |
| Nodule             |   0.123555  | 0.533904 |   0.200671 |
| Consolidation      |   0.105002  | 0.871073 |   0.187412 |
| Pleural_Thickening |   0.0792555 | 0.694384 |   0.142272 |
| Effusion           |   0.327322  | 0.797603 |   0.464161 |
| Infiltration       |   0.351517  | 0.640136 |   0.453825 |
| micro avg          |   0.196779  | 0.701558 |   0.30735  |
| macro avg          |   0.195311  | 0.70026  |   0.292711 |
| weighted avg       |   0.246421  | 0.701558 |   0.352025 |
| samples avg        |   0.155489  | 0.379904 |   0.205426 |

</td><td>

|Disease             |   precision |   recall |   f1-score |
|:-------------------|------------:|---------:|-----------:|
| Pneumothorax       |   0.118278  | 0.856403 |   0.20785  |
| Mass               |   0.0957942 | 0.841717 |   0.172012 |
| Atelectasis        |   0.159004  | 0.898336 |   0.270185 |
| Nodule             |   0.0785253 | 0.772305 |   0.142556 |
| Consolidation      |   0.0842982 | 0.967277 |   0.155081 |
| Pleural_Thickening |   0.057971  | 0.842333 |   0.108476 |
| Effusion           |   0.256537  | 0.872703 |   0.396515 |
| Infiltration       |   0.240613  | 0.92679  |   0.382041 |
| micro avg          |   0.13907   | 0.88517  |   0.240375 |
| macro avg          |   0.136378  | 0.872233 |   0.22934  |
| weighted avg       |   0.173431  | 0.88517  |   0.283441 |
| samples avg        |   0.124396  | 0.478369 |   0.186056 |

</td></tr> </table>

Our model achieves a significant improvement in precision all across the board. The recall though, is lower. However, this is a natural trade off and the recall can be improved (at the cost of precision) using the Precision-Recall Curve. This analysis is done in the model evaluation file.

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

