---
title: Jetson Nano
parent: AI
---

NVidia Jetson Nano
	Images:
		Standard image doesn't include Jupyter Lab, etc. that is used in Getting Started Class.
			Discussion:
			https://devtalk.nvidia.com/default/topic/1049646/jetson-nano/jupyter-notebook-in-jetson-nano/
			---
			Instructions to set up for Jetbot project, which overlaps with class install:
				https://github.com/NVIDIA-AI-IOT/jetbot/wiki/Create-SD-Card-Image-From-Scratch
			Instructions to set up to Jetcard
				https://github.com/NVIDIA-AI-IOT/jetcard

NVidia sdkmanager:
	Run application (since not keeping files in ~/Downloads):
		`sdkmanager --downloadfolder <path-to>/sdkm_downloads/`

Start jupyter:
```
	source ~/.virtualenvs/generative/bin/activate
	jupyter lab --ip=0.0.0.0 --no-browser
	http://10.42.0.248:8888
	(dlinano)
```

Run GDL_code
	https://stackoverflow.com/questions/53698035/failed-to-get-convolution-algorithm-this-is-probably-because-cudnn-failed-to-in
	---
	Jupyter server terminal provides more useful information than notebook interface.
		Loaded runtime CuDNN library: 7.3.1 but source was compiled with: 7.5.0.  CuDNN library major and minor version needs to match or have higher minor version in case of CuDNN 7.0 or later version. If using a binary install, upgrade your CuDNN library.  If building from sources, make sure the library loaded at runtime is compatible with the version specified during compile configuration.
			-> this means that build was expecting 7.5.0, but found 7.3.1.
			I have: `/usr/lib/aarch64-linux-gnu/libcudnn.so.7.3.1`
	I must use `tensorflow-gpu 1.14.0`, per NVidia repo content.
		Matching cuDNN as tested is 7.4
			https://www.tensorflow.org/install/source#tested_build_configurations
	Installed CUDA is 10.0
		`locate cuda`
	NVidia support points to SDK Manager as source for components.
		Appears geared towards complete reflash.
		See if I can access the libraries.

scipy 1.3.1 install failed due to missing Libraries
	Associated with Atlas, Lapack
		Atlas (http://math-atlas.sourceforge.net/) libraries not found.
		Lapack (http://www.netlib.org/lapack/) libraries not found.
	mkl_rt openblas tatlas lapack_atlas ptf77blas ptcblas atlas lapack
	---
	Forum post recommends:
		`apt install libblas-dev liblapack-dev libatlas-base-dev gfortran`
		https://askubuntu.com/questions/623578/installing-blas-and-lapack-packages

`ipykernel` needs to be local to `virtualenv` and run with it activated

nano
	Can I cache the build output, not just the sources? For quick install on other units. Can I cross-compile on a more powerful computer, such as in a container emulating the target? Or, are pre-built libraries / packages available elsewhere? Can and should I make these available to others?
	Can I cache the training data?
		-> `~/.keras/datasets/cifar-10-batches-py.tar.gz`
	Capture updated project in git, with instructions to recreate.

Why doesn't pip seem to cache in generative ?
	Maybe it doesn't like the relative path ~/, preferring $HOME/.
	https://docs.python-guide.org/dev/pip-virtualenv/

NVidia mirror
	https://developer.download.nvidia.com/compute/redist/jp/v42/
		for tensorflow-gpu
  Check sdkmanager and see where it gets components from.
  ---
Find local mirror for NVidia, et. al, or make my own local mirror on devpi or otherwise:
	https://github.com/pypa/bandersnatch
