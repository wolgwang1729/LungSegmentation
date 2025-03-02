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

The first step involved creating a script to extract CT images from the `.mhd` files and save them as `.jpg` files. This was done using the [`PreProcessing/mhdToJPG.ipynb`](PreProcessing/mhdToJPG.ipynb) notebook.

### 2. Converting Masks to COCO Format Annotations

Next, a script was created to convert the masks into COCO format annotations compatible with Detectron2. This was achieved using the  [`PreProcessing/MaskToAnnotations.ipynb`](PreProcessing/MaskToAnnotations.ipynb) notebook. The segmentation in the JSON file uses the RLE (Run-Length Encoding) format, which is a list in column-major form until the next complement pixel is found.

Example :
![RLE Annotation Example][1]


[1]: https://i.sstatic.net/Knq3CjpG.png

### 3. Fine-Tuning a Pre-Trained Model

A pre-trained model was used and fine-tuned on the VESSEL12 dataset. All the training notebooks are in [`Training Folder`](Training)

### 4. Running Inference

Finally, the fine-tuned model is used to run inference on the LIDC-IDRI Image to obtain segmentation results. This is done using the [`Inference/LungSegmentationInference.ipynb`](Inference/LungSegmentationInference.ipynb) notebook.

 ![Inference on LIDC-IDRI Image][2]


[2]: https://i.sstatic.net/51ZnLyEH.png


## Notebooks

- **[`mhdToJPG.ipynb`](PreProcessing/mhdToJPG.ipynb)**: Script to extract CT images from `.mhd` files and save them as `.jpg`.
- **[`MaskToAnnotations.ipynb`](PreProcessing/MaskToAnnotations.ipynb)**: Script to convert masks to COCO format annotations.
- **[`Training`](Training)**: Folder containing various notebooks for fine-tuning the pre-trained model on the VESSEL12 dataset.
- **[`LungSegmentationInference.ipynb`](Inference/LungSegmentationInference.ipynb)**: Notebook for running inference on LIDC-IDRI Image or any other Lung CT Scan.


## Usage

1. **For Training**: 
- Install the requirements from [`RequirementsTraining.txt`](Training/RequirementsTraining.txt).
- Copy the script [`LungSegmentation.ipynb`](Training/V13/LungSegmentation.ipynb) and change the appropriate fields according to your environment like Annotations path, Images path.

2. **For Inference**: 
- Install the requirements from [`RequirementsInference.txt`](Inference/RequirementsInference.txt).
- Request to access the model from [Drive Link](https://drive.google.com/file/d/1d0bhKc5xJjyFNemzDGF7eyx_pctgqUy4/view?usp=sharing).
- Copy the script [`LungSegmentationInference.ipynb`](Inference/LungSegmentationInference.ipynb) and move the `model_final.pth` to appropriate place.

## Metrics

The best results(according to validation dataset) were obtained from [`V13`](Training/V13) model and they are as follows:

- On **Validation** Set:

#### BBOX:
| AP     | AP50   | AP75   | APs    | APm    | APl    |
|--------|--------|--------|--------|--------|--------|
| 83.5287| 87.5968| 83.6156| 2.6997 | 69.9006| 97.8596|

#### SEGM:
| AP     | AP50   | AP75   | APs    | APm    | APl    |
|--------|--------|--------|--------|--------|--------|
| 76.1599| 90.8345| 81.9858| 2.7424 | 56.7885| 89.7311|

- On **Test** Set:

#### BBOX:
| AP     | AP50   | AP75   | APs    | APm    | APl    |
|--------|--------|--------|--------|--------|--------|
| 93.6290| 94.0256| 94.0241| 20.9390| 89.4532| 100.0000|

#### SEGM:
| AP     | AP50   | AP75   | APs    | APm    | APl    |
|--------|--------|--------|--------|--------|--------|
| 81.9866| 93.0000| 85.9504| 6.3418 | 41.9345| 92.9767|


where
- **AP**: Average Precision - This is the average of the precision values at different recall levels. It provides a single metric to summarize the precision-recall curve.
- **AP50**: AP at IoU=0.50 - This is the average precision when the Intersection over Union (IoU) threshold is 0.50. It measures how well the predicted bounding boxes overlap with the ground truth boxes at this threshold.
- **AP75**: AP at IoU=0.75 - This is the average precision when the Intersection over Union (IoU) threshold is 0.75. It is a stricter measure compared to AP50, requiring higher overlap between predicted and ground truth boxes.
- **APs**: AP for small objects - This is the average precision for objects that are small in size. It helps to evaluate the model's performance on detecting small objects.
- **APm**: AP for medium objects - This is the average precision for objects that are medium in size. It helps to evaluate the model's performance on detecting medium-sized objects.
- **APl**: AP for large objects - This is the average precision for objects that are large in size. It helps to evaluate the model's performance on detecting large objects.

Detailed metrics throughout the training can be found in the readme of respective Training folder as `metrics.json`

## Conclusion

This project demonstrates the process of preparing a medical imaging dataset for use with Detectron2, fine-tuning a pre-trained model, and running inference to obtain segmentation results.

## Acknowledgments

- The VESSEL12 Grand Challenge for providing the dataset.
- Kaggle for hosting the dataset.
- Detectron2 for the pre-trained model and segmentation framework.
- Google Colab for providing free GPU resources for training and inference.
