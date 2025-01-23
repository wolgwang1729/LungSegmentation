## Training Configurations

- **Pre-trained Model**: `COCO-InstanceSegmentation/mask_rcnn_R_101_FPN_3x`
- **Model Weights**: `model_zoo.get_checkpoint_url("COCO-InstanceSegmentation/mask_rcnn_R_101_FPN_3x.yaml")`
- **Optimizer**: AdamW

### DataLoader
- **Number of Workers**: 2

### Datasets
- **Train Dataset**: `my_dataset_train`
- **Validation Dataset**: `my_dataset_val`

### Input
- **Mask Format**: `bitmask`
- **Min Size Train**: 512
- **Max Size Train**: 512
- **Min Size Test**: 512
- **Max Size Test**: 512
- **Random Flip**: `none`

### Model
- **Device**: `cuda`
- **Backbone Freeze At**: 0
- **ROI Heads Batch Size Per Image**: 256
- **ROI Mask Head CONV Dimension**: 512
- **Number of Classes**: 1

### Solver
- **Max Iterations**: 1000
- **AMP Enabled**: True
- **Base Learning Rate**: 0.0001
- **Images Per Batch**: 32

- **Other configs are defaults from**: https://github.com/facebookresearch/detectron2/blob/main/detectron2/config/defaults.py

## Metrics
### After 1000 iterations:
- On Validation Set:

#### BBOX:
| AP     | AP50   | AP75   | APs    | APm    | APl    |
|--------|--------|--------|--------|--------|--------|
| 81.7048| 84.8606| 81.9145| 3.1192 | 62.2309| 97.4586|

#### SEGM:
| AP     | AP50   | AP75   | APs    | APm    | APl    |
|--------|--------|--------|--------|--------|--------|
| 74.2237| 88.9178| 80.8376| 0.8176 | 45.5577| 88.6633|

- On Test Set:

#### BBOX:
| AP     | AP50   | AP75   | APs    | APm    | APl    |
|--------|--------|--------|--------|--------|--------|
| 92.7313| 93.9825| 93.9369| 23.6281| 82.8875| 99.7317|

#### SEGM:
| AP     | AP50   | AP75   | APs    | APm    | APl    |
|--------|--------|--------|--------|--------|--------|
| 80.8355| 90.9237| 85.8966| 5.8048 | 38.0897| 91.8762|



where
- **AP**: Average Precision - This is the average of the precision values at different recall levels. It provides a single metric to summarize the precision-recall curve.
- **AP50**: AP at IoU=0.50 - This is the average precision when the Intersection over Union (IoU) threshold is 0.50. It measures how well the predicted bounding boxes overlap with the ground truth boxes at this threshold.
- **AP75**: AP at IoU=0.75 - This is the average precision when the Intersection over Union (IoU) threshold is 0.75. It is a stricter measure compared to AP50, requiring higher overlap between predicted and ground truth boxes.
- **APs**: AP for small objects - This is the average precision for objects that are small in size. It helps to evaluate the model's performance on detecting small objects.
- **APm**: AP for medium objects - This is the average precision for objects that are medium in size. It helps to evaluate the model's performance on detecting medium-sized objects.
- **APl**: AP for large objects - This is the average precision for objects that are large in size. It helps to evaluate the model's performance on detecting large objects.

Detailed metrics throughout the training can be found in the  `metrics.json`