# TensorFlow
    使用版本为tensorflow-2.0
    使用以下代码来查看当前tensorflow的版本
    ```py
    import tensorflow as tf
    print(tf.__version__)
    ```
## Tensorflow的安装
### CPU版本
    `pip install tensorflow==2.0.0-beta1`
    安装完成后，在终端输入python3， 然后输入
    ```py
    import tensorflow as tf
    print(tf.__version__)
    ```
    如果没有报错，并且显示的版本为 **2.0.0-beta1** 则安装成功
### GPU版本的安装
    1. 确保你有一张NVIDIA的显卡，并且支持CUDA加速
    2. 安装NVIDIA GPU驱动程序
    3. 安装CUDA工具包
    4. 下载cuDNN SDK
    5. 配置环境变量（Windows）
    在上面步骤完成后在终端输入
    ```py
    pip install tensorflow-gpu==2.0.0-alpha0
    ```
    在我写这篇README的时候tensorflow的官网上还是显示的alpha0版本
    可能会在不久的将来更新成beta

# 目录
## 第一章
    1. 构建一个基础的分类模型
    2. 模型优化——数据归一化
    3. 使用回调函数来显示模型信息
## 第二章
     构建一个基础的回归模型，并使用归一化提升其精确度，再画出学习曲线
