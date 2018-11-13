# horovod-environment

A yml and a set of instructions to build a functioning horovod environment for distributed learning using keras and tensorflow (and torch on Cheaha

# load modules
module load Anaconda3/5.2.0

module load cuda91

module load OpenMPI/3.1.2-gcccuda-2018b

# create anaconda environment
Download distribLearn2.yml from this repo

conda env create -f distribLearn2.yml --name distributedLearning

source activate distributedLearning

conda update automat

pip uninstall horovod

pip install --no-cache-dir horovod

#navigate to an example
This can be downloaded from https://github.com/uber/horovod

cd /data/user/blazerid/horovod-master/examples/

mpirun -np 8 -H host1:4,host2:4 -bind-to none -map-by slot -mca pml ob1 -mca btl_tcp_if_include ib0 python keras_mnist.py
