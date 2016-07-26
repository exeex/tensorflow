tensorflow
===

### description
- test code for tensorflow
- [tensorflow](https://www.tensorflow.org/)
  - version : 0.8
  - how to install in OS X
    - install docker
    - [tensorflow docker installation](https://www.tensorflow.org/versions/r0.8/get_started/os_setup.html#docker-installation)
	- [installation using pip](https://www.tensorflow.org/versions/r0.8/get_started/os_setup.html#pip-installation)
    - [installation from source](https://www.tensorflow.org/versions/r0.8/get_started/os_setup.html#installing-from-sources)

### simple test code
- [test.py](https://github.com/dsindex/tensorflow/blob/master/test.py)

### [tutorial video by hunkim(in korean)](http://hunkim.github.io/ml/)
- linear regression
  - predict real value
  - code
    - [linear_regression1.py](https://github.com/dsindex/tensorflow/blob/master/linear_regression1.py)
    - [linear_regression2.py](https://github.com/dsindex/tensorflow/blob/master/linear_regression2.py)
    - [linear_regression3.py](https://github.com/dsindex/tensorflow/blob/master/linear_regression3.py)
    - [linear_regression4.py](https://github.com/dsindex/tensorflow/blob/master/linear_regression4.py)
    - [train_linear.txt](https://github.com/dsindex/tensorflow/blob/master/train_linear.txt)
- logistic regression
  - binary classification 0 or 1
  - code
    - [logistic_regression1.py](https://github.com/dsindex/tensorflow/blob/master/logistic_regression1.py)
    - [train_logistic.txt](https://github.com/dsindex/tensorflow/blob/master/train_logistic.txt)
- softmax regression
  - multinomial (logistic) classification
  - code
    - [softmax_regression1.py](https://github.com/dsindex/tensorflow/blob/master/softmax_regression1.py)
    - [train_softmax.txt](https://github.com/dsindex/tensorflow/blob/master/train_softmax.txt)
- RNN
  - recurrent neural network
  - code
    - [simple_rnn1.py](https://github.com/dsindex/tensorflow/blob/master/simple_rnn1.py)

### IRIS softmax regression test code
- code
  - [softmax_regression_iris_train.py](https://github.com/dsindex/tensorflow/blob/master/softmax_regression_iris_train.py)
  - [softmax_regression_iris_inference.py](https://github.com/dsindex/tensorflow/blob/master/softmax_regression_iris_inference.py)
  - [train_iris.txt](https://github.com/dsindex/tensorflow/blob/master/train_iris.txt)
  - # training accuracy : around 96%
  - for other traning data
  ```shell
  - convert training data format into the format like train_iris.txt
  - modify softmax_regression3_train.py
  - train and save model
  - modify softmax_regression3_inference.py
  - restore model and test inference
  - these steps are basic usage what you are familar with
  ```

### IRIS multi-layer perceptron test code
- code
  - [mlp_iris.py](https://github.com/dsindex/tensorflow/blob/master/mlp_iris.py)
  - # training accuracy : around 96%

### MNIST softmax regression test code
- download MNIST data from http://yann.lecun.com/exdb/mnist/
- code
  - [softmax_regression_mnist.py](https://github.com/dsindex/tensorflow/blob/master/softmax_regression_mnist.py)
  - # accuracy : around 92%
- softmax regression is same as : 
  - multinomial logistic regression 
  - maximum entropy classifier
  - neural net without hidden layer

### MNIST multi-layer perceptron test code
- code
  - [mlp_mnist_train.py](https://github.com/dsindex/tensorflow/blob/master/mlp_mnist_train.py)
  - [mlp_mnist_inference.py](https://github.com/dsindex/tensorflow/blob/master/mlp_mnist_inference.py)
  - # accuracy : around 98%
- distributed version
  - [mlp_mnist_dist.py](https://github.com/dsindex/tensorflow/blob/master/mlp_mnist_dist.py)
  - training using parameter servers and workers
  ```shell
  $ ./mlp_mnist_dist.sh -v -v

  # worker0 log
  job : worker/0 step :  0 ,training accuracy : 0.9
  job : worker/0 step :  100 ,training accuracy : 0.9
  job : worker/0 step :  200 ,training accuracy : 0.86
  job : worker/0 step :  300 ,training accuracy : 0.9
  ...

  # worker1 log
  job : worker/1 step :  0 ,training accuracy : 0.12
  job : worker/1 step :  0 ,training accuracy : 0.14
  job : worker/1 step :  300 ,training accuracy : 0.82
  job : worker/1 step :  500 ,training accuracy : 0.92
  job : worker/1 step :  600 ,training accuracy : 0.94
  ....
  ```
  - # accuracy :  0.9604

### MNIST convolutaional neural network test code
- code
  - [conv_mnist.py](https://github.com/dsindex/tensorflow/blob/master/conv_mnist.py)
  - # accuracy : around 99%

### MNIST LSTM(recurrent neural network) test code
- code
  - [lstm_mnist.py](https://github.com/dsindex/tensorflow/blob/master/lstm_mnist.py)
  - # accuracy : around 97%

### RNN
- code
  - [simple lstm](https://github.com/dsindex/tensorflow/blob/master/simple_lstm.py)
- [segmentation(auto-spacing) using lstm](https://github.com/dsindex/segm-lstm)
- [char-rnn](https://github.com/sherjilozair/char-rnn-tensorflow)
  
### word2vec
- code
  - [build word2vec model](https://github.com/dsindex/tensorflow/blob/master/word2vec.py)
  - [more optimized model](https://github.com/dsindex/tensorflow/blob/master/word2vec_optimized.py)
  - [test and dump word2vec model](https://github.com/dsindex/tensorflow/blob/master/test_word2vec.py)
  ![T-SNE sample](https://github.com/dsindex/tensorflow/blob/master/tsne.png)

### tensorflow serving
- [setup tensorflow serving](https://tensorflow.github.io/serving/setup)
  - install serving current directory
  - [serving basic](https://tensorflow.github.io/serving/serving_basic)
- [mlp_mnist_export.py](https://github.com/dsindex/tensorflow/blob/master/mlp_mnist_export.py)
```shell
$ cd serving
$ ls serving/
... bazel-bin  bazel-genfiles  bazel-out  bazel-serving  bazel-testlogs  tensorflow  tensorflow_serving  tf_models  tools

$ cp ../mlp_mnist_export.py tensorflow_serving/example
$ cp ../mlp_mnist_interence.proto tensorflow_serving/example
$ cp ../mlp_mnist_inference.cc tensorflow_serving/example
$ cp ../mlp_mnist_client.py tensorflow_serving/example
$ cp ../serving_BUILD tensorflow_serving/example/BUILD

$ bazel build //tensorflow_serving/example:mlp_mnist_export
$ bazel build //tensorflow_serving/example:mlp_mnist_inference_proto
$ bazel build //tensorflow_serving/example:mlp_mnist_inference
# how to generate 'mlp_mnist_inference_pb2.py'? we need to install protoc version 3
$ curl -OL https://github.com/google/protobuf/releases/download/v3.0.0-beta-4/protobuf-python-3.0.0-beta-4.tar.gz
# follow instruction https://github.com/google/protobuf/tree/master/python
$ protoc --version
libprotoc 3.0.0
$ protoc --proto_path=tensorflow_serving/example --python_out=tensorflow_serving/example tensorflow_serving/example/mlp_mnist_inference.proto
$ ls tensorflow_serving/example/mlp_mnist_*
mlp_mnist_client.py         mlp_mnist_export.py         mlp_mnist_inference.cc      mlp_mnist_inference.proto   mlp_mnist_inference_pb2.py
# FIXME : mlp_mnist_inference_pb2.py is not property generated ;;
$ bazel build //tensorflow_serving/example:mlp_mnist_client

$ bazel-bin/tensorflow_serving/example/mlp_mnist_export --input_path=../MNIST_data --export_path=export
$ nohup bazel-bin/tensorflow_serving/example/mlp_mnist_inference --port=9000 ./export/00000001 &
$ bazel-bin/tensorflow_serving/example/mlp_mnist_client --num_tests=100 --server=localhost:9000
```
- if you want to run `mlp_mnist_export.py` without bazel support
```shell
# find out python_path
# vi bazel-bin/tensorflow_serving/example/mlp_mnist_export
  new_env['PYTHONPATH'] = python_path
  print python_path
$ export PYTHONPATH='......'
$ cd ..
$ python mlp_mnist_export.py --input_path=./MNIST_data --export_path=export
```

### references
- [Naive Bayesian, HMM, Maximum Entropy, CRF](https://github.com/dsindex/blog/wiki/%5Bstatistics%5D-Naive-Bayesian,-HMM,-Maximum-Entropy-Model,-CRF)
- [Neural Network and Deep Learning](https://github.com/dsindex/blog/wiki/%5Bneural-network%5D-neural-network-and-deep-learning)
- [RNN](http://www.wildml.com/2015/09/recurrent-neural-networks-tutorial-part-1-introduction-to-rnns/)
- [LSTM](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)
- [Word2Vec](https://github.com/dsindex/blog/wiki/%5BWord2Vec%5D-Neural-Language-Model-and-Word2Vec)
- tensorflow
  - [tensorflow mnist inference test using web interface](https://github.com/sugyan/tensorflow-mnist)
  - [distributed tensorflow](https://www.tensorflow.org/versions/r0.8/how_tos/distributed/index.html)
  - [tensorboard]( https://www.tensorflow.org/versions/master/how_tos/summaries_and_tensorboard/index.html)
  - [tensorflow C++ image recognition demo](https://github.com/tensorflow/tensorflow/tree/master/tensorflow/examples/label_image)
- gpu check
  - command
  ```shell
  $ lspci
  $ nvidia-smi
  $ cat /proc/driver/nvidia/gpus/0/information
  $ cat /proc/driver/nvidia/gpus/1/information
  ```
