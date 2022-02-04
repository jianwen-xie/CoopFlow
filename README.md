# CoopFlow
Cooperative learning of Langevin Flow (short-run EBM) and Normalizing Flow

This repository contains a pytorch implementation for ICLR 2022 poster paper "[A Tale of Two Flows: Cooperative Learning of Langevin Flow and Normalizing Flow Toward Energy-Based Model](https://openreview.net/forum?id=31d5RLCUuXC&referrer=%5BAuthor%20Console%5D(%2Fgroup%3Fid%3DICLR.cc%2F2022%2FConference%2FAuthors%23your-submissions))"

## Set Up Environment
We have provided the environment.yml file for setting up the environment. The environment can be set up with one command using conda
```bash
conda env create -f environment.yml
conda activate fpp
```

## Exp1: Image synthesis with pretrained models
1. To generate images using pretrained models, please first download the pretrained checkpoints follow "[this link](https://drive.google.com/drive/folders/1NY5NA7wIguuGEnH4jo-vQ4f4fxFyC-58?usp=sharing)". The folder contains checkpoints with different experimental settings. Please check the Readme file for detailed descriptions. The checkpoints should be downloaded to the ckpt folder (e.g. you should have 'ckpt/cifar10.pth.tar' for CoopFlow cifar10 setting).

2. After the checkpoint is downloaded, you can do image synthesis using the 'main_\*.py' code we provided here. Each individual code here corresponds to one of the settings on one dataset. The *main_cifar.py, main_celeba.py, main_svhn.py* are codes for basic CoopFlow setting. The *main_cifar_pretrain.py main_celeba_pretrain.py, main_svhn_pretrain.py* are codes for CoopFlow(Pre) setting. For CoopFlow(Long) setting, we use multi-gpu for training and the code will come later.  

For example, if you want to synthesizing image using pretrained CoopFlow model on cifar10 dataset. You can symply run
```bash
python main_cifar.py
```

3. Compute FID: The code will save generated images (should be 50000 in total) to folder './exp_cifar/gen_samples' and original images to './exp_cifar/ori_samples'. Then you can use "[pytorch_fid](https://github.com/mseitzer/pytorch-fid)" to calculate the FID score. For example, you can use the following command
```bash
python -m pytorch_fid ./exp_cifar/ori_samples ./exp_cifar_gen_samples
```

4. The generated samples should look like following. Please refer to the paper for more results.

cifar-10 (left: initial proposal by normalizing flow; right: modified version of Langevin flow) 
<img src="cifar_flow.png" width="425"/> <img src="Cifar10.png" width="425"/> 
