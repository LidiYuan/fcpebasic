# fcpeproc
## 头文件
#include  "fcpebasic/fcpe_proc.h"

## API介绍
### fcpeproc_info()

__函数原型__ <br/>
根据pid获得进程相关的各种信息。 <br/>
```
int fcpeproc_info(fcpemap *procmap,int pid,const char *keystrfmt,...)
```
__数介绍__ <br/>
|参数名|类型|说明|
|:--:|--|--|
|procmap|fcpemap *|返回一个map，存储获得的进程信息|
|pid|int|进程pid|
|keystrfmt|const char  *|要获得的进程信息key的格式化字符串，每个key间用 , 号分割。|
|...|可变参数|根据前面的key格式化字符串传入不同的参数|

__支持的key字符串__ <br/>
|key字符串|说明|
|:--:|--|
|name|进程名|
|state|进程状态， running,sleeping, disk sleep, stopped, tracing stop, "zombie, dead|
|uname|进程所属用户名|
|uid|进程所属用户uid|
|gname|进程所属的组名|
|gid|进程所属的组id|
|path|进程的路径|
|tracerpid|跟踪者进程的pid，记录谁在跟踪本进程(ptrace)，如果为0表示未被跟踪|
|threads|线程数|
|ppid|父进程的pid|
|rsspage_num| rss占用的物理页数, 0表示是内核线程，这是因为所有内核线程是共用内存空间的|
|rss|实际占用的物理内存，单位为KB|
|pgrp|进程组pid,0表示不存在组pid|
|session|会话pid,0表示不存在会话pid|
|ttynr|进程所属的终端号，0或-1表示未关联终端|
|ttyname|进程所属的终端名，根据终端号获得|
|cmdline|进程的命令行|
|fdsize|当前分配可使用的最大文件描述符数，在内核中文件描述符随着打开文件的数增多，会动态扩展可以使用的文件描述最大值，但不会超过/proc/sys/fs/nr_open中的值|

__返回值__ <br/>
|返回类型|成功|失败|备注|
|:---|:---|:---|:---|
|int|成功返回0|失败返回<0<br/>用fcpeerror_str(ret)获得错误描述|无|

__注意__ <br/>
 1) 最后需要使用fcpemap_free()释放 map
 
__例子__ <br/>
```
void test(void)
{
    char *value;		
    fcpemap mymap =NULL;

    fcpeproc_info(&mymap,getpid(),"name,path,state,uname,uid,gname,gid,threads,tracerpid,ppid,rsspage_num,pgrp,session,ttynr,rss,fdsize");
  
    FCPEMAP_IF_FIND_SUCCESS(mymap,"name",value)
    {
        printf("name=%s\n",value);
    }

    FCPEMAP_IF_FIND_SUCCESS(mymap,"state",value)
    {
        printf("state=%s\n",value);
    }  

    FCPEMAP_IF_FIND_SUCCESS(mymap,"uname",value)
    {
        printf("uname=%s\n",value);
    }  

	  FCPEMAP_IF_FIND_SUCCESS(mymap,"uid",value)
    {
        printf("uid=%s\n",value);
    }  

	  FCPEMAP_IF_FIND_SUCCESS(mymap,"gname",value)
    {
        printf("gname=%s\n",value);
    }  

	  FCPEMAP_IF_FIND_SUCCESS(mymap,"gid",value)
    {
        printf("gid=%s\n",value);
    } 

	  FCPEMAP_IF_FIND_SUCCESS(mymap,"path",value)
    {
        printf("path=%s\n",value);
    }  

	  FCPEMAP_IF_FIND_SUCCESS(mymap,"threads",value)
    {
        printf("threads=%s\n",value);
    }  

	  FCPEMAP_IF_FIND_SUCCESS(mymap,"ppid",value)
    {
        printf("ppid=%s\n",value);
    }  

    FCPEMAP_IF_FIND_SUCCESS(mymap,"tracerpid",value)
    {
        printf("tracerpid=%s\n",value);
    } 

    FCPEMAP_IF_FIND_SUCCESS(mymap,"rsspage_num",value)
    {
        printf("rsspage_num=%s\n",value);
    } 

    FCPEMAP_IF_FIND_SUCCESS(mymap,"pgrp",value)
    {
        printf("pgrp=%s\n",value);
    }  

    FCPEMAP_IF_FIND_SUCCESS(mymap,"session",value)
    {
        printf("session=%s\n",value);
    }

    FCPEMAP_IF_FIND_SUCCESS(mymap,"ttynr",value)
    {
        printf("ttynr=%s\n",value);
    }  

	  FCPEMAP_IF_FIND_SUCCESS(mymap,"rss",value)
    {
        printf("rss=%s KB\n",value);
    }
  
	  FCPEMAP_IF_FIND_SUCCESS(mymap,"fdsize",value)
    {
        printf("fdsize=%s\n",value);
    }  

    fcpemap_free(mymap);
}
```
______________________
