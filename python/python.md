---
tags:
  - python
  - linux
create: 2024-01-09 14:24
---


# python 

python 升级 3.7 版本

```sh
wget https://www.python.org/ftp/python/3.7.9/Python-3.7.9.tgz
tar -zxvf Python-3.7.9.tgz

cd Python-3.7.9
./configure --prefix=/usr/local/src/python37
sudo make
sudo make install

ln -s /usr/local/src/python37/bin/python3.7 /usr/bin/python3.7
ln -s /usr/local/src/python37/bin/pip3.7 /usr/bin/pip3.7
```

## pip 

```sh 
pip3 install mycli # mysql 客户端
```

使用时，输入pip <command> [options] 形式的指令，即可执行相应的命令，并且，command 和 options 可以任意组合

```sh
pip install --help
pip uninstall  --help
```
通过使用==, >=, <=, >, < 来指定一个版本号,未指定版本号，将默认下载最新版本。
```sh 
pip install SomePackage              # 最新版本
pip install SomePackage==1.0.4       # 指定版本
pip install 'SomePackage>=1.0.4'     # 最小版本

```
指定 requirements.txt 文件

```sh
pip install -r requirements.txt
```

freeze 用于输出已安装的软件包，并以 requirements 文件的格式显示.

```sh 

pip freeze > requirements.txt

```

## Anaconda

下载  ： https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/Anaconda3-2024.10-1-Linux-x86_64.sh

常用命令： 

```shell
# 查看当前有哪些虚拟环境
conda env list
conda info --envs
# 创建一个环境
conda create -n vrviu python=3.9
# 激活虚拟环境
conda activate jupyter_venv

# 退出当前虚拟环境
conda deactivate
# 删除某个虚拟环境
	conda remove -n your_env_name --all 
#复制某个虚拟环境
conda create --name new_env_name --clone old_env_name
# 导致环境配置到文件，要先激活环境
conda env export > environment.yml
# 通知配置文件创建环境
	conda env create -f environment.yml

# 包管理

# 安装包
conda install [package] 
conda install xlrd=1.2.0 
pip install xlrd==1.2.0 
# 批量导出依赖包
conda list -e > requirements.txt
# 删除当前环境中的某个包
conda remove [package]
# 升级当前环境中的某个包
conda update [package]
# 升级所有包  
conda update --all
# 搜索包
conda search [package]

# 删除没有用的安装包
conda clean -p
# 删除tar包
conda clean -t
conda clean --tarballs
# 删除所有的安装包及cache
conda clean -y --all

# 镜像源管理

# 查看镜像源
conda config --show channels
# 添加镜像源
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free 
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
# 配置安装包时显示安装来源
conda config --set show_channel_urls yes
# 清除索引缓存，保证用的是镜像站提供的索引
conda clean -i
# 切换回默认源
conda config --remove-key channels
# 移除某个镜像源
conda config --remove channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
# 临时指定安装某个包使用的镜像源
pip install [package] -i https://pypi.tuna.tsinghua.edu.cn/simple/
pip install [package] -i http://pypi.douban.com/simple/ --trusted-host pypi.douban.com
```


conda 的安装：

京东时的环境

1、登录11.40.234.64 拷贝安装包

```sh
scp /export/servers/Anaconda3-5.2.0-Linux-x86_64.sh boss@10.187.20.67 /export/boss
scp /export/servers/anaconda3/lib/python3.6/site-packages/wq boss@10.187.20.67 /export/boss（wq依赖包）
```

2、安装到/export/server/anaconda3(需要修改使用用户admin)

```sh
 ./Anaconda3-5.2.0-Linux-x86_64.sh -p /export/servers/anaconda3
```

3、拷贝wq依赖包到宝目录(需要修改用户admin)

```sh
mv wq /export/servers/anaconda3/lib/python3.6/site-packages/
```

4、切换环境命令

```sh
. /export/servers/anaconda3/bin/activate
```


Anaconda windows 安装

conda 的使用 ： 《[如何用Conda优雅的管理Python环境](https://ckfanzhe.github.io/About_conda/)》


## uvx 

uvx：命令行工具，用于快速运行 Python 脚本。

### 安装

mac、linux 方式：
```sh 
curl -LsSf https://astral.sh/uv/install.sh | sh

# mac 
  brew install uv

uv -V
uv 0.7.21 (77c771c7f 2025-07-14)

```
windows 

```sh 
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

### 卸载

如果需要从系统中移除 uv，只需删除 uv 和 uvx 二进制文件：

```sh 
$ rm $HOME\.local\bin\uv
$ rm $HOME\.local\bin\uvx
```

### 资料

1 、[https://zhuanlan.zhihu.com/p/1888904532131575259](https://zhuanlan.zhihu.com/p/1888904532131575259)

2、[https://hellowac.github.io/uv-zh-cn/getting-started/installation/#shell](https://hellowac.github.io/uv-zh-cn/getting-started/installation/#shell)
