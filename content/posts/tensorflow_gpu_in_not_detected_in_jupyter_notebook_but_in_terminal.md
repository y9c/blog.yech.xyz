+++
title = "Tensorflow Gpu in Not Detected in Jupyter Notebook but in Terminal"
description = "非 root 用户安装 cuda/cudnn 环境后，通过修改 PATH 和 LD_LIBRARY_PATH 变量，可以使 tensorflow 成功识别调用 GPU。但是，运行 jupyterhub notebook 后发现 GPU 调用失败..."
featured_image = ""
date = 2020-10-30T16:43:50+08:00
categories = ["coding"]
tags = ["Tensorflow", "Python", "Linux"]
+++

首先，在 jupyter notebook 环境中运行以下命令，可以查看 tensorflow 识别出的硬件。

```python
import tensorflow as tf
tf.config.list_physical_devices()
```

看到输出结果中并未包含 GPU。但是在 terminal 环境的 Python
中运行相同的命令，看到的结果是包含 GPU 的。

_刚开始以为是 cuda 没安装正确，重新安装了一下，依然无法识别。_

接着运行以下命令查看 Python 识别到的系统环境变量，看到其中没有了自定义的
`LD_LIBRARY_PATH`。

```python
import os
print(os.environ)
```

~~初步猜测是 Jupyter notebook 运行是忽略了 `~/.zshrc` 中的配置。~~但是，可以看到
`PATH` 变量显示的是修改过的内容。

因此打算生成 jupyter 的配置文件（_命令如下_）后，强制指定 `LD_LIBRARY_PATH`。

```bash
jupyterhub notebook --generate-config
```

仔细阅读了下配置文件（jupyterhub_config.py），留意到其中有这么一段话：

```
## Whitelist of environment variables for the single-user server to inherit from
#  the JupyterHub process.
#
#  This whitelist is used to ensure that sensitive information in the JupyterHub
#  process's environment (such as `CONFIGPROXY_AUTH_TOKEN`) is not passed to the
#  single-user server's process.
#  Default: ['PATH', 'PYTHONPATH', 'CONDA_ROOT', 'CONDA_DEFAULT_ENV', 'VIRTUAL_ENV', 'LANG', 'LC_ALL']
# c.Spawner.env_keep = ['PATH', 'PYTHONPATH', 'CONDA_ROOT', 'CONDA_DEFAULT_ENV', 'VIRTUAL_ENV', 'LANG', 'LC_ALL']
```

推测原因出在这里，single -user 的 JupyterHub 会隐藏掉系统的环境变量，只留下
whitelist 中的这几个。

因此把 `LD_LIBRARY_PATH` 加入 .env_keep 列表，

```python
c.Spawner.env_keep = ['PATH', 'PYTHONPATH', 'CONDA_ROOT', 'CONDA_DEFAULT_ENV', 'VIRTUAL_ENV', 'LANG', 'LC_ALL', "LD_LIBRARY_PATH"]
```

关闭 notebook server 进程后，重新开启，经测试，tensorflow 终于识别出 GPU 了。

```bash
jupyterhub notebook -f ~/jupyterhub_config.py
```
