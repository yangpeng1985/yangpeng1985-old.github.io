---
title: 使用pyenv配合virutalenv安装和管理多个python版本
layout: post
---

注： 这是一篇老文章，写于2019年12月29日

<div class="ez-toc-v2_0_66_1 counter-hierarchy ez-toc-counter ez-toc-grey ez-toc-container-direction" id="ez-toc-container"><div class="ez-toc-title-container">目录

<span class="ez-toc-title-toggle">[<span class="ez-toc-js-icon-con"><span class=""><span class="eztoc-hide" style="display:none;">Toggle</span><span class="ez-toc-icon-toggle-span"><svg class="list-377408" fill="none" height="20px" style="fill: #999;color:#999" viewbox="0 0 24 24" width="20px" xmlns="http://www.w3.org/2000/svg"><path d="M6 6H4v2h2V6zm14 0H8v2h12V6zM4 11h2v2H4v-2zm16 0H8v2h12v-2zM4 16h2v2H4v-2zm16 0H8v2h12v-2z" fill="currentColor"></path></svg><svg baseprofile="tiny" class="arrow-unsorted-368013" height="10px" style="fill: #999;color:#999" version="1.2" viewbox="0 0 24 24" width="10px" xmlns="http://www.w3.org/2000/svg"><path d="M18.2 9.3l-6.2-6.3-6.2 6.3c-.2.2-.3.4-.3.7s.1.5.3.7c.2.2.4.3.7.3h11c.3 0 .5-.1.7-.3.2-.2.3-.5.3-.7s-.1-.5-.3-.7zM5.8 14.7l6.2 6.3 6.2-6.3c.2-.2.3-.5.3-.7s-.1-.5-.3-.7c-.2-.2-.4-.3-.7-.3h-11c-.3 0-.5.1-.7.3-.2.2-.3.5-.3.7s.1.5.3.7z"></path></svg></span></span></span>](#)</span></div><nav>- [Best way to run python 3.7 on Ubuntu 16.04 which comes with python 3.5](http://thinknotes.cn/2024/03/02/install-pyenv-in-ubuntu/#Best_way_to_run_python_37_on_Ubuntu_1604_which_comes_with_python_35 "Best way to run python 3.7 on Ubuntu 16.04 which comes with python 3.5")
- [ubuntu 16.04上安装配置pyenv](http://thinknotes.cn/2024/03/02/install-pyenv-in-ubuntu/#ubuntu_1604%E4%B8%8A%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AEpyenv "ubuntu 16.04上安装配置pyenv")
  - [准备工作：](http://thinknotes.cn/2024/03/02/install-pyenv-in-ubuntu/#%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C%EF%BC%9A "准备工作：")
  - [开始安装配置：](http://thinknotes.cn/2024/03/02/install-pyenv-in-ubuntu/#%E5%BC%80%E5%A7%8B%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AE%EF%BC%9A "开始安装配置：")
- [pyenv 结合 virtualenv 创建虚拟环境](http://thinknotes.cn/2024/03/02/install-pyenv-in-ubuntu/#pyenv_%E7%BB%93%E5%90%88_virtualenv_%E5%88%9B%E5%BB%BA%E8%99%9A%E6%8B%9F%E7%8E%AF%E5%A2%83 "pyenv 结合 virtualenv 创建虚拟环境")
- [pyenv 常用的命令说明](http://thinknotes.cn/2024/03/02/install-pyenv-in-ubuntu/#pyenv_%E5%B8%B8%E7%94%A8%E7%9A%84%E5%91%BD%E4%BB%A4%E8%AF%B4%E6%98%8E "pyenv 常用的命令说明")
  - [python 配置](http://thinknotes.cn/2024/03/02/install-pyenv-in-ubuntu/#python_%E9%85%8D%E7%BD%AE "python 配置")
  - [python 切换](http://thinknotes.cn/2024/03/02/install-pyenv-in-ubuntu/#python_%E5%88%87%E6%8D%A2 "python 切换")
  - [python 优先级](http://thinknotes.cn/2024/03/02/install-pyenv-in-ubuntu/#python_%E4%BC%98%E5%85%88%E7%BA%A7 "python 优先级")
  - [pyenv 插件: pyenv-virtualenv](http://thinknotes.cn/2024/03/02/install-pyenv-in-ubuntu/#pyenv_%E6%8F%92%E4%BB%B6_pyenv-virtualenv "pyenv 插件: pyenv-virtualenv")
- [参考：](http://thinknotes.cn/2024/03/02/install-pyenv-in-ubuntu/#%E5%8F%82%E8%80%83%EF%BC%9A "参考：")
- [pyenv安装太慢？使用国内镜像解决](http://thinknotes.cn/2024/03/02/install-pyenv-in-ubuntu/#pyenv%E5%AE%89%E8%A3%85%E5%A4%AA%E6%85%A2%EF%BC%9F%E4%BD%BF%E7%94%A8%E5%9B%BD%E5%86%85%E9%95%9C%E5%83%8F%E8%A7%A3%E5%86%B3 "pyenv安装太慢？使用国内镜像解决")
  - [备忘: 因为没有提前安装必要的依赖包出现的报错](http://thinknotes.cn/2024/03/02/install-pyenv-in-ubuntu/#%E5%A4%87%E5%BF%98_%E5%9B%A0%E4%B8%BA%E6%B2%A1%E6%9C%89%E6%8F%90%E5%89%8D%E5%AE%89%E8%A3%85%E5%BF%85%E8%A6%81%E7%9A%84%E4%BE%9D%E8%B5%96%E5%8C%85%E5%87%BA%E7%8E%B0%E7%9A%84%E6%8A%A5%E9%94%99 "备忘: 因为没有提前安装必要的依赖包出现的报错")

</nav></div>## <span class="ez-toc-section" id="Best_way_to_run_python_37_on_Ubuntu_1604_which_comes_with_python_35"></span>Best way to run python 3.7 on Ubuntu 16.04 which comes with python 3.5<span class="ez-toc-section-end"></span>

> I would not recommend manually fiddling around with source code installations and paths. Use pyenv and save yourself the trouble.
> 
> All you have to do is:
> 
> ```
> Run the pyenv installer
> Follow the instructions
> Install the Python versions you need
> Choose which Python version you want to use for a given directory, or globally
> ```
> 
> For example, to install 3.7, check which versions are available:
> 
> pyenv install -l | grep 3.7
> 
> Then run:
> 
> pyenv install 3.7.1
> 
> Now, you can choose your Python version:
> 
> pyenv global 3.7.1
> 
> This switches your python to point to 3.7.1. If you want the system python, run:
> 
> pyenv global system
> 
> To check which Python versions are available, run pyenv versions.

## <span class="ez-toc-section" id="ubuntu_1604%E4%B8%8A%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AEpyenv"></span>ubuntu 16.04上安装配置pyenv<span class="ez-toc-section-end"></span>

### <span class="ez-toc-section" id="%E5%87%86%E5%A4%87%E5%B7%A5%E4%BD%9C%EF%BC%9A"></span>准备工作：<span class="ez-toc-section-end"></span>

1. 安装curl： sudo apt -y install curl
2. 安装pip，这里安装sudo apt -y install python3-pip，安装后需要执行pip3，使用别名实行输入pip执行pip3，添加alias pip='pip3'到~/.bashrc，为了在sudo到root时也生效，需要添加到/root/.bashrc中；然后执行source ~/.bashrc就会生效，Or you can make a link ln -s /usr/local/bin/pip3 /usr/local/bin/pip
3. ubuntu pyenv install python 3 缺很多包？ 需要先执行以下命令安装必要的包，否则会出现很多报错，我遇到的可以看后面备忘中的内容
  
  ```shell
  sudo apt-get install make build-essential libssl-dev zlib1g-dev
  sudo apt-get install libbz2-dev libreadline-dev libsqlite3-dev wget curl
  sudo apt-get install llvm libncurses5-dev libncursesw5-dev
  sudo apt-get update
  ```
4. pyenv太慢？手动下载pyenv install -v 3.7.3提示的安装包，放到~/.pyenv/cache这个目录下，再次执行pyenv install -v 3.7.3 ；网上查到的使用国内镜像解决pyenv安装太慢的方法，实际操作时，发现提供的国内镜像源访问不了

### <span class="ez-toc-section" id="%E5%BC%80%E5%A7%8B%E5%AE%89%E8%A3%85%E9%85%8D%E7%BD%AE%EF%BC%9A"></span>开始安装配置：<span class="ez-toc-section-end"></span>

1. 执行curl -L <https://raw.github.com/yyuu/pyenv-installer/master/bin/pyenv-installer> | bash自动安装配置pyenv,
2. 安装结束后会提示将以下内容添加到~/.bashrc
  
  ```shell
  export PATH="/home/dreamsn/.pyenv/bin:$PATH"
  eval "$(pyenv init -)"
  eval "$(pyenv virtualenv-init -)"
  ```
3. 执行source ~/.bashrc 或者 exec $SHELL 使配置生效

## <span class="ez-toc-section" id="pyenv_%E7%BB%93%E5%90%88_virtualenv_%E5%88%9B%E5%BB%BA%E8%99%9A%E6%8B%9F%E7%8E%AF%E5%A2%83"></span>pyenv 结合 virtualenv 创建虚拟环境<span class="ez-toc-section-end"></span>

> pyenv virtualenv 3.4.3 TEST
> 
> pyenv activate TEST
> 
> pyenv deactivate
> 
> pyenv uninstall TEST
> 
> For example, to install 3.7, check which versions are available:
> 
> pyenv install -l | grep 3.7
> 
> Then run:
> 
> pyenv install 3.7.1
> 
> Now, you can choose your Python version:
> 
> pyenv global 3.7.1
> 
> This switches your python to point to 3.7.1. If you want the system python, run:
> 
> pyenv global system
> 
> To check which Python versions are available, run pyenv versions.

以上是网上的指导，以下是具体操作：

```shell
pyenv install -l | grep 3.7
pyenv install 3.7.3
pyenv global 3.7.3
pyenv versions
pyenv virtualenv 3.7.3 my-virtual-env-3.7.3
pyenv virtualenvs
pyenv activate  my-virtual-env-3.7.3
```

命令解释：

1. 创建虚拟环境 $ pyenv virtualenv 2.7.10 my-virtual-env-2.7.10
2. 若不指定python 版本，会汇报认使用当前环境python版本。
3. 列出当前虚拟环境 pyenv virtualenvs
4. 激活虚拟环境 pyenv activate
5. 退出虚拟环境 pyenv deactivate
6. 删除虚拟环境 pyenv uninstall my-virtual-env

## <span class="ez-toc-section" id="pyenv_%E5%B8%B8%E7%94%A8%E7%9A%84%E5%91%BD%E4%BB%A4%E8%AF%B4%E6%98%8E"></span>pyenv 常用的命令说明<span class="ez-toc-section-end"></span>

> ```
> > 使用方式: pyenv  []
> >
> > 命令:
> > commands    查看所有命令
> > local       设置或显示本地的Python版本
> > global      设置或显示全局Python版本
> > shell       设置或显示shell指定的Python版本
> > install     安装指定Python版本
> > uninstall   卸载指定Python版本)
> > version     显示当前的Python版本及其本地路径
> > versions    查看所有已经安装的版本
> > which       显示安装路径
> 
> > pyenv
> > pyenv 1.2.8
> > Usage: pyenv <command> [<args>]
> >
> > Some useful pyenv commands are:
> > commands    List all available pyenv commands
> > local       Set or show the local application-specific Python version
> > global      Set or show the global Python version
> > shell       Set or show the shell-specific Python version
> > install     Install a Python version using python-build
> > uninstall   Uninstall a specific Python version
> > rehash      Rehash pyenv shims (run this after installing executables)
> > version     Show the current Python version and its origin
> > versions    List all Python versions available to pyenv
> > which       Display the full path to an executable
> > whence      List all Python versions that contain the given executable
> >
> > See `pyenv help <command>' for information on a specific command.
> > For full documentation, see: https://github.com/pyenv/pyenv#readme</command></args></command>
> ```

### <span class="ez-toc-section" id="python_%E9%85%8D%E7%BD%AE"></span>python 配置<span class="ez-toc-section-end"></span>

> pyenv versions -- 查看系统当前安装的python列表
> 
> pyenv install --list -- 查看可安装的版本
> 
> pyenv install -v 3.5.1 -- 安装python
> 
> pyenv uninstall 2.7.3 -- 卸载python
> 
> pyenv rehash -- 创建垫片路径（为所有已安装的可执行文件创建 shims，如：~/.pyenv/versions/*/bin/*，因此，每当你增删了 Python 版本或带有可执行文件的包（如 pip）以后，都应该执行一次本命令）

### <span class="ez-toc-section" id="python_%E5%88%87%E6%8D%A2"></span>python 切换<span class="ez-toc-section-end"></span>

> pyenv global 3.4.0 -- 设置全局的 Python 版本，通过将版本号写入 ~/.pyenv/version 文件的方式。
> 
> pyenv local 2.7.3 -- 设置面向程序的本地版本，通过将版本号写入当前目录下的 .python-version 文件的方式。通过这种方式设置的 Python 版本优先级较 global 高。
> 
> pyenv 会从当前目录开始向上逐级查找 .python-version 文件，直到根目录为止。若找不到，就用 global 版本。
> 
> pyenv shell pypy-2.2.1 -- 设置面向 shell 的 Python 版本，通过设置当前 shell 的 PYENV\_VERSION 环境变量的方式。这个版本的优先级比 local 和 global 都要高。--unset 参数可以用于取消当前 shell 设定的版本。  
> pyenv shell --unset

### <span class="ez-toc-section" id="python_%E4%BC%98%E5%85%88%E7%BA%A7"></span>python 优先级<span class="ez-toc-section-end"></span>

shell > local > global

### <span class="ez-toc-section" id="pyenv_%E6%8F%92%E4%BB%B6_pyenv-virtualenv"></span>pyenv 插件: pyenv-virtualenv<span class="ez-toc-section-end"></span>

使用自动安装 pyenv 后，它会自动安装部分插件，通过 pyenv-virtualenv 插件可以很好的和 virtualenv 结合：

```shell
[root@linux3311 ~]# cd .pyenv/plugins/
[root@linux3311 plugins]# ll
insgesamt 24
drwxr-xr-x. 4 root root 4096 19. Jun 05:17 pyenv-doctor
drwxr-xr-x. 5 root root 4096 19. Jun 05:18 pyenv-installer
drwxr-xr-x. 4 root root 4096 19. Jun 05:18 pyenv-update
drwxr-xr-x. 7 root root 4096 19. Jun 05:18 pyenv-virtualenv
drwxr-xr-x. 4 root root 4096 19. Jun 05:18 pyenv-which-ext
drwxr-xr-x. 5 root root 4096 19. Jun 05:17 python-build
```

使用 pyenv 来管理 python，使用 pyenv-virtualenv 插件来管理多版本 python 包。

此时，还需注意，当我们将项目运行的 env 环境部署到生产环境时，由于我们的python 包是依赖python 的，需要注意生产环境的python版本问题

## <span class="ez-toc-section" id="%E5%8F%82%E8%80%83%EF%BC%9A"></span>参考：<span class="ez-toc-section-end"></span>

- <https://www.daimafans.com/article/d15590909394550784-p1-o1.html>
- <https://yq.aliyun.com/articles/59243>
- <https://www.uedbox.com/post/9306/>
- <https://www.v2ex.com/t/420216>
- [https://blog.csdn.net/github\_35817521/article/details/53467610](https://blog.csdn.net/github_35817521/article/details/53467610)

## <span class="ez-toc-section" id="pyenv%E5%AE%89%E8%A3%85%E5%A4%AA%E6%85%A2%EF%BC%9F%E4%BD%BF%E7%94%A8%E5%9B%BD%E5%86%85%E9%95%9C%E5%83%8F%E8%A7%A3%E5%86%B3"></span>pyenv安装太慢？使用国内镜像解决<span class="ez-toc-section-end"></span>

参考链接： <https://www.uedbox.com/post/9306/>

```
pyenv 搜狐镜像源加速：http://mirrors.sohu.com/python/ 
下载需要的版本放到 ~/.pyenv/cache 文件夹下面
然后执行 pyenv install 版本号 安装对应的 python 版本
傻瓜式脚本如下，其中 v 表示要下载的版本号

v=3.6.5;wget http://mirrors.sohu.com/python/$v/Python-$v.tar.xz -P ~/.pyenv/cache/;pyenv install $v  
```

### <span class="ez-toc-section" id="%E5%A4%87%E5%BF%98_%E5%9B%A0%E4%B8%BA%E6%B2%A1%E6%9C%89%E6%8F%90%E5%89%8D%E5%AE%89%E8%A3%85%E5%BF%85%E8%A6%81%E7%9A%84%E4%BE%9D%E8%B5%96%E5%8C%85%E5%87%BA%E7%8E%B0%E7%9A%84%E6%8A%A5%E9%94%99"></span>备忘: 因为没有提前安装必要的依赖包出现的报错<span class="ez-toc-section-end"></span>

出现的报错（如果提前执行上面安装包的操作则不会出现以下问题）：  
使用pyenv install -v 3.7.3报错，如下：  
zipimport.ZipImportError: can't decompress data; zlib not available

需要执行 sudo apt install zlib1g-dev 安装缺失的包，注意：使用 sudo apt install zlib或者zlib-devel提示找不到包。 参考： <https://github.com/jiansoung/issues-list/issues/13>

再次报错： ModuleNotFoundError: No module named '\_ctypes'，执行sudo apt-get install libffi-dev尝试 参考： <https://stackoverflow.com/questions/27022373/python3-importerror-no-module-named-ctypes-when-using-value-from-module-mul>

再次出错：

WARNING: The Python bz2 extension was not compiled. Missing the bzip2 lib?  
WARNING: The Python readline extension was not compiled. Missing the GNU readline lib?  
ERROR: The Python ssl extension was not compiled. Missing the OpenSSL lib?