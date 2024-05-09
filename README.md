# Distributed TinyChat

if you need to set up AWQ please refer to the original [README](https://github.com/HPCSGOlab/llm-awq/blob/Abrozows_Spring_2024/AWQ_README.md)

This readme will go over the current progress made on the Distributed TinyChat project. 

**Key Pieces of Information** 

1. Tinychat was built to run on a Jetson Orin with 64Gb of memory

2. Our Jetson Orins have around 7GB of memory

3. We will ideally use Model Parallel practies to get Tiny Chat cistributed, particually Pipeline Parallelism.  

4. In order to do this we will be using Pytorches RPC library and modifying the [llm-awq/tinychat/models/llama.py](https://github.com/HPCSGOlab/llm-awq/blob/Abrozows_Spring_2024/tinychat/models/llama.py) file

    helpful recources will be [RPC_Intro](https://pytorch.org/tutorials/intermediate/rpc_tutorial.html) and [Pipeline_Paralelism](https://pytorch.org/tutorials/intermediate/dist_pipeline_parallel_tutorial.html)

## Set up

1. For Orion make sure the pytorch version in pyproject.toml is == 2.0.1

    Then just use cuda 11.4 which is already installed and just needs to be loaded in
2. For the Jetson use [Archiconda](https://github.com/Archiconda/build-tools/releases)

    This worked for me
3. Follow along with the AWQ and TinyChat READMEs 

**Using git clone on files larger then the Orin's memory will crash it**

you must use 
```
GIT_LFS_SKIP_SMUDGE=1 git clone Whatever_the_URL_is
```
enter the directory and then run
```
git lfs checkout
git pull
```
that should keep it from crashing

also note, the orin doesn't have a lot of storage. In fact im not entirely sure if it can hold llama-2 in its entirety

I also wouldn't recommend downloading the whole awq-model-zoo to the jetson, you can just download the file you need.

Note you probably will have weird error on Orion where some token from PyArrow isn't recognized.
if you run these commands
```
pip unistall pyarrow
conda install pyarrow
```
that should fix it




