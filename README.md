# Meta-Transfer Learning Tensorflow
[![LICENSE](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/y2l/meta-transfer-learning-tensorflow/blob/master/LICENSE)

This repo contains the TensorFlow implementation for CVPR 2019 Paper [Meta-Transfer Learning for Few-Shot Learning](https://arxiv.org/pdf/1812.02391.pdf) by [Qianru Sun](https://www.comp.nus.edu.sg/~sunqr/), [Yaoyao Liu](https://yaoyaoliu.m2i.ac.cn), [Tat-Seng Chua](https://www.chuatatseng.com/) and [Bernt Schiele](https://www.mpi-inf.mpg.de/departments/computer-vision-and-multimodal-computing/people/bernt-schiele/).

If you have any problems when running this repo, feel free to send me an email or open an issue. I will reply to you as soon as I see them.

<p align="center">
    <img src="https://raw.githubusercontent.com/y2l/meta-transfer-learning-tensorflow/master/docs/framework.png" width="700"/>
</p>

#### Summary:

* [Introduction](#introduction)
* [Installation](#installation)
* [Dataset](#Dataset)
* [Repo architecture](#repo-architecture)
* [Usage](#usage)
* [Citation](#citation)
* [Acknowledgements](#acknowledgements)


## Introduction

Meta-learning has been proposed as a framework to address the challenging few-shot learning setting. The key idea is to leverage a large number of similar few-shot tasks in order to learn how to adapt a base-learner to a new task for which only a few labeled samples are available. As deep neural networks (DNNs) tend to overfit using a few samples only, meta-learning typically uses shallow neural networks (SNNs), thus limiting its effectiveness. In this paper we propose a novel few-shot learning method called **meta-transfer learning (MTL)** which learns to adapt a **deep NN** for **few shot learning tasks**. Specifically, meta refers to training multiple tasks, and transfer is achieved by learning scaling and shifting functions of DNN weights for each task. In addition, we introduce the **hard task (HT) meta-batch** scheme as an effective learning curriculum for MTL. We conduct experiments using (5-class, 1-shot) and (5-class, 5-shot) recognition tasks on two challenging few-shot learning benchmarks: miniImageNet and Fewshot-CIFAR100. Extensive comparisons to related works validate that our **meta-transfer learning** approach trained with the proposed **HT meta-batch** scheme achieves top performance. An ablation study also shows that both components contribute to fast convergence and high accuracy.

## Installation

In order to run this repo, we advise you to install python 2.7 and TensorFlow 1.3.0 with Anaconda.

You may download Anaconda and read the installation instruction on their official website:
[https://www.anaconda.com/download/](https://www.anaconda.com/download/)

Create a new environment and install tensorflow on it:

```Bash
conda create --name tensorflow_1.3.0_gpu python=2.7
source activate tensorflow_1.3.0_gpu
pip install --ignore-installed --upgrade https://mirrors.tuna.tsinghua.edu.cn/tensorflow/linux/gpu/tensorflow_gpu-1.3.0-cp27-none-linux_x86_64.whl
```

Clone the repo:

```Bash
git clone https://github.com/y2l/meta-transfer-learning-tensorflow.git 
cd meta-transfer-learning-tensorflow
```

Requirements:
```
python 2.7
tensorflow 1.3.0
scipy
tqdm
opencv-python
```

Some basic requirements are not listed, you may install them easily with `pip`.

## Dataset

### miniImageNet

The miniImageNet dataset was proposed by [Vinyals et al.](http://papers.nips.cc/paper/6385-matching-networks-for-one-shot-learning.pdf) for few-shot learning evaluation. Its complexity is high due to the use of ImageNet images but requires fewer resources and infrastructure than running on the full [ImageNet dataset](https://arxiv.org/pdf/1409.0575.pdf). In total, there are 100 classes with 600 samples of 84×84 color images per class. These 100 classes are divided into 64, 16, and 20 classes respectively for sampling tasks for meta-training, meta-validation, and meta-test.

To generate this dataset, you may use the repo [miniImageNet Tools](https://github.com/y2l/mini-imagenet-tools).

### Fewshot-CIFAR100

We will release the code to generate this dataset soon. You may also generate it yourself with the splits provided by [TADAM](https://arxiv.org/pdf/1805.10123.pdf).

### *tiered*ImageNet 

The [*tiered*ImageNet](https://arxiv.org/pdf/1803.00676.pdf) dataset is a larger subset of ILSVRC-12 with 608 classes (779,165 images) grouped into 34 higher-level nodes in the ImageNet human-curated hierarchy. You may use this repo to generate the *tiered*ImageNet dataset: [*tiered*ImageNet Tools](https://github.com/y2l/tiered-imagenet-tools).

## Repo architecture

```
.
├── data_generator              # dataset generator 
|   ├── pre_data_generator.py   # data genertor for pre-train phase
|   └── meta_data_generator.py  # data genertor for meta-train phase
├── docs                        # project website source code
├── models                      # tensorflow model files 
|   ├── models.py               # basic model class
|   ├── pre_model.py.py         # pre-train model class
|   └── meta_model.py           # meta-train model class
├── trainer                     # tensorflow trianer files  
|   ├── pre.py                  # pre-train trainer class
|   └── meta.py                 # meta-train trainer class
├── utils                       # a series of tools used in this repo
|   └── misc.py                 # miscellaneous tool functions
├── main.py                     # the python file with main function and parameter settings
└── run_experiment.py           # the script to run the whole experiment
```

## Uasge

To run the experiment:
```bash
python run_experiment.py
```
You may edit the `run_experiment.py` file to change the hyperparameters and default settings. The details for the parameters are in `main.py`.

Pre-train phase is included in the current framework. In the default setting, if you run `python run_experiment.py`, the pretrain process will be conducted before the meta-train phase starts. If you want to use the model pretrained by us, you may download the model by the following link then replace the pretrain model loading directory in `trainer/meta.py`.

[Download Pretain Model (miniImageNet)](https://drive.google.com/uc?authuser=0&id=1pd8VSQfO7ILVT1OGDjARwHSRtAvwrsID&export=download)

## Todo

- [x] **Hard task meta batch.**
  The implement of hard task meta batch is not included in the published code. I still need time to rewrite the hard task meta batch code for the current framework.
- [x] **More network architectures.**
  We will add new backbones to the framework like ResNet18 and ResNet34.

## Citation

Please cite our paper if it is helpful to your work:

```
@inproceedings{Sun2019MTL,
  title={Meta-Transfer Learning for Few-Shot Learning},
  author={Qianru Sun and Yaoyao Liu and Tat{-}Seng Chua and Bernt Schiele},
  booktitle={CVPR},
  year={2019}
}
```

## Acknowledgements

This repo uses the source code from the following repos:

[Model-Agnostic Meta-Learning](https://github.com/cbfinn/maml)

[Optimization as a Model for Few-Shot Learning](https://github.com/gitabcworld/FewShotLearning)
