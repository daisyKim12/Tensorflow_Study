# TFDS
This folder contains projects with Tensorflow Datasets

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

## Dataset Covered
1. Image classification
   - [beans](https://www.tensorflow.org/datasets/catalog/beans?hl=ko)
