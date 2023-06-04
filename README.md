# openmmlab_work
## 这是openmmlab的实战作业，感谢子豪兄提供的代码！！
##
我利用anaconda创建了3.8.16的python虚拟环境：openmmlab 作为本次课程的专用环境
# 安装 Pytorch以及openmmlab相关的环境
### !pip3 install install torch==1.10.1+cu113 torchvision==0.11.2+cu113 torchaudio==0.10.1+cu113 -f https://download.pytorch.org/whl/cu113/torch_stable.html
### !pip install -U openmim
### !mim install mmengine
### !mim install 'mmcv==2.0.0rc3'
### !mim install "mmdet>=3.0.0rc6"
### !pip install opencv-python pillow matplotlib seaborn tqdm pycocotools -i https://pypi.tuna.tsinghua.edu.cn/simple
### !git clone https://github.com/open-mmlab/mmpose.git -b tutorial2023
### !mim install -e .

# 跟着子豪的教程测试了一下检测图片和视频的效果
![multi-person](https://github.com/whoiswennie/openmmlab_work/assets/104626642/fc046571-1640-4ea0-a4e2-26a53e7962fc)
![image](https://github.com/whoiswennie/openmmlab_work/assets/104626642/e46e9022-aef1-4081-968a-b9194f71a4cc)
## 预训练模型的效果很不错

# 接着下载子豪标注的耳朵数据集对模型进行训练和模型评估
## 重新训练目标检测
### python tools/train.py data/rtmdet_tiny_ear.py
### python tools/test.py data/rtmdet_tiny_ear.py work_dirs/rtmdet_tiny_ear/epoch_200.pth
![LWZ9 3W9C $SN9$US32R42Q](https://github.com/whoiswennie/openmmlab_work/assets/104626642/147d8ead-bc67-4a7f-9c4b-5680de9c465a)
## 重新训练关键点检测
### python tools/train.py data/rtmpose-s-ear.py
### python tools/test.py data/rtmpose-s-ear.py work_dirs/rtmpose-s-ear/epoch_300.pth
![O`T%L(L25R _7M1OOL2IUX](https://github.com/whoiswennie/openmmlab_work/assets/104626642/742612a4-2fd2-44e0-929e-3b3bd14d2443)
# 我提供了自己拍摄的一段视频对训练后的模型进行检测
![image](https://github.com/whoiswennie/openmmlab_work/assets/104626642/389dba79-d97b-4a8c-aed7-3acdd339d692)
## 模型对耳朵的检测和关键点定位效果十分优秀
# 最后我提供我相关的训练数据以及检测结果供大家学习交流
