# fcpebit
## 头文件
#include  "fcpe_bit.h"

## API介绍
### fcpebit_last_sbit()

__函数原型__ <br/>
返回输入参数的最高有效bit位（从低位往左数最后的有效bit位）的序号，该序号与常规0起始序号不同，它是1起始的（当没有有效位时返回0） <br/>
```
unsigned int fcpebit_last_sbit(unsigned long word)
```
__数介绍__ <br/>
|参数名|类型|说明|
|:--:|--|--|
|word|unsigned long|计算此值的最高有效bit位的序号。|

__返回值__ <br/>
|返回类型|成功|失败|备注|
|:---|:---|:---|:---|
|unsigned int|返回 >=0 <br/>>0:表示最高有效bit位的序号(从1开始计算)。<br/>=0:表示无有效bit位|无|无|

__注意__ <br/>
  1） 有效bit位表示的是在bit位上置了1。
 
__例子__ <br/>
```
void test(void)
{  
}
```
______________________
### fcpebit_roundup_powof2()

__函数原型__ <br/>
用于将一个数向上取整到最近的 2 的幂次方 <br/>
```
unsigned long fcpebit_roundup_powof2(unsigned long word)
```
__数介绍__ <br/>
|参数名|类型|说明|
|:--:|--|--|
|word|unsigned long|用于将此数向上取整到最近的 2 的幂次方。|

__返回值__ <br/>
|返回类型|成功|失败|备注|
|:---|:---|:---|:---|
|unsigned int|返回 >0，表示2 的幂次方值|无|无|

__注意__ <br/>
 
__例子__ <br/>
```
void test(void)
{  
}
```
______________________
### fcpebit_rounddown_powof2()

__函数原型__ <br/>
 用于将一个数向下取整到最近的 2 的幂次方 <br/>
```
unsigned long fcpebit_rounddown_powof2(unsigned long word)
```
__数介绍__ <br/>
|参数名|类型|说明|
|:--:|--|--|
|word|unsigned long|用于将此数向下取整到最近的 2 的幂次方。|

__返回值__ <br/>
|返回类型|成功|失败|备注|
|:---|:---|:---|:---|
|unsigned int|返回 >0，表示2 的幂次方值|无|无|

__注意__ <br/>
 
__例子__ <br/>
```
void test(void)
{  
}
```
______________________
