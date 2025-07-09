## CH3 运算方法

**补码加减**

### 1.溢出判别

只有当两个**同号数相加**或者**异号数相减**时才可能产生溢出。

#### 1.判别逻辑一：一位符号位

由于减法的机器实现也是由加法完成的，所以参加操作的两个数符号相同时，如果产生结果异号，则就是溢出。

Fa：a的符号位

Fb：b的符号位

Fs：s结果的符号位

<img src="C:\Users\Zhao Yitong\AppData\Roaming\Typora\typora-user-images\image-20250621093319330.png" alt="image-20250621093319330" style="zoom:50%;" />

0，无溢出；1，溢出。

#### 2.双符号位

只有两个符号位一样时没有溢出。如果不一样，真实的符号位是高位。

<img src="C:\Users\Zhao Yitong\AppData\Roaming\Typora\typora-user-images\image-20250621093443960.png" alt="image-20250621093443960" style="zoom:50%;" />

#### 3.根据进位判断溢出

<img src="C:\Users\Zhao Yitong\AppData\Roaming\Typora\typora-user-images\image-20250621093530834.png" alt="image-20250621093530834" style="zoom:50%;" />

