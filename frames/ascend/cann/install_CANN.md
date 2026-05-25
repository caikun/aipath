# 安装CANN

参考： 昇腾社区

### 安装python依赖

```
pip3 install attrs cython numpy==1.24.0 decorator sympy cffi pyyaml pathlib2 psutil protobuf==3.20 scipy
requests absl-py
```

> mkdir ~/.pip
>
> touch ~/.pip/pip.conf 
>
> cat  > ~/.pip/pip.conf << EOF
> [global]
> index-url = https://mirrors.huaweicloud.com/repository/pypi/simple
> trusted-host = mirrors.huaweicloud.com
> timeout = 120
> EOF

### 安装CANN

```
chmod +x Ascend-cann-toolkit_<version>_linux-<arch>.run
./Ascend-cann-toolkit_<version>_linux-<arch>.run --check
```

出现如下回显信息，表示软件包校验成功。

```
 Verifying archive integrity... 100% SHA256 checksums are OK. All good. 
```

##### 安装软件包。 

```
./Ascend-cann-toolkit__linux-.run --install
```

安装完成后，若显示如下信息，则说明软件安装成功：

```
 xxx install success 
```

> xxx表示安装的实际软件包名。 

配置环境变量，请根据set_env.sh的实际安装路径进行替换。

```
source /usr/local/Ascend/ascend-toolkit/set_env.sh 
```

> 永久生效：echo "source /usr/local/Ascend/ascend-toolkit/set_env.sh" >>  ~/.bashrc

##### 安装后检查。

执行如下命令查询CANN版本信息，查询结果与安装软件包的版本一致 时，则验证安装成功。

进入软件包安装信息文件目录，请用户根据实际安装路径替换。<arch>表示CPU 架构（aarch64或x86_64）。

```
 cd /usr/local/Ascend/ascend-toolkit/latest/<arch>-linux
```

执行以下命令获取版本信息。 

```
cat ascend_toolkit_install.info
```

#### 运行一个算子样例

下载samples

```
git clone https://gitee.com/ascend/samples.git
```

运行算子样例

```
cd samples/operator/ascendc/0_introduction/3_add_kernellaunch/AddKernelInvocationNeo
bash run.sh -r cpu
```

