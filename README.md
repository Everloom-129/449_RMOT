# ECE449-Final-Project: RMOT with Domain Adaptation
Jie Wang,  Mingchen Li,  Junjie Ren and Haoxuan Du
- Nov. 15, 2023 ~ Jan. 14, 2024

## Team Member Information

    - Jie Wang: Leader, MOT-side, jie.20@intl.zju.edu.cn
    - Mingchen Li: Member, LM-side, mingchen.20@intl.zju.edu.cn
    - Junjie Ren: Member, LM-side, junjier.20@intl.zju.edu.cn
    - Haoxuan Du: Member, MOT-side, haoxuan.20@intl.zju.edu.cn


A four-person course project for ECE449: Machine Learning. We do investigation on  a series of SOTA model together. 
## Final Project Milestone: Referring MOT with Domain Adaptation
Please see this repo for our milestone plannning and final presentation. 




---
> Below is our expanded readme for RMOT
# Referring Multi-Object Tracking

This repository is an official implementation of the paper [Referring Multi-Object Tracking](https://arxiv.org/abs/2303.03366). More project details can be found in the [website](https://referringmot.github.io/).

## Introduction


<div style="align: center">
<img src=./figs/TransRMOT.png/>
</div>

**Abstract.** 
Existing referring understanding tasks tend to involve the detection of a single text-referred object. In this paper, we propose a new and general referring understanding task, termed referring multi-object tracking (RMOT). Its core idea is to employ a  language expression as a semantic cue to guide the prediction of multi-object tracking. To the best of our knowledge, it is the first work to achieve an arbitrary number of referent object predictions in videos. To push forward RMOT, we construct one benchmark with scalable expressions based on KITTI, named Refer-KITTI. Specifically, it provides 18 videos with 818 expressions, and each expression in a video is annotated with an average of 10.7 objects. Further, we develop a transformer-based architecture TransRMOT to tackle the new task in an online manner, which achieves impressive detection performance.

## Updates
- (2023/03/19) RMOT dataset and code are released.
- (2023/03/07) RMOT paper is available on [arxiv](https://arxiv.org/abs/2303.03366).
- (2023/02/28) RMOT is accepted by CVPR2023! The dataset and code is coming soon!



## Getting started
### Installation

> The basic environment setup is on top of [MOTR](https://github.com/megvii-research/MOTR), including conda environment, pytorch version and other requirements. 

> The following step is suitable for AutoDL server

### Requirements
- Linux, CUDA>=9.2, GCC>=5.4

- Python>=3.7
### This step is config in autoDL platform, which is ready
- PyTorch>=1.5.1, torchvision>=0.6.1 (following instructions here)


```bash
git clone git@github.com:Everloom-129/449_RMOT.git
cd 449_RMOT # or you can cdd, I config an alias in '.bashrc'
pip install -r requirements.txt 
```
Then the necesary library is supposed to be ready
### more library
However, you need to pip install:
- transformer
- tensorboardX
- einops

### Build MultiScaleDeformableAttention
```bash
cd ./models/ops
sh ./make.sh
# unit test (should see all checking is True)
python test.py
```
### Test the model 
```bash
cd ./449_RMOT
git clone https://huggingface.co/roberta-base # install the language encoder locally
sh configs/r50_rmot_test.sh
```
If everything works well, with video set annotated, then the rmot framework is ready. 



### Dataset
You can download [our created expression](https://github.com/wudongming97/RMOT/releases/download/v1.0/expression.zip) and [labels_with_ids](https://github.com/wudongming97/RMOT/releases/download/v1.0/labels_with_ids.zip). 
The KITTI images are from [official website](https://www.cvlibs.net/datasets/kitti/eval_tracking.php), which are unzipped into `./KITTI/training`.
The Refer-KITTI is organized as follows:

```
.
├── refer-kitti
│   ├── KITTI
│           ├── training
│           ├── labels_with_ids
│   └── expression
```
Note: 
- Our expression (.json) contains corresponding object ids, and the corresponding boxes can be found in 'labels_with_ids' using these ids.
- The 'label_with_ids' is generated from a script from folder `tools`.
But we strongly recommend **not** using it because the generated track_id may not correspond the track_id of our expression files.

### Training
You can download COCO pretrained weights from [Deformable DETR](https://github.com/fundamentalvision/Deformable-DETR) ''+ iterative bounding box refinement''.
Then training TransRMOT on 8 GPUs as following:
```bash 
sh configs/r50_rmot_train.sh
```
Note:
- If the RoBERTa is not working well, please download the RoBERTa weights from [Hugging Face](https://huggingface.co/roberta-base/tree/main) for local using.

### Testing
You can download the pretrained model of TransRMOT (the link is in "Main Results" session), then run following command to generate and save prediction boxes:
```bash
sh configs/r50_rmot_test.sh
```

You can get the main results by runing the evaluation part. You can also use our [prediction and gt file](https://github.com/wudongming97/RMOT/releases/download/v1.0/results_epoch99.zip). 
```bash
cd TrackEval/script
sh evaluate_rmot.sh
```

## Results


The main results of TransRMOT:

| **Method** | **Dataset** | **HOTA** | **DetA** | **AssA** | **DetRe** | **DetPr** | **AssRe** | **AssRe** | **LocA** |                                           **URL**                                           |
|:----------:|:-----------:|:--------:|:--------:|:--------:|:---------:|:---------:|:---------:|-----------|----------| :-----------------------------------------------------------------------------------------: |
| TransRMOT  | Refer-KITTI |  38.06   |  29.28   |  50.83   |   40.19   |   47.36   |   55.43   | 81.36     | 79.93    | [model](https://github.com/wudongming97/RMOT/releases/download/v1.0/checkpoint0099.pth) |


We also provide [FairMOT results](https://github.com/wudongming97/RMOT/releases/download/v1.0/FairMOT_results.zip) as references.



## Citing RMOT
If you find RMOT useful in your research, please consider citing:

```bibtex
@inproceedings{wu2023referring,
  title={Referring Multi-Object Tracking},
  author={Wu, Dongming and Han, Wencheng and Wang, Tiancai and Dong, Xingping and Zhang, Xiangyu and Shen, Jianbing},
  booktitle={Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition},
  pages={14633--14642},
  year={2023}
}
```


## Acknowledgements

- [MOTR](https://github.com/megvii-research/MOTR)
- [Deformable DETR](https://github.com/fundamentalvision/Deformable-DETR)
- [TrackEval](https://github.com/JonathonLuiten/TrackEval)


