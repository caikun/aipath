## 昇腾开发常用命令

## 安装驱动和固件
确认操作系统和内核版本
```
uname -m && cat /etc/*release
uname -r
```


创建驱动运行用户HwHiAiUser（运行驱动进程的用户），安装驱动时无需指定运行用户，默认即为HwHiAiUser
```
groupadd HwHiAiUser
useradd -g HwHiAiUser -d /home/HwHiAiUser -m HwHiAiUser -s /bin/bash
```


驱动安装
```
./Ascend-hdk-310p-npu-driver_23.0.rc1_linux-aarch64.run --full  --install-for-all
```

固件安装
```
./Ascend-hdk-310p-npu-firmware_6.3.0.1.241.run --full
```

查看 pci设备
```
lspci
```

## 安装cann

![img](frequent_cmd.assets/zh-cn_image_0000001566253738.png)

参考：[cann官方手册](https://www.hiascend.com/document/detail/zh/CANNCommunityEdition/63RC2alpha003/softwareinstall/instg/instg_000002.html)

安装依赖
```
sudo apt-get install -y gcc g++ make cmake zlib1g zlib1g-dev openssl libsqlite3-dev libssl-dev libffi-dev unzip pciutils net-tools libblas-dev gfortran libblas3
```

安装Python
```
wget https://www.python.org/ftp/python/3.7.5/Python-3.7.5.tgz

tar -zxvf Python-3.7.5.tgz

cd Python-3.7.5
./configure --prefix=/usr/local/python3.7.5 --enable-loadable-sqlite-extensions --enable-shared
make
sudo make install
```

导入环境变量
```
#用于设置python3.7.5库文件路径
export LD_LIBRARY_PATH=/usr/local/python3.7.5/lib:$LD_LIBRARY_PATH
#如果用户环境存在多个python3版本，则指定使用python3.7.5版本
export PATH=/usr/local/python3.7.5/bin:$PATH
```
可以通过将以上命令写入~/.bashrc文件中，然后执行source ~/.bashrc命令，使上述环境变量永久生效。注意如果后续您有使用环境上其他python版本的需求，则不建议将以上命令写入到~/.bashrc文件中。

安装pip依赖
```
pip3 install --upgrade pip
pip3 install attrs
pip3 install numpy
pip3 install decorator
pip3 install sympy
pip3 install cffi
pip3 install pyyaml
pip3 install pathlib2
pip3 install psutil
pip3 install protobuf
pip3 install scipy
pip3 install requests
pip3 install absl-py
```

安装cann-toolkit
```
./Ascend-cann-toolkit_6.3.RC1_linux-aarch64.run --install
```
