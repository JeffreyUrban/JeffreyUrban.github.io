---
title: loose ends
parent: AI
---

Read paper: The unreasonable effectiveness of recurrent neural networks  
  Supervised  
  Cyclical data discover / prediction  

 Look into Acumos AI platform: [https://www.acumos.org/](https://www.acumos.org/)  

NVIDIA notes:
	`cat /proc/driver/nvidia/version`
	`nvtop`
	`nvidia-smi` (Nvidia System Management Interface) command line utility
	Benchmarks (inc. GPU): http://www.phoronix-test-suite.com/

Create full tensorflow-gpu environment:
	`conda create --name tf_gpu tensorflow-gpu`
Jupyter Notebook on public URL
	`jupyter notebook &`
	`ngrok http 8888`

GPU
	NVIDIA GPU management and performance analysis:
		https://developer.nvidia.com/tools-overview
		https://developer.nvidia.com/what-is-designworks
	Schedule to run phoronix-test-suite on recurring basis
		See Phoromatic: https://www.phoronix-test-suite.com/?k=phoromatic
		To trend performance / cooling.
		May be best way to remotely detect fan health and heatsink cleanliness.
	multi-GPU
		Experiment on https://vast.ai

Algorithms and Datasets
    https://github.com/switchablenorms
    https://github.com/open-mmlab
    http://mmlab.ie.cuhk.edu.hk/projects/CelebA.html
