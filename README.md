# Lung CT Scan Segmentation with VESSEL12 Dataset

## Overview

This project focuses on the segmentation of lung CT scans using the VESSEL12 dataset. The dataset contains 20 CT scans of lungs, each having 300-400 slices of 512x512 resolution, along with their respective masks. Both the CT scans and masks are in the `.mhd` format.

VESSEL12 Grand Challenge website : https://vessel12.grand-challenge.org/

Though it states:
> The challenge was closed on November 1st 2019, after evaluating 31 submissions by 18 different teams. For now, the data is still available on the download page.

But even after registering, it shows forbidden.

So one can download the dataset from Kaggle:
https://www.kaggle.com/datasets/andrewmvd/lung-vessel-segmentation



## Steps Involved

### 1. Extracting CT Images as JPG

The first step involved creating a script to extract CT images from the `.mhd` files and save them as `.jpg` files. This was done using the `mhdToJPG.ipynb` notebook.

### 2. Converting Masks to COCO Format Annotations

Next, a script was created to convert the masks into COCO format annotations compatible with Detectron2. This was achieved using the `MaskToAnnotations.ipynb` notebook. The segmentation in the JSON file uses the RLE (Run-Length Encoding) format, which is a list in column-major form until the next complement is found.
![RLE Annotation Example][1]


[1]: https://i.sstatic.net/Knq3CjpG.png

### 3. Fine-Tuning a Pre-Trained Model

A pre-trained model, `COCO-InstanceSegmentation/mask_rcnn_R_101_FPN_3x`, was used and fine-tuned on the VESSEL12 dataset. This was done using the `Segmentation.ipynb` notebook in the `DetectronCompatibleData` directory.

## Notebooks

- **mhdToJPG.ipynb**: Script to extract CT images from `.mhd` files and save them as `.jpg`.
- **MaskToAnnotations.ipynb**: Script to convert masks to COCO format annotations.
- **Segmentation.ipynb**: Notebook for fine-tuning the pre-trained model on the VESSEL12 dataset.
- **Test.ipynb**: Notebook for running inference on the test set.

## Usage

1. **Extract CT Images**: Run the `mhdToJPG.ipynb` notebook to extract CT images from the `.mhd` files.
2. **Convert Masks**: Run the `MaskToAnnotations.ipynb` notebook to convert the masks to COCO format annotations.
3. **Fine-Tune Model**: Use the `Segmentation.ipynb` notebook to fine-tune the pre-trained model on the VESSEL12 dataset.
4. **Inference**: Use the `Test.ipynb` notebook to run inference on the test set.

## Results

The fine-tuned model was able to segment the lung CT scans effectively. The results can be visualized using the `Test.ipynb` notebook.

## Conclusion

This project demonstrates the process of preparing a medical imaging dataset for use with Detectron2, fine-tuning a pre-trained model, and running inference to obtain segmentation results.
