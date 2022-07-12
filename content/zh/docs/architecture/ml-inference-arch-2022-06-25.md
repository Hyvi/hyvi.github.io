---
title: "模型推理架构"
date: 2022-06-25T11:33:47+08:00
draft: false
tags: 
categories: 
featured_image: 
description: 
---
## 概念解释

**Squared loss**

a popular loss function, also known as L2 Loss. 

Mean square error (MSE) is the average squared loss per example over the whole dataset.

**Gradient Descent**

SGD(Stochastic Gradient Descent) & Mini-Batch Gradient Descent.


**Predict Protocol**

This document proposes a predict/inference API independent of any specific ML/DL framework and model server.

This protocol is endorsed by NVIDIA Triton Inference Server, TensorFlow Serving, and ONNX Runtime Server.

Seldon has collaborated with the NVIDIA Triton Server Project and the KServe Project to create a new ML inference protocol. The core idea behind this joint effort is that this new protocol will become the standard inference protocol and will be used across multiple inference services.

详细见： [Predict Protocol - Version 2][2]

## 对标方案 - Run computer vision inference on large  videos 
![](https://d2908q01vomqb2.cloudfront.net/f1f836cb4ea6efb2a0b1b99f41ad8b103eff4b59/2021/09/29/ML-5668-Architecture.png)

An Example for SageMaker: Amazon SageMaker Processing Video2frame Model Inference


### Real-time Inference

Real-time inference is ideal for inference workloads where you have real-time, interactive, low latency requirements.

#### Use Your Own Inference Code with Hosting Services
how Amazon SageMaker interacts with a Docker container that runs your own inference code for hosting services.

How Containers Serve Requests: 

Containers need to implement a web server that responds to /invocations and /ping on port 8080.

How Your Container Should Respond to Inference Requests:

A customer's model containers must respond to requests within 60 seconds.

#### TensorRT through NVIDA Triton
TensorRT is a C++ library for high performance inference on NVIDIA GPUs and deep learning accelerators.

Tutorial: https://github.com/NVIDIA/TensorRT/blob/main/quickstart/SemanticSegmentation/tutorial-runtime.ipynb

- Load TensorRT Engine
- Run inference

TensorRT to Triton: https://github.com/NVIDIA/TensorRT/tree/main/quickstart/deploy_to_triton


### Asynchronous inference

### Batch Transform

### Serverless Inference

Amazon SageMaker Serverless Inference is a purpose-built inference option that makes it easy for you to deploy and scale ML models. Serverless Inference is ideal for workloads which have idle periods between traffic spurts and can tolerate cold starts.

## 对标方案 - Machine Learning Platform for AI - EAS

- 一健部署
- 高性能
- 蓝绿部署
- 弹性扩缩
- 编译优化

## 参考 



1. https://github.com/kserve/kserve/issues/892 

2. https://github.com/kserve/kserve/blob/master/docs/predict-api/v2/required_api.md#httprest

3. https://aws.amazon.com/cn/blogs/machine-learning/run-computer-vision-inference-on-large-videos-with-amazon-sagemaker-asynchronous-endpoints/

4. https://aws.amazon.com/cn/blogs/machine-learning/how-deepmap-optimizes-their-video-inference-workflow-with-amazon-sagemaker-processing/

5. https://www.alibabacloud.com/help/zh/machine-learning-platform-for-ai/latest/architecture

6. Kubeflow: https://github.com/kubeflow

7. Amazon SageMaker Processing Video2frame Model Inference https://github.com/aws-samples/amazon-sagemaker-processing-video2frame-model-inference
<br>

<center>  ·End·  </center>
