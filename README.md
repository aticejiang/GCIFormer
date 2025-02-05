# GCIFormer: Global Context Interaction Transformer for Volumetric Medical Image Segmentation

All code and data will be made available after the peer review process.

## Model Overview

<p align="center">
<img src="figs/GCIFormer_overall.png" width=100% height=100% 
class="center">
</p>
Overall architecture of GCIFormer. It adopts a U-shaped structure and mainly consists of a decoder, a bottleneck, a head, and GCI blocks. The GCI blocks integrate the semantic tokens with the lateral output features of the encoder and feed the refined features into the decoder.

## Requirements: 

Please use `Ubuntu 20.04` for environment setting.

1. python 3.10 + [torch](https://pytorch.org/get-started/locally/) 2.0.0 + torchvision 0.15.0 (cuda 11.7)
   ```bash
   conda create -n gciformer python=3.10
   conda activate gciformer
   pip install torch==2.0.0 torchvision==0.15.1 torchaudio==2.0.1
   ```

2. Clone this repository
   ```bash
   git clone https://github.com/aticejiang/GCIFormer
   cd GCIFormer
   pip install -e .
   ```

3. Install [monai](https://github.com/Project-MONAI/MONAI):
   ```bash
   pip install monai
   ```

## Dataset preparation

Download from our netdisk [Baidu](https://pan.baidu.com/s/1NO0X-RTACDBjrjmtwQbnBQ) and put them into the `data` folder, which includes original, raw, and preprocessed data. The dataset used in our paper was preprocessed according to the following guidelines.

GCIFormer is built on [nnU-Net](https://github.com/MIC-DKFZ/nnUNet) framework. If you want to train GCIFormer on your own dataset, please follow the nnUNet [guidelines](https://github.com/MIC-DKFZ/nnUNet/blob/master/documentation/dataset_format.md) to prepare the dataset.

1. Data download:
   - [BraTS21](https://www.med.upenn.edu/cbica/brats2021/)
   - [KiTS19](https://kits19.grand-challenge.org/)

2. Setting up paths:
   
   Please refer to [setting_up_paths(nnUNet)](https://github.com/MIC-DKFZ/nnUNet/blob/master/documentation/setting_up_paths.md)
   
3. Dataset conversion:
   
   Conversion via specific programs:
   e.g. ```python Dataset127_BraTS21.py``` for BraTS21 dataset. The converted data is denote as nnUNet_raw data.

4. Preprocessing:
   ```bash
   nnUNetv2_plan_and_preprocess -d DATASET_ID --verify_dataset_integrity
   ```

## Train models

```bash
nnUNetv2_train DATASET_ID 3d_fullres 0 -tr 
```
or using custom bath size
```bash
nnUNetv2_train DATASET_ID 3d_fullres_bsXX 0 -tr
```

## Acknowledgements

Thank the authors of [nnU-Net](https://github.com/MIC-DKFZ/nnUNet) for making their valuable code publicly available.

## Citation
