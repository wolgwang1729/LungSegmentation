# Changelog

## Changes from V1 to V2

- **Training Time**: Reduced by using automatic precision and by fixing the size of input image and turning off random flip.
- **Config File**: Refactored configurations for better readability

## Changes from V2 to V3

- **Optimizer**: Changed from `SGD with Momentum` to `Adam`.
- **Base Learning Rate**: Set to `0.0001`from `0.0025`

## Changes from V3 to V4

- **Optimizer**: Changed from `Adam` to `AdamW`.
- **Base Learning Rate**: Set to `0.0001`.

## Changes from V4 to V5

- **Pre Trained Model**:  Nask R-CNN ResNeXt-101 (32x8d) FPN
- **Optimizer**: Changed to `Adam`.
- **Base Learning Rate**: Set to `0.0001`.