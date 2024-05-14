# fcpekv
## 头文件
#include  "fcpe_kv.h"

## API介绍
### fcpekv_parse()
#### 函数原型
根据指定的字符串(key=value)类型，解析出key和value. <br/>
```
void fcpekv_parse(char *cstr,char **key,char **value)
```
#### 参数介绍
|参数名|类型|说明|
|:--:|--|--|
|cstr|char * <br/> 1)表示"key=value"类型的字符串.<br/>2)不能是常量字符串|此字符串会被修改(不能传入常量字符串).|
|key|char **|1)用于返回解析到的key,如果为空则不返回key.<br/>2)返回结果不需要释放.|
|value|char **|1)用于返回解析到的value,如果为空则不返回value.<br/>2)返回结果不需要释放|
#### 返回值
|返回类型|成功|失败|备注|
|:---|:---|:---|:---|

#### 注意
  1) 传入的cstr不能是常量，否则将引起异常.<br/>
  2) 传入的cstr必须是"key=value" 类型.并且会以最右边的'='作为分隔符.<br/>
  3) 解析出的key和value不会自动去除空白(如果存在).<br/>
#### 例子
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
