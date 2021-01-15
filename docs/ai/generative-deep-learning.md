---
title: Generative Deep Learning
parent: AI
---

Generative Deep Learning \(notes\)  
  Keras + TensorFlow is most popular and best documented  
  Keras  
   Recommend using Functional API \(vs Sequential\) for flexibility, even when building linear models  
  Layer types:  
   Flatten:  
    Converts multi-dimensional input into linear input \(needed for other types, inc. dense\)  
    Flattens on all dimensions except index into training set  
   Dense:  
    All units connected to all units in previous layer \(fundamental type\)  
   Convolutional \(e.g. Conv2D\):  
    Each unit performs a calculation on a range of neighbor units in previous layer, across all channels, plus a bias term \(e.g. Conv2D with kernel\_size=\(4,4\) on 3 color image inputs 4x4x3x1\).  
    Enable padding=same for output dimensions to equal input dimensions.  
    Parameters are adjusted per filter, which is applied across entire layer.  
    There are typically multiple filters per layer.  
    Filters will generally identify features such as edges or color combinations.  
   Dropout:  
    Passes through outputs from previous layer, except during training it randomly sets a fraction \(rate\) of outputs to 0 to avoid reliance on specific units and ensure knowledge is more distributed across network.  
    A regularization technique to mitigate overfitting to the training data, and better generalize across the sample space.  
    Most common after dense layers \(since they have so many weights and are therefore most prone to overfitting\), but also after convolutional layers.  
   Batch Normalization:  
    Calculates mean and standard deviation on each channel across each batches. Subtracts mean, then divides by standard deviation \(2 non-trainable parameters per channel\). Then scales \(gamma\) and shifts \(beta\) \(2 trainable parameters per channel\).  
    Keeps moving averages \(across batches\) of mean and standard deviation for each channel for use after training. Adjust sensitivity to new data via 'momentum'.  
    Mitigation for 'exploding gradient' problem \(covariate shift\), in which outputs overflow and loss function reports NaN. This may occur long after training has started.  
    Can also help with overfitting, often replacing dropout layers completely.  
    Typically placed after dense and convolutional layers.  
  Activation Function:  
   Response of each neuron. Must be non-linear.  
   ---  
   Activation Functions \(most important\)  
    ReLU: 0 at and below 0. y = x above 0.  
    LeakyReLU: small slope below 0. y = x above 0.  
    Sigmoid: 0 at -inf. 1 and +inf.  
    Softmax: Sum of all units at layer is 1.  
  Loss Function:  
   Calculation for scoring performance.  
   ---  
   Loss Functions \(most common\):  
   Mean Squared Error  
    Best for regression problems \(continuous output\)  
    Square of difference on all outputs  
   Categorical Cross-Entropy  
    Best for categorization problems where each observation belongs exclusively to one class  
   Binary Cross-Entropy  
    Best for binary classification \(yes or no\)  
    Best for categorization problems where each observation can belong to multiple classes  
  Optimizer:  
   Algorithm for adjustment of parameters in training.  
   ---  
   Optimizers \(most common\):  
    Adam  
     Usually need adjust only the learning rate \(lr\).  
    RMSProp  
     Shouldn't need to adjust parameters much. Read Keras documentation to understand them.  
  Training \(model.fit\):  
   Parameters:  
    batch\_size: Observations per training step.  
     Larger is more stable, but slower. Typically between 3 to 256.  
     Recommended to increase as training progresses.  
    epochs: Number of passes through all data  
    shuffle \(boolean\): Order of observations is randomized  
   Process:  
    Unit parameters initialized to small random values  
    Errors backpropagated per batch  
  Evaluation \(model.evaluate\):  
   Run network on data outside of training set.  
  Generative Architectures:  
   Autoencoder:  
    Encoder from observations to vector in lower dimensional latent space  
    Decode from latent space to generated observation  
    Minimize loss function on round trip \(generated observation vs observation\)  
    ---  
    Useful for de-noising, since noise is not important data for structure  
    ---  
    Encoder and Decoder can be architecturally different  
    Decoder:  
     Uses convolutional transpose layer \(Conv2DTranspose\)  
      Like a convolutional layer in reverse.  
      'strides' defines size enlargement  
    Loss Function \(common\):  
     Root Mean Squared Error \(RMSE\)  
      Preferable for maintaining vibrancy in images  
     Binary cross-entropy between individual pixels  
      Places heavier penalties on pixels that are badly wrong, resulting in duller images.  
   Variational Autoencoder:  
    Encoding:  
     All but last layers are same as autoencoder.  
     Encodes points with randomization on normal distribution around selected point \(mu, mean of distribution\), with width based on encoder confidence \(log\_var, logarithm of variances of each dimension\).  
    Decoder:  
     Same as autoencoder.  
    Loss function:  
     Includes reconstruction loss, as with autoencoder.  
     Also includes Kullback–Leibler \(KL\) divergence, which is a measure of the difference between probability distributions.  
     These must be balanced to work well \(apply r\_loss\_factor to the reconstruction loss\).  
     After training, check distribution of each dimension \(can check visually with graph - no specific metric provided\). If any are significantly non-normal, reduce reconstruction loss to emphasize KL divergence factor.  
 balanced with the KL divergence loss\).  
    Vs. Autoencoder  
     Better supports continuous sampling for decoding  
     Placement of points in the latent space approximates a normal distribution, allowing representative sampling using a normal distribution to randomize point selection.  
     Use batch normalization after each convolution layer to speed up training \(fewer batches required\).  
     If content is too much for memory, use a generator \(keras: fit\_generator\(\) \) to compile batches.  
     Calculate difference in coordiantes given labels to determine related dimension\(s\) for that attribute. Adding or subtracting the difference vector from a coordinate should adjust that attribute.
