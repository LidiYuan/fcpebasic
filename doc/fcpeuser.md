# fcpepuser
## 头文件
#include  "fcpebasic/fcpe_user.h"

## API介绍
### fcpeuser_info()

__函数原型__ <br/>
获取某个用户的各种相关信息。 <br/>
```
int fcpeuser_info(fcpemap *usermap,const char *user,const char *keystr)
```
__数介绍__ <br/>
|参数名|类型|说明|
|:--:|--|--|
|usermap|fcpemap *|返回一个map，存储获得的进程信息|
|usr|const char*|要查找的用户名|
|keystr|const char  *|要获得的用户信息key字符串，每个key间用 , 号分割。|

__支持的key字符串__ <br/>
|key字符串|说明|
|:--:|--|
|passwd|加密的密码|
|uid|用户uid|
|gid|用户uid|
|homedir|用户的家目录|
|shell|用户使用的shell|

__返回值__ <br/>
|返回类型|成功|失败|备注|
|:---|:---|:---|:---|
|int|成功返回0|失败返回<0<br/>用fcpeerror_str(ret)获得错误描述|无|

__注意__ <br/>
 1) 最后需要使用fcpemap_free()释放 map
 
__例子__ <br/>
```
void test()
{
    char *vstr = NULL;
    fcpemap mymap = NULL;

    fcpeuser_info(&mymap,"root","passwd,uid,gid,homedir,shell");

    FCPEMAP_IF_FIND_SUCCESS(mymap,"passwd",vstr)
    {
        if(NULL == vstr)
        {
            printf("passwd=""\n");
        }
        else
        {
            printf("passwd=%s\n",vstr);

        }
    }

    FCPEMAP_IF_FIND_SUCCESS(mymap,"uid",vstr)
    {
        printf("uid=%s\n",vstr);
    }

    FCPEMAP_IF_FIND_SUCCESS(mymap,"gid",vstr)
    {
        printf("gid=%s\n",vstr);
    }

    FCPEMAP_IF_FIND_SUCCESS(mymap,"homedir",vstr)
    {
        printf("homedir=%s\n",vstr);
    }

    FCPEMAP_IF_FIND_SUCCESS(mymap,"shell",vstr)
    {
        printf("shell=%s\n",vstr);
    }

    fcpemap_free(mymap);

    return;
}
```
