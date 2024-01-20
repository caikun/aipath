
# 安装操作系统
ubuntu20.04: https://mirrors.aliyun.com/oldubuntu-releases/releases/20.04/?spm=a2c6h.25603864.0.0.10eb7ff35r3X2f
安装指南: https://support.huawei.com/enterprise/zh/doc/EDOC1100258049/47513e18?idPath=23710424|251366513|22892968|252309113|250702818


# 安装驱动
> 参考：https://support.huawei.com/enterprise/zh/doc/EDOC1100349467/2645a51f?idPath=23710424|251366513|22892968|252764743

安装依赖
```
apt install -y make 
apt install -y dkms 
apt install -y gcc
apt install -y linux-header
```

以root用户登录服务器。
执行如下命令，创建运行用户。
```
groupadd HwHiAiUser
useradd -g HwHiAiUser -d /home/HwHiAiUser -m HwHiAiUser -s /bin/bash
```

执行如下命令，切换至root用户。
```
su - root
```

执行如下命令，进入软件包所在路径（如“/opt”）。
```
cd /opt
```

执行如下命令，增加软件包的可执行权限。
```
chmod +x Ascend-hdk-910-npu-driver_23.0.0_linux-aarch64.run 
```

执行如下命令，校验run安装包的一致性和完整性。
```
./Ascend-hdk-910-npu-driver_23.0.0_linux-aarch64.run  --check
```

若出现如下回显信息，表示软件包校验成功。
Verifying archive integrity...  100%   SHA256 checksums are OK. All good.

执行如下命令，完成驱动安装，软件包默认安装路径为“/usr/local/Ascend”。
```
./Ascend-hdk-910-npu-driver_23.0.0_linux-aarch64.run  --full
```

如果指定root用户为运行用户，则需要与--install-for-all参数配合使用，如下所示，该场景下权限控制可能存在安全风险。`--install-username=root --install-usergroup=root --install-for-all`

# 安装固件
> 参考：https://support.huawei.com/enterprise/zh/doc/EDOC1100349467/2645a51f?idPath=23710424|251366513|22892968|252764743


执行如下命令，切换至root用户。
```
su - root
```
执行如下命令，进入软件包所在路径（如“/opt”）。
```
cd /opt
```

执行如下命令，增加软件包的可执行权限。
```
chmod +x *.run
```

执行如下命令，校验run安装包的一致性和完整性。
```
./Ascend-hdk-910-npu-firmware_7.1.0.3.220.run --check
```

出现如下回显信息，表示软件包校验成功。

Verifying archive integrity...  100%   SHA256 checksums are OK. All good.

执行如下命令，完成安装。

```
./Ascend-hdk-910-npu-firmware_7.1.0.3.220.run  --full
```

若系统出现如下关键回显信息，表示固件安装成功，并根据提示信息决定是否立即重启系统。

Firmware package installed successfully!


执行如下命令，查看芯片固件版本号。
```
/usr/local/Ascend/driver/tools/upgrade-tool --device_index -1 --component -1 --version
```
若与固件软件包版本号一致，则说明安装成功。

# 安装CANN
> 参考: https://www.hiascend.com/document/detail/zh/CANNCommunityEdition/700alpha003/softwareinstall/instg/instg_000002.html


安装依赖
```
sudo apt-get install -y gcc g++ make cmake zlib1g zlib1g-dev openssl libsqlite3-dev libssl-dev libffi-dev unzip pciutils net-tools libblas-dev gfortran libblas3
```
检查系统是否安装满足版本要求的python开发环境（具体要求请参见依赖列表，此步骤以环境上需要使用python 3.7.x为例进行说明）。
执行命令python3 --version，如果返回信息满足python版本要求，则直接进入下一步。

否则可参考如下方式安装python3.7.5。

使用wget下载python3.7.5源码包，可以下载到安装环境的任意目录，命令为：
```
wget https://www.python.org/ftp/python/3.7.5/Python-3.7.5.tgz
```
进入下载后的目录，解压源码包，命令为：
```
tar -zxvf Python-3.7.5.tgz
```
进入解压后的文件夹，执行配置、编译和安装命令：
```
cd Python-3.7.5
./configure --prefix=/usr/local/python3.7.5 --enable-loadable-sqlite-extensions --enable-shared
make
make install
```
其中“--prefix”参数用于指定python安装路径，用户根据实际情况进行修改。“--enable-shared”参数用于编译出libpython3.7m.so.1.0动态库。“--enable-loadable-sqlite-extensions”参数用于加载libsqlite3-dev依赖。

本手册以--prefix=/usr/local/python3.7.5路径为例进行说明。执行配置、编译和安装命令后，安装包在/usr/local/python3.7.5路径，libpython3.7m.so.1.0动态库在/usr/local/python3.7.5/lib/libpython3.7m.so.1.0路径。

设置python3.7.5环境变量。
```
#用于设置python3.7.5库文件路径
export LD_LIBRARY_PATH=/usr/local/python3.7.5/lib:$LD_LIBRARY_PATH
#如果用户环境存在多个python3版本，则指定使用python3.7.5版本
export PATH=/usr/local/python3.7.5/bin:$PATH
```
通过以上export方式设置环境变量，该种方式设置的环境变量只在当前窗口有效。您也可以通过将以上命令写入~/.bashrc文件中，然后执行source ~/.bashrc命令，使上述环境变量永久生效。注意如果后续您有使用环境上其他python版本的需求，则不建议将以上命令写入到~/.bashrc文件中。

安装完成之后，执行如下命令查看安装版本，如果返回相关版本信息，则说明安装成功。
```
python3 --version
pip3 --version
```


安装前请先使用pip3 list命令检查是否安装相关依赖，若已经安装，则请跳过该步骤；若未安装，则安装命令如下
```
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

> 可以使用aliyun的源
> ```
> pip3 config set global.index-url http://mirrors.aliyun.com/pypi/simple
> pip3 config set install.trusted-host mirrors.aliyun.com
> ```

加对软件包的可执行权限。
chmod +x 软件包名.run
软件包名.run表示开发套件包Ascend-cann-toolkit_{version}_linux-{arch}.run，请根据实际包名进行替换。

执行如下命令校验软件包安装文件的一致性和完整性。
./软件包名.run --check
执行以下命令安装软件（以下命令支持--install-path=<path>等参数，具体参数说明请参见参数说明）。
./软件包名.run --install

用户需签署华为企业业务最终用户许可协议（EULA）后进入安装流程
```
#配置为英文
export LANG=en_US.UTF-8
```
安装完成后，若显示如下信息，则说明软件安装成功：
xxx install success
xxx表示安装的实际软件包名。

使用前要导入环境变量
```
Please make sure that the environment variables have been configured.
-  To take effect for all users, you can add "source /usr/local/Ascend/ascend-toolkit/set_env.sh" to /etc/profile.
-  To take effect for current user, you can exec command below: source /usr/local/Ascend/ascend-toolkit/set_env.sh or add "source /usr/local/Ascend/ascend-toolkit/set_env.sh" to ~/.bashrc.
```

# 安装Mindspore
> 版本配套参考： https://mindformers.readthedocs.io/zh-cn/latest/Version_Match.html
> 选择：MindFormers 0.8  MindSpore 2.2.0  CANN 7.0.RC.beta1: aarch64 x86_64


conda install mindspore=2.2.10 -c mindspore -c conda-forge