# Caffe模型转化TensorFlow模型
随着TensorFlow框架在谷歌的支持发展下，TensorFlow已经逐步取代了caffe等神经网络学习框架。考虑到TensorFlow框架的易部署情况下（Ubuntu 16.04 以上 直接使用pip install tensorflow 可直接安装），介绍一下caffe模型转化为TensorFlow模型方法。

step 1: 
git clone 开源项目：https://github.com/ethereon/caffe-tensorflow 到本地

step 2:
准备好caffe模型，即*.caffemodel文件，caffe 神经网络文件即*.deploy.prototxt，输出文件为TensorFlow神经网络文件*Tensorflow.py，TensorFlow数据文件（模型文件）*Tensorflow.npy，使用以下指令：

```
./convert.py *.deploy.prototxt --caffemodel *.model.caffemodel --code-output-path=*Tensorflow.py --data-output-path=*Tensorflow.npy
```

step 3:
编写TensorFlow代码，加载TensorFlow神经网络文件以及数据文件即可通过网络预测输出结果。
