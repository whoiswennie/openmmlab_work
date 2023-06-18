# 安装配置MMagic
```python
# 安装Pytorch
!pip3 install install torch==1.10.1+cu113 torchvision==0.11.2+cu113 torchaudio==0.10.1+cu113 -f https://download.pytorch.org/whl/cu113/torch_stable.html
!pip3 install openmim
!mim install 'mmcv>=2.0.0'
!mim install 'mmengine'
!mim install 'mmagic'
!git clone https://github.com/open-mmlab/mmagic.git
import os
os.chdir('mmagic')
!pip3 install -e . -i https://pypi.tuna.tsinghua.edu.cn/simple
!pip install opencv-python pillow matplotlib seaborn tqdm -i https://pypi.tuna.tsinghua.edu.cn/simple
!pip install clip transformers gradio 'httpx[socks]' diffusers==0.14.0 -i https://pypi.tuna.tsinghua.edu.cn/simple
!mim install 'mmdet>=3.0.0'
```
# 文生图-Stable Diffusion
## https://github.com/open-mmlab/mmagic/tree/main/configs/stable_diffusion
```python
from mmagic.apis import MMagicInferencer
sd_inferencer = MMagicInferencer(model_name='stable_diffusion')
text_prompts = 'A panda is having dinner at KFC'
text_prompts = 'A Persian cat walking in the streets of New York'
sd_inferencer.infer(text=text_prompts, result_out_dir='output/sd_res.png')

```
![image](https://github.com/whoiswennie/openmmlab_work/assets/104626642/bfdfd273-bf85-41db-b841-30b6a6f04810)
![image](https://github.com/whoiswennie/openmmlab_work/assets/104626642/ae883542-101c-41dc-86cf-60cc5b5e3033)
# 关于lora训练，我准备了一些数据集用于微调Anything-V3.0的lora
<img width="467" alt="image" src="https://github.com/whoiswennie/openmmlab_work/assets/104626642/ce2773c1-3aa7-4bac-8f5e-e2022c3a9147">
<img width="468" alt="image" src="https://github.com/whoiswennie/openmmlab_work/assets/104626642/53a7fc86-7625-4aef-bd84-bbf9031b971a">
# 效果测试
<img width="468" alt="image" src="https://github.com/whoiswennie/openmmlab_work/assets/104626642/582ec61a-dd2a-494e-a00c-da1588f81bbd">

## 利用controlnet的canny边缘检测
## 原图
![image](https://github.com/whoiswennie/openmmlab_work/assets/104626642/200b4ba1-ae38-4618-9855-04fc7733aa3c)

``python
import cv2
import numpy as np
import mmcv
from mmengine import Config
from PIL import Image

from mmagic.registry import MODELS
from mmagic.utils import register_all_modules

register_all_modules()

cfg = Config.fromfile('../../configs/controlnet/controlnet-canny.py')
controlnet = MODELS.build(cfg.model).cuda()

control_img = mmcv.imread('edges.jpg')
control = cv2.Canny(control_img, 100, 200)
control = control[:, :, None]
control = np.concatenate([control] * 3, axis=2)
control = Image.fromarray(control)

prompt = 'Room with light light silver walls and a pale gold ceiling.'

output_dict = controlnet.infer(prompt, control=control)
samples = output_dict['samples']
for idx, sample in enumerate(samples):
    sample.save(f'sample_{idx}.png')
controls = output_dict['controls']
for idx, control in enumerate(controls):
    control.save(f'control_{idx}.png')
```

# 效果展示
![image](https://github.com/whoiswennie/openmmlab_work/assets/104626642/e7561b3a-0e4e-4283-8536-6c46c8992816)
![image](https://github.com/whoiswennie/openmmlab_work/assets/104626642/42518e94-c018-4259-a9a9-161a43566299)


