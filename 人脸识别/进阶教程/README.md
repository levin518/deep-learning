# 人脸识别算法
  


## 1、Light CNN人脸特征提取算法
light_cnn出自2016 cvpr吴翔A Light CNN for Deep Face Representation with Noisy Labels 论文中，优势在于一个很小的模型和一个非常不错的识别率。使用maxout作为激活函数，实现了对噪声的过滤和对有用信号的保留，从而产生更好的特征图MFM(Max-Feature-Map)，作者使用了NIN(Network inNetwork)来减少参数。
为了提高人脸特征提取速度，高精度的特征的重要性反而比不上性能的提高，于是选择了该神经网络模型作为人脸特征提取模型。

[参考资料](https://github.com/AlfredXiangWu/face_verification_experiment)


## 2、Mtcnn 人脸检测算法

MTCNN 这个是基于深度学习做的一个人脸检测，它是一个级联的cnn结构。其检测效果很不错，也是现在用的最多的一个开源的人脸检测算法。

[参考资料](https://github.com/kpzhang93/MTCNN_face_detection_alignment)


## 3、dlib 库

dlib是一个现代的C ++工具包，包含了用C ++创建复杂软件来解决实际问题的机器学习算法和工具。它被广泛应用于工业界和学术界，包括机器人，嵌入式设备，手机以及大型高性能计算环境。

[dlib官网](http://dlib.net/)


### dlib的python接口

#### 1、Face Detector
功能：在图像中查找正面人脸。
原理：基于HOG特征，通过滑动窗口检测并结合线性分类器得到人脸坐标。
相关代码：

     ```
     import dlib
     detector = dlib.get_frontal_face_detector()
     dets = detector(img, 1) #返回人脸坐标，其中img为待检测图片
     ```
     
#### 2、face_landmark_detection
功能：在人脸图片的基础上进行人脸关键点检测（五官定位），一共有68个特征点。
原理：通过多级级联的回归树进行关键点回归。
相关代码：

     ```
     import dlib
     predictor = dlib.shape_predictor(predictor_path)  #需加载模型
     shape = predictor(img, d) #img:原图 d :人脸坐标 shape：68关键点坐标
     ```
     
#### 3、cnn_face_detector
功能：人脸检测
原理：基于CNN神经网络的人脸检测，精确到更高，但是对机器要求较高（用GPU或者压缩检测图片）
相关代码：

  ```
  cnn_face_detector = dlib.cnn_face_detection_model_v1(modelpath) #加载模型
  dets = cnn_face_detector(img, 1)  #存储着人脸坐标，其中img为图片数据
  ```
  
#### 4、face_recognition
功能：人脸识别
原理：通过神经网络提取人脸特征，通过欧式距离判断是否同一个人
相关代码：

   ```
   ```
