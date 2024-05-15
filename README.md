# fcpebasic
## 描述
&emsp;&emsp; **fcpebasic(my function componets extension)**,是在linux上用c语言实现的一系列API。 在Linux c开发的过程中，由于基础库的缺少，大部分的程序员都在重复造着轮子，又费时，又费力。为了让linux上开发的程序员专注于业务的开发，因此有了此库的开发。此库中代码有些来源于其它开源软件，有的来源于网络，有的是作者来编写。 希望在平常的开发过程中，此库能给你带来帮助，同时也希望各位大牛能给积极提意见，让我们一起来完善它.<br/>

## 代码维护
__维护人员邮件地址__ yldfree@163.com <br/>
__github地址__ https://github.com/LidiYuan/fcpebasic.git <br/>  

## 代码健壮性
&emsp;&emsp; 作者当前使用了 __gtest+lcov+valgrind+cppcheck__ 来保证代码的健壮性，其中gtest是为了编写单元测试，lcov是为了代码覆盖率，valgrind是为了检测内存泄露，cppcheck是为了对代码进行静态检测。

__依赖的软件安装__
```
yum install gtest gtest-devel
yum install valgrind lcov xmlstarlet httpd
```
__代码覆盖率的检测__ <br/>
代码覆盖率检测需要用到httpd软件.<br/>
```
service httpd start
service iptables stop
setenforce 0
1)需要启动httpd服务，并且文档目录为/var/www/html/
2)设置seliux 禁止
3)测试覆盖率查看的网址为 http://ip地址/results/index.html
```
__添加一个测试用例__
```
1) 添加一个测试模块(如果不存在) 比如要测试的测试模块为fcpe_bytes
1.1 运行runtest.sh  add_tmodule  mname=fcpe_bytes
   注意此处的mname不能为空 并且在../中存在 fcpe_bytes.c这个文件, 即测试模块名在../中有对应的 模块名.c 文件
   运行完则会在当前目录生成 fcpe_bytes目录。并且testsuit.xml 也被修改

1.2 添加一个测试套件(即测试函数)
   运行 runtest.sh  add_suit mname=fcpe_bytes suit=fcpebytes_add
   注意 mname和 suit参数不能为空， 并且测试模块必须是已经存在的，如果不存在则需要先看1.1添加测试模块
   注意 suit 必须是../fcpe_bytes.c中的一个函数(约定 不会强制做检查)
   运行完后会在 ./fcpe_bytes/目录下生成test_fcpebytes_add.cc文件  后续的测试案例需要卸载此函数中(自己手动写)
   运行完后会自动修改testsuit.xml 在对应的testmodule[name=fcpe_bytes]下添加 <testsuit name="fcpebytes_add"/>

1.3 修改fcpebasic_cc.h
 将测试模块的头文件加入到此文件中
 #include "fcpebasic/fcpe_bytes.h"
```

## 代码依赖
&emsp;&emsp; 代码不会依赖任何其它的代码，但是编译的时候会依赖fcpeaux(辅助用的一些列脚本)中的脚本。如果想正确编译此代码，需要先下载fcpeaux工程到本地,并且将fcpeaux和fcpebasic放在同一个目录下面。

## 代码编译
将fcpeaux和fcpebasic工程下载到同一个目录下面，然后执行如下。
```
cd fcpebasic
make all
```
make支持的选项如下。
```
Usage ...
  all                        #Compile the project
     DISABLE_STATIC=yes/no   #Static libraries are not compiled, default is no.
     DISABLE_SHARED=yes/no   #Shared libraries are not compiled, default is no.
     DISABLE_DEBUG=yes/no    #Disable compile debug version, default is no.
     PREFIX=xx               #Install the project to PREFIX
  clean                      #Clear this project
  depend                     #Establish a header file dependency
  strip                      #Strip symbols
  check                      #Use cppcheck check c code.
     CHECK_SRC=xx.c          #Set the source code file for detection
  install                    #Install this project
  uninstall                  #Uninstall this project
  output                     #Output CLFAGS info
```
可以使用 make install进行安装，默认会将libfcpebasic.so.1.0.1 libfcpebasic.a 安装到/usr/lib64/下面. 头文件安装到/usr/include/fcpebasic/下面


## 功能API
### [fcpekv](doc/fcpekv.md "click to jump")
key,value相关操作的API介绍

### [fcpecstr](doc/fcpecstr.md "click to jump")
c语言字符串相关操作的API介绍

### [fcpestr](doc/fcpestr.md "click to jump")
封装字符串相关操作的API介绍

### [fcpetime](doc/fcpetime.md "click to jump")
时间相关操作的API介绍

### [fcpeip](doc/fcpeip.md "click to jump")
IP相关操作的API介绍

### [fcpenet](doc/fcpenet.md "click to jump")
网络相关操作的API介绍

### [fcpefile](doc/fcpefile.md "click to jump")
文件相关操作的API介绍

### [fcpefd](doc/fcpefd.md "click to jump")
文件描述符相关操作的API介绍
