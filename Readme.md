# Densenet121 for Chest X-ray Classification

This repository contains a convolutional neural network based on **DenseNet121**, where all layers except the last block have been frozen and retrained on the **NIH Chest X-ray dataset**.

## Project Overview
- **Model:** DenseNet121 (pretrained on ImageNet)
- **Fine-tuning:** Last block trained, earlier layers frozen
- **Dataset:** NIH Chest X-ray Dataset
- **Task:** Image classification

##  Dataset
The **NIH Chest X-ray Dataset** contains **112,120** frontal-view X-ray images of **30,805** unique patients. It includes labels for **14 common thoracic diseases**.

Download the dataset from the official source: [NIH Chest X-ray Dataset](https://nihcc.app.box.com/v/ChestXray-NIHCC)


##  Results
We have graphed the RUC curves and created the classification reports for both our model and the pretrained model from the TorchXRayVision package. The code to create these figures is available in [Code 1](https://github.com/LaskawiecPiotr/X-ray-disease-detection/blob/main/pretrained%20%2B%20class_weights%20%2B%20layer%20freezing.ipynb) for our model and [Code 2](https://github.com/LaskawiecPiotr/X-ray-disease-detection/blob/main/x-rayvision%20copy.ipynb) for the X-Ray Vision model.
![Model Results](https://github.com/LaskawiecPiotr/X-ray-disease-detection/blob/main/AUC%2C%20our%20model.png)
![X-Ray Vision Model Results](https://github.com/LaskawiecPiotr/X-ray-disease-detection/blob/main/AUC%2C%20the%20XRayVision%20pretrained%20model.png)
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
