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

# Submitting a Job
#Step1:create a folder
nano run_G.slurm

#Step2: paste text below and press Ctrl+O then Ctrl+X to save changes
#!/bin/bash
#SBATCH --job-name=scvi
#SBATCH --output=scvi.out
#SBATCH --error=scvi.err
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=4
#SBATCH --mem=16G
#SBATCH --time=04:00:00
#SBATCH --gres=gpu:1

export PATH="/work/[username]/miniconda3/bin:$PATH"
source activate /work/[username]/G-env

python /work/fatemenz/CMMaturation/SCVI.py


#Step3: 
sbatch run_G.slurm

# Check the job
squeue -u fatemenz

# See new output in real-time
tail -f G.out


