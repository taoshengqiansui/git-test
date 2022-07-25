# Rstudio server 安装（centos8）

## R语言安装

### 第一步

```shell
第一部分
#https://www.cnblogs.com/1016391912pm/p/15266909.html
#https://www.jianshu.com/p/118baeab6362
wget https://mirrors.tuna.tsinghua.edu.cn/CRAN/src/base/R-4/R-4.0.4.tar.gz
tar -zxvf R-4.0.4.tar.gz
./configure --enable-R-shlib=yes --prefix=/disks/software/R-4.0.4
#注意后缀R-4.0.4
#报错：configure: error: PCRE2 library and headers are required, or use --with-pcre1 and PCRE >= 8.32 with UTF-8 support
# --enable-R-shlib：将 R 编译成 lib 模式，在此模式下，会生成 path-to-R/lib/libR.so 库

第二部分
#解决方法

wget https://ftp.pcre.org/pub/pcre/pcre-8.40.tar.gz --no-check-certificate
tar -zxvf pcre-8.40.tar.gz
cd pcre-8.40
./configure --prefix=/disks/software/pcre-8.4 --enable-utf8
make -j3 && make install
#报错后安装了这个包...
./configure --enable-R-shlib=yes --with-pcre1 --prefix=/disks/software/R-4.0.4
# 成功
make
make install
```

### 第二步

#https://blog.51cto.com/u_15069471/3331606（在安装R语言之后用上，即可能在第一步的第二部分之前用上）

### 第三步

```shell
#报错
Font T1/cmr/m/n/10=ecrm1000 at 10.0pt not loadable: Metric (TFM) file not fou
nd.
#解决方法
sudo yum install texlive 
```

```shell
#报错
compiling Tex file 'reshape.tex' failed with message: unable to run pdflatex on 'reshape.tex'
#解决
当前路径比如R-4.1.3这个路径名有问题，把R-4.1.3改成R或者其他不包含特殊符号的文件名，如果是这个问题的话注意要重新运行以下命令
./confiure
make
最后结果是虽然安装成功了，但是
R二进制文件在R路径下
而Rscript二进制文件在R-4.1.3路径下
```

```shell
此外，提前安装了rpm
yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm
yum install --skip-broken https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm
yum -y install R
yum -y --skip-broken install R#这种方法安装的R找不到
```

```
101  2022-03-19 16:00:48 tar -zxvf R-4.1.3.tar.gz
  102  2022-03-19 16:00:50 ll
  103  2022-03-19 16:00:53 cd R-4.1.3/
  104  2022-03-19 16:00:54 LL
  105  2022-03-19 16:01:01 ll
  106  2022-03-19 16:01:13 ./configure
  107  2022-03-19 16:01:19 make install
  108  2022-03-19 16:01:23 make install
  109  2022-03-19 16:01:28 ll
  110  2022-03-19 16:01:36 ./configure
  111  2022-03-19 16:02:47 yum -y install gcc
  112  2022-03-19 16:02:48 yum install glibc-headers
  113  2022-03-19 16:02:49 yum install gcc-c++
  114  2022-03-19 16:03:00 ./configure
  115  2022-03-19 16:04:31 yum install java-1.8.0-openjdk* -y
  116  2022-03-19 16:04:41 ./configure
  117  2022-03-19 16:06:43 yum install tex
  118  2022-03-19 16:07:59 ./configure
  119  2022-03-19 16:08:17 yum install texi2any
  120  2022-03-19 16:08:33 yum install texi2any
  121  2022-03-19 16:08:54 yum install firefox
  122  2022-03-19 16:09:18 ./configure
  123  2022-03-19 16:09:41 yum install  acroread
  124  2022-03-19 16:10:22 yum install texi2any
  125  2022-03-19 16:10:31 rpm install texi2any
  126  2022-03-19 16:10:35 ./configure
  127  2022-03-19 16:11:09 yum install java-1.8.0-openjdk-*
  128  2022-03-19 16:11:43 ./configure
  129  2022-03-19 16:12:08 yum install texi2dvi
  130  2022-03-19 16:12:38 yum install gcc-c++ -y
  131  2022-03-19 16:12:48 ./configure  --enable-R-shlib
  132  2022-03-19 16:13:07 yum install gcc-gfortran -y
  133  2022-03-19 16:13:19 ./configure  --enable-R-shlib
  134  2022-03-19 16:13:43 yum install readline-devel -y
  135  2022-03-19 16:13:53 ./configure  --enable-R-shlib
  136  2022-03-19 16:14:18 yum install libXt-devel -y
  137  2022-03-19 16:14:28 ./configure  --enable-R-shlib
  138  2022-03-19 16:14:41 yum install zlib-devel -y
  139  2022-03-19 16:14:52 ./configure  --enable-R-shlib
  140  2022-03-19 16:15:07 yum -y install bzip2-devel
  141  2022-03-19 16:15:12 ./configure  --enable-R-shlib
  142  2022-03-19 16:15:25 yum -y install xz-devel.x86_64
  143  2022-03-19 16:15:34 ./configure  --enable-R-shlib
  144  2022-03-19 16:15:46 yum install pcre-devel -y
  145  2022-03-19 16:15:54 ./configure  --enable-R-shlib
  146  2022-03-19 16:16:07 yum install curl curl-devel -y
  147  2022-03-19 16:16:12 ./configure  --enable-R-shlib
  148  2022-03-19 16:16:37 make
  149  2022-03-19 16:17:44 cd ..
  150  2022-03-19 16:17:46  wget https://ftp.pcre.org/pub/pcre/pcre-8.40.tar.gz --no-check-certificate
  151  2022-03-19 16:18:52 wget wget https://ftp.pcre.org/pub/pcre/pcre-8.44.tar.gz
  152  2022-03-19 16:18:54 wget https://ftp.pcre.org/pub/pcre/pcre-8.44.tar.gz
  153  2022-03-19 16:19:13 yum install pcre2
  154  2022-03-19 16:19:21 cd R-4.1.3/
  155  2022-03-19 16:19:36 ./configure  --enable-R-shlib
  156  2022-03-19 16:20:01 yum install pcre2
  157  2022-03-19 16:20:24 ./configure  --enable-R-shlib  --with-pcre1
  158  2022-03-19 16:22:20 wget http://mirrors.ctan.org/fonts/inconsolata.zip
  159  2022-03-19 16:22:33 unzip inconsolata.zip
  160  2022-03-19 16:22:48 cp -Rfp inconsolata/* /usr/share/texmf/
  161  2022-03-19 16:22:49 ll
  162  2022-03-19 16:22:56 make
  163  2022-03-19 16:46:45 sudo apt-get install libpng-dev
  164  2022-03-19 16:46:45 sudo apt-get install libjpeg-dev
  165  2022-03-19 16:46:45 sudo apt-get install libtiff-dev
  166  2022-03-19 16:46:45 sudo apt-get install libcairo-dev
  167  2022-03-19 16:47:13 sudo yum install libpng-dev
  168  2022-03-19 16:47:14 sudo yum install libjpeg-dev
  169  2022-03-19 16:47:15 sudo yum install libtiff-dev
  170  2022-03-19 16:47:16 sudo yum install libcairo-dev
```

## Rstudio server安装

```shell
#https://www.rstudio.com/products/rstudio/download-server/redhat-centos/
wget https://download2.rstudio.org/server/centos7/x86_64/rstudio-server-rhel-2022.02.0-443-x86_64.rpm
sudo yum install rstudio-server-rhel-2022.02.0-443-x86_64.rpm
#安全起见，不能用root登录Rstudio server，因而需要创建用户
user add
passwd user
...
然后
https://www.jianshu.com/p/d3509ff51e90
或者
https://www.jianshu.com/p/ffc86a580844

重启防火墙这步遇报错（sudo service iptables restart）

解决方法：https://blog.csdn.net/sinat_29821865/article/details/80982250或者https://stackoverflow.com/questions/24756240/how-can-i-use-iptables-on-centos-7

sudo rstudio-server verify-installation
遇报错libssl.so.10: cannot open shared object file: No such file or directoryl.so.10: cannot open shared object file: No such file or directory

解决方法
sudo yum install compat-openssl10

又遇到报错
TTY detected. Printing informational message about logging configuration. Logging configuration loaded from '/etc/rstudio/logging.conf'. Logging to '/var/log/rstudio/rstudio-server/rserver.log'.
2022-03-19T11:42:22.109151Z [rserver] ERROR Unable to determine real path of R script /usr/bin/R (system error 2 (No such file or directory)); LOGGED FROM: bool rstudio::core::r_util::{anonymous}::validateRScriptPath(const string&, std::string*) src/cpp/core/r_util/REnvironmentPosix.cpp:300
Unable to determine real path of R script /usr/bin/R (system error 2 (No such file or directory))

解决方法
https://stackoverflow.com/questions/62472855/rstudio-does-not-start-unable-to-determine-real-path-of-r-script-due-to-previo
sudo ln -s /software/R/bin/R /usr/bin/R
sudo ln -s /software/R/R-4.1.3/bin/Rscript /usr/bin/Rscript

继续报错
TTY detected. Printing informational message about logging configuration. Logging configuration loaded from '/etc/rstudio/logging.conf'. Logging to '/var/log/rstudio/rstudio-server/rserver.log'.
TTY detected. Printing informational message about logging configuration. Logging configuration loaded from '/etc/rstudio/logging.conf'. Logging to '/tmp/70cc-a0fd-e6aa-2472/.local/share/rstudio/log/rsession-rstudio-server.log'.
Error reading /etc/rstudio/rsession.conf: unrecognised option 'rsession-which-r'

随后把rsession-which-r这行删了




问题太多了

最后也是稀里糊涂解决的
https://zhuanlan.zhihu.com/p/419871924
https://www.jianshu.com/p/d3509ff51e90
https://www.jianshu.com/p/ffc86a580844
https://www.jianshu.com/p/44169741bd22
```

## 其他软件安装

```shell
#ssh登录后的提示设置
首先 /etc/ssh/sshd_conf配置文件里面PrintMotd 参数不能是no

/etc/issue   #登录前提示

/etc/motd   #登录后提示

ssh还可以修改/etc/ssh/sshd_config里Banner项所指示的文件
```

```shell
#内存监控工具
sudo yum install smem#https://mp.weixin.qq.com/s/02gosJ3SiejXcw1AJ4vxUA
sudo yum install htop

glances：更强大的 htop / top 代替者。

yum install -y lrzsz
sz/rz：交互式文件传输，在多重跳板机下传输文件非常好用，不用一级一级传输。

tmux：终端复用工具，替代screen、nohup。
```

```shell
groupadd groupA#创建用户组
usermod -a -G groupA user#将用户添加到用户组-a参数表示不退出用户本来的组
groups user或者cat /etc/group#查看用户所在的组
```

```shell
sudo yum install terminator
CTRL + ALT + T
CRTL + SHIFT + T，开新标签页
CRTL + SHIFT + E，垂直方向分屏
CRTL + SHIFT + O，水平方向分屏
`ALT + ↑ ↓ ← →`` 在同一个标签页中的各个分屏之间切换
CTRL + PAGEUP / PAGEDOWN 左右切换不同标签页
```

```shell
jupyter安装
pip install Jupyter#最好不用root用户
jupyter notebook --generate-config
pip install notebook
vi模式set hlsearch
```

```shell
vi主题配置
https://zhuanlan.zhihu.com/p/58188561
https://github.com/dracula/vim
https://draculatheme.com/vim
```

```shell
docker安装    

https://cloud.tencent.com/developer/article/1762098

https://mp.weixin.qq.com/s?__biz=MzAxMDkxODM1Ng==&mid=2247485854&idx=1&sn=a0f9cdd216a6b36e159185781043003f&scene=21#wechat_redirect
```

```
技巧
export PS1='\[\033[01;34m\]\t\[\033[01;32m\] \[\033[01;32m\]`pwd `\n$ \[\e[0m\]'
加到~/.bash_profile
source后有奇效
```

```shell
# 安装bd

wget -c http://git.what996.com/vigneshwaranr/bd/archive/refs/tags/v1.03.zip
echo 'alias bd=". bd -si"' >> ~/.bashrc
source ~/.bashrc
## 要启用区分大小写的目录名称匹配，请在别名中使用 -s 代替 -si：
## 来源：https://mp.weixin.qq.com/s/CO5b6mNLSx3Vre4d_PVlvQ
```
