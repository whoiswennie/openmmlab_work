# openmmlab-mmpretrain
# 环境配置
## 进入上一次创建的虚拟环境openmmlab
## git clone https://github.com/open-mmlab/mmpretrain
## pip install openmim
## cd C:\Users\32873\Desktop\ai\openmmlab\mmpretrain\mmpretrain
## mim install -e ".[multimodal]"
# 创建水果项目文件夹，和下载水果数据集
## mkdir data
## cd data 
## tar -xf ~Downloads/fruit30_train.tar
## cd fruit30_train
#  split dataset 拆分数据集
## pip install split-folders
## splitfolders --output ../data/fruit30 --ratio 0.8 0.1 0.1 -- ../data/fruit30_train
# 下载config文件
## https://github.com/MetaFeature/MMlab_Works/blob/main/resnet50_fruit_classification.py
![image](https://github.com/whoiswennie/openmmlab_work/assets/104626642/977d0395-7774-490e-945f-324fc0f61c4c)
# 模型训练
## python tools/train.py projects/fruit30_Classification/resnet50_fruit_classification.py --work-dir=./exp
![image](https://github.com/whoiswennie/openmmlab_work/assets/104626642/4eddbf5c-230b-4df4-b2e5-3795cab8029a)
