---
abbrlink: ''
author: null
categories: []
cover: false
coverImg: null
date: '2025-07-02T11:33:22.710575+08:00'
img: null
keywords: null
mathjax: false
password: null
summary: null
tags: []
title: test
toc: true
top: false
updated: '2025-07-02T11:33:22.948+08:00'
---
# 核心代码说明

## Pytorch-Unet

本项目提供了四种语义分割模型的实现与对比，包括 **UNET**、**BBSNET**、**UCNET** 及改进版 **UNET**。支持在 RGB-D 图像数据集（如 NYUv2）上运行，并输出分割结果。

---

## 1. 目录结构

```
├── Pytorch-UNet # 原始 UNET 实现 + 个人修改
├── Unet-for-rgbd-sod # RGB-D UNET 训练  +  增强版 UNET
├── BBS-Net # BBSNET 官方实现 + 个人修改
├── UCNet # UCNET 官方实现  + 个人修改
├── data # 数据集存放路径（需自行准备）
├── results # 输出结果保存路径
└── readme.md # 本说明文件
```

---

## 2. 环境依赖

```py
# 创建并激活 Python 3.8 虚拟环境
sudo apt update && sudo apt install python3.8-venv
python3.8 -m venv seg_env
source seg_env/bin/activate

# 安装基础依赖
pip install --upgrade pip
pip install torch==1.12.1+cu113 torchvision==0.13.1+cu113 \
            numpy opencv-python matplotlib pillow
```

确保安装以下 Python 库：

```
pip install torch torchvision numpy opencv-python matplotlib pillow
```

**特殊依赖**：

- **PyTorch** 版本需与模型代码兼容（建议使用与作者一致的版本，如 `torch==1.7.0`）
- 部分模型可能依赖 `scipy` 或 `tifffile`，可通过以下命令安装：

```
pip install scipy tifffile
```

---

**环境要求**：Ubuntu Linux + Python 3.8 + NVIDIA RTX 4090

## 3. 数据集准备

### 3.1 下载数据集

以 **NYUv2** 为例：

1. 下载 NYUv2 Depth V2
2. 解压后将 `images` 和 `masks` 文件夹放入 `data/` 目录
3. 其他 RGBD  图片下载按照对应文件夹中的配置即可

> 注意要修改对应 train 中数据集的位置, 以确保能够正确导入数据

### 3.2 数据格式要求

- 输入图像：RGB 格式（H×W×3）
- 深度图：单通道灰度图（H×W×1）
- mask图：类别标签（H×W×1，整数类型）

---

## 4. 模型运行指南

### 4.1 原始 UNET (`Pytorch-UNet`)

```
cd Pytorch-UNet
python train.py --dataset nyuv2 --batch-size 8 --epochs 50
```

- 输出结果保存在 `Pytorch-UNet/results/` 目录
- 可视化训练过程：`tensorboard --logdir=runs`

  ```
  python train.py \
    --dataset nyuv2 \
    --batch-size 8 \
    --epochs 50 \
    --scale 0.5 \          # 图像缩放因子
    --classes 2 \          # 类别数
    --amp                  # 可选：启用混合精度训练
  ```

### 4.2 RGB-D 增强版 UNET (`Unet-for-rgbd-sod`)

```
cd Unet-for-rgbd-sod
python main.py --mode train --data-root data/nyuv2
```

- 支持 RGB-D 融合输入，需确保深度图与图像对齐
- 修改 `config.py` 中的 `depth_weight` 参数调整深度图权重
- 其中包含消融实验和改进后的 UNET训练代码, 配置同 UNET

### 4.3 BBSNET (`BBS-Net`)

```
 -BBS_dataset\ 
   -RGBD_for_train\  
   -RGBD_for_test\
   -test_in_train\
 -BBSNet
   -models\
   -model_pths\
      -BBSNet.pth
   ...
```

- 模型训练

```
cd BBS-Net
python BBSNet_train.py --batchsize 10 --gpu_id 0
```

- 模型测试

```
python BBSNet_test.py --gpu_id 0 
```

- sota 模型下载 :  [code: dwcp]  https://pan.baidu.com/s/1Fn-Hvdou4DDWcgeTtx081g?_at_=1748571067778
- 输出包含边界感知的分割结果

### 4.4 UCNET (`UCNet`)

```
cd UCNet
python train.py 
```

- 使用多尺度训练提升精度

cite:

```tex
@inproceedings{Zhang2020UCNet,
  title={UC-Net: Uncertainty Inspired RGB-D Saliency Detection via Conditional Variational Autoencoders},
  author={Zhang, Jing and Fan, Deng-Ping and Dai, Yuchao and Anwar, Saeed and Sadat Saleh, Fatemeh and Zhang, Tong and Barnes, Nick},
  booktitle={Proceedings of the IEEE conference on computer vision and pattern recognition},
  year={2020}
}
```

```tex
@article{zhang2021uncertainty,
  title={Uncertainty Inspired RGB-D Saliency Detection},
  author={Jing Zhang and Deng-Ping Fan and Yuchao Dai and Saeed Anwar and Fatemeh Saleh and Sadegh Aliakbarian and Nick Barnes},
  journal={IEEE Transactions on Pattern Analysis and Machine Intelligence}, 
  year={2021}
}
```

![image-20250701194706995](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20250701194706995.png)
