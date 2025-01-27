## Training Configurations

- **Pre-trained Model**: `Misc/cascade_mask_rcnn_R_50_FPN_3x.yaml`
- **Model Weights**: `model_zoo.get_checkpoint_url("Misc/cascade_mask_rcnn_R_50_FPN_3x.yaml")`
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
- **Max Iterations**: 2000
- **AMP Enabled**: True
- **Base Learning Rate**: 0.0001
- **Images Per Batch**: 32

- **Other configs are defaults from**: https://github.com/facebookresearch/detectron2/blob/main/detectron2/config/defaults.py

## Metrics
### After 2000 iterations:
- On Validation Set:

#### BBOX:
| AP     | AP50   | AP75   | APs    | APm    | APl    |
|--------|--------|--------|--------|--------|--------|
| 83.5287| 87.5968| 83.6156| 2.6997 | 69.9006| 97.8596|

#### SEGM:
| AP     | AP50   | AP75   | APs    | APm    | APl    |
|--------|--------|--------|--------|--------|--------|
| 76.1599| 90.8345| 81.9858| 2.7424 | 56.7885| 89.7311|

- On Test Set:

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

Detailed metrics throughout the training can be found in the  `metrics.json`