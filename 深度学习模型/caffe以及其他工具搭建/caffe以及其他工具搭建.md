# caffe部署

## caffe的安装
### 安装依赖包
```
     sudo apt-get install build-essential
     sudo apt-get install vim cmake git
     sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libboost-all-dev libhdf5-serial-dev 
     sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev protobuf-compiler
     sudo apt-get install libhdf5-serial-dev hdf5-tools  #Ubuntu 16.04 需要
     sudo apt-get install python-dev
```
### 安装运算库
   安装ATLAS
   ```
   sudo apt-get install libatlas-base-dev
   ```
   cd /opt/yuntu/soft/
   下载openblas:
   ```
   git clone https://github.com/xianyi/OpenBLAS
   ```
   安装Openblas:    
   ```
      cd OpenBLAS   
      make -j8    
      sudo make PREFIX=/opt/yuntu-base-soft/OpenBLAS-0.2.20 install -j8     #选择此目录
   ```
      安装完后添加lib路径，在/etc/ld.so.conf.d/目录下新建OpenBLAS.conf，
      ```
      vim /etc/ld.so.conf.d/OpenBLAS.conf
      ```
      加入内容：
      ```
       /opt/yuntu-base-soft/OpenBLAS-0.2.20/lib
       ```
      使之生效：
      ```
        sudo ldconfig
     ```
### 下载caffe
```
      cd /opt/soft/       
      git clone https://github.com/BVLC/caffe.git 
      cd /opt/soft/caffe
```



### 安装python扩展包
      进入caffe的python目录
      ```
      cd /opt/soft/caffe
      sudo apt-get install python-pip
      ```
      安装virtualenv
      ```
      sudo pip install virtualenv  
      ```
      利用virtualenv创建虚拟环境 普通用户权限
      ```
      cd /home/edrive
      virtualenv python-yuntu
      ```
      进入虚拟环境安装python扩展包
      ```
      source python-yuntu/bin/activate
      ```
      进入caffe中的python目录：
      ```
      cd /opt/soft/caffe/python/
      ```
      ```
      for req in $(cat requirements.txt); do pip install -i https://pypi.tuna.tsinghua.edu.cn/simple $req; done
      ```
      如果提示报错，一般是缺少必须的包引起的，直接根据提示 pip install <package-name>就行了
      退出虚拟环境 
      ```
      deactivate
      ```
      
### 编译caffe
      进入caffe目录
      ```
      cd /opt/soft/caffe
      cp Makefile.config.example Makefile.config
      vim Makefile.config
      ```
       这里仅需修改两处：
          1、   # CPU_ONLY := 1（第6行）取消注释，使用CPU_ONLY模式（无GPU）
          2、   BLAS := atlas （第50行）BLAS使用openblas改为：BLAS := open
          3、  指定openblas路径： 
          ```
          # BLAS_INCLUDE := /path/to/your/blas（取消注释，并指定BLAS_INCLUDE :=/opt/yuntu-base-soft/OpenBLAS-0.2.20/include/）
          # BLAS_LIB := /path/to/your/blas（取消注释，并指定BLAS_LIB := /opt/yuntu-base-soft/OpenBLAS-0.2.20/lib/）
          ```
          
          保存退出
      开始编译：
      ```
      make all -j8
      make pycaffe
      ```

      成功后在虚拟环境中加入caffe环境变量：
      进入虚拟环境:
      ```
      source python-yuntu/bin/activate
      cd /opt/python-yuntu/lib/python2.7/site-packages
      vim MyModule.pth
      ```
      加入：/opt/soft/caffe/python
      在任意目录下进入python调用import caffe 看是否成功
      退出虚拟环境 
      ```
      deactivate
      ```
      

## opencv-2.4.13 安装
  
   下载安装包
   ```
   cd opencv-2.4.13
   ```
      安装opencv依赖项
      ```
      sudo apt-get install build-essential libgtk2.0-dev pkg-config python-numpy libavcodec-dev libavformat-dev libswscale-dev
      cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/opt/opencv-2.4.13/ .
      make -j8
      sudo make install -j8
      ```
   
   进入终端python中，输入import cv2 看是否安装成功
   
   
## dlib 安装
```
   pip install dlib
   ```
   
   进入终端python中，输入import dlib 看是否安装成功
   
   
   







