# Balanced Mixture of Supernets for Learning CNN Pooling

This repository contains the release of PyTorch code to replicate all main results, figures and tabels presented in the paper: Balanced Mixture of Supernets for Learning the CNN Pooling Architecture

The repository structure is as follows:
  * `requirements.txt`, contains all required libraries
  * `figures/`, contains all figures represented in the paper 
  
`experiments/Pooling Experiments/` contains: 
  * `resnet20/`, contains code for CIFAR10 experiments with Resnet20 backbone architecture 
  * `cifar/`, contains code for CIFAR10/CIFAR100 experiments with Resnet18/Resnet50 backbone architectures
  * `food101/`, contains code for food101 experiments on Resnet50 backbone architecture 
  
Each folder contains a ReadMe file for more information.
  

## Getting Started
### Install
It's recommended to use Python3.9 and create a virtual environment first:
`>>> torch.__version__
'1.13.1+cu117'
`
to install please use one of the two ways:

   ```bash
   $ pip install -r requirements.txt
   ```
Or:
   ```bash
$ conda create -n ffcv2 python==3.9
$ conda activate ffcv2
$ pip install -r requirements.txt
   ```
   
Please note that FFCV library is not required for running experiments in resnet20 folder and only necessary for food101 and cifar folder. Please note that FFCV might have problems for installation in older cuda versions. 
 
### Dataset Preperation
Please note that for experiments in  `cifar/` and `food101/` , datasets need to be converted to [FFCV](https://ffcv.io/) format. For experimetns with resnet20 this is not required. Furthermore, for NAS methods presented in this paper, training datasets are split 50/50:

   * For cifar datasets experiments (assuming in respective dirctory such as `cifar/resnet18/`), to download and convert them for CIFAR100 run:

   ```bash
   $ ./write_cifar.sh
   ```
To split CIFAR datsets before conversion, run:

   ```bash
   $ ./write_cifar_50.sh
   ```
   * For Food101 tests the dataset should be downloaded from [here](https://data.vision.ee.ethz.ch/cvl/datasets_extra/food-101/) and placed in food101 folder. To convert image folder dataset to FFCV format run:

```bash
$ create_dataset.py
```

For our NAS method, split training set to 50/50 subsets per class before conversion by running: 

```bash
$ python split_dataset.py
```

This will create two folders `train_50/` and `val_50/` that can be converted to FFCV files using create_dataset.py .


### Experiments
Experiment contains code to run Balanced Mixture of models as ```main.py``` and an individual training for retraining architectures. See Readme file on each expermints for more details.

# Training Time and Hyperparameter Search


For Resnet20 experiments reported in table 1:

| Experiment | Approximate GPU hours    | Approximate Hyperparameter Search (min)    |
| :---:   | :---: | :---: |
| DARTS (all cases) | 9.5   |  15  |
| SPOS (all cases)  | 3   | 15   |
| Balanced Mixtures (Ours)  | 9.5   | 15   |

For Resnet20 experiments reported in table 2:

| Experiment | Approximate GPU hours    | Approximate Hyperparameter Search (min)    |
| :---:   | :---: | :---: |
| DARTS/DARTS+GAEA  | 9.5   |  15  |
| SPOS/MCT UCB/MCT + Uniform/SBE  | 3   | 15   |
| Default | 1.5   | 15   |
| Balanced Mixtures (Ours)  | 9.5   | 15   
| Bruteforce | 108   | 500   |

For cifar experiments reported in table 3:

| Experiment | Approximate GPU hours    | Approximate Hyperparameter Search (min)    |
| :---:   | :---: | :---: |
| CIFAR10, Resnet18  | 12.5   |  20  |
| CIFAR100, Resnet50  | 18   | 30   |

For Food101 experiments reported in table 4:

| Experiment | Approximate GPU hours    | Approximate Hyperparameter Search (min)    |
| :---:   | :---: | :---: |
| Defalut  | 2   |  20  |
| M=1  | 3   | 30   |
| M=2  | 5   | 30   |
| M=4  | 8.5   | 30   |
| M=8  | 16   | 30   |

NOTE: For hyperparameter search, we performed a grid search for few iterations. The code was originally ran on a cluster with 1 GPU NVIDIA V100 Volta (32G HBM2 memory). However, the files are edited to be ran locally.












