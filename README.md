# horovod-environment

A yml and a set of instructions to build a functioning horovod environment for distributed learning using keras and tensorflow (and torch on Cheaha

# clone this repo

and cd to the working directory

```
git clone git@gitlab.rc.uab.edu:wsmonroe/horovod-environment.git
cd horovod-environment
```

# request gpu resources (one way of doing it), this needs to be done everytime

```
sinteractive --ntasks=8 --time=08:00:00 --exclusive --partition=pascalnodes -N2 --gres=gpu:4
```

# load modules, this needs to be done everytime
```
module load Anaconda3/5.2.0

module load cuda91

module load OpenMPI/3.1.2-gcccuda-2018b
```

# create anaconda environment
Download distribLearn2.yml from this repo

```
conda env create -f distribLearn2.yml --name distributedLearning
```

## source activate env needs to be done everytime
```
source activate distributedLearning
```

These next 3 bits only need to be done to setup the env

```
conda update automat

pip uninstall horovod

pip install --no-cache-dir horovod
```

# Download examples
This can be downloaded from https://github.com/uber/horovod

As always, it is recommended to download data and scripts to your data directory if you would like it to remain persistent
```
/data/user/$USER/horovod-master/examples/
```

# Run the mnist example
While it is possible to run the 
```
mpirun
```
command from the command line, errors are much less likely to occur if the code is run via job script. If the examples are downloaded at the above location, the following example should work
```
sbatch horovod-mnist-training.job
```
make sure you are running your sbatch command from the login node.
# Run benchmarks

```
cd /data/user/$USER

git clone -b cnn_tf_v1.10_compatible https://github.com/tensorflow/benchmarks
```

assuming the benchmarks were downloaded at the above location, the following job script should run a benchmark test
```
sbatch horovod-benchmark.job
```
make sure you are running your sbatch command from the login node.

For the resnet101 benchmark test, 

running using 4 GPUs across 1 nodes gives: total images/sec: 491.34

running using 8 GPUs across 2 nodes gives: total images/sec: 915.31

running using 12 GPUs across 3 nodes gives: total images/sec: 1450.00
