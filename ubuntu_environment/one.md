#  ros2 使用和学习  

## 1. ros2 安装

https://blog.csdn.net/weixin_55944949/article/details/140373710?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522b31f866e2402c6fea74283889ab1ad7c%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=b31f866e2402c6fea74283889ab1ad7c&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-140373710-null-null.142^v102^control&utm_term=ros2%E5%AE%89%E8%A3%85%E6%95%99%E7%A8%8B&spm=1018.2226.3001.4187


使用小鱼ROS一键安装
**wget http://fishros.com/install -O fishros && . fishros**

下载rosdep（rosdep是用于安装ROS依赖包的工具）（rosdepc）

同样使用小鱼一键安装

报错： sudo pip3 install -i https://pypi.tuna.tsinghua.edu.cn/simple rosdepc

error: externally-managed-environment

× This environment is externally managed
╰─> To install Python packages system-wide, try apt install
    python3-xyz, where xyz is the package you are trying to
    install.
    
    If you wish to install a non-Debian-packaged Python package,
    create a virtual environment using python3 -m venv path/to/venv.
    Then use path/to/venv/bin/python and path/to/venv/bin/pip. Make
    sure you have python3-full installed.
    
    If you wish to install a non-Debian packaged Python application,
    it may be easiest to use pipx install xyz, which will manage a
    virtual environment for you. Make sure you have pipx installed.
    
    See /usr/share/doc/python3.12/README.venv for more information.

应该是ros2与anaconda冲突，创建虚拟环境，安装rosdepc

python3 -m venv ~/ros2_venv

source ~/ros2_venv/bin/activate

pip install rosdepc

rosdepc update

## 2. ros2 基础

 