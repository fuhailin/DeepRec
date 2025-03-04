# TFServing源代码编译&安装

## 开发环境准备

**CPU Base Docker Image**

| GCC Version | Python Version |                           IMAGE                           |
| ----------- | -------------- | --------------------------------------------------------- |
|   7.5.0     |    3.6.9       | alideeprec/deeprec-base:deeprec-base-cpu-py36-ubuntu18.04 |
|   9.4.0     |    3.8.10      | alideeprec/deeprec-base:deeprec-base-cpu-py38-ubuntu20.04 |
|   11.2.0    |    3.8.6       | alideeprec/deeprec-base:deeprec-base-cpu-py38-ubuntu22.04 |

**GPU Base Docker Image**

| GCC Version | Python Version | CUDA VERSION |                           IMAGE                                 |
| ----------- | -------------- | ------------ | --------------------------------------------------------------- |
|    7.5.0    |    3.6.9       | CUDA 11.6.1  | alideeprec/deeprec-base:deeprec-base-gpu-py36-cu116-ubuntu18.04 |
|    9.4.0    |    3.8.10      | CUDA 11.6.2  | alideeprec/deeprec-base:deeprec-base-gpu-py38-cu116-ubuntu20.04 |
|    11.2.0   |    3.8.6       | CUDA 11.7.1  | alideeprec/deeprec-base:deeprec-base-gpu-py38-cu117-ubuntu22.04 |

**CPU Dev Docker (with bazel cache)**

| GCC Version | Python Version |                           IMAGE                           |
| ----------- | -------------- | --------------------------------------------------------- |
|   7.5.0     |    3.6.9       | alideeprec/deeprec-build:deeprec-dev-cpu-py36-ubuntu18.04 |
|   9.4.0     |    3.8.10      | alideeprec/deeprec-build:deeprec-dev-cpu-py38-ubuntu20.04 |

**GPU(cuda11.6) Dev Docker (with bazel cache)**

| GCC Version | Python Version | CUDA VERSION |                           IMAGE                                 |
| ----------- | -------------- | ------------ | --------------------------------------------------------------- |
|    7.5.0    |    3.6.9       | CUDA 11.6.1  | alideeprec/deeprec-build:deeprec-dev-gpu-py36-cu116-ubuntu18.04 |
|    9.4.0    |    3.8.10      | CUDA 11.6.2  | alideeprec/deeprec-build:deeprec-dev-gpu-py38-cu116-ubuntu20.04 |


## TFServing代码库及分支

我们提供了针对DeepRec版本的TFServing，该版本指向DeepRec Repo.

代码库：[https://github.com/DeepRec-AI/serving](https://github.com/DeepRec-AI/serving)

开发分支：master，最新Release分支：deeprec2310

## TFServing编译&打包

**代码编译-CPU版本**

```bash
bazel build -c opt tensorflow_serving/...
```

**编译开启OneDNN + Eigen Threadpool工作线程池版本（CPU）**

```bash
bazel build -c opt --config=mkl_threadpool --define build_with_mkl_dnn_v1_only=true tensorflow_serving/...
```

**代码编译-GPU版本**

```bash
bazel build -c opt --config=cuda tensorflow_serving/...
```

**生成Client Wheel包**

```bash
bazel-bin/tensorflow_serving/tools/pip_package/build_pip_package /tmp/tf_serving_client_whl
```

**Server Bin**

Server Bin生成在下面路径中：
```bash
bazel-bin/tensorflow_serving/model_servers/tensorflow_model_server
```
