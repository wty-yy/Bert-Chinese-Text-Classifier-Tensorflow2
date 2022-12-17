# Bert-Chinese-Text-Classifier-Tensorflow2
## Tensorflow2 - 基于Bert的文本分类模型

中文商品评论分类，基于Bert模型，TensorFlow2.

### 环境

```
Python 3.9.x
TensorFlow 2.9.2
tqdm
numpy
matplotlib
pandas
```

### 中文商品数据集

使用由[jinhuakst](https://github.com/SophonPlus/ChineseNlpCorpus/commits?author=jinhuakst)整理的[ChineseNlpCorpus](https://github.com/SophonPlus/ChineseNlpCorpus)中的两个数据集，分别作为训练集与测试集：

1. [online_shopping_10_cats](https://github.com/SophonPlus/ChineseNlpCorpus/blob/master/datasets/online_shopping_10_cats/intro.ipynb)：10种类别，总共62773条数据，其中正向评论：31727条，负向评论：31046条.
2. [yf_amazon](https://github.com/SophonPlus/ChineseNlpCorpus/blob/master/datasets/yf_amazon/intro.ipynb)(亚马逊数据集)：总共有720万条评论，从中筛选出和上述十个类别中的商品评论，作为测试集.

该模型的输出包含评论的情感与分类两个，将第一个数据集进行3:1划分为训练集与验证集（由于每种类别的商品数目不同如下表，我还将每种类别的商品评论进行了补全到7500）：

|  类别  | 总数目 | 正例 | 负例 |
| :----: | :----: | :--: | :--: |
|  书籍  |  3851  | 2100 | 1751 |
|  平板  | 10000  | 5000 | 5000 |
|  手机  |  2323  | 1165 | 1158 |
|  水果  | 10000  | 5000 | 5000 |
| 洗发水 | 10000  | 5000 | 5000 |
| 热水器 |  574   | 474  | 100  |
|  蒙牛  |  2033  | 992  | 1041 |
|  衣服  | 10000  | 5000 | 5000 |
| 计算机 |  3992  | 1996 | 1996 |
|  酒店  | 10000  | 5000 | 5000 |

最终训练集与验证集大小为

| 数据集 | 数据量 |
| :----: | :----: |
| 训练集 | 75000  |
| 验证集 | 15691  |

### 模型搭建

Tensorflow中Bert模型分为两个部分，可以从Tensorflow-Hub中下载，链接为[bert_zh_preprocess](https://tfhub.dev/tensorflow/bert_zh_preprocess/3)和[bert_zh_L-12_H-768_A-12](https://tfhub.dev/tensorflow/bert_zh_L-12_H-768_A-12/4)，分别为预处理模型（句子分词和向量化）和bert模型.

模型导入方法我是将两个模型分别下载到本地的 `./model/bert_preprocessor `和`./model/bert_encoder`中，由于GitHub的上传文件大小限制，无法上传bert模型，只能够自己去下然后解压到这两个文件夹中.

