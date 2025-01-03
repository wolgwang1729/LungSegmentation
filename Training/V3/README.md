## Training Configurations

- **Pre-trained Model**: `COCO-InstanceSegmentation/mask_rcnn_R_101_FPN_3x`
- **Model Weights**: `model_zoo.get_checkpoint_url("COCO-InstanceSegmentation/mask_rcnn_R_101_FPN_3x.yaml")`
- **Optimizer**: Adam

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
- **Backbone Freeze At**: 2
- **ROI Heads Batch Size Per Image**: 128
- **Number of Classes**: 1

### Solver
- **Max Iterations**: 3000
- **AMP Enabled**: True
- **Base Learning Rate**: 0.0001
- **Images Per Batch**: 4

- **Other configs are defaults from**: https://github.com/facebookresearch/detectron2/blob/main/detectron2/config/defaults.py

## Metrics
### After 3000 iterations:
- On Validation Set:

#### BBOX:
| AP     | AP50   | AP75   | APs    | APm    | APl    |
|--------|--------|--------|--------|--------|--------|
| 70.1547| 75.4085| 70.8800| 1.6261 | 64.2922| 95.9697|

#### SEGM:
| AP     | AP50   | AP75   | APs    | APm    | APl    |
|--------|--------|--------|--------|--------|--------|
| 63.5748| 76.9854| 69.1167| 0.3748 | 48.8380| 88.4578|


- On Test Set:

#### BBOX:
| AP     | AP50   | AP75   | APs    | APm    | APl    |
|--------|--------|--------|--------|--------|--------|
| 75.7252| 79.0398| 78.9865| 2.1591 | 77.0466| 97.5526|

#### SEGM:
| AP     | AP50   | AP75   | APs    | APm    | APl    |
|--------|--------|--------|--------|--------|--------|
| 68.3715| 78.9538| 71.3822| 1.3740 | 36.7941| 92.0620|


where
- **AP**: Average Precision - This is the average of the precision values at different recall levels. It provides a single metric to summarize the precision-recall curve.
- **AP50**: AP at IoU=0.50 - This is the average precision when the Intersection over Union (IoU) threshold is 0.50. It measures how well the predicted bounding boxes overlap with the ground truth boxes at this threshold.
- **AP75**: AP at IoU=0.75 - This is the average precision when the Intersection over Union (IoU) threshold is 0.75. It is a stricter measure compared to AP50, requiring higher overlap between predicted and ground truth boxes.
- **APs**: AP for small objects - This is the average precision for objects that are small in size. It helps to evaluate the model's performance on detecting small objects.
- **APm**: AP for medium objects - This is the average precision for objects that are medium in size. It helps to evaluate the model's performance on detecting medium-sized objects.
- **APl**: AP for large objects - This is the average precision for objects that are large in size. It helps to evaluate the model's performance on detecting large objects.

Detailed metrics throughout the training can be found in the  `metrics.json`