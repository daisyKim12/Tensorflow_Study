# CNN

**CONTENT COVERED**
- CNN
- Conv2D layer
- Pooling Layer
- Flatten Layer
- Transfer learning

## CNN
A CNN is a kind of network architecture for deep learning algorithms and is specifically used for image recognition and tasks that involve the processing of pixel data.

A deep learning CNN consists of three layers: a convolutional layer, a pooling layer and a fully connected (FC) layer.

![CNN](/X/Screenshot%20from%202023-09-03%2014-13-43.png)

1. `Convolutional layer`: The majority of computations happen in the convolutional layer, which is the core building block of a CNN. A second convolutional layer can follow the initial convolutional layer. **The process of convolution involves a `kernel or filter` inside this layer moving across the receptive fields of the image, checking if a `feature` is present in the image**.

Over multiple iterations, the `kernel` sweeps over the entire image. After each iteration a dot product is calculated between the input pixels and the filter. The final output from the series of dots is known as a `feature map`` or `convolved feature`. Ultimately, the image is converted into numerical values in this layer, which allows the CNN to interpret the image and extract relevant patterns from it.

2. `Pooling layer`: Like the convolutional layer, the pooling layer also sweeps a kernel or filter across the input image. But unlike the convolutional layer, the **pooling layer reduces the number of parameters in the input and also results in some information loss**. On the positive side, **this layer reduces complexity and improves the efficiency of the CNN**.

3. `Fully connected layer`: **The FC layer is where image classification happens in the CNN based on the features extracted in the previous layers**. Here, fully connected means that all the inputs or nodes from one layer are connected to every activation unit or node of the next layer.

## Conv2D layer
> This layer creats a 2D convolution layer. This layer creates a convolution kernel that is convolved with the layer input to produce a tensor of outputs.

When using this layer as the first layer in a model, provide the keyword argument input_shape (tuple of integers or None, does not include the sample axis), e.g. input_shape=(128, 128, 3) for 128x128 RGB pictures in data_format="channels_last". You can use None when a dimension has variable size.

![Conv2D](../X/Screenshot%20from%202023-09-03%2014-24-24.png)

```
tf.keras.layers.Conv2D(
    filters,
    kernel_size,
    strides=(1, 1),
    padding="valid",
    data_format=None,
    dilation_rate=(1, 1),
    groups=1,
    activation=None,
    use_bias=True,
    kernel_initializer="glorot_uniform",
    bias_initializer="zeros",
    kernel_regularizer=None,
    bias_regularizer=None,
    activity_regularizer=None,
    kernel_constraint=None,
    bias_constraint=None,
    **kwargs
)
```

**example**
```
model= Sequential([
    Conv2D(64, (3,3), input_shape=(224,224,3), activation='relu'),
    MaxPooling2D(2,2),
    Conv2D(128, (3,3), activation='relu'),
    MaxPooling2D(2,2),
    Conv2D(128, (3,3), activation='relu'),
    MaxPooling2D(2,2),
    Flatten(),
    Dropout(0.25),
    Dense(512, activation='relu'),
    Dense(128, activation='relu'),
    Dense(2, activation='softmax'),
])
```

## Pooling Layer
> Max pooling operation for 2D spatial data. Downsamples the input along its spatial dimensions (height and width) by taking the maximum value over an input window (of size defined by pool_size) for each channel of the input. The window is shifted by strides along each dimension.

![MaxPooling](/X/Screenshot%20from%202023-09-03%2014-24-39.png)

```
tf.keras.layers.MaxPooling2D(
    pool_size=(2, 2), strides=None, padding="valid", data_format=None, **kwargs
)
```

## Flatten layer
> Flatten layer change flattens the dimension into 1D.

```
tf.keras.layers.Flatten(data_format=None, **kwargs)
```

## Transfer learning
> Transfer learning involves using an existing architecture and incorporating pre-trained weights from a large dataset.
> 
### VGG net
![VGG Net](../X/Screenshot%20from%202023-09-03%2014-48-14.png)

[Reference](https://arxiv.org/abs/1409.1556)
VGG Net suggests that when building a deep network, Conv2D (3x3) layers deliver the best performance. For example, Conv3-64 equals Conv2D(64, (3x3), ...).

In practical applications, VGG 16 is more commonly used than VGG 19. The reason for this is that, while increasing the number of layers generally improves performance, there's a point of diminishing returns. VGG 16 and VGG 19 have very similar performance, and beyond that, performance tends to decrease. Consequently, VGG 16, with three fewer layers, is preferred.


### Transfer learning VGG net
VGG net's effectiveness is guaranteed, so we'll just import the VGG 16 model as is and fine-tune only the last FC-4096, FC-1000, and softmax layers to achieve the desired task.

Simply implementing VGG 16 as it is doesn't yield good performance. The reason is that VGG requires training on tens of millions of images, whereas we're working with just a few hundred.

So tuning the model for perticular application is essential.


There are many models to use in keras.
[keras application](https://keras.io/api/applications/)
```
from tensorflow.keras.applications import VGG16
```

```
transfer_model = VGG16(weights='imagenet', include_top=False, input_shape=(224, 224, 3))
transfer_model.trainable=False
```
- include_top: whether to include the 3 fully-connected layers at the top of the network. Set False to implement only Conv2D and MaxPooling2D layers.
- model.trainable: Set trainable to False in order to **freeze the model**. In other words, I want to keep the model's weights unchanged, fix the pre-trained weights, and proceed with training.


```
model = Sequential([
    transfer_model,
    Flatten(),
    Dropout(0.5),
    Dense(512, activation='relu'),
    Dense(128, activation='relu'),
    Dense(2, activation='softmax'),
])
```