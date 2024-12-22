# Lung CT Scan Segmentation with VESSEL12 Dataset

## Overview

This project focuses on the segmentation of lung CT scans using the VESSEL12 dataset. The dataset contains 20 CT scans of lungs, each having 300-400 slices of 512x512 resolution, along with their respective masks. Both the CT scans and masks are in the `.mhd` format.

- **VESSEL12 Grand Challenge**: [VESSEL12 Grand Challenge Website](https://vessel12.grand-challenge.org/)

Though it states:
> The challenge was closed on November 1st 2019, after evaluating 31 submissions by 18 different teams. For now, the data is still available on the download page.

But even after registering, it shows forbidden on the download page.

So one can download the dataset from Kaggle:
- **Kaggle dataset** : [Lung Vessel Segmentation](https://www.kaggle.com/datasets/andrewmvd/lung-vessel-segmentation)



## Steps Involved

### 1. Extracting CT Images as JPG

The first step involved creating a script to extract CT images from the `.mhd` files and save them as `.jpg` files. This was done using the `mhdToJPG.ipynb` notebook.

### 2. Converting Masks to COCO Format Annotations

Next, a script was created to convert the masks into COCO format annotations compatible with Detectron2. This was achieved using the `MaskToAnnotations.ipynb` notebook. The segmentation in the JSON file uses the RLE (Run-Length Encoding) format, which is a list in column-major form until the next complement pixel is found.

Example :
![RLE Annotation Example][1]


[1]: https://i.sstatic.net/Knq3CjpG.png

### 3. Fine-Tuning a Pre-Trained Model

A pre-trained model, `COCO-InstanceSegmentation/mask_rcnn_R_101_FPN_3x`, was used and fine-tuned on the VESSEL12 dataset. This was done using the `LungSegmentationTraining2500iters.ipynb` notebook.

### 4. Running Inference

Finally, the fine-tuned model is used to run inference on the LIDC-IDRI Image to obtain segmentation results. This is done using the `LungSegmentationInference.ipynb` notebook.

 ![Inference on LIDC-IDRI Image][2]


[2]: https://i.sstatic.net/51ZnLyEH.png


## Notebooks

- **[`mhdToJPG.ipynb`](mhdToJPG.ipynb)**: Script to extract CT images from `.mhd` files and save them as `.jpg`.
- **[`MaskToAnnotations.ipynb`](MaskToAnnotations.ipynb)**: Script to convert masks to COCO format annotations.
- **[`LungSegmentationTraining1500iters.ipynb`](LungSegmentationTraining1500iters.ipynb)**: Notebook for fine-tuning the pre-trained model on the VESSEL12 dataset for 1500 iterations.
- **[`LungSegmentationTraining2500iters.ipynb`](LungSegmentationTraining2500iters.ipynb)**: Notebook for fine-tuning the pre-trained model on the VESSEL12 dataset for 2500 iterations.
- **[`LungSegmentationInference.ipynb`](LungSegmentationInference.ipynb)**: Notebook for running inference on LIDC-IDRI Image or any other Lung CT Scan.


## Usage

1. **For Training**: 
- Install the requirements from [`RequirementsTraining.txt`](RequirementsTraining.txt) .
- Copy the script [`LungSegmentationTraining2500iters.ipynb`](LungSegmentationTraining2500iters.ipynb) and change the appropriate fields according to your environment like Annotations path, Images path.

2. **For Inference**: 
- Install the requirements from [`RequirementsTesting.txt`](RequirementsTesting.txt) .
- Request to access the model along with reason from [Drive Link](https://drive.google.com/file/d/1-H4WKMDVFD_YX86_i-nMBUARM9ytXrPv/view?usp=sharing).
- Copy the script [`LungSegmentationInference.ipynb`](LungSegmentationInference.ipynb) and move the `model_final.pth` to appropriate place.

## Metrics
### After 1500 iterations:
- On Validation Set:

|   AP   |  AP50  |  AP75  |  APs  |  APm   |  APl   |
|:------:|:------:|:------:|:-----:|:------:|:------:|
| 63.752 | 77.880 | 69.507 | 1.684 | 47.518 | 87.681 |


- On Test Set:

|   AP   |  AP50  |  AP75  |  APs  |  APm   |  APl   |
|:------:|:------:|:------:|:-----:|:------:|:------:|
| 67.513 | 77.104 | 71.320 | 1.717 | 36.812 | 91.222 |

### After 2500 iterations:
- On Validation Set:

|   AP   |  AP50  |  AP75  |  APs  |  APm   |  APl   |
|:------:|:------:|:------:|:-----:|:------:|:------:|
| 64.421 | 77.521 | 69.677 | 1.641 | 51.233 | 88.494 |


- On Test Set:

|   AP   |  AP50  |  AP75  |  APs  |  APm   |  APl   |
|:------:|:------:|:------:|:-----:|:------:|:------:|
| 67.212 | 79.115 | 71.891 | 2.268 | 39.388 | 90.062 |

where 
where 
- **AP**: Average Precision - This is the average of the precision values at different recall levels. It provides a single metric to summarize the precision-recall curve.
- **AP50**: AP at IoU=0.50 - This is the average precision when the Intersection over Union (IoU) threshold is 0.50. It measures how well the predicted bounding boxes overlap with the ground truth boxes at this threshold.
- **AP75**: AP at IoU=0.75 - This is the average precision when the Intersection over Union (IoU) threshold is 0.75. It is a stricter measure compared to AP50, requiring higher overlap between predicted and ground truth boxes.
- **APs**: AP for small objects - This is the average precision for objects that are small in size. It helps to evaluate the model's performance on detecting small objects.
- **APm**: AP for medium objects - This is the average precision for objects that are medium in size. It helps to evaluate the model's performance on detecting medium-sized objects.
- **APl**: AP for large objects - This is the average precision for objects that are large in size. It helps to evaluate the model's performance on detecting large objects.

Detailed metrics throughout the training can be found in the [`metrics.json`](metrics.json) file.

## Conclusion

This project demonstrates the process of preparing a medical imaging dataset for use with Detectron2, fine-tuning a pre-trained model, and running inference to obtain segmentation results.

## Acknowledgments

- The VESSEL12 Grand Challenge for providing the dataset.
- Kaggle for hosting the dataset.
- Detectron2 for the pre-trained model and segmentation framework.
