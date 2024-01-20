# 安装Mindspore
> 版本配套参考： https://mindformers.readthedocs.io/zh-cn/latest/Version_Match.html
> 选择：MindFormers 0.8  MindSpore 2.2.0  CANN 7.0.RC.beta1: aarch64 x86_64


conda install mindspore=2.2.10 -c mindspore -c conda-forge

conda activate py39ms2.2

配置环境变量
如果昇腾AI处理器配套软件包没有安装在默认路径，安装好MindSpore之后，需要导出Runtime相关环境变量，下述命令中LOCAL_ASCEND=/usr/local/Ascend的/usr/local/Ascend表示配套软件包的安装路径，需注意将其改为配套软件包的实际安装路径。
```
# control log level. 0-DEBUG, 1-INFO, 2-WARNING, 3-ERROR, 4-CRITICAL, default level is WARNING.
export GLOG_v=2

# Conda environmental options
LOCAL_ASCEND=/usr/local/Ascend # the root directory of run package

# lib libraries that the run package depends on
export LD_LIBRARY_PATH=${LOCAL_ASCEND}/ascend-toolkit/latest/lib64:${LOCAL_ASCEND}/driver/lib64:${LOCAL_ASCEND}/ascend-toolkit/latest/opp/built-in/op_impl/ai_core/tbe/op_tiling:${LD_LIBRARY_PATH}

# Environment variables that must be configured
## TBE operator implementation tool path
export TBE_IMPL_PATH=${LOCAL_ASCEND}/ascend-toolkit/latest/opp/built-in/op_impl/ai_core/tbe
## OPP path
export ASCEND_OPP_PATH=${LOCAL_ASCEND}/ascend-toolkit/latest/opp
## AICPU path
export ASCEND_AICPU_PATH=${ASCEND_OPP_PATH}/..
## TBE operator compilation tool path
export PATH=${LOCAL_ASCEND}/ascend-toolkit/latest/compiler/ccec_compiler/bin/:${PATH}
## Python library that TBE implementation depends on
export PYTHONPATH=${TBE_IMPL_PATH}:${PYTHONPATH}
```

验证是否成功安装
方法一：
```
python -c "import mindspore;mindspore.set_context(device_target='Ascend');mindspore.run_check()"
```
如果输出：

MindSpore version: 版本号
The result of multiplication calculation is correct, MindSpore has been installed on platform [Ascend] successfully!
说明MindSpore安装成功了。

方法二：
```
import numpy as np
import mindspore as ms
import mindspore.ops as ops

ms.set_context(device_target="Ascend")
x = ms.Tensor(np.ones([1,3,3,4]).astype(np.float32))
y = ms.Tensor(np.ones([1,3,3,4]).astype(np.float32))
print(ops.add(x, y))
```
如果输出：

[[[[2. 2. 2. 2.]
   [2. 2. 2. 2.]
   [2. 2. 2. 2.]]

  [[2. 2. 2. 2.]
   [2. 2. 2. 2.]
   [2. 2. 2. 2.]]

  [[2. 2. 2. 2.]
   [2. 2. 2. 2.]
   [2. 2. 2. 2.]]]]
说明MindSpore安装成功了。

## 日常使用

激活环境
```
conda activate py39ms2.2
```

导入环境变量
```
#安装toolkit包时配置
. /usr/local/Ascend/ascend-toolkit/set_env.sh

# Mindspore环境变量
# control log level. 0-DEBUG, 1-INFO, 2-WARNING, 3-ERROR, 4-CRITICAL, default level is WARNING.
export GLOG_v=2

# Conda environmental options
LOCAL_ASCEND=/usr/local/Ascend # the root directory of run package

# lib libraries that the run package depends on
export LD_LIBRARY_PATH=${LOCAL_ASCEND}/ascend-toolkit/latest/lib64:${LOCAL_ASCEND}/driver/lib64:${LOCAL_ASCEND}/ascend-toolkit/latest/opp/built-in/op_impl/ai_core/tbe/op_tiling:${LD_LIBRARY_PATH}

# Environment variables that must be configured
## TBE operator implementation tool path
export TBE_IMPL_PATH=${LOCAL_ASCEND}/ascend-toolkit/latest/opp/built-in/op_impl/ai_core/tbe
## OPP path
export ASCEND_OPP_PATH=${LOCAL_ASCEND}/ascend-toolkit/latest/opp
## AICPU path
export ASCEND_AICPU_PATH=${ASCEND_OPP_PATH}/..
## TBE operator compilation tool path
export PATH=${LOCAL_ASCEND}/ascend-toolkit/latest/compiler/ccec_compiler/bin/:${PATH}
## Python library that TBE implementation depends on
export PYTHONPATH=${TBE_IMPL_PATH}:${PYTHONPATH}
```

> 用户也可以通过修改~/.bashrc文件方式设置永久环境变量，操作如下：
> 1.以运行用户在任意目录下执行vi ~/.bashrc命令，打开.bashrc文件，在文件最后一行后面添加上述内容。
> 2.执行:wq!命令保存文件并退出。
> 3.执行source ~/.bashrc命令使其立即生效。

# 安装MindFormers
> 参考 https://gitee.com/mindspore/mindformers