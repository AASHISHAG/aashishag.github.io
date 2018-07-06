---
title:  "Overcoming Hurdles - Connecting CNN with LSTM"
date:   2018-7-05
layout: single
author_profile: true
comments: true
tags: [GSoC, AVSR]
category: GSoC
---

![](/others/GSOC.png)

## Overcoming Hurdles - Connecting CNN with LSTM

There are times when even after searching for solutions in the right places you face disappointment and can't find a way out, thats when experts come to rescue as they are experts for a reason! Thats what happened to me when I was trying to find a way to feed CNN features from visual modality to be fed in to LSTM layers to be then processed sequentially.

Given my input is of tensor of shape [batch_size, sequence_length, 112, 112, 5] I needed a way to pass each time step tensor of shape [112, 112, 5] to my VGG-M model to extract features. Here [112, 112, 5] represents a group of 5 sequential frames in a lip video and 112 is the dimension of image frames.


After searching for reasonable amount of time how to implement this in TensorFlow and not finding a way I decided to give Keras a try. There exists a layer wrapper called [TimeDistributed](https://keras.io/layers/wrappers/) which does exactly what I wanted i.e apply a layer or operation in a time distributed manner to a sequential input. Here's are some links on usage of that:

- [How to Use the TimeDistributed Layer for Long Short-Term Memory Networks in Python](https://machinelearningmastery.com/timedistributed-layer-for-long-short-term-memory-networks-in-python/)
- [CNN Long Short-Term Memory Networks](https://machinelearningmastery.com/cnn-long-short-term-memory-networks/)

But since whole project was meant to be implemented in TensorFlow, using Keras wasn't really an option. After seeking help from my mentor Karan, he suggested me using a [tf.map_fn](https://www.tensorflow.org/api_docs/python/tf/map_fn). This API repeatedly applies the callable function to a sequence of elements from first to last. A possible implementation will look something as below:

``` python
inputs = tf.placeholder(shape=[batch_size,sequence_length,112,112,5] ,dtype = tf.float32)

def CNN_features(lip_images):
    with tf.variable_scope('CNN_features'):
        # define VGG-M CNN model here
        return features # shape=[batch_size,sequence_length,512]
        
lip_features = tf.map_fn(CNN_features, inputs, back_prop=True,
                          parallel_iterations=30,
                         swap_memory=True, dtype=tf.float32)
```
But there is a caveat in this approach. The swap_memory parameter controls swapping memory between GPU and CPU and may lead to performance bottleneck during training and inference.

Another better approach suggested by him was to use [tf.reshape](https://www.tensorflow.org/api_docs/python/tf/reshape). This would avoid the performance issue caused earlier by using tf.map_fn. Finally I decided to apply the latter approach and a possible usage would look like below:

``` python
inputs = tf.placeholder(shape=[batch_size,sequence_length,112,112,5] ,dtype = tf.float32)
inputs = tf.reshape(inputs, shape= [-1, 112,112,5]) # reshaping into [batch_size*sequence_length,112,112,5]

with tf.variable_scope('CNN_features'):
        # define VGG-M CNN model here
        return features # shape=[batch_size*sequence_length,512]
        
features = tf.reshape(features, shape = [batch_size,max_sequence_length,512]) # this will reshape a tensor back to batch_size as first dimension.
```

The final extracted features are now compatible to be fed in the LSTM layer.

And this concludes a blog. My next blog will be on creating data input pipeline using tfrecords and the newly released [tf.data](https://www.tensorflow.org/programmers_guide/datasets) API.