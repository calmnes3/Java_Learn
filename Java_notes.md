### 1.Java基本程序设计结构

#### 1.1 数据类型

> 必须为每个变量声明一种类型
>
> 注：Java有一个给能够表示任意进度的算术包，通常称为“大数值”（big number）。虽然被称为大数值，但它并不是一种新的Java类型，而是一个Java对象。

##### 1.1.1 整型

整型用于表示没有小数部分的数值，它允许是负数。

| 类型  | 存储需求 | 取值范围                    |
| ----- | -------- | --------------------------- |
| int   | 4字节    | -2147483848~214...          |
| short | 2字节    | -32768~32767                |
| long  | 8字节    | -9223372036854775808~922... |
| byte  | 1字节    | -128~127                    |

> byte和short类型主要用于特定的应用场合，例如底层文件处理或者需要控制占有储存空间量的大数组。

##### 1.1.2 浮点类型

| 类型   | 存储需求 | 取值范围                     |
| ------ | -------- | ---------------------------- |
| float  | 4字节    | 大约±3.4+38F（有效位6-7位）  |
| double | 8字节    | 大约±1.79...（有效位为15位） |

* double表示这种类型的数值进度是float类型的两倍；

* 一般采用double类型，float类型精度难以满足需求；

* 需要使用单精度的库或者需要存储大量的数据，适合用float类型。

* float类型的数字有一个后缀F或f（例如，3.14F）。没有后缀F的浮点型（如3.14）默认为double类型。

> 所有的浮点数值计算都遵循IEEE754规范。具体来说，喜爱按用于表示移出和出错秦广的三个特殊的浮点数值：
>
> * 正无穷大
> * 负无穷大
> * NaN（不是一个数字）
>
> 例如，一个正整数除以0的结果为正无穷大。计算0/0或者复数的平方根结果为NaN。

##### 1.1.3 char类型

char类型的字面量值要用单引号括起来。

**特殊字符转义序列：**

| 转义序列 | 名称   | Unicode值 |
| -------- | ------ | --------- |
| \b       | 退格   | \u0008    |
| \t       | 制表   | \u0009    |
| \n       | 换行   | \u000a    |
| \r       | 回车   | \u000d    |
| \‘’      | 双引号 | \u0022    |
| \\*      | 单引号 | \u0027    |
| \\\      | 反斜杠 | \u005c    |

##### 1.1.4 Unicode和char类型

##### 1.1.5 boolean类型

boolen（布尔）类型有两个值：false和true，用来判定逻辑条件。整型值和布尔值之间不能进行相互转换。

#### 1.2 变量

每个变量都有一个类型（type），在声明变量时，变量的类型位于变量名之前。

##### 1.2.1 变量初始化

声明一个变量之后，必须用复制语句对变量进行显示初始化，千万不要使用未初始化的变量。

##### 1.2.2 常量

在Java中，利用关键字final指示常量。

**关键字final表示这个常量只能被赋值一次，一旦被赋值后，就不能够再更改了。**习惯上，常量名使用全大写。

当某个常量需要在一个类中多个方法中使用，通常将这类常量成为类常量，使用关键字static final设置一个类常量。例：

```java
public class Constants{
    public static final double TEST = 2.54;
    public static void main(String[] args){
        double test1 = 8.5;
        double test2 = 11;
        System.out.println("输出："+ test1*TEST+"和"+test2*TEST);
    }
}
```

类常量的定义位于main方法的外部，因此，在同一个类的其他方法中也可以使用这个常量。而且一个常量被声明为public，那么其他类的方法也可以使用这个常量。

#### 1.3 运算符

##### 1.3.1 数字函数与常量

在

##### 1.3.2 数值类型之间的转换

当使用两个不同数值类型进行二元操作时，先将两个操作数转化为同一类型，然后再进行计算。 

* 如果两个操作数中有一个是double类型，另一个操作数就会转换为double类型。
* 否则，如果其中一个操作数是float类型，另一个操作数将会转换为float类型。
* 否则，如果其中一个操作数是long类型，另一个操作数将会转换为long类型。
* 否则，两个操作数都将被转换为int类型。

> 无信息丢失转换：
>
> byte→short→int→long;
>
> char→int、int→double、float→double；
>
> 可能有精度损失转换：
>
> int→float、long→float、long→double；

##### 1.3.3 强制类型转换

强制类型转换语法格式：

```java
double x = 9.997;
int nx = (int)x;
//变量nx的值为9，强制类型转换通过阶段小数部分浮点值转换为整型。
```

如果相对浮点数进行舍入运算，以便得到最接近的整数（在很多情况下，这种操作更有用），那就使用Math.round方法：

```java
double x = 9.997；
int nx = (int)Math.round(x);
//当调用round的时候，仍然需要使用强制类型转换（int）。其原因是round方法返回的结果为long类型，由于存在信息丢失的可能性，所以只有使用显式的强制类型转换才能够将long类型转换成int类型。
```

> **注：**如果试图将一个数值从一种类型强制转换为另一种类型，而又超出了目标类型的表示范围，结果就会截断成一个完全不同的值。例如：（byte）300的实际值为44。

##### 1.3.4 结合赋值和运算符

可以在赋值中使用二元运算符，这是一种很方便的简写形式。例如：

x += 4；

等价于：

x = x + 4；

（一般，要把运算符放在=号左边，如*=或%=。）

> 如果运算符得到一个值，其类型与左侧操作数的类型不同，就会发生强制类型转换。例如，如果x是一个强制int，则以下语句：
>
> x += 3.5；
>
> 是合法的，将把x设置为(int)(x+3.5)。

##### 1.3.5 自增与自减运算符

后缀或前缀形式都会使变量值加1或减1：

在表达式中，前缀形式会先完成加1，而后缀形式会使用变量原来的值。

```java
int m = 7;
int n = 7;
int a = 2 * ++m;//a=16
int b = 2 * n++;//b=14
```

##### 1.3.6 位运算符

处理整数类型时，可以直接对组成整型数值的各个位完成操作，这意味着可以使用掩码技术得到整数中各个位，位运算包括：

&("and")	|("or")	^("xor")	~("not")

这些运算符按位模式处理。例如，如果n是一个整数变量，而且用二进制表示的n从右边数第4位为1，则：

int fourthBitFromRight = （n & 0b1000）/ 0b1000；

会返回1，否则返回0，利用&并结合使用适当的2的幂，可以把其他位掩掉，而只保留其中某一位。

**>>**和**<<**运算符将位模式左移或者右移。需要建立位模式来完成位掩码时，这两个运算符会很方便：

int fourthBitFromRight = (n &(1 << 3) >> 3);

最后，>>>运算符会用0填充高位，这与>>不同，它会用符号位填充高位，不存在<<<运算符。

##### 1.3.7 括号与运算符级别

如果不适用圆括号，就按照给出的运算符优先级次序进行计算。同一个级别的运算符按照从左到右的次序进行计算。例如：由于&&的优先级比||优先级高，所以表达式

a&&b||c

等价于

(a&&b)||c

又因为+=是右结合运算符，所以表达式

a += b += c

等价于

a += (b +=c)

| 运算符                                                | 结合性   |
| ----------------------------------------------------- | -------- |
| [].()(方法调用)                                       | 从左向右 |
| ! ~ ++ -- +(一元运算) - (一元运算)()(强制类型转换)new | 从右向左 |
| */%                                                   | 从左向右 |
| +-                                                    | 从左向右 |
| <<  >>  >>>                                           | 从左向右 |
| <  <=  > >=  instanceof                               | 从左向右 |
| ==  !=                                                | 从左向右 |
| &                                                     | 从左向右 |
| ^                                                     | 从左向右 |
| \|                                                    | 从左向右 |
| &&                                                    | 从左向右 |
| \|\|                                                  | 从左向右 |
| ?:                                                    | 从右向左 |
| =  +=  -=  *=  /=  %=  \|=  ^=  <<=  >>=  >>>=        | 从右向左 |

#### 1.4 字符串

##### 1.4.1 子串

String类的substring方法可以从一个较大的字符串提取出一个子串。例如：

```java
String greeting = "Hello";
String s = greeting.substring(1,3);
//创建了一个由字符“Hel”组成的字符串
```

substring方法的第二个参数是不想复制的第一个位置，这里需要复制位置为0、1和2（从0到2，包括0和2）的字符，再substring中从0开始计数，直到3为止，但不包含3。

##### 1.4.2 不可变字符串

```java
String greeting = "Hello";
greeting = greeting.substring(0,3)+"P!";//greeting的值为Help！
//String类没有提供用于修改的字符串，所以需要先提取需要的字符，再拼接上替换的字符串。
```

由于不能修改Java字符串中的字符，所以在Java文档中将String类对象成为不可变字符串

##### 1.4.3 检测字符串是否相等

可以使用equals方法检测两个字符串是否相等

表达式：

```java
s.equals(t)
```

如果字符串s与字符串t相等，则返回true；否则，返回false，需要注意，s和t可以是字符串变量，也可以是字符串字面量，例如，下列表达式是合法的：

```java
"Hello".equals(greeting)
```

要想监测两个字符串是否相等，而不区分大小写，可以使用equalsIgnoreCase方法：

```java
"Hello".equalsIgnoreCase("hello")
```

不要使用==运算符检测两个字符串是否相等！这个运算符只能确定两个字符串是否放置在同一个位置上。

##### 1.4.4 空串与Null值

空串""是长度为0的字符串。可以调用以下代码检查一个字符串是否为空：

```java
if(str.length() == 0)
或
if(str.equals(""))
```

空串是一个Java对象，有自己的串长度（0）和内容（空）。

String变量还可以存放一个特殊的值，名为null，这表示目前没有任何对象与该变量关联。

检查一个字符串是否为null，要使用以下条件：

```java
if(str == null)
```

检查一个字符串既不是null也不是空串，使用以下条件：

```java
if(str != null && str.length != 0)
```

##### 1.4.5 码点与代码单元

length方法将返回采用UTF-16编码表示的给定字符串所需要的代码单元数量。例如：

```java
String greeting = "Hello";
int n = greeting.length();//is 5
```

想要得到实际的长度，即码点数量，可以调用：

```java
int cpCount = greeting.codePointCount(0,greeting.length());
```

调用s.charAt(n)将返回位置n的代码单元，n介于0 ~ s.length()-1 之间。例如：

```java
char first = greeting.charAt(0);//is H
char last = greeting.charAt(4);//is o
```

要想得到第i个码点，应该使用下列语句

```java
int index = greeting.offsetByCodePoints(0,i);
int cp = greeting.codePointAt(index);
```

##### 1.4.6 String API

**常用的String方法：**

* char charAt(int index)

  返回给定位置的代码单元。除非对底层的代码单元感兴趣，否则不需要调用这个方法

* int codePointAt(int index) 5.0

  返回从给定位置开始的码点

* int offsetByCodePoints(int startIndex,int cpCount)5.0

  返回从startIndex代码点开始，位移cpCount后的码点索引

* int copareTo(String other)

  按照字典顺序，如果字符串位于other之前，返回一个负数；如果字符串位于other之后，返回一个正数；如果连个字符串相等，返回0

* InStream codePoints()8

  将这个字符串的码点作为一个流返回。调用toArray将它们放在一个数组中

* new String(int[] codePoints,int offset,int count)5.0

  用数组中从offset开始的count个码点构造一个字符串

* boolean equals(Object other)

  如果字符串与other相等，返回true

* boolean equalsIgnoreCase(String other)

  如果字符串与other相等（忽略大小写），返回true

* boolean startsWith(String prefix)

* boolean endsWidth(String suffix)

  如果字符串以suffix开头或结尾，则返回true

* int indexOf(String str)

* int indexOf(String str,int fromIndex)

* int indexOf(int cp)

* int index(int cp,int fromIndex)

  返回与字符串str或代码点cp匹配的第一个串的开始位置。这个位置从索引0或fromIndex开始计算。如果在原始串中不存在str，返回-1

* int lastIndexOf(String str)

* int lastIndexOf(String str,int fromIndex)

* int lastindexOf(int cp)

* int lastindexOf(int cp,int fromIndex)

  返回与字符串str或代码cp匹配的最后一个子串的开始位置。这个位置从原始串尾端或fromIndex开始计算。

* int length()

  返回字符串的长度

* int codePointCount(int startIndex,int endIndex)5.0

  返回startIndex和endIndex-1之间的代码点数量，没有配成对的待用字符将记入代码点。

* String replace(CharSequence oldString,CharSequence newString)

  返回一个新字符串，这个字符串用newString代替原始字符串中所有的oldString。可以用String或StringBuilder对象作为CharSequence参数。

* String substring(int beginIndex)

* String substring(int beginIndex,int endIndex)

  返回一个新字符串。这个字符串包含原始字符串中从beginIndex到串尾或endIndex-1的所有代码单元

* String toLowerCase()

* String toUpperCase()

  返回一个新字符串，这个字符串将原始字符串中的大写字母改为小写，或者将原始字符串中的所有小写字母改成了大写字母。

* String trin()

  返回一个新字符串，这个字符串将删除了原始字符串头部和尾部的空格。

* String join(CharSequence delimiter,CharSequence... elements)8

  返回一个新字符串，用给定的定界符连接所有元素。

##### 1.4.7 构建字符串

**StringBuilder类中的重要方法：**

* StringBuilder()

  构造一个空的字符串构建器

* int length()

  返回构建器或缓冲器中的代码单元数量

* StringBuilder append(String str)

  追加一个字符串并返回this

* StringBuilder appendCodepoint(int cp)

  追加一个代码点，并将其转换为一个或两个代码单元并返回this

* void setCharAt(int i, char c)

  将第i个代码单元设置为c

* StringBuilder insert(int offset,String str)

  在offset位置插入一个字符串并返回this

* StringBuilder insert(int offset,Char c)

  在offset位置插入一个代码单元并返回this

* StringBuilder delete(int startIndex,int endIndex)

  删除偏移量从startIndex到-endIndex-1的代码单元并返回this

* String toString()

  返回一个构建器或缓冲器内容相同的字符串

#### 1.5 输入输出

##### 1.5.1 读取输入

读取“标准输入流”System.in就没有那么简单了。要想通过控制台进行输入，首先需要构造一个Scanner对象，并与“标准输入流”System.in关联。

```java
Scanner in = new Scanner(System.in);
```

可以使用Scanner类的各种方法输入操作了。例如，nextLine方法将输入一行。

```java
System.out.print("What is your name?");
String name = in nestLine();
```

在这里，使用nextLine方法是因为子啊输入行中有可能包含空格。要想读取一个单词（以空白符作为分隔符），就调用：

```java
String firstName = in.next();
```

要想读取一个整数，就调用nextInt方法。

```java
System.out.print("How old are you?");
int age = in.nextInt();
```

与此类似，要想读取下一个浮点数，就调用nextDouble方法。

因为输入是可见的，所以Scanner类不适用于从控制台读取密码。引用Console类实现这个目的。

```java
Console cons = System.console();
String username = con.readLine("User name:");
char[] passwd = cons.readPassword("Password:");
```

为了安全起见，返回的密码存放在一堆字符数组中，而不是字符串中。对密码进行处理后，应该马上用一个填充值覆盖数组元素。采用Console对象处理输入不如采用Scanner方便。每次只能读取一行数据，而没有能够读取一个单词或一个数值的方法。

> java.util.Scanner 5.0

* Scanner (InputStream in)
  用给定的输入流创建一个Scanner对象

* String nextLine()

  读取输入的下一行内容

* String next()

  读取输入的下一个单词（以空格作为分隔符）

* int nextInt()

* double nextDouble()

  读取并转换下一个表示整数或浮点数的字符序列

* boolean hasNext()

* boolean hasNextDouble()

  检测是否还有表示整数或浮点数的下一个字符序列

> java.lang.System 1.0

* static Console console() 6

  如果有可能进行交互操作，就通过控制台窗口为交互的用户返回一个Console对象，否则返回null。对于任何一个通过控制台窗口启动的程序，都可以使用Console对象。否则，其可能性将与所使用的系统有关。

> java.io.Console 6

* static char[] readPassword(String prompt,Object...args)

* static String readLine(String prompt,Object...args)

  显示字符串prompt并且读取用户输入，直到输入行结束，args参数可以用来提供输入格式。

##### 1.5.2 格式化输出

可以使用System.out.print(x)将数值x输入到控制台。这条命令将以x对应的数据类型所允许的最大0数字位数打印输出x。

```java
double x = 10000.0/3.0;
System.out.print(x);
//打印：
	3333.3333333333335
```

printf方法：

```java
printf("<式样化字符串>",<参数表>);
```

例如：调用：

```java
System.out.printf("%8.2f",x);
//可以用8个字符的宽度和小数点后两个字符的进度打印x。也就是，打印输出一个空格和7个字符，输出：“3333.33”
```

每一个以%字符开始的格式说明符都用相应的参数替换。格式说明符尾部的转换符将指示被格式化的数值类型：

| 转换符 | 类型                  | 举例                              |
| ------ | --------------------- | --------------------------------- |
| d      | 十进制整数            | 159                               |
| x      | 十六进制整数          | 9f                                |
| o      | 八进制整数            | 237                               |
| f      | 定点浮点数            | 15.9                              |
| c      | 指数浮点数            | 1.59e+01                          |
| g      | 通用浮点数            | —                                 |
| a      | 十六进制浮点数        | 0x1.fccdp3                        |
| s      | 字符串                | Hello                             |
| c      | 字符                  | H                                 |
| b      | 布尔                  | True                              |
| h      | 散列码                | 42628b2                           |
| tx或TX | 日期时间（T强制大写） | 已经过时，应当改为使用java.time类 |
| %      | 百分号                | %                                 |
| n      | 与平台有关的行分隔符  | —                                 |

 另外，还可以给出控制格式输出的各种的标志。逗号标志增加了分组的分隔符。即：

```java
System.out.printf("%,2f",10000.0/3.0);
//打印：
//3，333.33
```

可以使用多个标志，例如，"%,(.2f"  使用分组的分隔符并将附属括在括号内。

| 标志            | 目的                                                         | 举例         |
| --------------- | ------------------------------------------------------------ | ------------ |
| +               | 打印正数和负数的符号                                         | +3333.33     |
| 空格            | 在正数之前添加空格                                           | \| 3333.33\| |
| 0               | 数字前面补0                                                  | 003333.33    |
| -               | 左对齐                                                       | \|3333.33 \| |
| (               | 将负数括在括号内                                             | (3333.33)    |
| ,               | 添加分组分隔符                                               | 3,333.33     |
| #(对于f格式)    | 包含小数点                                                   | 3.333.       |
| #(对于x或0格式) | 添加前缀0x或0                                                | 0xcafe       |
| $               | 给定被格式化的参数索引。例如，%1$d,%1$x将以十进制和十六进制格式打印第1个参数 | 159 9F       |
| <               | 格式化前面说明的数值，例如，%d%<x以十进制和十六进制打印同一个数组 | 159 9F       |

> 可以使用s转换格式化任意的对象。对于任意实现了Formattable接口的对象都将调用formatTo方法；否则将调用toString方法，它可以将对象转换为字符串。

可以使用静态String.format方法创建一个格式化的字符串，而不打印输出：

```java
String	message = String.format("Hello,%s,Next year,you'll be %d",name,age);
```

##### 1.5.3 文件输入与输出

要想对文件进行读取，就需要一个用File对象构造一个Scanner对象，如下所示：

```Java
Scanner in = new Scanner(Paths.get("myfile.txt"),"UTF-8");
```

如果文件名中包含反斜杠符号，就要记住在每个反斜杠之前再加一个格外的反斜杠：

```
"c:\\mydirectory\\myfile.txt"
```

写入文件，需要构造一个PrintWriter对象。在构造器中，只需要提供文件名：

```Java
PrintWriter out = new PrintWriter("myfile.txt","UTF-8");
```

如果文件不存在，创建该文件。可以向输出到System.out一样使用print、println以及printf命令。

> **警告：**可以构建一个待有字符串参数的Scanner，但这个Scanner将字符串解释为数据，而不是文件名。例如，如果调用：
>
> ```java
> Scanner in = new Scanner("myfile.txt");
> ```
>
> 这个scanner会将参数作为包含10个字符的数据

#### 1.6 控制流程

##### 1.6.1 块作用域

块（block）概念：块（即复合语句）是指一对大括号括起来的若干条简单的Java语句。块确定了变量的作用域。一个块可以嵌套在另一个块中。下面就是在main方法嵌套另一个语句块的示例：

```java
public static void main(String[] args){
    in n;
    ...
    {
        in k;
    }//k之定义到这里
}
```

##### 1.6.2 条件语句

##### 1.6.3 循环

当条件为true时，while循环执行一条语句（也可以是一个语句块）。一般格式为：

```java
while(condition)statement
```

如果开始执行循环条件的值就为false，则while循环体一次也不执行。

while循环语句首先检测循环条件。因此，循环体中的代码可能不被执行。如果希望循环体至少被执行一次，则应该将检测条件放在最后，使用do/while虚幻语句可以实现这种操作方式。它的语法格式为：

```java
do statement while (condition);
```

##### 1.6.4 确认循环

for循环语句是支持迭代的一种的通用结构，利用每次迭代之后更新的计数器或类似的变量来控制迭代次数。

##### 1.6.5 多重选择：switch语句

#### 1.7 大数值

Java.math包中的两个类：BigInteger和BigDecimal，这两个类可以处理包含任意长度数字序列的数值。BigInteger类实现了忍一进度的整数运算，BigDecimal实现了任意精度的浮点数运算。

使用静态的valueOf方法可以将普通的数值转换为大数值：

```java
BigInteger a = BigInteger.valueOf(100);
```

注意：不能使用算术运算符（如：+和*）处理大数值。而需要使用大数值类中的add和multiply方法。

```java
BigInteger c = a.add(b);//c = a + b
BigInteger d = c.multiply(b.add(BigInteger.valueOf(2)));//d=c*(b+2)
```

> API Java.math.BigInteger 1.1

* BigInteger add(BigInteger other)

* BigInteger subtract(BigInteger other)

* BigInteger multiply(BigInteger other)

* BigInteger divide(BigInteger other)

* BigInteger mod(BigInteger other)

  返回这个大整数和另一个大整数other的和、差、积、商以及余数。

* int compareTo(BigInteger other)

  如果这个大整数与另一个大整数other相等，返回0；如果这个大整数小于另一个大整数other，返回负数；否则，返回正数。

* static BigInteger valueOf(long x)

  返回值等于x的大整数

> java.math.BigInteger 1.1

* BigDecimal add(BigDecimal other)

* BIgDecimal subtract(BigDecimal other)

* BigDecimal multiply(BigDecimal other)

* BIgDecimal divide(BigDecimal other roundingMode mode)5.0

  返回这个大实数与另一个大实数other的和、差、积、商。要想计算商，必须给出舍入方式（rounding mode）。RoundingMode.HALF_UP是四舍五入方式。

* int compareTo(BigDecimal other)

  如果这个大实数与另一个大实数相等，返回0；如果这个大实数小于另一个大实数，返回负数；否则返回正数。

* static BigDecimal valueOf(long x)

* static BigDecimal valueOf(long x,int scale)

  返回值为x或x/10scale的一个大实数

#### 1.8 数组

​	数组是一种数据结构，用来存储同一类型值的集合。通过一个整型下标可以访问数组中的每一个值。例如，如果a是一个整数数组，a[i]就是数组中下标为i的整数。

​	在声明数组变量时，需要指出数组类型（数据元素类型紧跟[]）和数组变量名字，下面声明了整型数组a：

```java
int[] a;
```

上面只声明了变量a，并没有将a初始化为一个真正的数组。应该使用new运算符创建数组。

```java
int[] a = new int[100];
```

这条语句创建了一个可以储藏100个整数的数组，数组长度不要求是常量：new int[n]会创建一个长度为n的数组。

> 注释：int[] a;  或  int a[];























 
