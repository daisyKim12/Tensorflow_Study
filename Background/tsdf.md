# TFDS
This folder contains projects with Tensorflow Datasets

## Dataset Covered
1. Image classification
   - [beans](https://www.tensorflow.org/datasets/catalog/beans?hl=ko)

## Using TensorFlow Datasets

One can use the data set tensorflow provides in the link below
`Datasets`: [TendorFlow DataSets](https://www.tensorflow.org/datasets/catalog/overview?hl=ko#all_datasets)

In order to use the dataset you must import packages load the data using a `load()`method
[tfds.load()](https://www.tensorflow.org/datasets/api_docs/python/tfds/load)
```
import tensorflow as tf
import tensorflow_datasets as tfds

ds = tfds.load('mnist', split='train', shuffle_files=True)
```

## tfds.load()
[tfds.load()](https://www.tensorflow.org/datasets/api_docs/python/tfds/load)

## tf.image.resize()
[tf.image.resize()](https://www.tensorflow.org/api_docs/python/tf/image/resize)
