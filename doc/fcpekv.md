# fcpekv
## 头文件
#include  "fcpe_kv.h"

## API介绍
### fcpekv_parse()

__函数原型__ <br/>
根据指定的字符串(key=value)类型，解析出key和value. <br/>
```
void fcpekv_parse(char *cstr,char **key,char **value)
```
__数介绍__ <br/>
|参数名|类型|说明|
|:--:|--|--|
|cstr|char * <br/> 1)表示"key=value"类型的字符串.<br/>2)不能是常量字符串|此字符串会被修改(不能传入常量字符串).|
|key|char **|1)用于返回解析到的key,如果为空则不返回key.<br/>2)返回结果不需要释放.|
|value|char **|1)用于返回解析到的value,如果为空则不返回value.<br/>2)返回结果不需要释放|

__返回值__ <br/>
|返回类型|成功|失败|备注|
|:---|:---|:---|:---|

__注意__ <br/>
  1) 传入的cstr不能是常量，否则将引起异常.<br/>
  2) 传入的cstr必须是"key=value" 类型.并且会以最右边的'='作为分隔符.<br/>
  3) 解析出的key和value不会自动去除空白(如果存在).<br/>
  
__例子__ <br/>
```
void test(void)
{
    char *keytmp;
    char *valuetmp;
    char mystr[]={"key1=value1"};

    //mystr不能是常量
    fcpekv_parse(mystr,&keytmp,&valuetmp);

    printf("%s %s\n",keytmp,valuetmp);
}
```
______________________
### fcpekv_k2f()

__函数原型__ <br/>
根据用户填入k2f数组中的key，自动匹配出kvarr中的key和value,然后将获得的key和value传入到k2f数组中的回调函数中.<br/>
如果存在多个相同的key则会每匹配到一个则调用一次回调.<br/>
```
void fcpekv_k2f(const char *kvarr[],unsigned int kvnum, const fcpek2f_t *k2farr, unsigned int arrnum)
```
__数介绍__ <br/>
|参数名|类型|说明|
|:--:|--|--|
|kvarr|const char *[]|元素是"key=value"字符串的数组.|
|kvnum|unsigned int|kvarr数组中元素的个数.|
|k2farr|const fcpek2f_t *|存放一系列key以及key对应的回调函数.|
|arrnum|unsigned int|k2farr数组元素的个数|

```
typedef struct{
    const char *key; /*字符串key*/
    void *cbdata;     /*传给回调的私有数据*/
    long  extdata;    /*传给回调的额外数据*/ 
    int (*cb)(const char *k,const char*v,void *privdata , long extd);/*key对应的回调函数
                                                                       如果回调返回  !=0  则会立即结束解析*/
}fcpek2f_t;
```

__返回值__ <br/>
|返回类型|成功|失败|备注|
|:---|:---|:---|:---|

__注意__ <br/>
无
  
__例子__ <br/>
```
int key1_cb(const char *k,const char*v,void *privdata , long extd)
{
    char *vstr = (char*)privdata;
    snprintf(vstr,(int)extd,"%s",v);
    return 0;
}

int key2_cb(const char *k,const char*v,void *privdata , long extd)
{
    int *vint=(int*)privdata;

    (*vint) = atoi(v);

    return 0;
}

void test(void)
{
    char vstr[128]={0};
    int vint=0;

    const char *mykvarr[]={
      "key1=value1",
      "key2=10",
      "key3=value3",
    };

    fcpek2f_t k2f[]={
        FCPEK2F_INIT("key1",vstr,sizeof(vstr),key1_cb),
        FCPEK2F_INIT("key2",&vint,0,key2_cb),
    };
    
    fcpekv_k2f(mykvarr,sizeof(mykvarr)/sizeof(mykvarr[0]),k2f,sizeof(k2f)/sizeof(k2f[0]));
    
    printf("%s %d\n",vstr,vint);
    
    return;
}
```


