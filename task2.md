# 1.划分数据集
参照了这位同学的笔记https://github.com/songty21110133/OpenMMLabCamp/tree/master/task2
```
import splitfolders
splitfolders.ratio(input='/root/autodl-tmp/MMPretrain/fruit30', output='/root/autodl-tmp/MMPretrain/fruit30_splited', seed=1337, ratio=(0.8, 0.2))

chinese2english = {
    '菠萝':'pineapple',
    '草莓':'strawberry',
    '车厘子':'cherry',
    '桂圆':'longan',
    '哈密瓜':'hami-melon',
    '胡萝卜':'carrot',
    '黄瓜':'cucumber',
    '火龙果':'pitaya',
    '苦瓜':'balsam-pear',
    '梨':'pear',
    '荔枝':'litchi',
    '榴莲':'durian',
    '芒果':'mango',
    '猕猴桃':'kiwifruit',
    '柠檬':'lemon',
    '苹果-红':'red-apple',
    '苹果-青':'green-apple',
    '葡萄-白':'white-grape',
    '葡萄-红':'red-grape',
    '脐橙':'navel-orange',
    '砂糖橘':'sugar-orange',
    '山竹':'mangosteen',
    '圣女果':'cherry-tomato',
    '石榴':'pomegranate',
    '西瓜':'watermelon',
    '西红柿':'tomato',
    '香蕉':'banana',
    '杨梅':'red-bayberry',
    '椰子':'coconut',
    '柚子':'grapefruit',
}

import os
def myrename(path):
    file_list=os.listdir(path)
    for fi in file_list:
        old_name=os.path.join(path,fi)
        new_name=os.path.join(path,chinese2english[str(fi)])
        os.rename(old_name,new_name)
       
myrename('/content/drive/MyDrive/Colab Notebooks/mmpretrain/data/fruit30_splited/train')#将中文文件夹改为英文
myrename('/content/drive/MyDrive/Colab Notebooks/mmpretrain/data/fruit30_splited/val')
```
 # 2.按照 MMPreTrain CustomDataset 格式组织训练集和验证集
 ```
 # dataset settings
dataset_type = 'CustomDataset'
data_preprocessor = dict(
    num_classes=30,
    # RGB format normalization parameters
    mean=[123.675, 116.28, 103.53],
    std=[58.395, 57.12, 57.375],
    # convert image from BGR to RGB
    to_rgb=True,
)

train_pipeline = [
    dict(type='LoadImageFromFile'),
    dict(type='RandomResizedCrop', scale=224),
    dict(type='RandomFlip', prob=0.5, direction='horizontal'),
    dict(type='PackInputs'),
]

test_pipeline = [
    dict(type='LoadImageFromFile'),
    dict(type='ResizeEdge', scale=256, edge='short'),
    dict(type='CenterCrop', crop_size=224),
    dict(type='PackInputs'),
]

train_dataloader = dict(
    batch_size=64,
    num_workers=2,
    dataset=dict(
        type=dataset_type,
        data_root='data/fruit30_splited/train',
        pipeline=train_pipeline),
    sampler=dict(type='DefaultSampler', shuffle=True),
)

val_dataloader = dict(
    batch_size=64,
    num_workers=2,
    dataset=dict(
        type=dataset_type,
        data_root='data/fruit30_splited/val',
        pipeline=test_pipeline),
    sampler=dict(type='DefaultSampler', shuffle=False),
        sampler=dict(type='DefaultSampler', shuffle=False),
)
val_evaluator = dict(type='Accuracy', topk=(1, 5))
```
# 3.使用 MMPreTrain 算法库，编写配置文件，正确加载预训练模型
此处主要注意改写好各处的num_classes，使其等于我们自己数据的种类数量，并添加预训练权重
```
model = dict(
    type='ImageClassifier',
    backbone=dict(
        type='ResNet',
        depth=50,
        num_stages=4,
        out_indices=(3, ),
        style='pytorch'),
    neck=dict(type='GlobalAveragePooling'),
    head=dict(
        type='LinearClsHead',
        num_classes=30,
        in_channels=2048,
        loss=dict(type='CrossEntropyLoss', loss_weight=1.0),
        topk=(1, 5),
    ),
    init_cfg=dict(type="Pretrained",checkpoint="https://download.openmmlab.com/mmclassification/v0/resnet/resnet50_8xb32_in1k_20210831-ea4938fc.pth")#此处为初始添加的预训练权重
)
```
# 4.在水果数据集上进行微调训练
`mim train mmpretrain resnet50_8xb32_mydataset.py` 

***mmengine - INFO - Epoch(test) [14/14]    accuracy/top1: 92.4550  accuracy/top5: 99.4369  data_time: 0.0884  time: 0.3905***
# 5.使用 MMPreTrain 的 ImageClassificationInferencer 接口，对网络水果图像，或自己拍摄的水果图像，使用训练好的模型进行分类
图片上传探索中，后续上传
