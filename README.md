# VeDaDet

# 项目背景

随着我国汽车保有量的进一步增加，街道上汽车密度逐渐增加，随之而来的汽车之间的碰撞也在增加，而大多数的车祸都是损失较小的擦碰事件，或者车辆与建筑物的擦碰。在二手车市场或汽车维修时，检测汽车损坏情况仍需要人工投入。面对日益扩张的二手车市场以及保险领域，快速确定汽车损伤情况对二手车定价和汽车定损有极大的帮助，能够大大减轻人工压力，使人工仅需要在检测有损的车中进行具体定损，从而提升效率。通过目标检测的算法，可将模型部署于移动端中，相关从业人员仅需要环绕拍照即可确定汽车损伤情况。

![introduction](https://raw.githubusercontent.com/smy1999/VeDaDet/release/2.3/images/introduction.jpeg)

# 数据集介绍

数据集包含多个损坏零件的汽车图像，来源于Kaggle的[车损检测数据集](https://www.kaggle.com/lplenka/coco-car-damage-detection-dataset)。该数据集属于交通领域，适合计算机视觉中目标检测或实例分割任务。

数据集共有78张图片，分割成train、val、test三个部分，分别包括59、11和8张图片，每张图片以jpg格式存储。其中，训练集和验证集包含COCO格式的注释文件。数据集提供的COCO格式注释，分为两个类型。一部分是仅描述了损坏发生的位置，即仅有damage一类目标；另一部分则描述了损坏具体发生的位置，共有headlamp、front_bumper、hood、door、rear_bumper五类。

<img src="https://raw.githubusercontent.com/smy1999/VeDaDet/release/2.3/images/dataset_image.png" style="zoom:50%;" />

# 模型介绍

`PP-PicoDet`是百度飞桨PaddlePaddle在`PaddleDetection`中提出的全新轻量级系列模型，在移动端具有卓越的性能，是全新SOTA轻量级模型。

<img src="https://raw.githubusercontent.com/smy1999/VeDaDet/release/2.3/images/model_architecture.png" alt="model_architecture" style="zoom:50%;" />

# 快速开始

### 安装

项目的安装参考`PaddleDetection`的[安装文档](https://github.com/PaddlePaddle/PaddleDetection/blob/release/2.3/docs/tutorials/INSTALL_cn.md)。

- 安装`PaddlePaddle`

```shell
# CUDA10.1
python -m pip install paddlepaddle-gpu==2.2.0.post101 -f https://www.paddlepaddle.org.cn/whl/linux/mkl/avx/stable.html

# CPU
python -m pip install paddlepaddle -i https://mirror.baidu.com/pypi/simple
```

- 安装`PaddleDetection`

```shell
# 克隆PaddleDetection仓库
cd <path/to/clone/PaddleDetection>
git clone https://github.com/PaddlePaddle/PaddleDetection.git

# 安装其他依赖
cd PaddleDetection
pip install -r requirements.txt

# 编译安装paddledet
python setup.py install
```

### 训练

模型训练采用的配置文件参见项目configs内。

在单卡GPU上训练：

```shell
python tools/train.py -c configs/picodet/picodet_l_640_coco.yml
```

### 评估

```shell
python tools/eval.py -c configs/picodet/picodet_l_640_coco.yml -o weights=output/model_final.pdparams
```

### 测试

```shell
python tools/infer.py -c configs/picodet/picodet_l_640_coco.yml -o weights=weight/model_final.pdparams --infer_img=path/to/xx.jpg
```

![test_image](https://raw.githubusercontent.com/smy1999/VeDaDet/release/2.3/images/test_66.jpg)

### 导出

```shell
python tools/export_model.py -c configs/picodet/picodet_l_640_coco.yml -o weights=output/model_final.pdparams
```

# 个人介绍

中央民族大学2021级研究生 邵明钺

邮箱 smy19990312@gmail.com

欢迎大家反馈交流