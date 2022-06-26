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

**Predict Protocol**

This document proposes a predict/inference API independent of any specific ML/DL framework and model server.

This protocol is endorsed by NVIDIA Triton Inference Server, TensorFlow Serving, and ONNX Runtime Server.

Seldon has collaborated with the NVIDIA Triton Server Project and the KServe Project to create a new ML inference protocol. The core idea behind this joint effort is that this new protocol will become the standard inference protocol and will be used across multiple inference services.

详细见： [Predict Protocol - Version 2][2]

## 对标方案 - Run computer vision inference on large  videos 
![](https://d2908q01vomqb2.cloudfront.net/f1f836cb4ea6efb2a0b1b99f41ad8b103eff4b59/2021/09/29/ML-5668-Architecture.png)

An Example for SageMaker: Amazon SageMaker Processing Video2frame Model Inference

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
