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

# navigate to an example
This can be downloaded from https://github.com/uber/horovod

```
cd /data/user/blazerid/horovod-master/examples/

mpirun -np 8 -bind-to none -map-by slot -mca pml ob1 -mca btl_tcp_if_include ib0 python keras_mnist.py
```

# or run benchmarks

```
git clone -b cnn_tf_v1.10_compatible https://github.com/tensorflow/benchmarks

cd benchmarks/

mpirun -np 8 -bind-to none -map-by slot -mca pml ob1 -mca btl_tcp_if_include ib0 python scripts/tf_cnn_benchmarks/tf_cnn_benchmarks.py --model resnet101 --batch_size 64 --variable_update horovod
```

For the resnet101 benchmark test, 

running using 4 GPUs across 1 nodes gives: total images/sec: 491.34

running using 8 GPUs across 2 nodes gives: total images/sec: 915.31

running using 12 GPUs across 3 nodes gives: total images/sec: 1450.00
