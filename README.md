# fcpebasic
## 描述
&emsp;&emsp; **fcpebasic(my function componets extension)**,是在linux上用c语言实现的一系列API。 在Linux c开发的过程中，由于基础库的缺少，大部分的程序员都在重复造着轮子，又费时，又费力。为了让linux上开发的程序员专注于业务的开发，因此有了此库的开发。此库中代码有些来源于其它开源软件，有的来源于网络，有的是作者来编写。 希望在平常的开发过程中，此库能给你带来帮助，同时也希望各位大牛能给积极提意见，让我们一起来完善它.<br/>

## 代码维护
__维护人员邮件地址__ yldfree@163.com <br/>
__github地址__ https://github.com/LidiYuan/fcpebasic.git <br/>  

## 代码健壮性
&emsp;&emsp; 作者当前使用了 __gtest+lcov+valgrind+cppcheck__ 来保证代码的健壮性，其中gtest是为了编写单元测试，lcov是为了代码覆盖率，valgrind是为了检测内存泄露，cppcheck是为了对代码进行静态检测。

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
安装的话可以使用 make install进行安装，默认会将libfcpebasic.so.1.0.1 libfcpebasic.a 安装到/usr/lib64/下面. 头文件安装到/usr/include/fcpebasic/下面


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
