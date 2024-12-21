The following installation process is verified in A100/V100 + CUDA12.1.

# Prepare the Environment
[中文文档](./install_guide-zh.md)
This guide is about building a python environment for MimicTalk with Conda (the same as `Real3D-Portrait`).

0- Update system and build tools
```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install build-essential
```

1- Clone repo
```bash
[git clone https://github.com/yerfor/MimicTalk.git](https://github.com/Devinance/MimicTalk.git)
```

2- Install Conda (miniconda)
```bash
wget https://repo.anaconda.com/archive/Anaconda3-2024.10-1-Linux-x86_64.sh
bash Anaconda3-2024.10-1-Linux-x86_64.sh
pip install --upgrade pip
```

3- Install CUDA 12.1 & Additional packages
```bash
# Before install pytorch3d, you need to install CUDA-12.1 
# and make sure /usr/local/cuda points to the `cuda-12.1` directory
wget https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/cuda-keyring_1.0-1_all.deb
sudo dpkg -i cuda-keyring_1.0-1_all.deb
sudo apt-get update
sudo apt-get -y install cuda
```

4- Install Python Packages & CUDA
```bash
cd <MimicTalkRoot>
source <CondaRoot>/bin/activate
conda create -n mimictalk python=3.9
conda activate mimictalk
pip install --upgrade pip

# MMCV for SegFormer network structure
# other dependencies
pip install pyworld webrtcvad
conda install pyaudio:pyaudio
pip install -r docs/prepare_env/requirements.txt -v
pip install torch==2.4.0 torchvision==0.19.0 torchaudio==2.4.0 --index-url https://download.pytorch.org/whl/cu121
pip install cython
pip install openmim==0.3.9
mim install mmcv==2.1.0 # use mim to speed up installation for mmcv
## build pytorch3d from Github's source code. 
## It may take a long time (maybe tens of minutes), Proxy is recommended if encountering the time-out problem
pip install "git+https://github.com/facebookresearch/pytorch3d.git@stable"
## if building fails or takes too long
conda install pytorch3d::pytorch3d
```
