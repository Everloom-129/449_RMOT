# How to install this fucking RMOT

## AutoDL plan


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
- torchtext ....
This is to be confirm, I will update this in the future.


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
sh configs/r50_rmot_test.sh
```
If everything works well, with video set annotated, that's wonderful



---
# Old data: do not follow this on our AutoDL platform
1. deformable detr: initial shit

https://github.com/fundamentalvision/Deformable-DETR/blob/main/README.md?plain=1

## Installation

### Requirements

* Linux, CUDA>=9.2, GCC>=5.4
  
* Python>=3.7

    We recommend you to use Anaconda to create a conda environment:
    ```bash
    conda create -n deformable_detr python=3.7 pip
    ```
    Then, activate the environment:
    ```bash
    conda activate deformable_detr
    ```
  
* PyTorch>=1.5.1, torchvision>=0.6.1 (following instructions [here](https://pytorch.org/))

    For example, if your CUDA version is 9.2, you could install pytorch and torchvision as following:
    ```bash
    conda install pytorch=1.5.1 torchvision=0.6.1 cudatoolkit=9.2 -c pytorch
    ```
  
* Other requirements
    ```bash
    pip install -r requirements.txt
    ```

### Compiling CUDA operators
```bash
cd ./models/ops
sh ./make.sh
# unit test (should see all checking is True)
python test.py
```

2. MOTR: 
https://github.com/megvii-research/MOTR

Installation
The codebase is built on top of Deformable DETR.

Requirements
Linux, CUDA>=9.2, GCC>=5.4

Python>=3.7

We recommend you to use Anaconda to create a conda environment:

conda create -n deformable_detr python=3.7 pip
Then, activate the environment:

conda activate deformable_detr

PyTorch>=1.5.1, torchvision>=0.6.1 (following instructions here)

For example, if your CUDA version is 9.2, you could install pytorch and torchvision as following:

conda install pytorch=1.5.1 torchvision=0.6.1 cudatoolkit=9.2 -c pytorch
Other requirements

pip install -r requirements.txt
Build MultiScaleDeformableAttention

cd ./models/ops
sh ./make.sh

3. RMOT: final fuck
Installation
The basic environment setup is on top of MOTR, including conda environment, pytorch version and other requirements.




20, 18, 16, 15,14, 12,10, 9, 8, 7,6, 4, 3, 2, 1

delete: 00, 19
Old training set
[1, 2, 3, 4, 6, 7, 8, 9, 10, 12, 14, 15, 16, 18, 20]
New training set
[01, 02, 03, 04, 06, 07, 08, 09, 10, 12, 14 ]
