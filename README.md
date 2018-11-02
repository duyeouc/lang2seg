# lang2seg

## Prerequisites

* Python 2.7
* Pytorch 0.2 or higher
* CUDA 8.0

## Training
1. Train the baseline segmentation model:
```
./experiments/scripts/train_baseline.sh <GPUID> <DATASET> <SPLITBY> <OUTPUT_POSTFIX>
```
<DATASET> <SPLITBY>: refcoco unc/refcoco+ unc/refcocog umd/refcocog google

Output model will be saved at <DATASET>_<SPLITBY>/output_<OUTPUT_POSTFIX>.

The Mask-RCNN model is in `pyutils/mask-faster-rcnn/lib/nets/resnet_v1.py` and `pyutils/mask-faster-rcnn/lib/nets/network.py`.

1. Train the model with spatial dynamic filters:
```
./experiments/scripts/train_spatial.sh <GPUID> <DATASET> <SPLITBY> <OUTPUT_POSTFIX>
```
The Mask-RCNN model is in `pyutils/mask-faster-rcnn/lib/nets/resnet_v1_7f.py` and `pyutils/mask-faster-rcnn/lib/nets/network_7f.py`.

2. Train the whole model with caption loss:
```
./experiments/scripts/train_cycle.sh <GPUID> <DATASET> <SPLITBY> att2in2 <CAPTION_LOSS_WEIGHT>
```
The whole model is in `pyutils/mask-faster-rcnn/lib/nets/resnet_v1_cycle.py` and `pyutils/mask-faster-rcnn/lib/nets/network_cycle.py`.

Losses are calculated in [_add_losses()](https://github.com/wenz116/lang2seg/blob/master/pyutils/mask-faster-rcnn/lib/nets/network_cycle.py#L396).

## Evaluation
1. Evaluate the baseline segmentation model:
```
./experiments/scripts/eval_baseline.sh <GPUID> <DATASET> <SPLITBY> <OUTPUT_POSTFIX> <MODEL_ITER>
```
Evaluate the model at <DATASET>_<SPLITBY>/output_<OUTPUT_POSTFIX>, of trained iteration <MODEL_ITER>.
