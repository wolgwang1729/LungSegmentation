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
- **ROI Heads Batch Size Per Image**: 128
- **Number of Classes**: 1

### Solver
- **Max Iterations**: 6000
- **AMP Enabled**: True
- **Base Learning Rate**: 0.0001
- **Images Per Batch**: 32

- **Other configs are defaults from**: https://github.com/facebookresearch/detectron2/blob/main/detectron2/config/defaults.py

## Metrics
### After 6000 iterations:
- On Validation Set:

#### BBOX:
| AP     | AP50   | AP75   | APs    | APm    | APl    |
|--------|--------|--------|--------|--------|--------|
| 82.4566| 85.9963| 82.6388| 5.5673 | 66.1544| 97.5071|

#### SEGM:
| AP     | AP50   | AP75   | APs    | APm    | APl    |
|--------|--------|--------|--------|--------|--------|
| 75.0216| 89.9688| 81.8198| 3.8816 | 51.6050| 88.3646|

- On Test Set:

#### BBOX:
| AP     | AP50   | AP75   | APs    | APm    | APl    |
|--------|--------|--------|--------|--------|--------|
| 93.4378| 94.0470| 94.0470| 25.7219| 88.8025| 99.9897|

#### SEGM:
| AP     | AP50   | AP75   | APs    | APm    | APl    |
|--------|--------|--------|--------|--------|--------|
| 78.5026| 94.0470| 84.6483| 11.0381| 42.0749| 88.6709|



where
- **AP**: Average Precision - This is the average of the precision values at different recall levels. It provides a single metric to summarize the precision-recall curve.
- **AP50**: AP at IoU=0.50 - This is the average precision when the Intersection over Union (IoU) threshold is 0.50. It measures how well the predicted bounding boxes overlap with the ground truth boxes at this threshold.
- **AP75**: AP at IoU=0.75 - This is the average precision when the Intersection over Union (IoU) threshold is 0.75. It is a stricter measure compared to AP50, requiring higher overlap between predicted and ground truth boxes.
- **APs**: AP for small objects - This is the average precision for objects that are small in size. It helps to evaluate the model's performance on detecting small objects.
- **APm**: AP for medium objects - This is the average precision for objects that are medium in size. It helps to evaluate the model's performance on detecting medium-sized objects.
- **APl**: AP for large objects - This is the average precision for objects that are large in size. It helps to evaluate the model's performance on detecting large objects.

Detailed metrics throughout the training can be found in the  `metrics.json`