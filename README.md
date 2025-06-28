# hpc-setup-scripts
#Scripts and instructions to install Miniconda on HPC 
#!/bin/bash

# Go to work directory
cd /work/[username]

# Download Miniconda
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh

# Run installer
bash Miniconda3-latest-Linux-x86_64.sh

# During install, set path to:
# /work/[username]/miniconda3

# Add conda to PATH
export PATH=/work/[username]/miniconda3/bin:$PATH

# Optional: make permanent
echo 'export PATH=/work/[username]/miniconda3/bin:$PATH' >> ~/.bashrc
source ~/.bashrc

# Check conda
which conda
conda --version

# Update conda
conda update -n base -c defaults conda

# Create new environment
conda create -n G-env python=3.10

# Activate environment
conda activate G-env

# Upgrade pip
pip install --upgrade pip


