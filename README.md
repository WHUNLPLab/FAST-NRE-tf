# FAST-NRE-tf

#### 项目介绍
FAST neural relation extraction。本项目实现了一些基本的神经关系抽取方法，旨在以比较清晰的结构引导初学者快速搭建自己的网络。其中，项目的代码参考但不限于[Lin et.al (2016)](https://github.com/thunlp/OpenNRE)。

#### 项目依赖

1. Python（2或3）
2. Numpy
3. Tensorflow （>=1.4)
4. sklearn

#### 使用说明

本项目同样将网络划分为**Embedding**层，**Encoder**层，**Selector**层和**Classifier**层。其中，Encoder层和Selector层是重点进行拓展的网络层。各层次作用如下：

1. Embedding-layer：将文本id转换为word embedding和position embedding等
2. Encoder-layer：用CNN、PCNN等对sentences进行编码
3. Selector-layer：通过Attention机制为bag中的sentences分配权重，得到bag feature
4. Classifier-layer：计算交叉熵作为网络损失

现有模型大多采用Sequential model，即依次将上述四个层次相连组成网络。

##### 代码说明

- `init_data.py`文件主要负责将txt格式的原始数据转换为numpy数组格式的数据，供多次使用
- `engine.py`文件包含训练和测试逻辑的控制
- `main.py`是程序的入口，主要负责处理命令行参数和初始化
- `model.py`是模型的主要代码，其中部分层由`layers`模块提供
- `utils.py`包含工具代码

##### 运行说明

首次运行代码进行训练时，需要进行数据的初始化操作。

```bash
python main.py --is_train=True --preprocess=True [--clean=True]
```

其中`--clean`选项决定是否清除现有模型文件。之后训练过程，就不需要初始化数据。

```bash
python main.py --is_train=True
```

测试模型：

```bash
python main.py --is_train=False
```

#### 数据说明

本项目原始数据经过细微改动，主要为在Lin et.al. 基础上加入了实体类型。其中数据文件包含如下：

1. relation2id.txt：关系标签到id的映射
2. type2id.txt：实体类型到id的映射
3. vec.txt：词向量文件
4. train.txt：训练集数据
5. test.txt：测试集数据

其中，数据集可以从[这里](https://pan.baidu.com/s/1C-z_v-PivAlQvmL9S3ySkg)下载，训练集和测试集基本格式如下：

```bash
entity1_mid entity2_mid entity1 entity2 entity1_type entity2_type relation_label sentence ###END###
```

上面展示的是一行数据，共分为9个部分，每个部分由制表符`\t`分隔

#### 贡献说明

1. 本项目旨在方便入门，如有不妥，请多包涵
2. 欢迎同道中人献计献策，努力完善


#### 参考文献

1. **Neural Relation Extraction with Selective Attention over Instances.** *Yankai Lin, Shiqi Shen, Zhiyuan Liu, Huanbo Luan, Maosong Sun.* ACL2016. [paper](http://www.aclweb.org/anthology/P16-1200)
2. **Distant supervision for Relation Extraction via Piecewise Convolutional Neural Networks.** Zeng D, Liu K, Chen Y, et al. EMNLP2015. [paper](http://www.aclweb.org/anthology/D15-1203)