# Notebook of the week 

A yml and a set of instructions to build a functioning environment for the Research Computing notebook of the week club on Cheaha

# clone this repo and update with the job composer

Copy and paste the following job script into a job composer job on rc.uab.edu

```
#!/bin/bash
#SBATCH --partition=pascalnodes
#SBATCH --gres=gpu:1

git clone https://gitlab.rc.uab.edu/rc-data-science/horovod-environment.git /data/user/$USER/nbotw

module load cuda10.0/toolkit
module load Anaconda3

cd /data/user/$USER/nbotw

conda env create -f nbotw.yml --name nbotw

```

# Check to see if the environment works

After the environment is created, you can start up an interactive Jupyter notebook session through rc.uab.edu to check if the environment works.

Under environment setup, specify

```
# Load required modules
module load cuda10.0/toolkit
module load Anaconda3


```

Under Extra jupyter arguments, specify

```
--notebook-dir=/data/user/$USER/nbotw
```

For partition, specify

```
pascalnodes
```
