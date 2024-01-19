
# 安装操作系统
ubuntu20.04: https://mirrors.aliyun.com/oldubuntu-releases/releases/20.04/?spm=a2c6h.25603864.0.0.10eb7ff35r3X2f
安装指南: https://support.huawei.com/enterprise/zh/doc/EDOC1100258049/47513e18?idPath=23710424|251366513|22892968|252309113|250702818


# 安装驱动
> 参考：https://support.huawei.com/enterprise/zh/doc/EDOC1100349467/2645a51f?idPath=23710424|251366513|22892968|252764743

安装依赖
apt install -y make 
apt install -y dkms 
apt install -y gcc
apt install -y linux-header


以root用户登录服务器。
执行如下命令，创建运行用户。
groupadd HwHiAiUser
useradd -g HwHiAiUser -d /home/HwHiAiUser -m HwHiAiUser -s /bin/bash

执行如下命令，切换至root用户。
su - root

执行如下命令，进入软件包所在路径（如“/opt”）。
cd /opt

执行如下命令，增加软件包的可执行权限。
chmod +x Ascend-hdk-910-npu-driver_23.0.0_linux-aarch64.run 

执行如下命令，校验run安装包的一致性和完整性。
./Ascend-hdk-910-npu-driver_23.0.0_linux-aarch64.run  --check

若出现如下回显信息，表示软件包校验成功。
Verifying archive integrity...  100%   SHA256 checksums are OK. All good.

执行如下命令，完成驱动安装，软件包默认安装路径为“/usr/local/Ascend”。
./Ascend-hdk-910-npu-driver_23.0.0_linux-aarch64.run  --full

如果指定root用户为运行用户，则需要与--install-for-all参数配合使用，如下所示，该场景下权限控制可能存在安全风险。--install-username=root --install-usergroup=root --install-for-all

# 安装固件
> 参考：https://support.huawei.com/enterprise/zh/doc/EDOC1100349467/2645a51f?idPath=23710424|251366513|22892968|252764743


执行如下命令，切换至root用户。
su - root

执行如下命令，进入软件包所在路径（如“/opt”）。
cd /opt

执行如下命令，增加软件包的可执行权限。
chmod +x *.run

执行如下命令，校验run安装包的一致性和完整性。
./Ascend-hdk-910-npu-firmware_7.1.0.3.220.run --check

出现如下回显信息，表示软件包校验成功。
Verifying archive integrity...  100%   SHA256 checksums are OK. All good.

执行如下命令，完成安装。
./Ascend-hdk-910-npu-firmware_7.1.0.3.220.run  --full

若系统出现如下关键回显信息，表示固件安装成功，并根据提示信息决定是否立即重启系统。

Firmware package installed successfully!

执行如下命令，查看芯片固件版本号。
/usr/local/Ascend/driver/tools/upgrade-tool --device_index -1 --component -1 --version

若与固件软件包版本号一致，则说明安装成功。