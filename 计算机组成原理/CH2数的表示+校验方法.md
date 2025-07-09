## CH2数的表示+校验方法

### 1.数的表示

<img src="C:\Users\Zhao Yitong\AppData\Roaming\Typora\typora-user-images\image-20250621070055174.png" alt="image-20250621070055174" style="zoom:50%;" />

<img src="C:\Users\Zhao Yitong\AppData\Roaming\Typora\typora-user-images\image-20250621070114508.png" alt="image-20250621070114508" style="zoom:50%;" />

<img src="C:\Users\Zhao Yitong\AppData\Roaming\Typora\typora-user-images\image-20250621070134764.png" alt="image-20250621070134764" style="zoom:50%;" />

<img src="C:\Users\Zhao Yitong\AppData\Roaming\Typora\typora-user-images\image-20250621070152272.png" alt="image-20250621070152272" style="zoom:50%;" />

**注意：**IEEE754中，阶码的存储值是实际阶码+127后的结果，这个结果（1-254恒正）以原码的形式存储，不需要考虑移码。最前面的s位，是整个数据的符号位。

32位单精度浮点数表示范围：[-2^127,(1-2^(-23))*2^127]

eg.浮点表示时，阶码6位，其中阶符1位；尾数10位，其中数符1位；阶码的基数为2 。求浮点原码表示时，最大浮点数和最小浮点数？

<img src="C:\Users\Zhao Yitong\AppData\Roaming\Typora\typora-user-images\image-20250621131623850.png" alt="image-20250621131623850" style="zoom:50%;" />

**尾数一定是小数，尾数按照小数范围计算。**

**规格化尾数：尾数的最高有效位和符号位相反**，所以当尾数不为0时，尾数的绝对值都大于等于0.5

规格化目的：提高数的表示精度

<img src="C:\Users\Zhao Yitong\AppData\Roaming\Typora\typora-user-images\image-20250621064839693.png" alt="image-20250621064839693" style="zoom:33%;" />

浮点数有尾数溢出和阶值溢出

尾数溢出，尾数右移一位，阶码+1即可。

阶码下溢，超出了机器可以处理的最小值，则直接把这个浮点数看做0；

阶码上溢，超出最大值。

**注意区分有效位(数值位)和字长！！！**

1.原码字长为n，说明数据位n-1，符号位1位。绝对值转2进制后前面写符号位就行。表示范围

<img src="C:\Users\Zhao Yitong\AppData\Roaming\Typora\typora-user-images\image-20250621072134595.png" alt="image-20250621072134595" style="zoom: 50%;" />

**注意区分真值和原码的区别！！！**

**eg. 反码：1.1010，则原码：1.0101，真值：-0.0101，别一激动目测出真值，把真值当原码，原码中不可能出现“-”！**

**补码：1.1010，则原码：1.0110，真值：-0.0110**

**移码：1.1010，则原码：0.1010，真值：0.1010**

2.反码，注意正数0负数1。绝对值计算二进制后正数前面填符号位，负数**所有位取反**前面**符号位置1**.**表示范围和原码一样**

<img src="C:\Users\Zhao Yitong\AppData\Roaming\Typora\typora-user-images\image-20250621072411563.png" alt="image-20250621072411563" style="zoom:50%;" />

3.补码：正0负1.正数计算绝对值，前加0做符号位；负数计算绝对值，取反，加1，前添符号位。

范围：负数多一个因为10000000表示-2^(n-1)

**快速转换原码补码：从右往左找到第一个1，这个“1”左边所有的数值位取反！**

<img src="C:\Users\Zhao Yitong\AppData\Roaming\Typora\typora-user-images\image-20250621072807939.png" alt="image-20250621072807939" style="zoom:50%;" />

**补码的加法运算：**两补码加法运算，**结果仍然是补码**；[**X+Y]补=[X]补+[Y]补**；**符号位和数值位一样参与运算。**

**补码减法：[X-Y]补=[X]补+[-Y]补**，先求出-Y的补码，再进行加法运算。

4.移码：正1负0.数值位的计算方法和补码一样，注意符号位不同就行。

<img src="C:\Users\Zhao Yitong\AppData\Roaming\Typora\typora-user-images\image-20250621073011002.png" alt="image-20250621073011002" style="zoom:50%;" />



**补码和移码有唯一0：补码：00000000；移码：10000000**

**原码分正0和负0：[+0]=00000000;[-0]=10000000**

**反码：[+0]=00000000;[-0]=11111111**

**原码和反码的表示范围一样；补码和移码的表示范围一样**

### 2.校验方法

码距：两个数据之间有几位不一样的编码。不同的位数被称为编码。

**码距大于1的编码才能发现错误或校正错误**

#### 1.奇偶校验

实现的具体方法，通常是为一个字节补充一个 二进制位，称为校验位，用设置校验位的值为0 或1，**使字节的8位和该校验位含有1值的个数为 奇数或偶数**。在使用奇数个1的方案进行校验时， 称为奇校验，反之，则称为偶校验。（**加上校验位后是奇数、偶数**）

<img src="C:\Users\Zhao Yitong\AppData\Roaming\Typora\typora-user-images\image-20250621080356380.png" alt="image-20250621080356380" style="zoom:50%;" />

#### 2.CRC校验码

二进制的信息位沿着一条线在部件之间传送称为串行传送

CRC码指**k位的信息码**之**后拼接**r位校验码。

关键：1.如何从k位信息码得到r位校验码。2.如何根据k+r位信息码判断是否出错

**模2运算：**运算时**不考虑进位和借位**。

<img src="C:\Users\Zhao Yitong\AppData\Roaming\Typora\typora-user-images\image-20250621081200897.png" alt="image-20250621081200897" style="zoom: 50%;" />

<img src="C:\Users\Zhao Yitong\AppData\Roaming\Typora\typora-user-images\image-20250621081302531.png" alt="image-20250621081302531" style="zoom:50%;" />

<img src="C:\Users\Zhao Yitong\AppData\Roaming\Typora\typora-user-images\image-20250621081453354.png" alt="image-20250621081453354" style="zoom:50%;" />

##### CRC码的编码方法：

<img src="C:\Users\Zhao Yitong\AppData\Roaming\Typora\typora-user-images\image-20250621082506678.png" alt="image-20250621082506678" style="zoom:50%;" />

**k位是校验位，那么生成多项式G(x)一定要是k+1位，n位是数据原长。余数补在后k位，那么生成的CRC码（循环校验码）一定可以被G(x)整除**

<img src="C:\Users\Zhao Yitong\AppData\Roaming\Typora\typora-user-images\image-20250621082702545.png" alt="image-20250621082702545" style="zoom:50%;" />

<img src="C:\Users\Zhao Yitong\AppData\Roaming\Typora\typora-user-images\image-20250621082801157.png" alt="image-20250621082801157" style="zoom:50%;" />

##### 纠错原理：用循环校验码去除生成多项式，如果位数都对，那余数肯定是0；如果不能整除，则一个余数可以判断哪一个位数出错。

<img src="C:\Users\Zhao Yitong\AppData\Roaming\Typora\typora-user-images\image-20250621082959181.png" alt="image-20250621082959181" style="zoom:50%;" />

**余数和出错位的对应关系是不变的，只有当码制和生成多项式G(x)改变时才改变**

##### 生成多项式的要求：1.任何一位出错都应该让余数不等于0

​                                   2.不同位出错的余数不一样

​                                   3.对余数继续做模2除，使余数循环。