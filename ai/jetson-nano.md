---
title: Jetson Nano
parent: AI
---

# [](#header-1)Images
Standard image doesn't include Jupyter Lab, etc. that is used in Getting Started class.

[Discussion](https://devtalk.nvidia.com/default/topic/1049646/jetson-nano/jupyter-notebook-in-jetson-nano/)

[Instructions to set up for Jetbot project, which overlaps with class install](https://github.com/NVIDIA-AI-IOT/jetbot/wiki/Create-SD-Card-Image-From-Scratch)

[Instructions to set up to Jetcard](https://github.com/NVIDIA-AI-IOT/jetcard)

# [](#header-1)NVidia sdkmanager
Run application (since not keeping files in `~/Downloads`):

`sdkmanager --downloadfolder <path-to>/sdkm_downloads/`

# [](#header-1)Start jupyter
```
source ~/.virtualenvs/generative/bin/activate
jupyter lab --ip=0.0.0.0 --no-browser
http://10.42.0.248:8888
(dlinano)
```

# [](#header-1)Run GDL_code

Saw error: `Failed to get convolution algorithm. This is probably because cuDNN failed to initialize, so try looking to see if a warning log message was printed above.`
[Helpful discussion](https://stackoverflow.com/questions/53698035/failed-to-get-convolution-algorithm-this-is-probably-because-cudnn-failed-to-in)

_Jupyter server terminal provides more useful information than notebook interface:_

```
Loaded runtime CuDNN library: 7.3.1 but source was compiled with: 7.5.0.  CuDNN library major and minor version needs to match or have higher minor version in case of CuDNN 7.0 or later version. If using a binary install, upgrade your CuDNN library.  If building from sources, make sure the library loaded at runtime is compatible with the version specified during compile configuration.
```
	
This means that build was expecting 7.5.0, but found 7.3.1. I have: `/usr/lib/aarch64-linux-gnu/libcudnn.so.7.3.1`

I must use `tensorflow-gpu 1.14.0`, per NVidia repo content. As shown in [Tensorflow tested build configurations](https://www.tensorflow.org/install/source#tested_build_configurations), the matching cuDNN as tested is 7.4
		
Installed CUDA is 10.0 `locate cuda`

NVidia support points to SDK Manager as source for components, appears geared towards complete reflash rather than making components available separately.
_TODO: See if I can access the libraries._

# [](#header-1)scipy
scipy 1.3.1 install failed due to missing Libraries associated with Atlas, Lapack:
```
Atlas (http://math-atlas.sourceforge.net/) libraries not found.
Lapack (http://www.netlib.org/lapack/) libraries not found.
mkl_rt openblas tatlas lapack_atlas ptf77blas ptcblas atlas lapack
```

[Forum post](https://askubuntu.com/questions/623578/installing-blas-and-lapack-packages) recommends:
`apt install libblas-dev liblapack-dev libatlas-base-dev gfortran`

`ipykernel` needs to be local to `virtualenv` and run with it activated

# [](#header-1)Other

[NVidia mirror for tensorflow-gpu](https://developer.download.nvidia.com/compute/redist/jp/v42/)

TODO: Check sdkmanager and see where it gets components from.

TODO: Find local mirror for NVidia, et. al, or make my own local mirror on devpi or otherwise. See: https://github.com/pypa/bandersnatch

Questions
* Can I cache the build output, not just the sources? For quick install on other units. 
* Can I cross-compile on a more powerful computer, such as in a container emulating the target? Or, are pre-built libraries / packages available elsewhere? 
* Can and should I make these available to others?
* Can I cache the training data `~/.keras/datasets/cifar-10-batches-py.tar.gz`?
* Why doesn't pip seem to cache in generative ?
	* Maybe it doesn't like the relative path ~/, preferring $HOME/. See: https://docs.python-guide.org/dev/pip-virtualenv/
