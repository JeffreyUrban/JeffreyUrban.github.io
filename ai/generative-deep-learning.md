---
title: Generative Deep Learning
parent: AI
---

_Keras + TensorFlow is most popular and best documented_

# [](#header-1)Keras  
Recommend using Functional API (vs Sequential) for flexibility, even when building linear models  

# [](#header-1)Layer types
* Flatten:  
  * Converts multi-dimensional input into linear input \(needed for other types, inc. dense\)  
  * Flattens on all dimensions except index into training set  
* Dense:  
  * All units connected to all units in previous layer \(fundamental type\)  
* Convolutional (e.g. Conv2D):  
  * Each unit performs a calculation on a range of neighbor units in previous layer, across all channels, plus a bias term \(e.g. Conv2D with kernel\_size=\(4,4\) on 3 color image inputs 4x4x3x1\).  
  * Enable padding=same for output dimensions to equal input dimensions.  
  * Parameters are adjusted per filter, which is applied across entire layer.  
  * There are typically multiple filters per layer.  
  * Filters will generally identify features such as edges or color combinations.  
* Dropout:  
  * Passes through outputs from previous layer, except during training it randomly sets a fraction \(rate\) of outputs to 0 to avoid reliance on specific units and ensure knowledge is more distributed across network.  
  * A regularization technique to mitigate overfitting to the training data, and better generalize across the sample space.  
  * Most common after dense layers \(since they have so many weights and are therefore most prone to overfitting\), but also after convolutional layers.  
* Batch Normalization:  
  * Calculates mean and standard deviation on each channel across each batches. Subtracts mean, then divides by standard deviation \(2 non-trainable parameters per channel\). Then scales \(gamma\) and shifts \(beta\) \(2 trainable parameters per channel\).  
  * Keeps moving averages \(across batches\) of mean and standard deviation for each channel for use after training. Adjust sensitivity to new data via 'momentum'.  
  * Mitigation for 'exploding gradient' problem \(covariate shift\), in which outputs overflow and loss function reports NaN. This may occur long after training has started.  
  * Can also help with overfitting, often replacing dropout layers completely.  
  * Typically placed after dense and convolutional layers.  

# [](#header-1)Activation Function
_Response of each neuron. Must be non-linear._

Activation Functions (the most important ones)  
* ReLU: 0 at and below 0. y = x above 0.  
* LeakyReLU: small slope below 0. y = x above 0.  
* Sigmoid: 0 at -inf. 1 and +inf.  
* Softmax: Sum of all units at layer is 1.  

# [](#header-1)Loss Function
_Calculation for scoring performance._

Loss Functions (the most common):  
* Mean Squared Error  
  * Best for regression problems \(continuous output\)  
  * Square of difference on all outputs  
* Categorical Cross-Entropy  
  * Best for categorization problems where each observation belongs exclusively to one class  
* Binary Cross-Entropy  
  * Best for binary classification \(yes or no\)  
  * Best for categorization problems where each observation can belong to multiple classes  

# [](#header-1)Optimizer
_Algorithm for adjustment of parameters in training._

Optimizers (the most common):  
* Adam  
  * Usually need adjust only the learning rate (lr).  
* RMSProp  
  * Shouldn't need to adjust parameters much. Read Keras documentation to understand them.  

# [](#header-1)Training (model.fit)

## [](#header-2)Parameters
* batch_size: Observations per training step.  
    * Larger is more stable, but slower. Typically between 3 to 256.  
    * Recommended to increase as training progresses.  
* epochs: Number of passes through all data  
* shuffle (boolean): Order of observations is randomized  

## [](#header-2)Process
1. Unit parameters initialized to small random values  
1. Errors backpropagated per batch  

# [](#header-1)Evaluation (model.evaluate)
Run network on data outside of training set.  

# [](#header-1)Generative Architectures

## [](#header-2)Autoencoder
1. Encode from observations to vector in lower dimensional latent space  
1. Decode from latent space to generated observation  
1. Minimize loss function on round trip \(generated observation vs observation\)  

_Useful for de-noising, since noise is not important data for structure_

Encoder and Decoder can be architecturally different  

Decoder Uses convolutional transpose layer (Conv2DTranspose)  
* Like a convolutional layer in reverse.  
* 'strides' defines size enlargement  

Loss Function (common):  
* Root Mean Squared Error (RMSE)  
    * Preferable for maintaining vibrancy in images  
* Binary cross-entropy between individual pixels  
    * Places heavier penalties on pixels that are badly wrong, resulting in duller images.  

## [](#header-2)Variational Autoencoder
Encoder:  
* All but last layers are same as autoencoder.  
* Encodes points with randomization on normal distribution around selected point \(mu, mean of distribution\), with width based on encoder confidence \(log\_var, logarithm of variances of each dimension\).  

Decoder:  
* Same as autoencoder.  

Loss function:  
* Includes reconstruction loss, as with autoencoder.  
* Also includes Kullback–Leibler (KL) divergence, which is a measure of the difference between probability distributions.  
* These must be balanced to work well (apply r_loss_factor to the reconstruction loss).  

_After training, check distribution of each dimension (can check visually with graph - no specific metric provided). If any are significantly non-normal, reduce reconstruction loss to emphasize KL divergence factor. (balanced with the KL divergence loss)._

Vs. Autoencoder  
* Better supports continuous sampling for decoding  
* Placement of points in the latent space approximates a normal distribution, allowing representative sampling using a normal distribution to randomize point selection.  

Use batch normalization after each convolution layer to speed up training (fewer batches required).  
If content is too much for memory, use a generator (keras: fit_generator() ) to compile batches.  
Calculate difference in coordinates given labels to determine related dimension(s) for that attribute. Adding or subtracting the difference vector from a coordinate should adjust that attribute.
