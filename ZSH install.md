# 在CentOS上使用oh-my-zsh
### 使用root用户登录 or 切换至root用户操作

使用root用户登录，下面的操作基本都没有root的困扰，如果非root用户请切换至root用户操作。

### 1、查看系统当前的shell
```
echo $SHELL
```
返回结果如下：
```
/bin/bash
```
PS.默认的shell一般都是bash

### 2、查看bin下是否有zsh包
```
cat /etc/shells
```
返回结果如下：

/bin/sh
/bin/bash
/sbin/nologin
/bin/dash
/bin/tcsh
/bin/csh

PS.默认没有安装zsh

### 3、安装zsh包
```
yum -y install zsh
```
安装完成后查看shell列表：
```
cat /etc/shells
```
返回结果如下：

/bin/sh
/bin/bash
/sbin/nologin
/bin/dash
/bin/tcsh
/bin/csh
/bin/zsh

现在zsh已经安装完成了，需要把系统默认的shell由bash切换为zsh

### 3、切换shell至zsh，代码如下：
```
chsh -s /bin/zsh
```
chsh用法请自行查找，返回结果如下：
```
Changing shell for root.
Shell changed.
```
按提示所述，shell已经更改为zsh了，现在查看一下系统当前使用的shell，
```
echo $SHELL
```
返回结果如下：
```
/bin/bash
```
看样子还没切换过来，需要重启一下服务器，我的习惯做法是在ECS的web管理平台重启，reboot到底好不好使还没试过，大家可以试试
重启过后，使用代码查看当前使用的shell
```
echo $SHELL
```
返回结果：
```
/bin/zsh
```
得到如此结果，证明shell已经切换成功了。

下面开始安装oh-my-zsh
oh-my-zsh源码是放在github上的，所以先要安装git

### 4、安装git：
```
yum -y install git
```
### 5、安装oh-my-zsh:
```
wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh
```

如果显示如下界面表示成功：
```
         __                                     __   
  ____  / /_     ____ ___  __  __   ____  _____/ /_  
 / __ \/ __ \   / __ `__ \/ / / /  /_  / / ___/ __ \ 
/ /_/ / / / /  / / / / / / /_/ /    / /_(__  ) / / / 
\____/_/ /_/  /_/ /_/ /_/\__, /    /___/____/_/ /_/  
                        /____/                       ....is now installed!
Please look over the ~/.zshrc file to select plugins, themes, and options.

p.s. Follow us at https://twitter.com/ohmyzsh.

p.p.s. Get stickers and t-shirts at http://shop.planetargon.com.
```
如果添加插件、更改themes请修改~/.zshrc或自行查询其它资料。

### 至此，zsh安装完毕，
#### 开始享受oh-my-zsh吧，如果执行命令时提示warning: cannot set LC_CTYPE locale可用以下方法解决：

修改profile：
```
vi /etc/profile
```

在profile末尾添加以下代码：
```
export LC_ALL=en_US.UTF-8
export LC_CTYPE=en_US.UTF-8
```
 
引用更改后的profile：
```
source /etc/profile
```
此时bash已切换至zsh。
