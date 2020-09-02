## 3.1一个简单的Java应用程序

+ Java区分大小写
+ 名字必须以字母开头，长度不限，不能使用保留字
+ 类名以大写字母开头，每个单词开头都要大写，即驼峰命名法（camel case）
+ 回车不是语句结束的标志，所以可以把一条语句拆分成几行

## 3.2 注释

+ // 单行注释
+ /* */  较长注释 跨行
+ /** */  较长注释 可以自动生成文档

## 3.3 数据类型

+ Java中共有8种基本类型，包括4种整形、2种浮点类型、1种字符类型和表示真值的boolean类型
+ #### 3.3.1 整形
  
  + 例如int 一共32位 第一位是符号位 所以范围的指数是31
  
  + 长整型long有一个后缀大写L
  
  + 16进制有前缀0x/0X
  
  + 2进制有前缀0b/0B
  
  + 可以给数字中间插下划线 方便阅读 比如1_000_000
  
  + | 类型  |   存储需求    |   取值范围   |
    | :---: | :-----------: | :----------: |
    | byte  | 1字节（8位）  |  -2^7 ~ 2^7  |
    | short | 2字节（16位） | -2^15 ~ 2^15 |
    |  int  | 4字节（32位） | -2^31~ 2^31  |
  | long  | 8字节（64位） | -2^63 ~ 2^63 |
  
+ #### 3.3.2 浮点类型

  + float表示的数有后缀F/f  没有后缀的浮点数默认为double double也可以有后缀D/d

    ```java
    float a=3.14; //报错
    float a=3.14f; //正确
    ```

  + 在16进制中 指数用p表示 而不是e e=14

  + 浮点数有3个特殊浮点数值

    + 正无穷大
    + 负无穷大
    + NaN  非数 要判断一个数是NaN 要用Double.isNaN(x)
  
  + |  类型  | 存储需求 |                取值范围                |
    | :----: | :------: | :------------------------------------: |
    | float  |  4字节   |     +-3.40282347E+38F（有效位6~7）     |
    | double |  8字节   | +-1.79769313486231570E+308（有效位15） |

+ #### 3.3.3 char类型
  
  + 4字节
  + char要用单引号‘’括起来，双引号是字符串
  + 可以使用\uFFFF 表示字符
  + 注释中：//\u000A is a new line  000A是一个换行符
+ #### 3.3.5 boolean类型
  
  + 只有两个值true/false
  + 整形值和boolean值不能相互转换

## 3.4 变量与常量

+ 3.4.1 声明变量

  + 大小写敏感，基本上无长度限制，尽量不要使用$
  + 尽量不要使用诸如 int i,j; 而用多行来表示

+ #### 3.4.2 变量初始化

  + ```java
    int vacationDays = 12;	//直接赋值
    int salary;
    salary = 10000;	//先声明再赋值
    var greeting = "Hello"; //如果可以从变量初始值推断出类型，就不用声明类型
    ```

  + 

+ #### 3.4.3 常量

  + 在Java中，利用final指示常量（const是Java的保留字，但是从不使用，必须用final表示常量）

  + 习惯上，常量对象名使用全大写

  + 类常量

    + ```java
      public clas Constants{
          public static final double CM_PER_INCH = 2.54;
      }
      ```

    + 类常量可以在一个类的多个方法中使用，使用关键字static final来声明

    + 如果前面还声明为public，就可以在其他类的方法中使用这个常量

+ #### 3.4.4 枚举类型

  + 实用场景：变量的取值只在一个有限的集合内

  + ```java
    enum Size {SMALL, MEDIUM, LARGE, EXTRA_LARGE};
    Size s=Size.MEDIUM;//也可以赋值null,表示这个变量没有设置任何值
    ```

## 3.5 运算符

+ #### 3.5.1 算数运算符

  + ```java
    + - * / %
    System.out.print(0/10); // 0
    System.out.print(10/0); //java.lang.ArithmeticException: / by zero
    System.out.print(0/0);  //java.lang.ArithmeticException: / by zero
    System.out.print(0.0/0);  //NaN
    System.out.print(0/10.0); //0.0
    System.out.print(10.0/0); //infinity
    ```

  + 所有整数（包括0）除以0都会报错

  + 非0浮点数除以0是无限infinity

  + 0.0浮点数除以0是非数NaN

  + 严格的浮点计算：

  + ```java
    public static strictfp void main(String[] args)
    ```

+ #### 3.5.2 数学函数与常量

  + 常见的Math类方法

  + ```java
    Math.sqrt(x);//x^2
    Math.pow(x,a);//x^a
    Math.sin
    Math.cos
    Math.tan
    Math.exp
    Math.log
    Math.log10
    Math.PI
    Math.E
    ```

  + 用Math类可以抛出异常 比如10亿*3 就会生成一个奇怪的数继续算 但是用Math.MultplyExact(1000000000,3)则会终止运行，生成异常

+ #### 3.5.3 数值转换

  + ```mermaid
    graph LR
    	A[byte]-->B[short]
    	B-->C[int]
    	E[char]-->C
    	C-->D[long]
    	C-.->F[float]
    	C-->G[double]
    	F-->G
    	D-.->F
    	D-.->G
    ```

  + 虚线会导致精度损失

  + 转换一般为转到箭头能指向的最远类型
  
+ #### 3.5.4 强制类型转换

  + ```java
    double x = 9.997;
    int nx = (int) x;//nx=9
    int nx = (int) Math.round(x);//nx=10
    ```

  + 如果强制转换为一个超过范围的类型，就会得到一个完全不同的结果 (byte)300=44 300-256

  + boolean - > int    b?1:0

+ #### 3.5.5 结合赋值和运算符

  + ```java
    x+=4;//x=x+4
    x+=3.5;// valid, if x is a integer,x=(int)(x+3.5)
    ```

+ #### 3.5.6 自增与自减运算符

  + ```java
    n++;
    n--;
    ++n;
    --n;
    ```

+ #### 3.5.7 关系和boolean运算符

  + 关系运算符:==、!=、<、>、<=、>=、&&、||
  + 三元表达式：condition?expression1(true):expression2(false)

+ #### 3.5.8 位运算符

  + &(and) |(or) ^(xor) ~("nor")

  + ```java
    int test=0b1000;
    int result = (test & 0b1000) / 0b1000;//返回1
    >>和<< 可以将位模式左移和右移 >>>会填充高位
    test=test<<3;//0b1000000 64
    test=test>>3;//0b1 1
    test=test>>>3;//  1
    ```

  + 在boolean运算中也会有&和| 和&&与||不同的是 前者会把前后两个表达式都计算 不采用“短路” 后者则采用短路 比如a||b 如果a为true 直接返回true

+ #### 3.5.9 括号与运算符级别

  + &&比||优先级高

  + +=是右结合运算符从右向左

  + ```java
    a&&b||c;//(a&&b)||c
    a+=b+=c;//a+=(b+=c)
    ```

## 3.6 字符串（String）

+ Java字符串就是Unicode字符序列

+ #### 3.6.1 子串

  + ```java
    String greeting = "Hello";
    String s = greeting.substring(0,3);//Hel
    ```

  + substring方法第一个参数是想复制的第一个字符，第二个参数是**不想复制的第一个位置** 上代码例子即为0~2 到3结束 不包括3 这样比较方便计算子串长度 直接第二个参数-第一个参数就可以计算出

+ #### 3.6.2 拼接

  + Java允许使用+号拼接两个字符串

  + ```java
    String a="123";
    String b="456";
    String c=a+b;//123456
    ```

  + 字符串与任意非字符串拼接都会转换成字符串

  + ```java
    int age=13;
    String rating="PG"+13;//"PG13"
    ```

  + 如果需要把多个字符串放在一起，用界定符分隔，可以用静态join方法

  + 如果要重复，就可以使用repeat

  + ```java
    String all = String.join("/","j","a","v","a");//j/a/v/a
    String repeated = "Java".repeat(3);//"JavaJavaJava"
    ```

+ #### 3.6.3 不可变字符串

  + **String类没有提供修改字符串中某个字符的方法**，因此Java文档中将String类对象称为是**不可变的(immutable)**

  + 如果要修改，可以提取要保留的子串，然后拼接

  + ```java
    String greeting = "Hello";
    greeting = greeting.substring(0,3)+"p!";//"Help!"
    ```

+ #### 3.6.4 字符串相等检测

  + 使用equals方法检测，如果希望不区分大小写，则使用equalsIgnoreCase
  + **千万不要使用**==来判断字符串相等，==判断的是两个字符串存储是否存储在同一个位置

+ #### 3.6.5 空串与Null串

  + 空串""即为长度为0的串 可以使用str.length()==0来判断
  + Null是字符串的一个特殊值，可以直接使用str==null来判断

+ #### 3.6.6 码点与代码单元

  + Java字符串由char值序列组成。char数据类型是一个采用UTF-16编码表示Unicode码点(codePoint)的代码单元。最常用的Unicode字符使用一个代码单元可以表示，辅助字符则需要一对两个代码单元表示  

  + 一个字符char对应一个码点，但是一个码点可能要一个或者两个代码单元表示
  
  + 一个char类型正好保存一个代码单元的值。也就是说，String类型中的char数组，保存的其实是字符串对应的代码单元
  
  + ```java
    String test="Hello";
    int n = test.codePointCount(0,test.length());//5
    String pijiu="🍺"
    pijiu.length();//2
    pijiu.codePointCount(0,pijiu.length());//1
    ```
  
  + 可以使用charAt(int index)获取字符串中第index位置的字符
  
  + ```java
    String test="Hello";
    char first = test.charAt(0);
    ```
  
+ #### 3.6.9 构建字符串

  + 如果要用许多小字段构建一个字符串，可以使用StringBuilder类的append方法，之后用toString()

  + ```java
    char a='a';
    String b="zhaokanglun ";
    String c="is ";
    StringBuilder Builder = new StringBuilder( );
    Builder.append(b);
    Builder.append(c);
    Builder.append(a);
    String result = Builder.toString(); //zhaokanglun is a
    ```

## 3.7 输入与输出

+ #### 3.7.1 读取输入

  + 要使用与“标准输入流”System.in关联的Scanner对象

  + ```java
    Scanner in = new Scanner(System.in);
    //假设输入 Li Jiaqi
    String name = in.nextLine();//Li Jiaqi
    String name = in.next();//Li
    ```

+ #### 3.7.2 格式化输出

  + Java沿用了C语言函数库中的printf方法

  + ```java
    float x = 123.45f;
    System.out.printf("%8.2f",x);//输出8个字符，精度为小数点后2位 小数点算一个字符
    //结果：  123.45（注意前面2个空格）
    ```

  + 每一个以%字符开始的格式说明都用相应的参数替换

  + 常见：d 十进制  f 定点浮点数  s 字符串  c 字符   b 布尔  n 换行

  + 如果要输出金钱

  + ```java
    System.out.printf("%,.2f",10000.0/3.0);//3,333.33
    ```

  + 可以使用String.format方法创建一个格式化的字符串，而不打印输出

  + ```
    String message = String.format("Hello,%s!",name);
    ```

  + 两种重复引用方法

  + ```java
    System.out.printf("%1$s %2$tB %2$te, %2$tY","date:",new Date());//1$为第一个索引，2$为第二个索引
    System.out.printf("%s %tB %<te, %<tY","date:",new Date());//<意为使用上一个的索引
    ```

  + 

