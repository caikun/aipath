
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
conda config --set show_channel_urls yes 

conda create -n py39 python=3.9

# CUDA 10.1
pip install torch==1.8.1+cu101 torchvision==0.9.1+cu101 torchaudio==0.8.1 -f https://download.pytorch.org/whl/torch_stable.html
https://blog.csdn.net/qq_40630902/article/details/118356845
https://pytorch.org/get-started/previous-versions/

import torch
print(torch.__version__)
print(torch.cuda.is_available())