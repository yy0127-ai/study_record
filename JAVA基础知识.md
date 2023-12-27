JAVA基础知识

Java程序中支持书写二进制、八进制、十六进制的数据，分别需要以0B或者0b（二进制数）、0（八进制数）、0X或者0x（十六进制数）开头。

## 一、基础语法

### 1.数据类型分类

![](.\images\1.png)

### 2.Java关键字

![](.\images\QQ截图20221018212147.png)

### 3.java命名规则

![](.\images\3.png)

## 二、基础部分

### （1）类型转换

1.自动类型转换（类型范围小的变量，可以直接赋值给类型范围大的变量）

```java
byte a = 20;
int b = a;
```

![](.\images\4.png)

2.表达式的自动类型转换

表达式的最终结果类型由表达式中的最高类型决定

```java
byte a = 20;
int b = a;
double c = 2.5;
double d = a + b + c;
```

3.强制类型转换

类型范围大的数据或者变量，不能直接赋值给类型范围小的变量，会报错

（注：强制类型转换可能造成数据丢失（溢出），浮点型强转成整形，直接丢掉小数部分，保留整数部分返回。）

```java
int i = 1;
byte j = (byte)i;
System.out.println(j);
```

## 四、数组

### 4.1数组的定义

### 4.1.1静态初始化数组

### 4.1.2动态初始化数组(里面的元素是默认值)

- 定义数组的时候只确定元素的类型和数组的长度,之后再存入具体数据.

```java
int[] arr = new int[3];
//后赋值
arr[0] = 10;
```

两种数组定义时的特点和场景有什么区别?

- 当前已经知道存入的元素值,用静态初始化.
- 当前还不清楚要存入哪些数据,用动态初始化.

动态初始化数组,没有指定每个元素存放的数据,则会有**默认值.**

- 基本数据类型:  byte short char int long 默认值为0

  ​						float double 默认值为0.0

  ​						boolean 默认值为false

- 引用数据类型:类 接口 数组 String 默认值为null

```java
#测试默认值
byte[] byte1 = new byte[2]
System.out.println(byte1[0])
```

### 4.2数组的遍历

```java
//遍历数组
int[] ages = {20, 30, 40, 50};
for(int i = 0; i<ages.length; i++){
	System.out.printLn(ages[i]);
}
```

### 4.3数组的案例

**数组元素求和**

```java
int[] arrs = {1,2,3,4,5,6};
int sum = 0;
for(int i = 0; i < arrs.length; i++){
	sum += sum+ arrs[i];
}
```

**数组求最值**

```java
int[] arrs = {1,2,3,4,5,6};
int max = arrs[0];
for(int i = 0; i < arrs.length; i++){
	if(arrs[i] > max){
        max = arrs[i]
    }
}
System.out.printLn(max)
```

**猜数字游戏**

随机生成1-20之间的5个数:未猜中,继续猜;猜中后,输出该数据第一次出现的位置,并输出全部的五个数

分析:①随机生成5个1-20之间的数据并存储起来-->使用数组  ②定义一个死循环,输入数据猜测,遍历数组,判断是否存在数组中

```java
int[] arrs = new int[5];
Random r  = new Random();
for(int i=0; i <arrs.length;i++){
    arrs[i] = r.nextInt(20) + 1;
}
Scanner sc = new Scanner(System.in);
OUT:
while(true){
    System.out.printLn("请输入猜测的数据")
    int data = sc.nextInt();
    for(int i=0;i<arrs.length;i++){
        if(data == arrs[i]){
        	System.out.println("出现的位置为"+i);
        	break OUT;
        } 
        System.out.println("没猜中,继续猜");
    }
     for(int i = 0; i< arrs.length; i++){
         System.out.println(arrs[i]);
     }     
}
```

**随机排名**

```java
//产生一个随机数,当前遍历的数据与索引为该随机数的数据进行交换
int[] arrs = {22,33,35,13,88};
Random r = new Random();
for(int i =0;i<arrs.length;i++){
    int index = r.nextInt(arrs.length) //0-4的随机数
    int temp = arrs[i];
    arr[i] = arrs[index];
    arrs[index] = temp;
}
```

**冒泡排序**

```java
int[] arrs = {3,1,8,5};
for(int i =0;i<arrs.length-1;i++){
    for(int j = 0;j<arrs.length-1-i;j++){
        if(arrs[j]>arrs[j+1]){
            temp = arrs[j];
            arrs[j] = arrs[j+1];
            arrs[j+1] = temp;
        }
    }
}
```

### 4.4 Java内存分配、数组的内存图

Java内存分配：分为栈、堆、方法区、本地方法栈、寄存器

方法区：字节码文件加载时进入的内存

栈内存：方法运行时进入的内存，变量也在这里

堆内存：new出来的东西会在这块内存中开辟空间并产生地址

![](.\images\QQ截图20221118114601.png)

### 4.5Debug工具的使用

IDEA自带的断点调试工具，可以控制代码从断点开始一行一行的执行，然后详细观看程序执行情况。

**DEBUG工具使用步骤**

1. 在需要控制的代码左侧，点击一下，形成断点
2. 选择使用DEBUG方式启动程序，启动后程序会在断点暂停
3. 控制代码一行一行的往下执行

### 4.5数组总结

数组定义：数组是一个容器，用于在程序中存储一批同种类型的数据

## 五、方法

### 5.1 方法的概述、调用

**方法**：是一种语法结构，可以把一段代码封装成一个功能，以方便重复调用

**好处**：

- 提高代码的复用性
- 让程序的逻辑更清晰

方法定义的**完整格式**：  

```
修饰符  返回类型  方法名(形参列表){
	方法体代码（需要执行的功能代码）
	return 返回值;
}
```

```java
public static int add(int a, int b){
    int c = a+b;  //方法的执行代码
    return c;
}
```

调用格式：方法名(参数)；

注意事项：

1. 如果方法不需要返回结果，返回值类型必须声明成void(无返回值)，此时方法内部不可以使用return返回数据。
2. 方法如果没有参数，或者返回值类型声明为void可以称为无参数、无返回值的方法，依次类推

### 5.2常见问题

1. 方法的编写顺序无所谓。
2. 方法与方法之间是平级关系，不能嵌套定义。
3. 方法的返回值类型为void(无返回值),方法内则不能使用return返回数据，返回类型要与定义的类型一致。
4. return语句下面，不能编写代码，因为永远执行不到，属于无效代码
5. 方法不调用就不执行，调用时必须严格匹配方法的参数情况
6. 有返回值的方法调用时可以选择定义变量接收结果，或者直接输出调用，甚至直接调用，无返回值的调用只能直接调用一下。

### 5.3方法案例

####  5.3.1 定义方法的技巧，计算1-n的和

方法名称：自己取名，有意义，英文小写，驼峰模式

```java
//计算1-n的和
public static int sum(int n){
    int sum = 0 ;
    for(int i = 1;i<=n;i++){
        sum += i;
    }
    return sum;
}
//调用
int sum1 = sum(100);
System.out.println("1-100的和为"+sum1);
```

#### 5.3.2判断整数是偶数还是奇数

```java
public static void check(int n){
    if(n % 2 == 1){
        System.out.println(n+"是奇数")
    }else{
        System.out.println(n+"是偶数")
    }
}
//调用
check(100);
check(55);
```

#### 5.3.3数组求最值改方法实现

```java
public static int getArrayMaxData(int[] arrs){
    int max = arrs[0];
    for(int i = 1;i<arrs.length;i++){
        if(arrs[i]>max){
            max = arrs[i];
        }
    }
    return max;
}
```

### 5.4方法调用的内存图

- 方法没有被调用的时候，在方法区中的字节码文件中存放。
- 方法被调用的时候，需要进入到栈内存中运行。

![](.\images\2022-11-18.png)

### 5.5方法的参数传递机制

#### 5.5.1基本类型的参数传递

Java的参数传递机制：**值传递**

在传输实参给方法的形参的时候，并不是传输实参变量本身，而是传输实参变量中存储的值，这就是值传递 

**注意**：

- 实参：如在方法内部定义的变量
- 形参：如在定义方法时，"()"中所声明的参数

![](.\images\2022-11-18 (1).png)

#### 5.5.2引用类型的参数传递

![引用](.\images\2022-11-18 (2).png)

### 5.6方法的参数传递案例

#### 5.6.1打印数组内容

```java
public static void printArray(int[] arrs){
    System.out.print("[");
    if(arrs != null && arrs.length > 0){
        for(int i = 0 ; i<arrs.length;i++){
        	System.out.print(i == arrs.length ? arrs[i] : arrs[i] + ",");
    }
    }
    System.out.print("]");
}
```

#### 5.6.2从数组中查询元素的索引返回

```java
public static int searchIndex(int a,int[] arrs){
    for(int i=0;i<arrs.length;i++){
        if(a == arrs[i])
            return i;
    }
    return -1;
}
```

### 5.6.3比较两个数组内容是否相等

```java
public static boolean  equalsArrays(int[] arrs1,int arrs2){
    int length;
    if(arrs1.length == arrs2.length){
        for(int i = 0 ;i<length;i++){
        if(arrs1[i] != arrs2[i]){
            return false;
        }
    }
        return true;
   }else{
        return false;
    }
}
```

### 5.6方法重载

#### 5.6.1方法重载的形式、作用

**方法重载**：同一个类中，出现多个方法名称相同，但是形参列表是不同的，那么这些方法就是重载方法。

**作用**：可读性好，方法名称相同提示是同一类型的功能，通过形参不同实现功能差异化的选择，这是一种专业的代码设计

#### 5.6.2方法重载的识别技巧

```java
public static void open(){}
public static void open(int a){}
public static void open(int a, double b){}
public static void open(int a,int b){}
```

### 补充知识：return 关键字单独使用

return;  可以立即跳出并结束当前方法的执行；

return; 关键字单独使用可以放在任何

```java
public static void chu(int a, int b){
    if(b == 0){
        System.out.println("您的数据有误！！不执行");
        return; //直接结束当前方法chu
    }
    int c = a/b;
    System.out.println("除法结果是："+c);
}
```

## 6.编程训练案例

#### 6.1案例一：买飞机票

```java
/**
     * 买飞机票
     * 需求：机票价格按照淡季和旺季、头等舱和经济舱收费、输入机票原价、月份和头等舱或经济舱
     * 机票最终优惠价格的计算方案如下：旺季（5-10月）头等舱九折，经济舱8.5折
     * 淡季（11月到来年4月）头等舱7折，经济舱6.5折。
     * 分析：输入机票原价，仓位类型、月份，调用方法返回机票最终价格
     * 方法中要判断淡季和旺季，以及经济舱还是头等舱
     */
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入机票价格：");
        double price = sc.nextDouble();
        System.out.println("请输入仓位类型（头等舱或经济舱）：");
        String planetype = sc.next();
        System.out.println("请输入机票月份：");
        int month = sc.nextInt();
        price = planePrice(price,planetype,month);
        System.out.println("优惠后的价格为："+price);
    }
    public static double planePrice(double price,String planetype,int month){
        if (month>=5 && month <= 10){
            //旺季
            switch (planetype){
                case "头等舱":
                    price = 0.9*price;
                    break;
                case "经济舱":
                    price = 0.85*price;
                    break;
            }
        }else if (month==11 || month==12 || month>=1 && month<=4){
            //淡季
            switch (planetype){
                case "头等舱":
                    price = 0.7*price;
                    break;
                case "经济舱":
                    price = 0.65*price;
                    break;
            }
        }else{
            System.out.println("输入月份有误");
            price = -1;
        }
        return price;
    }
```

### 6.2找素数

```java
/**
     * 找素数
     * 素数：除了1和本身，不能被其他正整数整除，就叫素数
     * 分析：
     * 101-200之间的数据可以采用循环依次拿到；每拿一个数，判断该数是否是素数
     * 判断规则：从2开始遍历到该数的一半的数据，看是否有数据可以整除它，有则不是素数
     */
    public static void main(String[] args) {
        isSushu();
    }
    public static void isSushu(){

        for (int i = 101;i<= 200;i++){
            //信号位：标记
            int flag = 1; //假设一开始是素数
            for (int j = 2;j< i/2;j++){
                if (i%j == 0){
                    flag = 0; //不是素数
                    break;
                }
            }
            if (flag == 1){
                System.out.print(i+" ");
            }
        }
    }
```

### 6.2产生验证码

```java
/**
 * 开发验证码
 * 需求：定义方法实现随机产生一个5位验证码，每位可能是数字，大小写字母
 * 分析：
 * ①定义一个方法，生成验证码返回：方法参数是位数，返回值类型为String
 * ②在方法内部使用for循环生成指定位数的随机字符，并连接起来
 * ③把连接好的随机字符作为一组验证码返回
 */
public static void main(String[] args) {
    //生成一个5位数的随机验证码
    String code = createCode(5);
    System.out.println(code);
}
public static String createCode(int n){
    Random random = new Random();
    String code = "";
    for (int i = 0; i < n; i++) {
        //生成一个随机字符
        int type = random.nextInt(3);
        switch (type){
            case 0:
                //生成大写字符
                char ch = (char)(random.nextInt(26)+65);
                code += ch;
                break;
            case 1:
                //生成小写字符
                char ch1 = (char)(random.nextInt(26)+97);
                code  += ch1;
                break;
            case 2:
                //生成数字
                int a = random.nextInt(10);
                code += a;
                break;
        }
    }
    return code;
}
```

### 6.4数组的复制

```java
public static void main(String[] args) {
    /**
     * 数组元素的复制
     * 需求：把一个数组中的元素复制到另一个新的数组中
     * 分析：需要动态初始化一个数组，长度与原数组一样
     */
    int[] arr1 = new int[5];
    Scanner sc = new Scanner(System.in);
    for (int i =0;i<arr1.length;i++){
        System.out.println("请输入数组的第"+(i+1)+"个元素的值");
        arr1[i] = sc.nextInt();
    }
    int[] arr2 = new int[arr1.length];
    copyArray(arr1,arr2);
    System.out.print("[");
    for (int i =0;i<arr2.length;i++){
        System.out.print(i == arr2.length-1 ? arr2[i] : arr2[i]+",");
    }
    System.out.print("]");
}
public static void copyArray(int[] arr1,int[] arr2){
    for (int i = 0; i<arr1.length;i++){
        arr2[i] = arr1[i];
    }
}
```

### 6.5评委打分案例

```java
public static void main(String[] args) {
    /**
     * 评委打分案例
     * 需求：在唱歌比赛中，有六位评委打分，分数范围0-100，选手最后得分：去掉最高分、最低分后的平均分
     * 分析：把6位评委的分数录入到程序中----使用数组
     * 遍历数组中每个元素，找出最大值最小值，后进行累加
     */
    int[] arr = new int[6];
    Scanner sc = new Scanner(System.in);
    for (int i = 0; i < arr.length; i++) {
        System.out.println("请输入第"+(i+1)+"评委的分数：");
        arr[i] = sc.nextInt();
    }
    System.out.println("平均分为："+average(arr));
}
public static double average(int[] arr){
    int max= arr[0];
    int min = arr[0];
    double average;
    int sum = 0;
    for (int i = 0; i < arr.length; i++) {
        if (arr[i]>max){
            max = arr[i];
        }
        if (arr[i]<min){
            min = arr[i];
        }
        sum += arr[i];
    }
    average = (sum-max-min)/(arr.length-2);
    return average;
}
```

### 6.6数字加密

```java
public static void main(String[] args) {
    /**
     * 数字加密
     * 需求：1983，采用加密方式进行传输，规则如下
     * 先得到每位数，然后每位数都加上5，再对10求余，最后将所有数字反转，得到一个新数
     */
    Scanner sc = new Scanner(System.in);
    System.out.println("请输入需要加密的数字个数：");
    int num = sc.nextInt();
    int[] arr = new int[num];
    for (int i = 0; i < arr.length; i++) {
        System.out.println("请输入第"+(i+1)+"数字为:");
        arr[i] = sc.nextInt();
    }
    int[] arr1 = secreat(arr);
    for (int i = 0; i < arr1.length; i++) {
        System.out.print(arr1[i]);
    }
}
public static int[] secreat(int[] arr){
    for (int i = 0; i < arr.length; i++) {
        arr[i] = (arr[i] + 5)%10;
    }
    for (int i = 0,j = arr.length-1; i<j; i++,j--) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
    return arr;
}
```

### 6.7双色球系统

```java
public static void main(String[] args) {

    /**
     * 双色球系统-业务分析、随机生成一组中将号码
     * 投注号码由6个红色球号码和1个蓝色球号码组成，红色号码从1-33中选择
     * 蓝球号码从1-16中选择；
     */
    int[] userNumbers = userInputNumbers();
    int[] luckNumbers = createLuckNumebers();

    judge(luckNumbers,userNumbers);
}
public static int[] createLuckNumebers(){
    //随机产生6个红球号码，不重复
    int[] ball = new int[7];
    Random random = new Random();
    for (int i = 0;i<6;i++){
        while (true){
            int data = random.nextInt(33)+1;
            int flag = 0; //假设0为不重复，1为重复
            for (int j = 0;j<i;j++){
                if (ball[i] == ball[j]){
                    flag = 1;
                    break;
                }
            }
            if (flag == 0){
                ball[i] = data;
                break;
            }
        }
    }
    ball[6] = random.nextInt(16)+1;
    System.out.print("[");
    for (int i = 0; i < ball.length; i++) {
        System.out.print(i==ball.length-1 ? ball[i] : ball[i]+",");
    }
    System.out.print("]");
    return ball;
}
public static int[] userInputNumbers(){
    int[] numbers = new int[7];
    Scanner sc = new Scanner(System.in);
    for (int i = 0; i < numbers.length-1; i++) {
        System.out.println("请输入第"+(i+1)+"个红球号码(1-33),要求不重复：");
        numbers[i] = sc.nextInt();
    }
    System.out.println("请输入蓝球号码(1-16):");
    numbers[6] = sc.nextInt();
    return numbers;
}
public static void judge(int[] luckNumbers, int[] userNumbers){
    int count1 = 0;
    int count2 = 0;
    for (int i = 0; i < luckNumbers.length-1; i++) {
        for(int j = 0;j < userNumbers.length-1;j++){
            if (luckNumbers[i] == userNumbers[j]){
                count1+=1;
                break;//若是有重复也只会有一个，因为每个红球的号码不同
            }
        }
    }
    if (luckNumbers[6] == userNumbers[6]){
        count2++;
    }
    System.out.println("中了"+count1+"个红球,"+count2+"个蓝球");
}
```

## 7.面向对象

### 7.1面向对象：概述

通俗来说：面向就是找或拿，对象就是东西，面向对象编程就是找或拿东西过来编程。

找对象或者设计对象来解决问题

### 7.2面向对象：设计对象、注意事项

**设计类，创建对象并使用**

- 类：对象共同特征的描述
- 对象：真实存在的具体实例

先设计类，才能够创建对象

```java
public class 类名{
    //1.成员变量（代表属性，一般是名词）
    //2.成员方法（代表行为，一般是动词）
    //3.构造器
    //4.代码块
    //5.内部类
}
```

```java
//汽车类
public class Car {
    String name;
    double price;
    public void start(){
        System.out.println(name+"启动了");
    }
    public void run(){
        System.out.println("价格是："+price+"的"+name+"跑得快");
    }
}
```

```java
public class work01 {
    public static void main(String[] args) {
        Car car = new Car();
        car.name = "奔驰";
        car.price = 1000000;
        car.start();
        car.run();
    }
}
```

**定义类的几个补充注意事项**

- 类名首字母建议大写，且有意义，满足“驼峰模式”
- 一个Java文件中可以定义多个class类，但只能一个类是public修饰，而且public修饰的类名必须称为代码文件名，**实际开发建议一个文件定义一个class类。**
- 成员变量的完整定义格式为：**修饰符 数据类型 变量名称=初始化值**；一般无需指定初始化值，存在默认值。

![](.\images\2022-11-22.png)

### 7.3面向对象：内存机制

#### 7.3.1对象在内存中的运行机制

**多个对象的内存图**

![](.\images\QQ图片20221122145646.png)

![](.\images\QQ截图20221122150236.png)

**两个变量指向同一个对象内存图**

![](.\images\QQ截图20221122151725.png)

**垃圾回收**

**注意：**当堆内存中的对象，没有被任何变量引用（指向）时，就会被判定为内存中的“垃圾”. 

**Java存在自动垃圾回收器，会定期进行清理**

### 7.4面向对象实战：购物车案例

- 需求分析、框架搭建

需求：模拟购物车模块的功能，需要实现添加商品到购物车中去，同时需要修改商品的购买数量，结算商品价格功能。

分析：

- 购物车中的每个商品都是一个对象，需要定义一个商品类
- 购物车本身也是一个对象；可以使用数组对象去代表它
- 完成界面架构，让用户选择操作的功能。

需要完成的功能

- 添加商品到购物车 ：add
- 查看购物车信息：query
- 修改商品信息：update
- 结算金额：pay

```java
public class Goods {
    int id; //商品编号
    String name; //商品名称
    int count; //商品数量
    double price; //商品价格
}
```

```java
public class ShopCarTest {
    public static void main(String[] args) {
        //1.定义商品类，用于后期创建商品

        //2.定义购物车对象，使用数组来表示（后期用集合）
        Goods[] shopCar = new Goods[100];
        //3.搭建操作架构
        //添加商品到购物车 ：add
        //查看购物车信息：query
        //修改商品信息：update
        //结算金额：pay
        while (true){
            System.out.println("请您选择如下命令进行操作：");
            System.out.println("1.添加商品到购物车");
            System.out.println("2.查看购物车信息");
            System.out.println("3.修改商品信息");
            System.out.println("4.结算金额");
            Scanner sc = new Scanner(System.in);
            System.out.print("请输入您的选择：");
            int command = sc.nextInt();
            switch (command){
                case 1:
                    addGoods(shopCar);
                    break;
                case 2:
                    queryGoods(shopCar);
                    break;
                case 3:
                    updateGoods(shopCar);
                    break;
                case 4:
                    payGoods(shopCar);
                    break;
                default:
                    System.out.println("没有该选择功能");
                    return;
            }
        }
    }
    //增加商品
    public static void addGoods(Goods[] shopCar){
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入您所需购买的商品编号（不可重复）：");
        int id = sc.nextInt();
        System.out.println("请输入您所需购买商品的名称");
        String name = sc.next();
        System.out.println("请入您的价格：");
        double price = sc.nextDouble();
        System.out.println("请输入您需要购买的数量：");
        int count = sc.nextInt();
        Goods goods1 = new Goods();
        goods1.id = id;
        goods1.name = name;
        goods1.price = price;
        goods1.count = count;
        for (int i = 0; i < shopCar.length; i++) {
            if (shopCar[i]==null){
                shopCar[i] = goods1;
                break;
            }
        }
        System.out.println("添加商品成功!");
    }
    //查看商品信息
    public static void queryGoods(Goods[] shopCar){
        System.out.println("编号\t\t名称\t\t价格\t\t数量\t\t");
        for (int i = 0; i < shopCar.length; i++) {
            if (shopCar[i] != null){ System.out.println					(shopCar[i].id+"\t\t"+shopCar[i].name+"\t\t"+shopCar[i].price+"\t\t"+shopCar[i].count);
            }
            else {
                break;
            }
        }
    }
    //修改商品
    public static void updateGoods(Goods[] shopCar){
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入您需要修改商品的编号：");
        int id = sc.nextInt();
        Goods goods = getGoodsById(shopCar,id);
        int choose;
        while (true){
            if (goods == null){
                System.out.println("无该商品");
            }else {
                //存在该商品
                System.out.println("1.修改编号");
                System.out.println("2.修改名称");
                System.out.println("3.修改价格");
                System.out.println("4.修改数量");
                System.out.println("请输入您需要修改的内容选项");
                choose = sc.nextInt();
                switch (choose){
                    case 1:
                        System.out.println("请输入修改后的编号：");
                        int changeId = sc.nextInt();
                        goods.id = changeId;
                        break;
                    case 2:
                        System.out.println("请输入修改后的名称：");
                        String changeName = sc.next();
                        goods.name = changeName;
                        break;
                    case 3:
                        System.out.println("请输入修改后的价格：");
                        double changePrice = sc.nextDouble();
                        goods.price = changePrice;
                        break;
                    case 4:
                        System.out.println("请输入修改后的数量");
                        int changeCount = sc.nextInt();
                        goods.count = changeCount;
                        break;
                    default:
                        System.out.println("没有该选择功能");
                }
                System.out.println("修改成功");
                break;
            }
        }

    }
    public static Goods getGoodsById(Goods[] shopCat,int id){
        for (int i = 0; i < shopCat.length; i++) {
            if (shopCat[i]!=null){
                if (shopCat[i].id == id){
                    return shopCat[i];
                }
            }else {
                return null;
            }
        }
        return null;
    }
    public static void payGoods(Goods[] shopCar){
        int totalPrice = 0;
        for (int i = 0; i < shopCar.length; i++) {
            if (shopCar[i] !=null){
                totalPrice += shopCar[i].price*shopCar[i].count;
            }else {
                break;
            }
        }
        System.out.println("商品总价为："+totalPrice);
    }

}
```

### 7.5面向对象：构造器、this

目的：

- 真正知道对象具体通过调用什么代码得到的
- 能够掌握为对象赋值的其他简便写法
- 为以后学习面向对象编程的其他内容做支撑

构造器的作用：定义在类中，可以用于初始化一个类的对象，并返回对象的地址。

- 无参构造器（默认存在）：初始化对象时，成员变量的数据均采用默认值
- 有参构造器：在初始化对象时，同时可以接收参数为对象进行赋值

```java
public class Car {
    String name;
    double price;
    public Car(){
        System.out.println("无参构造器");
    }
    public Car(String name,double price){
        this.name = name;
        this.price = price;
        System.out.println("调用了有参构造器");
    }
}
```

**this关键字**：用于指定访问当前对象的成员变量、成员方法

- 可以出现在构造器、方法中
- 代表当前对象的地址

### 7.6面向对象：封装

**封装**：

面向对象的三大特征：封装、继承、多态

封装：告诉我们，如何正确设计对象的属性和方法

封装的原则：对象代表什么，就得封装对应的数据，并提供数据对应的行为。

比如人画圆，画draw这个行为是圆的行为，而不是人的行为

**如何进行封装更好？**

- 一般建议对应成员变量使用private(私有、隐藏)关键字进行修饰（private修饰的成员只能在当前类中访问）
- 为每个成员变量提供配套public修饰的getter、setter方法暴露其取值和赋值

### 7.7面向对象：Javabean、综合案例

JavaBean：也可以称为实体类，其对象可以用于在程序中封装数据。

标准JavaBean须满足如下书写要求：

- 成员变量使用private修饰
- 提供成员变量对应的setXxx()/getXxx()方法
- 必须提供一个无参构造器；有参构造器是可写可不写的。

**成员变量和局部变量的区别**

|              | 成员变量                                   | 局部变量                                       |
| ------------ | ------------------------------------------ | ---------------------------------------------- |
| 类中位置不同 | 类中、方法外                               | 常见于方法中                                   |
| 初始化值不同 | 有默认值，无需初始化                       | 没有默认值，使用之前需要完成赋值               |
| 内存位置不同 | 堆内存                                     | 栈内存                                         |
| 生命周期不同 | 随着对象的创建而存在，随之对象的消失而消失 | 随着方法的调用而存在，随着方法的运行结束而消失 |
| 作用域       |                                            | 在所属的大括号内                               |

综合案例

```java
public class Movipublic class Movie {
    private String name;
    private double score;
    private String actor;
    public Movie() {
    }
    public Movie(String name, double score, String actor) {
        this.name = name;
        this.score = score;
        this.actor = actor;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public double getScore() {
        return score;
    }
    public void setScore(double score) {
        this.score = score;
    }
    public String getActor() {
        return actor;
    }
    public void setActor(String actor) {
        this.actor = actor;
    }
}e{
    public Movie()
}
```

```java
public static void main(String[] args) {
    Movie[] movies = new Movie[3];
    movies[0] = new Movie("长津湖",9.4,"吴京");
    movies[1] = new Movie("我和我的父亲",8.5,"吴京");
    movies[2] = new Movie("濮水少年",7.8,"王传");
    for (int i = 0; i < movies.length; i++) {
        System.out.println("电影名称："+movies[i].getName());
        System.out.println("得分："+movies[i].getScore());
        System.out.println("作者："+movies[i].getActor());
        System.out.println("--------------------------");
    }
}
```

## 8.String、ArrayList

**String**简单介绍：String类定义的变量可以用于存储字符串，同时String类提供了很多操作字符串的功能，可以直接使用。

关于String要学的内容：

1. String定义变量存储字符串：需要知道如何创建字符串对象，并使用String定义变量指向该字符串对象。
2. String的内存原理：字符串对象在内存中的原理是怎样的，能够解决一些字符串常见面试题。
3. String提供了哪些API：能够说出并使用String类提供的操作字符串的功能：遍历、替换、截取、相等、包含
4. String解决实际案例：能够利用String的常用API去解决实际场景的业务需求，真正做到学以致用

**ArrayList**简单介绍：

- ArrayList代表的是集合类，集合是一种容器，与数组类似，不同的是集合大小是不固定的。
- 通过创建ArrayList的对象表示得到一个集合容器，同时ArrayList提供了比数组更好用，更丰富的API功能给程序员使用。

关于ArrayList类需要学习的内容：

- ArrayList集合如何创建对象：知道如何利用ArrayList创建对象来代表集合容器来存放数据。
- ArrayList常用API：能够说出并使用ArrayList类提供的丰富的元素操作功能：如添加、获取、删除、修改等功能。
- ArryList存储自定义对象：能够使用ArrayList存储自定义的对象，并清楚ArrayList集合存储对象的底层原理
- ArrayList解决实际问题：能够使用ArrayList存储对象并完成数据搜索，删除等常见业务需求。

### 8.1String

### 8.1.1String概述

java.lang.String 类代表字符串，String类定义的变量可以用于指向字符串对象，然后操作该字符串

提出问题：String其实常被称为不可变字符串类型，在被创建后不能被更改。

但是

```java
String name = "传智";//(在字符串常量池中)
name +="教育";  //输出是传智教育  （运算出来的，在堆内存中）
```

问题：这不明显被更改了吗？

字符串对象存储的位置：以""方式给出的字符串对象，在字符串常量池中存储（字符串常量池在堆内存里面）

没有改变的原因：创建出来在字符串常量池中的对象并没有改变，改变的只是堆内存（常量池外）的对象

- String变量每次的修改其实都是产生并指向了**新的字符串对象**。
- 原来的字符串对象都是没有改变的，所以称不可变字符串。

![](.\images\QQ截图20221123202737.png)

![](.\images\QQ截图20221123203042.png)

### 8.1.2String类创建对象的两种方式

方式：

- 直接使用""定义
- 通过String类的构造器来创建对象

![](.\images\QQ截图20221123203530.png)

```java
![QQ截图20221123205104](D:\mybatis笔记\images\QQ截图20221123205104.png)public class StringDemo {
    public static void main(String[] args) {
        //方式一：直接定义
        String name = "我爱你中国";
        System.out.println(name);
        //方式二
        //public String():创建一个空白字符串对象，不包含任何内容（几乎不用）
        String s1 = new String();
        System.out.println(s1); // 空白字符串
        //public String(String):根据传入的字符串内容来创建字符串对象(几乎不用)
        String s2 = new String("我爱你北京");
        System.out.println(s2);
        //public String(char[] c):根据字符数组的内容，来创建字符串对象
        char[] c = {'a','b','中','国'};
        String s3 = new String(c);//该构造器默认连接字符
        System.out.println(s3);
        //public String(byte[] b):根据字符数组的内容，来创建字符串对象
        byte[] b = {97,98,99,65};
        String s4 = new String(b);
        System.out.println(s4);
    }
}
```

**有什么区别吗？**

- 以""方式给出的字符串对象，在字符串常量池中存储，而且相同内容只会在其中存储一份。
- 通过构造器new对象，每new一次都会产生一个新对象，放在堆内存中

![](.\images\QQ截图20221123205104.png)

![](.\images\QQ截图20221123205245.png)

**字符串对象特点：**

- 双引号创建的字符串对象，在字符串常量池中存储同一个
- 通过new构造器创建的字符串对象，在堆内存中分开存储。

### 8.1.3String类常见的面试题

![](.\images\QQ截图20221123210419.png)

因为""创建出来的放在字符串常量池，而new出来的放在堆内存中，所以第一行会创建出两个对象出来，而第二行没有创建对象，因为直接指向字符串常量池中的abc。

结果为false：s2结果指向堆内存，而s1结果指向常量池。

![](.\images\QQ截图20221123210852.png)

结果为false，地址不一样，s1指向字符串常量池中的abc，而s3指向堆内存中的abc

![](.\images\QQ截图20221123210936.png)

结果为true(java存在编译优化机制，程序在编译时："a"+"b"+"c"会直接转成"abc")

### 8.1.4String类常用API-字符串内容比较

**字符串的内容比较：**

- 推荐使用String类提供的"equals"比较：只关心内容一样即可

![](.\images\QQ截图20221123212253.png)

```java
public class StringEqualsDemo3 {
    public static void main(String[] args) {
        //1.正确登录名和密码
        String okName = "yyue";
        String okPassword = "123456";
        Scanner sc = new Scanner(System.in);
        System.out.println("请您输入登录名称：");
        String name = sc.next();
        System.out.println("登录密码：");
        String password = sc.next();
        if (okName.equals(name) && okPassword.equals(password)){
            System.out.println("正确");
        }else {
            System.out.println("失败");
        }

        //忽略大小写比较内容的API：一般用于比较验证码这样的业务逻辑
        String sysCode = "23AdFh";
        String code1 = "23adfh";
        System.out.println(sysCode.equalsIgnoreCase(code1)); //true
    }
}
```

### 8.1.5String类常用API-遍历、替换、截取、分割操作

![](.\images\QQ截图20221123213224.png)

```java
public class StringAPIDemo4 {
    public static void main(String[] args) {
        String name = "abcd";
        for (int i = 0; i < name.length(); i++) {
            System.out.println(name.charAt(i));
        }
        System.out.println("---------------");
        System.out.println(name.length());
        System.out.println(name.charAt(1));
        System.out.println("---------------");
        char[] chars = name.toCharArray();
        for (int i = 0; i < chars.length; i++) {
            System.out.println(chars[i]);
        }
        System.out.println("-------------------");
        System.out.println(name.substring(1,3));
        System.out.println(name.substring(1));
        System.out.println(name.replace("d","e"));
        System.out.println(name.contains("a"));
        String name1 = "a,b,c,d";
        String[] newName = name1.split(",");
        for (int i = 0; i < newName.length; i++) {
            System.out.println(newName[i]);
        }
    }
}
```

### 8.1.6String案例

#### 案例1：String类开发验证码功能

```java
public class Judge {
    public static void main(String[] args) {
        /**
         * 需求：随机产生一个5位的验证码，每位可能是数字，大写字母、小写字母
         * 分析：
         * 定义一个String类型的变量存储a-zA-Z0-9之间的全部字符
         * 循环5次，随机一个范围内的索引，获取对应字符连接起来即可
         */
        String datas = "0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";
        String data ="";
        Random random = new Random();
        for (int i = 0; i < 5; i++) {
            int index = random.nextInt(datas.length());
            data += datas.charAt(index);
        }
        System.out.println(data);
    }
}
```

#### 案例2：模拟用户登录功能

```java
public class Login {
    public static void main(String[] args) {
        /**
         * 需求：模拟用户登录功能，最多给三次机会
         * 分析：
         * 系统后台定义好正确的登录名称，密码
         * 使用循环控制三次，让用户输入正确的登录名和密码，判断是否登录成功，登录成功则不再进行登录，登录失败给出提示，并让用户继续登录
         *
         */
        String okLoginName = "admin";
        String okPassword = "123456";
        Scanner sc = new Scanner(System.in);
        //定义一个循环循环三次输入
        for (int i = 0; i < 3; i++) {
            System.out.println("请输入登录名：");
            String name = sc.next();
            System.out.println("请输入密码");
            String password = sc.next();
            if(name.equals(okLoginName)){
                if (password.equals(okPassword)){
                    System.out.println("登录成功");
                    break;
                }else {
                    System.out.println("密码错误");
                }
            }else {
                System.out.println("用户名错误");
            }
        }
    }
}

```

#### 案例3：手机号码屏蔽

```java
public class Phone {
    public static void main(String[] args) {
        /**
         * 需求：以字符串的形式从键盘接受一个手机号，将中间四位号码屏蔽
         * 分析：
         * 键盘录入一个字符串，用Scanner实现
         * 截取字符串前三位，截取字符串后四位
         * 将截取后的两个字符串，中间加上****进行拼接，输出即可
         */
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入手机号：");
        String phone = sc.next();
        String phone1 = phone.substring(0,3);
        String phone2 = phone.substring(7);
        String result = phone1+"****"+phone2;
        System.out.println(result);
    }
}
```

### 8.2ArrayList

### 8.2.1集合概述

集合：与数组类似，是一种容器，用于装数据

数组特点：数组定义完成并启动后，数组的类型、长度都是固定的了，所以存在问题，在个数不确定的情况下，要进行增删数据操作时，数组是不太合适的。

集合：大小不固定，启动后可以动态变化，类型也可以选择不固定，

- 非常适合做元素不确定，且要进行增删操作的业务场景
- 集合提供了许多丰富、好用的功能，而数组的功能相对单一

### 8.2.2ArrayList集合快速入门

```java
public class ArrayListDemo {
    public static void main(String[] args) {
        //创建ArrayList集合对象
        ArrayList arrayList = new ArrayList();
        arrayList.add(1);
        arrayList.add(2);
        arrayList.add("a");
        arrayList.add("Java");
        System.out.println(arrayList); // 结果并不是地址，而是内容
    }
}
```

### 8.2.3ArrayList对于泛型的支持

泛型概述：

- ArrayList<E>:其实是一个泛型类，可以在编译阶段约束集合对象只能操作某种数据类型

举例：

ArrayList<String>:此集合只能操作字符串类型的元素

ArrayList<Integer>:此集合只能操作整数类型的元素

```java
//确定数据类型
ArrayList<String> arrayList1 = new ArrayList<>(); //后面的数据类型可以不写
arrayList1.add("我");
arrayList1.add("爱");
arrayList1.add("中国");
System.out.println(arrayList1);
```

### 8.2.4ArrayList常用API、遍历

![](.\images\QQ截图20221124150857.png)

```java
System.out.println(arrayList1.get(1)); //根据索引查找元素
        System.out.println(arrayList1.size());//元素个数
//        System.out.println(arrayList1.remove(0));//根据索引删除
//        System.out.println(arrayList1);
        System.out.println(arrayList1.remove("我"));//根据内容删除
        System.out.println(arrayList1);
        System.out.println(arrayList1.set(0,"我爱"));//根据索引创建值
        System.out.println(arrayList1);
        for (int i = 0; i < arrayList1.size(); i++) {//遍历集合
            System.out.println(arrayList1.get(i));
        }
```

### 8.2.5ArrayList集合案例：遍历并删除元素

从集合中遍历元素，并筛选出元素删除它，解决方案：

- 从集合后面遍历然后删除，可以避免漏掉元素
- 或者每删除一个元素后，i退一步

```java
public class ArrayListDemo2 {
    public static void main(String[] args) {
        /**
         * 需求：
         * 某个班级的考试在系统上进行，成绩大致为：98，77，66，89，79，50，100
         * 现在需要把成绩低于80分以下的数据去掉。
         * 分析：
         * 定义ArrayList集合存储多名学员的成绩
         * 遍历集合每个元素，如果元素值低于80分，去掉它
         */
        ArrayList<Integer> scores = new ArrayList<>();
        scores.add(98);
        scores.add(77);
        scores.add(66);
        scores.add(89);
        scores.add(79);
        scores.add(50);
        scores.add(100);
        System.out.println(scores);
        //有错误的代码，因为删除一个元素时，后一个元素会补上来，但是下次循环是从该元素后开始循环
//        for (int i = 0; i < scores.size() ; i++) {
//            if (scores.get(i)<80){
//                scores.remove(i);
//            }
//        }
        //正确代码一：倒着删除
        for (int i = scores.size()-1; i >= 0 ; i--) {
            if (scores.get(i)<80){
                scores.remove(i);
            }
        }
        System.out.println(scores);
        //正确代码二：每删成功时，i--，元素退一步
        for (int i = 0; i < scores.size() ; i++) {
            if (scores.get(i)<80){
                scores.remove(i);
                i--;
            }
        }
        System.out.println(scores);
    }
}
```

### 8.2.6ArrayList集合案例：存储自定义类型

比如学生、老师、商品等对象就是自定义类型对象

集合中存储的元素并不是对象本身而是对象的地址

```java
public class Test {
    public static void main(String[] args) {
        /**
         * 需求：
         * 某影院系统需要在后台存储上述三部电影，然后依次展示出来
         * 分析：
         * 定义一个电影类，定义一个集合存储电影对象
         * 创建3个电影对象，封装相关数据，把3个对象存入到集合中去
         * 遍历集合中的3个对象，输出相关信息
         */
        Movie movie1 = new Movie("《肖申克的救赎》",8.9,"罗宾斯");
        Movie movie2 = new Movie("《霸王别姬》",8.4,"张国荣");
        Movie movie3 = new Movie("《阿甘正传》",9.5,"汤姆");
        ArrayList<Movie> movies = new ArrayList<>();
        movies.add(movie1);
        movies.add(movie2);
        movies.add(movie3);
        for (int i = 0; i < movies.size(); i++) {
            System.out.println(movies.get(i).getName());
            System.out.println(movies.get(i).getScore());
            System.out.println(movies.get(i).getActor());
            System.out.println("------------------");
        }
    }
```

### 8.2.7ArrayList集合案例：元素搜索

```java
public class StudentTest {
    public static void main(String[] args) {
        /**
         * 案例：学生信息系统的数据搜索
         * 需求：后台程序需要存储如上学生信息并展示，然后要提供按照学号搜索学生信息的功能
         * 分析：
         * 定义一个Student类，定义ArrayList集合存储如上学生对象信息，并遍历展示出来
         * 提供一个方法，可以接受ArrayList集合，和要搜索的学号，返回搜索到学生对象信息，并展示
         * 使用死循环，使用户可以不同的搜索
         */
        ArrayList<Student> students = new ArrayList<>();
        students.add(new Student("20180301","叶古城",23,"护理一班"));
        students.add(new Student("20180302","东方不败",23,"推拿二班"));
        students.add(new Student("20180303","西门",23,"中药学四班"));
        students.add(new Student("20180304","yyue",23,"神经科2班"));
        System.out.println("学号\t\t\t姓名\t\t年龄\t班级");
        for (int i = 0; i < students.size(); i++) {
            System.out.println(students.get(i).getId()+"\t\t"+students.get(i).getName()+"\t\t"+students.get(i).getAge()+"\t\t"+students.get(i).getStudentClass());
        }

        Scanner sc = new Scanner(System.in);
        while (true){
            System.out.println("请输入需要查询学生的学号");
            String id = sc.next();
            Student student = queryById(students,id);
            if (student!=null){
                System.out.println("学号："+student.getId());
                System.out.println("姓名："+student.getName());
                System.out.println("年龄："+student.getAge());
                System.out.println("班级："+student.getStudentClass());
            }else {
                System.out.println("查无此人");
            }
        }
    }
    /**
     * 按照id查询学生信息
     * @param students  存储全部学生对象的集合
     * @param id  搜索学生的学号
     * @return 学生对象/null
     */
    public static Student queryById(ArrayList<Student> students,String id){
        for (int i = 0; i < students.size(); i++) {
            if (students.get(i).getId().equals(id)){
                return students.get(i);
            }
        }
        return null;
    }
}
```

### 9.综合案例：ATM系统

```java
package com.yyue.ATMDemo;

import com.sun.org.apache.xerces.internal.impl.xs.SchemaNamespaceSupport;

import java.util.ArrayList;
import java.util.Random;
import java.util.Scanner;

public class ATMSystem {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        //创建一个集合对象，用于后期存入账号对象
        ArrayList<Account> accounts = new ArrayList<>();
        System.out.println("======欢迎您进入yyue的ATM系统=======");
        while (true){
            System.out.println("1.登录账户");
            System.out.println("2.注册账户");
            System.out.println("请您选择操作：");
            int command = sc.nextInt();
            switch (command){
                case 1:
                    //登录操作
                    login(accounts,sc);
                    break;
                case 2:
                    //注册账户
                    register(accounts,sc);
                    break;
                default:
                    System.out.println("您输入的操作命令不存在");
            }
        }

    }

    /**
     * 用户登录
     * @param accounts
     * @param sc
     */
    public static void login(ArrayList<Account> accounts,Scanner sc){
        System.out.println("=======欢迎您进入登录操作======");
        if (accounts.size() == 0){
            System.out.println("当前系统无任何账户，请先注册再登录！");
            return;//卫语言风格，解决方法的执行
        }
        while (true){
            System.out.println("请您输入登录的卡号：");
            String id = sc.next();
            Account account = getAccountByCardId(id,accounts);
            if (account != null){
                while (true){
                    System.out.println("请您输入登录的密码");
                    String passWord = sc.next();
                    //密码正确，办理业务
                    if (passWord.equals(account.getPassword())){
                        takeService(account,sc,accounts);
                        return;
                    }else {
                        System.out.println("密码错误");
                    }
                }
            }else {
                System.out.println("对不起，系统中不存在该账户卡号--");
            }
        }
    }

    /**
     * 用户注册
     * @param accounts
     * @param sc
     */
    public static void register(ArrayList<Account> accounts,Scanner sc){
        System.out.println("=====欢迎您进入到开户操作=====");
        System.out.println("请您输入账户名称：");
        String registerName = sc.next();
        //创建一个新的账户信息
        Account account = new Account();
        account.setName(registerName);
        while (true){
            System.out.println("请你输入账户密码：");
            String registerPassword = sc.next();
            System.out.println("请您输入确认密码：");
            String okPassword = sc.next();
            //若确认密码不正确
            if (okPassword.equals(registerPassword)){
                account.setPassword(okPassword);
                break;
            }else {
                System.out.println("两次输入密码不一致！");
            }
        }
        System.out.println("请您设置当前取现额度：");
        double quatoMoney = sc.nextDouble();
        account.setQuotaMoney(quatoMoney);
        String registerId = createId(accounts);
        account.setId(registerId);
        accounts.add(account);
        System.out.println("恭喜您，"+registerName+"先生/女士,您开户完成，您的卡号是"+registerId);
    }

    /**
     * 随机创建一个卡号id
     * @return  String
     */
    public static String createId(ArrayList<Account> accounts){
        Random random = new Random();
        while (true){
            String datas = "";
            for (int i = 0; i < 8; i++) {
                int data = random.nextInt(10);//产生9个0-9随机数
                datas += data;
            }
            Account account = getAccountByCardId(datas,accounts);
            if (account == null){
                //说明卡号未重复
                return datas;
            }
        }


    }

    /**
     * 根据卡号查账户信息
     * @param id
     * @param accounts
     * @return
     */
    public static Account getAccountByCardId(String id,ArrayList<Account> accounts){
        for (int i = 0; i < accounts.size(); i++) {
            if (id.equals(accounts.get(i).getId())){
                return accounts.get(i);
            }
        }
        return null;
    }

    /**
     *
     * @param account
     * @param sc
     */
    public static void takeService(Account account,Scanner sc,ArrayList<Account> accounts){
        System.out.println("=====欢迎您进入到操作界面=====");
        while (true){
            System.out.println("1.查询");
            System.out.println("2.存款");
            System.out.println("3.取款");
            System.out.println("4.转账");
            System.out.println("5.修改密码");
            System.out.println("6.退出");
            System.out.println("7.注销账户");
            System.out.println("请您输入操作命令：");
            int command = sc.nextInt();
            switch (command){
                case 1:
                    query(account);
                    break;
                case 2:
                    //存款
                    store(account,sc);
                    break;
                case 3:
                    //取款
                    drawMoney(account,sc);
                    break;
                case 4:
                    //转账
                    transMoney(account,sc,accounts);
                    break;
                case 5:
                    //修改密码
                    changePassword(account,sc);
                    return;
                case 6:
                    //退出
                    System.out.println("退出成功!");
                    return;//让当前方法停止
                case 7:
                    if (destroyUser(account,accounts,sc)){
                        return;
                    }
                    else {
                        break;
                    }
                default:
                    System.out.println("您输入的操作命令不正确---");
            }
        }

    }

    /**
     * 注销用户
     * @param account
     */
    private static boolean destroyUser(Account account,ArrayList<Account> accounts,Scanner sc) {
        //注销账户
        boolean flag = false;
        System.out.println("您真的要注销用户？y/n");
        String rs = sc.next();
        switch (rs){
            case "y":
                if (account.getMoney()>0){
                    System.out.println("您的账户还有余额，注销失败");
                }else {
                    accounts.remove(account);
                    System.out.println("您的账户注销成功");
                    flag = true;
                }
                break;
            default:
                System.out.println("当前账户保留");
        }
        return flag;
    }

    /**
     * 修改密码
     * @param account
     * @param sc
     */
    private static void changePassword(Account account, Scanner sc) {
        System.out.println("=====用户密码修改=====");
        while (true){
            System.out.println("请输入当前密码");
            String passWord = sc.next();
            //1.判断密码是否正确
            if (passWord.equals(account.getPassword())){
                while (true) {
                    System.out.println("请输入新密码：");
                    String okPassWord = sc.next();
                    System.out.println("请确认新密码：");
                    String newPassWord = sc.next();
                    if (okPassWord.equals(newPassWord)) {
                        account.setPassword(okPassWord);
                        System.out.println("修改密码成功");
                        return;
                    } else {
                        System.out.println("两次密码不一样");
                    }
                }
            }else {
                System.out.println("您输入的密码不正确");
            }
        }

    }

    /**
     * 转账
     * @param account
     * @param sc
     * @param accounts
     */
    private static void transMoney(Account account, Scanner sc, ArrayList<Account> accounts) {
        System.out.println("=====用户转账操作=====");
        if (accounts.size() < 2){
            //账户不足两个，无法转账
            System.out.println("当前系统中不足两个账户，无法进行转账");
            return;
        }
        //2.判断自己的账户是否有钱
        if (account.getMoney() == 0){
            System.out.println("账户余额为0,无法转账");
            return;
        }
        //转账
        while (true){
            System.out.println("请您输入对方的卡号：");
            String id = sc.next();
            //卡号不能是自己的卡号
            if (id.equals(account.getId())){
                System.out.println("您不能给自己转账");
                continue;//结束当前执行，进行下一次死循环
            }
            Account account1 = getAccountByCardId(id,accounts);
            if (account1 == null){
                System.out.println("该账户卡号不存在");
            }else {
                String name = account1.getName();
                String tip = "*"+name.substring(1);
                System.out.println("请您输入["+tip+"]的姓氏");
                String preName = sc.next();
                //认证姓氏是否正确
                if (name.startsWith(preName)){
                    while (true){
                        System.out.println("请输入需要转账的金额");
                        double money = sc.nextDouble();
                        if (money>account.getMoney()){
                            System.out.println("对不起，您的余额不足");
                        }else {
                            account.setMoney(account.getMoney()-money);
                            account1.setMoney(account1.getMoney()+money);
                            System.out.println("转账成功");
                            return;
                        }
                    }
                }
                else {
                    System.out.println("对不起，您输入的信息有误===");
                }
            }
        }

    }

    /**
     * 查询账户信息
     * @param account
     */
    private static void query(Account account) {
        System.out.println("卡号："+account.getId());
        System.out.println("账户名："+account.getName());
        System.out.println("账户余额："+account.getMoney());
        System.out.println("限额："+account.getQuotaMoney());
    }
    public static void store(Account account,Scanner sc){
        System.out.println("====欢迎您进入yyue银行用户存款界面====");
        System.out.println("请您输入存款的金额：");
        Double storeMoney = sc.nextDouble();
        account.setMoney(storeMoney+account.getMoney());
        System.out.println("您已经存款成功！");
        System.out.println("=======当前账户信息如下=======");
        System.out.println("卡号："+account.getId());
        System.out.println("户主："+account.getName());
        System.out.println("账户余额："+account.getMoney());
        System.out.println("限额："+account.getQuotaMoney());
    }

    /**
     * 取款功能
     * @param account
     * @param sc
     */
    public static void drawMoney(Account account,Scanner sc){
        System.out.println("====欢迎您进入yyue银行用户取款界面====");
        if (account.getMoney()<100){
            System.out.println("账户余额不足100元，先去存钱吧！");
            return;
        }else {
            while (true){
                System.out.println("请您输入取款的金额：");
                Double drawMoney = sc.nextDouble();
                if (drawMoney > account.getQuotaMoney()){
                    System.out.println("您当前取款超过当前限额！");
                }else {
                    if (drawMoney>account.getMoney()){
                        System.out.println("余额不足");
                    }
                    else {
                        System.out.println("取款成功");
                        account.setMoney(account.getMoney()-drawMoney);
                        query(account);
                        return;
                    }

                }

        }
    }
    }
}
```

## 9.面向对象进阶

### 9.1static静态关键字

#### 9.1.1**static是什么**

- static是静态的意思，可以修饰成员变量和成员方法
- static修饰成员变量表示该成员变量只在内存中**存储一份**，可以被共享访问、修改

如下图所示161人，该公司所有人都可以看见这个人数，都可以对其进行修改，所以将其设置为static修饰的变量



![](.\images\j1.png)

成员变量分为两类：

- 静态成员变量（有static修饰，属于类，内存中加载依次）：常表示如在线人数信息，等需要被共享的信息，可以被共享访问。访问方式：类名.静态成员变量（推荐），或者1对象.静态成员变量（不推荐）
- 实例成员变量(无static修饰，存在于每个对象中)：常表示姓名name、年龄age等属于每个对象的信息

#### 9.1.2static修饰成员变量的内存原理

在加载类的时候，类的静态变量会在堆内存中加载在类静态变量区中。

![](.\images\j2.png)

#### 9.1.3static修饰成员方法的基本用法

成员方法的分类：

- 静态成员方法（有static修饰），建议用类名访问，也可以用对象访问（不建议）
- 实例成员方法

使用场景：表示对象自己的行为的，且方法中需要访问实例成员的，则该方法必须申明成实例方法。如果该方法是以执行一个共用功能为目的，则可以声明成静态方法。

#### 9.1.4static修饰成员方法的内存原理

当类加载进方法区时，类中的静态方法也会被加载到方法区

![](D:\mybatis笔记\images\j3.png)

#### 9.1.5static注意事项（扩展）

static访问注意事项：

- 静态方法只能访问静态的成员，不可以直接访问实例成员（因为实例成员属于对象，只能用对象来访问它）
- 实例方法可以访问静态的成员，也可以访问实例成员
- 静态方法中是不可以出现this关键字的（this代表当前对象，而静态方法不一定会用对象来调用，也可以用类来调用，但是this不能代表类）

### 9.2static应用知识：工具类

**工具类**是什么？类中都是一些静态方法，每个方法都是以完成一个共用的功能为目的，这个类用来给系统开发人员共同使用。

使用工具类好处：调用方便，提高代码复用性

为什么工具类中的方法不用实例方法做？

- 实例方法需要创建对象调用
- 此时用对象只是为了调用方法，这样只会浪费内存。

工具类定义时的其他要求：由于工具里面都是静态方法，直接用类名即可访问，因此，工具类无需创建对象，建议将工具类的构造器进行**私有**

### 9.3static应用知识：代码块

代码块的分类、作用

![](D:\mybatis笔记\images\j4.png)

静态代码块的应用案例

```java
package com.yyue.d3_static_code;


import java.util.ArrayList;

public class StaticDemo3 {
    /**
     * 定义一个静态集合，这样的集合只需要加载一个，因为当前房间只需要一副牌
     */
    public static ArrayList<String> cards = new ArrayList<>();

    /**
     * 在程序正真运行main方法前，把54张牌放进去，后续游戏可以直接使用
     */
    static {
        //牌大小
        String[] sizes = {"3","4","5","6","7","8","9","10","J","Q","K","A","2"};
        //牌花色
        String[] colors = {"♥","♦","♣","♠"};
        for (int i = 0; i < sizes.length; i++) {
            for (int i1 = 0; i1 < colors.length; i1++) {
                String card = sizes[i]+colors[i1];
                cards.add(card);
            }
        }
        cards.add("小🃏");
        cards.add("大🃏");
    }

    public static void main(String[] args) {
        System.out.println(cards);
    }
}
```

### 9.4static应用知识：单例设计模式

- 设计模式、单例模式介绍、饿汉单例模式

- 懒汉单例模式

单例模式：

- 可以保证系统中，应用该模式的这个类永远只有一个实例，即一个类永远只能创建一个对象。
- 例如任务管理器对象我们只需要一个就可以解决问题了，这样可以节省空间内存。

饿汉单例设计模式：在用类获取对象的时候，对象已经提前为你创建好了

```java
//定义一个单例类
public class SingleInstance {
    public static SingleInstance instance = new SingleInstance();
    //
    private SingleInstance(){
        System.out.println("创建一个对象");
    }
}
```

```java
SingleInstance instance1 = SingleInstance.instance;
```

懒汉单例设计模式：在真正需要该对象的时候，才去创建一个对象(延迟加载对象)

```java
//定义一个单例类
public class SingleInstance {
    private static SingleInstance instance; //设置为私有化，因为别人要点的画，拿到的可能是null
    //
    //单例必须私有化构造器
    private SingleInstance(){
    }
    //必须提供一个方法返回一个单例对象
    public static SingleInstance getInstance(){
        //不能这样写，别人一调用就会新new一个单例
//        instance = new SingleInstance();
        if (instance == null){
            instance = new SingleInstance();
        }
        return instance;
    }
}
```

```java
SingleInstance instance1 = SingleInstance.getInstance();
SingleInstance instance2 = SingleInstance.getInstance();
System.out.println(instance1 == instance2);
```

### 9.5面向对象三大特征之二：继承

#### 9.5.1继承概述、使用继承好处

什么是继承？

- java中提供一个关键字extends，用这个关键字，我们可以让一个类和另一个类建立起父子关系。
- public class Student extends People{}
- Student称为子类（派生类），People称为父类（基类或超类）
- 作用：当子类继承父类后，就可以直接使用父类公共的属性和方法了
- 好处：可以提高代码的复用性

#### 9.5.2继承的设计规范、内存运行原理

继承设计规范：子类们相同特征(共性属性、方法)放在父类中定义，子类独有的属性和行为应该定义在子类自己里面

为什么：如果子类的独有属性、行为定义在父类中，会导致其他子类也会得到这些属性和行为，不符合面向对象逻辑

案例：

![](D:\mybatis笔记\images\java1.png)

#### 9.5.3继承的特点

1. 子类可以继承父类的属性和行为，但是子类不能继承父类的构造器（子类有自己的构造器，父类构造器用于初始化父类对象）
2. java是单继承模式：一个类只能继承一个直接父类
3. java不支持多继承，只支持多层继承
4. java中所有的类都是Object类的子类（Java中所有类，要么直接继承Object类，要么默认继承Object类，要么间接继承Object，Object是祖宗类）

问题：

1.子类是否可以继承父类的构造器？

答：子类不可以继承父类构造器，子类有自己的构造器，父类构造器用于初始化父类对象

2.子类是否可以继承父类的私有成员？

答：可以的，只是不能直接访问

![](D:\mybatis笔记\images\j5.png)

3.子类是否可以继承父类的静态成员？

- 有争议的知识点
- 子类可以直接使用父类的静态成员（共享）
- 但个人认为：子类不能继承父类的静态成员（共享并非继承）

#### 9.5.4继承后：成员变量、成员方法的访问特点

在子类方法中访问成员(成员变量、成员方法)满足：**就近原则**

- 先子类局部范围找
- 然后子类成员范围找
- 然后父类成员范围找，如果父类范围还没有找到则报错

如果子父类中，出现了重名的成员，会优先使用子类的，此时如果一定要在子类中使用父类怎么办？

- 可以通过**super关键字**，指定访问父类的成员
- 格式：super.父类成员变量/父类成员方法

#### 9.5.5继承后：方法重写

**什么是方法重写？**

- 在继承体系中，子类出现了和父类一模一样的方法声明，我们就称子类这个方法是重写的方法。

**方法重写的应用场景**

- 当子类需要父类的功能，但父类的该功能不完全满足自己的需求时

**@Override重写注解**

- @Override是放在重写后的方法上，作为重写是否正确的校验注解
- 加上该注解后如果重写错误，编译阶段会出现错位提示
- 建议重写方法都加上@Override注解，代码安全，优雅

**方法重写注意事项和要求：**

- 重写方法的名称、形参列表必须与被重写方法的名称和参数列表一致
- 私有方法不能被重写
- 子类重写父类方法时，访问权限必须大于或者等于父类（缺省<protected<public)
- 子类不能重写父类的静态方法，如果重写会报错

#### 9.5.6继承后：子类构造器的特点

特点：子类中所有的构造器（无参、有参）默认都会先访问父类中无参的构造器，再执行自己

**为什么？**

- 子类在初始化的时候，有可能会使用到父类中的数据，如果父类没有完全初始化，子类将无法使用父类的数据。
- 子类初始化之前，一定要调用父类构造器先完成父类数据空间的初始化。

怎么调用父类构造器？

子类构造器的第一行语句默认都是：super(),不写也存在

#### 9.5.7继承后：子类构造器访问父类有参构造器

![](D:\mybatis笔记\images\j6.png)

super调用父类有参数构造器的作用：

- 初始化继承自父类的数据

如果父类中没有无参数构造器，只有有参数构造器，会出现什么现象？

- 会报错。因为子类默认是调用父类无参构造器的

如何解决？

- 子类构造器可以通过书写super(...),手动调用父类的有参数构造器
- 或者把父类的无参构造器写上

#### 9.5.8this、super使用总结

this和super详情

**this：**代表本类对象的引用；**super：**代表父类存储空间的标识。

![](D:\mybatis笔记\images\j7.png)

**注意：**this()和super()都只能放在构造器的第一行，所以二者不能共存在同一个构造器中。

### 10.语法知识

#### 10.1语法：包

什么是包？

- 包是用来分门别类的管理各种不同类的，类似于文件夹、建包利于程序的管理和维护
- 建包的语法格式：package 公司域名倒写.技术名称。包名建议全部英文小写，且具备意义

```java
package com.itheima.javabean;
public class Student{}
```

- 建包语句必须在第一行，一般IDEA工具会帮助创建

**导包**

- 同包下的类可以直接访问，不同包下的类必须要导包，才可以使用！导包格式：import 包名.类名
- 如果这个类中使用不同包下的相同类名，此时默认只能导入一个类的包，另一个类要使用全名访问。

#### 10.2语法：权限修饰符

- **权限修饰符**：是用来控制一个成员能够被访问的范围
- 可以修饰**成员变量，方法，构造器，内部类**，不同修饰符的成员能够被访问的范围将受到限制

**权限修饰符的分类和具体作用范围：**

- 权限修饰符：有四种作用范围由小到大（private->缺省->protected->public）

![](D:\mybatis笔记\images\j.png)

学完权限修饰符需要具备如下能力

能够识别别人定义的成员的访问范围

自己定义成员（方法，成员变量，构造器等）一般需要满足如下要求：

- 成员变量一般私有
- 方法一般公开
- 如果该成员只希望本类访问，使用private修饰
- 如果该成员只希望本类，同一个包下的其他类和子类访问，使用protected修饰

#### 10.3语法：final

**final**作用：

- final关键字是最终的意思，可以修饰（类、方法、变量）
- 修饰类：表明该类是最终类，不能被继承
- 修饰方法：表明该方法是最终方法，不能被重写
- 修饰变量：标识该变量第一次赋值后，不能再次被赋值（有且仅能被赋值一次）

**注意：**

- final修饰的变量是基本类型：那么变量存储的数据值不能发生改变
- final修饰的变量是引用类型：那么变量存储的地址值不能发生改变，但是地址指向的对象内容是可以发生变化的。

#### 10.4语法：常量

- 常量是使用了public static final 修饰的成员变量，必须有初始值，而且执行的过程中其值不能被改变
- 常量的作用和好处：可以用作系统的配置信息，方便程序的维护，同时也能提高可读性

常量命名规范：英文单词全部大写，多个单词下划线连接起来

```java
public class Constant{
    public static final String SCHOOL_NAME = "船只教育";
    public static final String LOGIN_NAME = "admin";
    public static final String PASS_WORD = "123456";
}
```

常量的执行原理

- 在编译阶段会进行”宏替换“，把使用常量的地方全部替换成真实的字面量
- 这样做的好处是让使用常量的程序的执行性能与直接使用字面量是一样的

#### 10.5语法：枚举

- 枚举的概述：枚举是JAVA中的一种特殊类型
- 枚举的作用：为了做信息的标志和信息的分类

定义枚举类的格式

```java
修饰符 enum 枚举名称{
    第一行都是罗列枚举类实例的名称。
}
enum Season{
    SPRING,SUMMER,AUTUMN,WINTER;
}
```

反编译出来的文件内容是：（在桌面编写java文件，打开该位置的cmd，执行该Java文件javac .java,  产生一个class文件，在反编译class文件javap .class）

```java
public final class Season extends java.lang.Enum<Season> {
  public static final Season SPRING;
  public static final Season SUMMER;
  public static final Season AUTUMN;
  public static final Season WINTER;
  public static Season[] values();
  public static Season valueOf(java.lang.String);
  static {};
}
```

枚举的特征：

- 枚举类都是继承了枚举类型：java.lang.Enum
- 枚举都是最终类，不能被继承
- 枚举的构造器都是私有的，枚举对外不能创建对象
- 枚举类的第一行默认都是罗列枚举对象的名称的
- 枚举类相当于是多例模式

枚举的使用场景演示

```java
public enum Direction {
    UP, DOWN, LEFT, RIGHT;
}
```

```java
package com.yyue.d5_enum;

import javax.swing.*;
import java.awt.event.ActionEvent;

public class EnumDemo1 {
    public static void main(String[] args) {
        JFrame jFrame = new JFrame();
        JPanel jPanel = new JPanel();
        jFrame.add(jPanel);
        JButton button1 = new JButton("上");
        JButton button2 = new JButton("下");
        JButton button3 = new JButton("左");
        JButton button4 = new JButton("右");
        jPanel.add(button1);
        jPanel.add(button2);
        jPanel.add(button3);
        jPanel.add(button4);
        jFrame.setLocationRelativeTo(null);
        jFrame.setSize(300,400);
        jFrame.setVisible(true);
        button1.addActionListener(new AbstractAction() {
            @Override
            public void actionPerformed(ActionEvent e) {
                move(Direction.UP);
            }
        });

        button2.addActionListener(new AbstractAction() {
            @Override
            public void actionPerformed(ActionEvent e) {
                move(Direction.DOWN);
            }
        });

        button3.addActionListener(new AbstractAction() {
            @Override
            public void actionPerformed(ActionEvent e) {
                move(Direction.LEFT);
            }
        });

        button4.addActionListener(new AbstractAction() {
            @Override
            public void actionPerformed(ActionEvent e) {
                move(Direction.RIGHT);
            }
        });
    }
    public static void move(Direction d){
        switch (d){
            case UP:
                System.out.println("向上飞");
                break;
            case DOWN:
                System.out.println("向下飞");
                break;
            case LEFT:
                System.out.println("向左飞");
                break;
            case RIGHT:
                System.out.println("向右飞");
                break;
        }
    }
}

```

#### 10.6语法：抽象类

抽象类

- 在Java中abstract是抽象的意思，可以修饰类、成员方法。
- abstract修饰类，这个类就是抽象类；修饰方法，这个方法就是抽象方法

```java
修饰符 abstract class 类名{
    修饰符 abstract 返回值类型 方法名称(形参列表);
}
public abstract class Animal{
    public abstract void run();
}
```

**注意事项**

- **抽象方法只有方法签名，不能声明方法体。**
- 一个类中如果定义了抽象方法，这个类必须声明成抽象类，否则报错。

抽象的使用场景

- 抽象类可以理解成不完整的设计图，一般作为父类，让子类来继承
- 当父类知道子类一定要完成某些行为，但是每个子类该行为的实现又不同，于是该父类就把该行为定义成抽象方法的形式，具体实现交给子类去完成。此时这个类就被声明成抽象类。

**继承抽象类注意事项**

- 一个类如果继承了抽象类，那么这个类必须重写完抽象类的全部抽象方法，否则这个类也必须定义成抽象类。

**抽象类的案例**

```java
系统需求：
某加油站推出2种支付卡，一种是预存10000的金卡，后续加油享受8折优惠，另一种是预存5000的银卡，后续加油享受8.5折优惠
请分别实现2种卡片进入收银系统后的逻辑，卡片需要包含主人名称，余额，支付功能
分析实现：
创建一张卡片父类：定义属性包括主人名称，余额，支付功能（具体实现交给子类）
创建一张白金卡类：重写支付功能，按照原价的8折计算输出。
创建一张银卡类：重写支付功能，按照原价的8.5折计算输出
package com.yyue.d6_abstract;
public abstract class Card {
    private String name;
    private Double check;
    public abstract void pay(Double money);
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public Double getCheck() {
        return check;
    }
    public void setCheck(Double check) {
        this.check = check;
    }
}
```

```java
package com.yyue.d6_abstract;

public class GoldenCard extends Card{
    @Override
    public void pay(Double money) {
        Double remainMoney = getCheck()-money*0.8;
        setCheck(remainMoney);
        System.out.println("余额还剩"+remainMoney);
    }
}
```

```java
package com.yyue.d6_abstract;

public class AgCard extends Card {
    @Override
    public void pay(Double money) {
        Double remainMoney = getCheck()-money*0.85;
        setCheck(remainMoney);
        System.out.println("余额还剩"+remainMoney);
    }
}
```

抽象类特征及注意事项：

- 类有的成员（成员变量、方法、构造器）抽象类都具备
- 抽象类中不一定有抽象方法，有抽象方法的类一定是抽象类
- 一个类继承了抽象类必须重写完抽象类的全部抽象方法，否则这个类也必须定义成抽象类
- 不能用abstract修饰变量、代码块、构造器
- **最重要的特征**：得到抽象方法，失去创建对象的能力（**抽象类不能够创建对象**）

final和abstract是什么关系？

- 互斥关系
- abstract定义的抽象类作为模板让子类继承，final定义的类不能被继承
- 抽象方法定义的通用功能让子类重写，final定义的方法子类不能重写

**抽象类的应用知识：模板方法模式**

什么时候使用模板方法模式？

- 使用场景说明：当系统中出现同一个功能多处在开发，而该功能中大部分代码是一样的，只有其中部分可能不同的时候

**模板方法模式实现步骤**

- 把功能定义成一个所谓的模板方法，放在抽象类中，模板方法中只定义通用且能确定的代码
- 模板方法中不能决定的功能定义成抽象方法让子类去实现

案例：

```java
/**
*需求：现在又两类学生，一类是中学生，一类是小学生，他们都要写《我的爸爸》这篇作文
      要求每种类型的学生，标题第一段和最后一段内容必须一样，正文部分自己发挥
      请选择最有的面向对象方案进行设计
*/
public abstract class Student {
    public final void write(){
        System.out.println("标题第一段======");
        writeMiddle();
        System.out.println("最后一段======");
    }
    public abstract void writeMiddle();
}

public class MiddleStudent extends Student{
    @Override
    public void writeMiddle() {
        System.out.println("中学生中间部分自由发挥");
    }
}

public class Primary extends Student {
    @Override
    public void writeMiddle() {
        System.out.println("小学生中间部分自由发挥");
    }
}

public class Test {
    public static void main(String[] args) {
        MiddleStudent middleStudent = new MiddleStudent();
        middleStudent.write();
        Primary primary = new Primary();
        primary.write();
    }
}
```

模板方法我们是建议使用final修饰，这样会更专业，为什么？

答：模板方法是给子类直接使用的，不是让子类重写的，一旦子类重写了模板方法，则模板方法就失效了，因此，加上final后可以防止子类重写模板方法，这样更安全，专业。

模板方法模式解决了什么问题？

- 提高了代码的复用性
- 模板方法已经定义了通用结构，模板方法不能确定的部分定义成抽象方法，交给子类实现，因此，使用者只需要关心自己需要实现的功能即可。

#### 10.7语法：接口

##### 10.7.1接口概述、特点

接口定义与特点

接口的格式如下

```java
# 接口用关键字interface来定义
public interface 接口名{
	//常量
	//抽象方法
    public abstact void run();
    void run1();
    //注意：由于接口体现的是规范思想，而规范默认都是公开的，所以代码层面：public abstract可以省略不写。
    //而常量前面的public static final也可以省略不写
}
```

什么是接口：接口是一种规范，规范一定是公开的 

##### 10.7.2接口的基本使用：被实现

接口的用法：

- 接口是用来被类实现(implements)的，实现接口的类称为实现类，实现类可以理解成所谓的子类。

- ```java
  修饰符 class 实现类 implements 接口1，接口2，接口3,....{
  }
  实现的关键字：implements
  ```

- 接口可以被类单实现，也可以被类多实现

接口实现的注意事项：一个类实现接口，必须重写全部接口的全部抽象方法，否则这个类需要定义成抽象类。

##### 10.7.3接口与接口的关系：多继承

一个接口可以同时继承多个接口

接口多继承的作用：规范合并，整合多个接口为同一个接口，便于子类实现

```java
public interface People(){
	void eat();
	void sleep();
}
public interface SportMan(){
    void run();
}
public interface Law(){
    void make();
}
public class BasketBallMan implements People, SportMan, Law(){
    //实现上述方法
}

//改写成
public interface SportMan extends Law, People(){
    
}
//然后BasketBallMan再实现SportMan
public class BasketBallMan implements SportMan(){
    //实现上述所有方法
}
```

##### 10.7.4JDK8开始接口新增方法

提出问题：需要对接口进行丰富，加入10个新的抽象方法，此时改了接口就要所有实现类实现这些方法，这样就会改很多文件

所以提出允许接口中直接定义带有方法体的方法。

第一种：默认方法

- 类似之前写的普通实例方法：必须用default修饰
- 默认会public修饰。需要用接口的实现类的对象来调用

```java
default void run(){
	System.out.println("===开始跑===")
}
```

```java
//使用方法
public interface SportMan(){
    default void run(){
        System.out.println("跑得快");
        go();
    }
    public static void inAddr(){
        System.out.println("我们都在学习Java新增方法的语法，它是Java源码自己会用到的===")
    }
    private void go(){
        System.out.println("开始跑")
    }
}
class PingPongMan implements SportMan(){
    
}
class Test(){
    public static void main(String[] args){
        PingPongMan p = new PingPongMan();
        p.run();//实现类的对象直接调用
        SportMan.inAdd(); //直接用本身的接口名来调用
    }
}
```

第二种：静态方法

- 默认会public修饰，必须static修饰

- 注意：接口的静态方法必须用本身的接口名来调用（因为当一个类实现了两个接口，而这两个接口中有同名方法，如果这个类可以调用这个静态方法的话，不知道调用哪一个，所以只能由本身的接口名来调用）

- ```java
  static void inAddr(){
  	System.out.println("=======")
  }
  ```

第三种：私有方法

- 就是私有的实例方法，必须使用private修饰，从JDK1.9才开始有的

- 只能在本类中被其他的默认方法或者私有方法访问。

- ```java
  private void go(){
  	System.out.println("===准备===")
  }
  ```

**注**：JDK8新增的3种方法我们自己在开发中很少使用，通常是Java源码涉及到。现阶段需要理解、识别语法、明白调用关系即可。

##### 10.7.5使用接口的注意事项

**注意事项：**

- 接口不能创建对象
- 一个类实现多个接口，多个接口种有同样的静态方法不冲突
- 一个类继承了父类，同时又实现了接口，父类中和接口中有同名方法，默认使用父类的
- 一个类实现了多个接口，多个接口中存在同名的默认方法，不冲突，这个类重写改该方法即可
- 一个接口继承多个接口，是没有问题的，如果多个接口中存在规范冲突则不能多继承。

###  11 面向对象三大特征之三：多态

#### 11.1.1多态的概述，多态的形式

多态：同类型的对象，执行同一个行为，会表现出不同的行为特征

常见形式：

```
父类类型 对象名称 = new 子类构造器
接口 对象名称 = new 实现类构造器
```

```java
public abstract class Animal{
    public String name = "父类动物";
    public abstract void  run();
}
public class Dog extends Animal{
    public String name = "子类狗";
    @Override
    public void run(){
        System.out.println("🐕跑的贼快");
    }
}
public class Tortoise extends Animal{
    public String name = "子类乌龟";
    @Override
    public void run(){
        System.out.println("🐢跑的慢");
    }
}
public class Test{
    public static void main(String[] args){
        //1.多态的实现形式
        Animal dog = new Dog();
        dog.run();
        System.out.println(dog.name);  //父类动物
        Animal tortoise = new Tortoise();
        tortoise.run();
        System.out.println(tortoise.name);//父类动物
    }
}
```

**多态中成员访问特点**

- 方法调用：编译看左边，运行看右边
- 变量调用：编译看左边，运行看左边（多态侧重行为多态）

**多态使用前提**

- 有继承/实现关系；有父类引用指向子类对象；有方法重写；

#### 11.1.2多态的好处

- 优势：在多态形式下，右边对象可以实现解耦合，便于扩展和维护
- 定义方法的时候，使用父类型作为参数，该方法就可以接收这父类的一切子类对象，体现出多态的扩展性与便利

比如：

```java
Animal a = new Dog()
a.run();
// 此时若是需要的是Animal a = new Tortoise();
// 则直接将右边对象修改即可，不需要修改左边以及方法的调用
```

```java
//要求所有动物都可以进来比赛
public static void go(Animal a){
    System.out.println("开始");
    a.run();
    System.out.println("结束");
}
```

多态下会产生一个问题：多态下不能使用子类的独有功能

#### 11.1.3多态下引用数据类型的类型转换

自动类型转换(从子到父)：子类对象赋值给父类类型的变量指向

强制类型转换(从父到子)：

- 此时必须进行强制类型转换：子类 对象变量 = (子类)父类类型的变量

- ```
  // 强制类型转换
          Aniaml dog = new Dog();
          Dog dog1 = (Dog) dog; //从父类类型到子类类型，必须强制类型转换
          dog1.run();
          dog1.lookDoor();
  ```

- 作用：可以解决多态下的劣势，可以实现调用子类独有的功能

- **注意**：如果转型后的类型和对象真实类型不是同一种类型，那么在转换的时候就会出现ClassCastException错误

  ```java
  Animal dog = new Dog();
  Tortoise tortoise = (Tortoise) dog; //强制类型转换，编译阶段不报错（注意：有继承或者实现关系编译阶段可以强制）
  //此时运行时会出现异常ClassCastException
  ```

Java建议强制转换前使用instanceof判断当前对象的真实类型，在进行强制转换

```java
变量名 instanceof 真实类型
判断关键字左边的变量指向的对象的真实类型，是否是右边的类型或者是其子类类型，是则返回true，反之。
```

```java
if (dog instanceof Dog){
            Dog dog2 = (Dog) dog; //强制类型转换，编译阶段不报错（注意：有继承或者实现关系编译阶段可以强制）
            dog2.lookDoor();
            System.out.println("可以转换狗");
        }else if (dog instanceof Tortoise){
            Tortoise tortoise = (Tortoise) dog;
            tortoise.sleep();
        }
```

总结：

1.引用数据类型的类型转换，有几种方式？

- 自动类型转换、强制类型转换

2.强制类型转换能解决什么问题？强制类型转换需要注意什么

- 可以转换成真正的子类类型，从而调用子类独有的功能
- 有继承关系/实现的2个类型就可以进行强制转换，编译无问题
- 运行时，如果发现强制转换后的类型不是对象真实类型则会报错ClassCastException

#### 11.1.4多态的综合案例

需求：

- 使用面向对象编程模拟：设计一个电脑对象，可以安装2个USB设备
- 鼠标：被安装时可以完成接入、调用点击功能、拔出功能
- 键盘：被安装时可以完成接入、调用打字功能、拔出功能

分析：

- 定义一个USB的接口（声明USB设备的规范必须是：可以接入和拔出）
- 提供2个USB实现类代表鼠标和键盘，让其实现USB接口，分别定义独有功能
- 创建电脑对象，创建2个USB实现类对象，分别安装到电脑中并触发功能的执行

```java
package com.yyue.d9_polymorphic_convert;

public interface USB {
    //接入
    void connect();
    //拔出
    void unconnect();
}
```

```java
package com.yyue.d9_polymorphic_convert;
public class KeyBoard implements USB{
    private String name;
    public KeyBoard(String name) {
        this.name = name;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    @Override
    public void connect() {
        System.out.println(name+"成功接入电脑");
    }
    @Override
    public void unconnect() {
        System.out.println(name+"成功拔出");
    }
    public void keyDown(){
        System.out.println(name+"敲击了:来了来了");
    }
}
```

```java
package com.yyue.d9_polymorphic_convert;

public class Mouse implements USB{

    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Mouse(String name) {
        this.name = name;
    }

    @Override
    public void connect() {
        System.out.println(name+"成功接入电脑");
    }

    @Override
    public void unconnect() {
        System.out.println(name+"成功拔出");
    }

    public void click(){
        System.out.println(name+"双击:点亮星星");
    }
}
```

```java
package com.yyue.d9_polymorphic_convert;

public class Computer {
    private String name;

    public Computer(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    /**
     提供安装USB设备的入口
     */
    public void installUSB(USB usb){
        //多态 usb 可能是鼠标也可能是键盘
        usb.connect();
        //独有功能  要先判断再强转
        if (usb instanceof Mouse){
            Mouse m = (Mouse) usb;
            m.click();
        }else if(usb instanceof  KeyBoard){
            KeyBoard keyBoard = (KeyBoard) usb;
            keyBoard.keyDown();
        }
        usb.unconnect();
    }
}
```

```java
package com.yyue.d9_polymorphic_convert;

import java.nio.file.attribute.UserDefinedFileAttributeView;

public class Test {
    public static void main(String[] args) {
        Computer computer = new Computer("yyue电脑");
        USB u1 = new KeyBoard("键盘");
        computer.installUSB(u1);
        System.out.println("===================");
        USB u2 = new Mouse("鼠标");
        computer.installUSB(u2);
    }
}
```

### 12内部类

#### 12.1内部类概述

内部类就是定义在一个类里面的类，里面的类可以理解成(寄生)，外部类可以理解成(宿主)

```java
public class People{
	//内部类
	public class Heart{
		
	}
}
```

内部类使用场景、作用

- 当一个事物的内部，还有一部分需要一个完整的结构进行描述，而这个内部的完整的结构又只为外部事物提供服务，那么整个内部的完整结构可以选择使用内部类来设计。
- 内部类通常可以方便访问外部类的成员，包括私有的成员
- 内部类提供了更好的封装性，内部类本身就可以用private protected等修饰，封装性可以做更多控制。

#### 12.2内部类之一：静态内部类(了解)

内部静态类：

- 有static修饰，属于外部类本身

- 它的特点和使用与普通类是完全一样的，类有的成分它都有，只是位置在别人里面而已。

- ```java 
  public class Outer{
  	//静态成员内部类
  	public static class Inner{
  	}
  }
  ```

静态内部类创建对象的格式：

- 格式：外部类名.内部类名 对象名 = new 外部类名.内部类构造器；
- 范例：Outer.Inner in = new Outer.Inner();

静态内部类的访问扩展：

- 静态内部类中是否可以直接访问外部类的静态成员？
  - 可以，外部类的静态成员只有一份可以被共享访问
- 静态内部类中是否可以直接访问外部类的实例成员？
  - 不可以的，外部类的实例成员必须用外部类对象来访问

总结：

1.静态内部类的使用场景、特点、访问总结。

- 如果一个类中包含了一个完整的成分，如汽车类中的发动机类。
- 特点、使用与普通类是一样的，类有的成分它都有，只是位置在别人里面而已
- 可以直接访问外部类的静态成员，不能直接访问外部类的实例成员。
- 注意：实际上开发用的还是比较少的

#### 12.3内部类之二：成员内部类（了解）

- 无static修饰，属于外部类的对象

- JDK16之前，成员内部类不能定义静态成员，JDK16开始也可以定义静态成员了

- ```java
  public class Outer{
      //成员内部类
      public class Inner{}
  }
  ```

成员内部类创建对象的格式：

- 格式：外部类名.内部类名 对象名 = new 外部类构造器.new 内部类构造器
- 范例：Outer.Inner in = new Outer().new Inner();

成员内部类的访问扩展：

- 成员内部类中是否可以直接访问外部类的静态成员？
  - 可以，外部类的静态成员只有一份可以被共享访问
- 成员内部类的实例方法中是否可以直接访问外部类的实例成员？
  - 可以的，因为必须先有外部类对象，才能有成员内部类对象，所以可以直接访问外部类对象的实例成员。

内部类面试题：

![](D:\mybatis笔记\images\java2.png)

heartbeat、this.heartbeat、People.this.heartbeat

#### 12.4内部类之三：局部内部类(了解即可)

- 局部内部类放在方法、代码块、构造器等执行体中
- 局部内部类的类文件名为：外部类$N内部类.class

#### 12.5内部类之四：匿名内部类概述（重点！）

本质上是一个没有名字的局部内部类，定义在方法中、代码块中

作用：方便创建子类对象，最终目的为了简化代码编写

格式：

- ```java
  new 类|抽象类名|接口名(){
  	重写方法
  };
  ```

- ```java
  Employee a = new Employee() {
  	public void work(){
  	
  	}
  };
  a.work;
  ```

- 以往写法

- ```java
  package com.yyue.d12_innerclass_anonymous;
  
  public class Test {
      public static void main(String[] args) {
          Animal tiger = new Tiger();
          tiger.run();
      }
  }
  
  abstract class Animal{
      public abstract void run();
  }
  
  class Tiger extends Animal{
      @Override
      public void run(){
          System.out.println("老虎跑的快");
      }
  }
  
  ```

- 现在写法：

- ```java
  package com.yyue.d12_innerclass_anonymous;
  
  public class Test {
      public static void main(String[] args) {
          Animal tiger = new Animal() {
              @Override
              public void run() {
                  System.out.println("老虎跑的快");
              }
          };
          tiger.run();
      }
  }
  
  abstract class Animal{
      -
  }
  
  ```

特点总结：

- 匿名内部类是一个没有名字的内部类
- 匿名内部类写出来就会产生一个匿名内部类的对象
- 匿名内部类的对象类型相当于是当前new的那个类型的子类类型

#### 12.6匿名内部类常见使用形式

```java
/**
 * 目标:掌握匿名内部类的使用形式(语法)
 */
public class Test2 {
    public static void main(String[] args) {
        Swimming swimming = new Swimming() {
            @Override
            public void swim() {
                System.out.println("学生参加比赛");
            }
        };
        go(swimming);
        System.out.println("================");
        Swimming swimming1 = new Swimming() {
            @Override
            public void swim() {
                System.out.println("老师参加比赛");
            }
        };
        go(swimming);
    }
    /*
    学生 老师 运动员可以一起参加游泳比赛
     */
    public static void go(Swimming swimming){
        System.out.println("开始游泳");
        swimming.swim();
        System.out.println("比赛结束");
    }
}
interface Swimming{
    void swim();
}

```

#### 12.7匿名内部类真实使用场景演示

![](D:\mybatis笔记\images\java3.png)

### 13常用API

- API应用程序编程接口
- 简单来说：就是Java帮我们已经写好的一些方法，我们可以直接拿过来用就可以

Object类作用：

- 一个类要么默认继承了Object类，要么间接继承了Object类，Object类是Java的祖宗类
- Object类的方法是一切子类都可以直接使用的

#### Object常用方法

- toString方法：public String toString()默认是返回当前对象在堆内存中的地址信息：类的全限名@内存地址

  - 问题：

    - 开发中直接输出对象，默认输出对象的地址其实是毫无意义的
    - 开发中输出对象变量，更多时候是希望看到对象的内容数据而不是对象的地址信息

  - toString存在意义

    - 父类toString()方法存在的意义就是为了被子类重写，以便返回对象的内容信息，而不是地址信息

    - ```java
      @Override
          public String toString() {
              return "Student{" +
                      "name='" + name + '\'' +
                      ", age=" + age +
                      '}';
          }
      ```

- equals方法：public Boolean equals(Object o)默认比较当前对象与另一个对象的地址是否相同，相同返回true，不同返回false

  - 问题：

    - 直接比较两个对象的地址是否相同 完全可以用“==”替代equals

  - equals存在的意义

    - 父类equals方法存在的意义就是为了被子类重写，以便子类自己来定制比较规则

  - ```java
    /**
         自己重写equals,自己定制相等规则
         两个对象的内容一样就认为是相等的
         s1.equals(s2)
         比较者:s1  == this
         被比较者:s2 == obj
         */
    
        @Override
        public boolean equals(Object obj) {
            //判断是否为学生类型
            if (obj instanceof Student){
                Student s2 = (Student) obj;
    //            if (this.name.equals(s2.name) && this.age == s2.age){
    //                return true;
    //            }else {
    //                return false;
    //            }
                return this.name.equals(s2.name) && this.age == s2.age;
            }else {
                return false;
            }
        }
    ```

  - 官方自动生成写法

  - ```java
    @Override
        public boolean equals(Object o) {
            //判断是否为同一对象
            if (this == o) return true;
            //如果o是null  或者类型作比较
            if (o == null || getClass() != o.getClass()) return false;
            //说明一定是Student类型,并且不为null 强转
            Student student = (Student) o;
            //Object类里面的equals更安全
            return age == student.age &&
                    Objects.equals(name, student.name);
        }
    ```

#### Objects

- objects类与Object还是继承关系，Object类是从JDK1.7开始有的

- 官方在进行字符串比较时，没有用对象自己的equals方法，而是选择了Objects的equals方法来比较两个对象

- 因为Objects的equals方法比较的结果是一样的，但是更安全

- 常见方法

  - public static boolean equals(Object a,Object b)比较两个对象，底层会先进行非空判断，从而可以避免空指针异常。再进行equals比较
  - public static boolean isNull(Object obj) 判断变量是否为null，为null返回true，反之

- 源码

  ```java
  public static boolean equals(Object a, Object b) {
          return (a == b) || (a != null && a.equals(b));
      }
  ```

**注总结**：对象进行内容比较的时候建议使用？

- 建议使用Objects提供的equals方法
- 比较的结果是一样的，但是结果更安全

#### StringBuilder

- 概述：StringBuilder是一个可变的字符串类，我们可以把它看成是一个对象容器
- 作用：提高字符串的操作效率，如拼接、修改等

StringBuilder构造器

- public StringBuilder()   创建一个空白的可变的字符串对象，不包含任何内容
- public StringBuilder(String str) 创建一个指定字符串内容的可变字符串对象
- ![](D:\mybatis笔记\images\j8.png)

String类拼接字符串

```java
public static void main(String[] args) {
    StringBuilder stringBuilder = new StringBuilder();
    stringBuilder.append(1);
    stringBuilder.append("a");
    stringBuilder.append("b");
    stringBuilder.append("c");
    stringBuilder.append(false);
    stringBuilder.append("abc");
    System.out.println(stringBuilder.toString());
    System.out.println(stringBuilder);

    StringBuilder s1 = new StringBuilder();
    //支持链式编程
    s1.append(1).append("c").append("我爱你中国");
    System.out.println(s1);

    //反转
    s1.reverse();
    System.out.println(s1);

    //注意：StringBuilder只是拼接字符串的手段，效果好
    //最终目的还是要恢复成String类型
    String s = s1.toString();
    System.out.println(s);
}
```

原理图

![](D:\mybatis笔记\images\s12.png)

![](D:\mybatis笔记\images\j9.png)

总结：1.为什么拼接、反转字符串建议使用StringBuilder？

- String：内容是不可变的、拼接字符串性能差
- StringBuilder：内容是可变的、拼接字符串性能好、代码优雅
- 定义字符串使用String
- 拼接、修改等操作字符串使用StringBuilder

**案例：打印整型数组内容**

需求：设计一个方法用于输出任意整型数组的内容，要求输出成如下格式：

“该数组内容为：[11, 22, 33, 44, 55]”

分析：

1. 定义一个方法，要求该方法能够接收数组，并输出数组内容。-》需要参数吗？需要返回值类型声明吗
2. 定义一个静态初始化的数组，调用该方法，并传入该数组

```java
public class StringBuilderDemo2 {
    public static void main(String[] args) {
        int[] arr = {11,22,33,44,55};
        System.out.println(toString(arr));
    }
    public static String toString(int[] arr){
        if (arr != null){
            //开始拼接
            StringBuilder sb = new StringBuilder("[");
            for (int i = 0; i < arr.length; i++) {
                sb.append(arr[i]).append(i == arr.length-1 ? "":", ");
            }
            sb.append("]");
            return sb.toString();
        }else {
            return null;
        }
    }
}
```

#### Math

Math类

- 包含执行基本数字运算的方法，Math类没有提供公开的构造器
- 如何使用类中成员呢？看类的成员是否都是静态的，如果是，通过类名就可以直接调用
- ![](D:\mybatis笔记\images\j10.png)

#### System

System类

- System的功能是通用的，都是直接用类名调用即可，所以System不能被实例化
- ![](D:\mybatis笔记\images\j11.png)

#### BigDecimal

BigDecimal作用

- 用于解决浮点型运算精度失真的问题

使用步骤

- 创建对象BigDecimal封装浮点型数据（最好的方式是调用方法)

  - ```java
    public static BigDecimal valueOf(double val); //包装浮点数称为BigDecimal对象
    ```

- ![](D:\mybatis笔记\images\j12.png)

- ![](D:\mybatis笔记\images\j13.png)

- double rs = recommend1.doubleValue(); //可以将BigDecimal类型的数据转换成double类型的数据

- **注：BigDecimal是一定要精度运算的**

  ```java
  BigDecimal a11 = BigDecimal.valueOf(10.0);
  BigDecimal b11 = BigDecimal.valueOf(3.0);
  //BigDecimal c11 = a11.divide(b11);
  //System.out.println(c11)  //会出现异常，因为BigDecimal必须要精度运算，而10/3没办法精度运算，所以报错
  //所以只能规定保留几位小数；保留两位小数并且四舍五入。
  //参数一：除数；参数二：保留小数位数，参数三：舍入方式
  BigDecimal c11 = a11.divide(b11, 2, RoundingMode.HALF_UP);
  System.out.println(c11)
  ```

### 14 常用API 、lambda、常见算法

这一章要学会什么？

1. 如何处理时间：在程序中经常需要处理时间，获取时间，时间判断，运算等
2. 认识包装类：Java认为一切皆对象，8种基本类型不是，如何实现的，集合，泛型也不支持基本类型，怎么解决
3. 正则表达式：程序种需要对各种信息进行格式合法性的校验，比如手机号码，邮箱等
4. 经常需要操作数组元素：如何快捷操作数组元素，如输出数组内容、排序、元素搜索等。排序和搜索算法是什么样的
5. Lambda表达式：匿名内部类的代码是可以进一步简化的，什么情况下可以简化，需要用什么知识完成？

#### 14.1日期与时间

##### Date类

- Date类的对象在Java中代表的是当前所在系统的此刻日期时间。

- Date的构造器

  - public Date() 创建一个Date对象，代表的是系统当前此刻日期时间

  - ```java
    //创建一个日期对象
    Date d = new Date();
    System.out.println(d);
    ```

- Date的常用方法

  - public long getTime()  获取时间对象的毫秒值，指的是从1970年1月1日  00:00:00走到此刻的总的毫秒数

  - ```java
    long time = d.getTime();
    System.out.println(time);
    ```

案例

- 请计算出当前时间往后走1小时121秒之后的时间是多少

![](D:\mybatis笔记\images\j32.png)

- ```java
  //案例：计算当前时间往后走1小时121秒之后的时间是多少
  long time2 = System.currentTimeMillis()+(60*60 + 121) * 1000;
  Date date = new Date(time2);
  System.out.println(date);
  ```

- ```java
  //方法二
  Date date1 = new Date();
  date1.setTime(time2);
  System.out.println(date1);
  ```

##### SimpleDateFormat

SimpleDateFormat类作用

- 可以对Date对象或事件毫秒值格式化成喜欢的时间形式

- 也可以把字符串的时间形式解析成日期对象

- ![](D:\mybatis笔记\images\j33.png)

- ![](D:\mybatis笔记\images\j34.png)

- ```java
  //格式化日期对象（指定最终格式化的形式）
  SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss EEE a");
  //日期对象
  Date date = new Date();
  //开始格式化日期对象成为喜欢的字符串形式
  String rs = simpleDateFormat.format(date);
  System.out.println(rs);
  
  //格式化时间毫秒值
  long time = System.currentTimeMillis();
  long time1 = time + (60*60+121)*1000;
  String rs1 = simpleDateFormat.format(time1);
  System.out.println(rs1);
  ```

- 案例：请计算出2021年08月06日11点11分11秒，往后走2天14小时49分06秒的时间是多少。

- ```java
  //目标：学会使用SimpleDateFormat解析字符串时间成为日期对象
  //请计算出2021年08月06日11点11分11秒，往后走2天14小时49分06秒的时间是多少。
  //把字符串时间拿到程序中来
  String datestr = "2021年08月06日 11点11分11秒";
  SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy年MM月dd日 HH点mm分ss秒");
  Date date = simpleDateFormat.parse(datestr);
  long time = date.getTime()+(2*24*60*60+14*60*60+49*60+6) * 1000;
  date.setTime(time);
  simpleDateFormat.format(date);
  System.out.println(date);
  ```

案例：秒杀案例

```java
public static void main(String[] args) throws ParseException {
    /**
     秒杀开始时间：2020年11月11日 0:0:0
     秒杀结束时间：2020年11月11日 0:10:0
     需求
        小家下单并付款的时间为：2020年11月11日 0:03:47
        小皮下单并付款的时间为：2020年11月11日 0:10:11
        用代码说明这两位铜须有没有参加上秒杀活动？
     分析：
        判断下单时间是否在开始到结束的范围内
        把字符串形式的时间变成毫秒值
     */
    String dateStr1 = "2020年11月11日 0:03:47";
    String dateStr2 = "2020年11月11日 0:10:11";
    SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss");
    Date jiaTime = simpleDateFormat.parse(dateStr1);
    Date piTime = simpleDateFormat.parse(dateStr2);

    String startDate = "2020年11月11日 0:0:0";
    Date startTime = simpleDateFormat.parse(startDate);
    String endDate = "2020年11月11日 0:10:0";
    Date endTime = simpleDateFormat.parse(endDate);
    if (jiaTime.after(startTime) && jiaTime.before(endTime)){
        System.out.println("小家下单成功");
    }
    if (piTime.after(startTime) && piTime.before(endTime)){
        System.out.println("小皮下单成功");
    }
```

##### Calendar

Calendar概述

- Calendar代表了系统此刻日期对应的日历对象

- Calendar是一个抽象类，不能直接创建对象

- public static Calendar getInstance():获取当前日历对象

- 常用方法：  

  - ![](D:\mybatis笔记\images\j35.png)

  - ```java
    Calendar calendar = Calendar.getInstance();
    int year = calendar.get(Calendar.YEAR);
    System.out.println(year);
    int month = calendar.get(Calendar.MONTH)+1;
    System.out.println(month);
    int days = calendar.get(Calendar.DAY_OF_YEAR);
    System.out.println(days);
    ```

  - **注：**calendar是可变日期对象，一旦修改后其对象本身表示的时间将产生变化

#### 14.2JDK8新增日期类

新增的API严格区分了时刻、本地日期、本地时间，并且，对日期和时间进行运算更加方便。
其次，新API的类型几乎全部是不变类型（和String的使用类似），可以放心使用不必担心被修改。

##### 概述、LocalTime(不含日期的时间)、LocalDate(不包含具体时间的日期)、LocalDateTime(包含日期及时间)

![](D:\mybatis笔记\images\j36.png)

```java
//1.获取本地日期对象
LocalDate nowDate = LocalDate.now();
System.out.println(nowDate); //今天日期

int year = nowDate.getYear();
System.out.println("year:"+year);

int month = nowDate.getMonthValue();
System.out.println("month:"+month);

int day = nowDate.getDayOfMonth();
System.out.println(day);

//当年的第几天
int dayOfYear = nowDate.getDayOfYear();
System.out.println(dayOfYear);

//星期几
System.out.println(nowDate.getDayOfWeek());
System.out.println(nowDate.getDayOfWeek().getValue());
//月份
System.out.println(nowDate.getMonth());
System.out.println(nowDate.getMonth().getValue());
LocalDate bt = LocalDate.of(1991, 11, 11);
System.out.println(bt);//直接传入对应的年月日
System.out.println(LocalDate.of(1991,Month.NOVEMBER, 11));
```

```java
//获取本地时间对象
    LocalTime nowTime = LocalTime.now();
    System.out.println(nowTime); //今天时间

    int hour = nowTime.getHour();
    System.out.println(hour);

    int minute = nowTime.getMinute();
    System.out.println(minute);

    int second = nowTime.getSecond();
    System.out.println(second);

    int nano = nowTime.getNano();//纳秒
    System.out.println(nano);

    System.out.println(LocalTime.of(8, 20));//时分
    System.out.println(LocalTime.of(8, 20, 30));
    System.out.println(LocalTime.of(8,20,30, 19000000));

    //LocalDateTime
    System.out.println(LocalDateTime.of(1991,11,11,8,20));
    System.out.println(LocalDateTime.of(1991, Month.NOVEMBER,11,8,20,30));
    System.out.println(LocalDateTime.of(1991,11,11,8,20,30,190000000));
```

![](D:\mybatis笔记\images\j37.png)

![](D:\mybatis笔记\images\j38.png)

##### Instant(代表的是时间戳)

- JDK8获取时间戳特别简单，且功能更丰富。Instant类由一个静态的工厂方法now()可以返回当前时间戳
- ![](D:\mybatis笔记\images\j39.png)
- 时间戳是包含日期和时间的，与java.util.Date很类似，事实上Instant就是类似JDK8以前的Date
- Instant和Date两个类可以进行转换

##### DateTimeFormatter(用于做时间的格式化和解析的)

- 在JDK8中，引入一个全新的日期与时间格式器DateTimeFormatter
- 正反都能调用format方法

##### Duration(用于计算两个"时间"间隔)、Period(用于计算两个"日期"间隔)

- 在Java8中，可以使用以下类计算**时间**间隔差异：java.time.Duration

- 提供了使用基于时间的值测量时间量的方法

- 用于LocalDateTime之间的比较。也可用于Instance之间的比较

- ```java
  LocalDateTime localDateTime = LocalDateTime.now();
  System.out.println(localDateTime);
  LocalDateTime birthDate = LocalDateTime.of(1998,10,1,10,50,30);
  System.out.println(birthDate);
  Duration duration = Duration.between(birthDate, localDateTime);
  System.out.println(duration.toDays());
  System.out.println(duration.toHours());
  System.out.println(duration.toMinutes());
  System.out.println(duration.toMillis());
  System.out.println(duration.toNanos());
  ```

##### period

- 在Java8中，我们可以使用以下类来计算**日期**间隔差异：java.time.Period

- 主要是Period类方法getYears(),getMonths()和getDays()来计算，只能精确到年月日

- 用于LocalDate之间的比较

- ```java
  LocalDate today = LocalDate.now();
  System.out.println(today);
  LocalDate birthday = LocalDate.of(1995, 1, 11);
  System.out.println(birthday);
  Period period = Period.between(birthday,today);
  System.out.printf("年龄:%d年%d月%d日",period.getYears(),period.getMonths(),period.getDays());
  ```

##### ChronoUnit

- ChronoUnit类用于在单个时间单位内测量一段时间，这个工具类是最全的，可以用于比较所有的时间单位
- ![](D:\mybatis笔记\images\j40.png)

#### 14.3包装类

- 其实就是8种基本数据类型对应的引用类型
- ![](D:\mybatis笔记\images\j41.png)

为什么提供包装类？

- Java为了实现一切皆对象，为8种基本类型提供了对应的引用类型
- 后面的集合和泛型其实也只能支持包装类型，不支持基本数据类型

自动装箱：基本类型的数据和变量可以直接赋值给包装类型的变量

自动拆箱：包装类型的变量可以直接赋值给基本数据类型的变量

包装类的特有功能

- 包装类的变量的默认值可以是null，容错率更高
- 可以把基本类型的数据转换成字符串类型(用处不大)
  - 调用toString()方法得到字符串结果
  - 调用Integer.toString(基本类型的数据)
- 可以把字符串类型的数值转换成真实的数据类型(有用)
  - Integer.parseInt("字符串类型的整数")   可以直接调用valueof
  - Double.parseDouble("字符串类型的小数")     可以直接调用valueof

#### 14.4正则表达式

##### 1.匹配规则

正则表示

- 正则表达式可以用一些规定的字符来指定规则，并用来校验数据格式的合法性

正则表达式初体验

- 需求：假如现在要求校验一个qq号码是否正确，6位及20位之内，必须全部是数字

- 先使用目前所学知识完成校验需求；然后体验一下正则表达式校验

- ```java
  public static void main(String[] args) {
      //需求：校验qq号，必须全部数字6-20位
      System.out.println("请输入qq号码:");
      Scanner scanner = new Scanner(System.in);
      String qq = scanner.next();
      System.out.println(checkQQ(qq));
      System.out.println(checkQQByRegex(qq));
  }
  
  //正则表达式
  public static boolean checkQQByRegex(String qq){
      return qq != null && qq.matches("\\d{6,20}");
  }
  
  public static boolean checkQQ(String qq){
      //1.判断qq长度是否满足要求
      if (qq == null || qq.length() < 6 || qq.length() > 20){
          return false;
      }
      for (int i = 0; i < qq.length(); i++) {
          if (qq.charAt(i) > '9' || qq.charAt(i) < '0'){
              return false;
          }
      }
      return true;
  }
  ```

匹配规则

![](D:\mybatis笔记\images\j42.png)

##### 2.使用正则表达式完成需求

![](D:\mybatis笔记\images\j43.png)

```java
public static void main(String[] args) {
    //手机号、验证格式正确
    //邮箱号码
    //电话号码
    checkPhone();
    checkEmail();
    checkTel();

}
//手机号码
public static void checkPhone(){
    while (true){
        System.out.println("请输入您的手机号");
        Scanner scanner = new Scanner(System.in);
        String phone = scanner.next();
        if (phone.matches("1[3-9]\\d{9}")){
            System.out.println("手机格式正确，注册完成");
            break;
        }else {
            System.out.println("格式有误");
        }
    }
}

//邮箱
public static void checkEmail() {
    while (true) {
        System.out.println("请输入您的邮箱");
        Scanner scanner = new Scanner(System.in);
        String phone = scanner.next();
        if (phone.matches("\\w{1,30}@[A-Za-z0-9]{2,20}(\\.[a-zA-Z0-9]{2,20}){1,2}")) {
            System.out.println("邮箱格式正确，注册完成");
            break;
        } else {
            System.out.println("格式有误");
        }
    }
}
    //校验电话号码
    public static void checkTel(){
        while (true){
            System.out.println("请输入您的电话");
            Scanner scanner = new Scanner(System.in);
            String phone = scanner.next();
            if (phone.matches("0\\d{2,6}-?\\d{5,20}")){
                System.out.println("格式正确，注册完成");
                break;
            }else {
                System.out.println("格式有误");
            }
        }
    }
```

##### 3.正则表达式在方法中的应用

![](D:\mybatis笔记\images\j44.png)

```java
public static void main(String[] args) {
    String name = "小路adsfsd小小sjkdj大大";
    String[] arr = name.split("\\w+");
    System.out.println(Arrays.toString(arr));
    String name2 = name.replaceAll("\\w+","  ");
    System.out.println(name2);
}
```

##### 4.匹配爬取到的内容

```java
String rs = "来黑马程序学Java，电话020-43422424，或者联系邮箱"+
        "itcast@itcast.cn，电话1876283633，0203232323"+
        "邮箱bazai@itcast.cn，400-100-3233，4001003232";
//需求：从上面的内容中爬取出 电话号码和邮箱
//1.定义爬取规则
String regex = "(\\w{1,}@\\w{2,10}(\\.\\w{2,10}){1,2})|" +
        "(1[3-9]\\d{9})|(0\\d{2,5}-?\\d{5,15})|400-?\\d{3,8}-?\\d{3,8}";
//2.编译正则表达式成为一个匹配规则对象
Pattern pattern = Pattern.compile(regex);
//3.通过匹配规则对象得到一个匹配数据内容的匹配器对象
Matcher matcher = pattern.matcher(rs);
//4.通过匹配器去内容中爬取出信息
while (matcher.find()){
    System.out.println(matcher.group());
}
```

#### 14.5Arrays类

#### 14.6常见算法

#### 14.7Lambda表达式枚举

## 15.集合

### 15.3常见数据结构

- 1.栈
  
  - 先进后出，后进先出
  
- 2.队列
  
  - 先进先出，后进后出
  
- 3.数组
  - 查询速度快：通过地址值和索引定位，查询任意数据耗时相同（元素在内存中连续存储）
  - 删除效率低：要将原始数据删除，同时后面每个数据前移
  - 添加效率低：添加位置后的每个数据后移，再添加元素
  
- 4.链表
  - 链表中的元素是在内存中不连续存储的，每个元素节点包含数据值和下一个元素的地址。
  - 查询慢：无论查询哪个数据都要从头开始找
  - 删除添加相对快
  - 种类：单向链表、双向链表
  
- 5.二叉树、二叉查找树 

- 6.平衡二叉树 

- 7.红黑树

  - 是一种自平衡的二叉查找树
  - 每一个节点可以是红或者黑，红黑树不是通过高度平衡的，是通过红黑规则进行实现的

  红黑规则：

  - 每个节点红或黑，根节点必须是黑色
  - 如果一个节点没有子节点或者父节点，则该节点相应的指针属性值为Nil，这些Nil视为叶节点，叶节点是黑色的
  - 如果某一个节点是红色，那么它的子节点必须是黑色（不能出现两个红色节点相连的情况）
  - 对每一个节点，从该节点到其所有后代叶节点的简单路径上，均包含相同数目的黑色节点

  添加节点：

  - 添加的节点的颜色可以是红色，也可以黑色
  - 默认用红色效率高
  - 若是用黑色，添加三个元素一共要调整两次
  - 若是用红色，添加三个元素一共要调整一次

### 15.4List系列集合

### 15.5Map集合体系

#### 1.概述

- Map集合是一种双列集合，每个元素包含两个数据
- Map集合的每个元素的格式：key=value（键值对元素）
- 也称“键值对集合”

Map集合整体格式：

- Collection集合的格式：[元素1，元素2，元素3...]
- Map集合的完整格式：{key1=value1, key2=value2，key3=value3,....}

Map集合的使用场景之一：

- 如购物车的商品和购买数量一一对应
- 把商品看作是Map集合的键，购买数量看成Map集合的值
- {商品1=2，商品2=3}

#### 2.集合体系特点

![](D:\mybatis笔记\images\j45.png)

- Map集合的键无序，不重复，无索引，Map集合的值不做要求
- Map集合后面重复的键对应的值会覆盖前面重复键的值
- Map集合的键值对都可以为null

Map集合实现类的特点

- HashMap：键无序，不重复，无索引，值不做要求
- LinkedHashMap：元素按照键有序，不重复，无索引，值不做要求
- TreeMap：元素按照键有序，不重复，无索引，值不做要求

#### 3.常用API

- Map是双列集合的祖宗接口，它的功能是全部双列集合都可以继承使用

![](D:\mybatis笔记\images\j46.png)

#### 4.遍历方式一：键找值

- 先获取Map集合的全部键的Set集合

  - Set<K> keySet()   获取所有键的集合

- 遍历键的Set集合，然后通过键提取对应值

  - V get(Object key)    根据键获取值

  - ```java
    Set<String> keys = maps.keySet();
    for (String key : keys) {
        System.out.println(key+"="+maps.get(key));
    }
    ```

#### 5.遍历方式二：键值对

- 先把Map集合转换成Set集合，Set集合中每个元素都是键值对实体类型了
  - Set<Map.Entry<K,V>> entrySet()      获取所有键值对对象的集合
- 遍历Set集合，然后提取键以及提取值
  - K getKey()   获取键
  - K getValue()    获取值

```java
Set<Map.Entry<String, Integer>> entries = maps.entrySet();
for (Map.Entry<String, Integer> entry : entries) {
    System.out.println(entry.getKey()+"===="+entry.getValue());
}
```

#### 6.遍历方式三：lambda表达式

- Map结合Lambda遍历的API
- default void forEach(BiConsumer<? super K, ? super V> action)    结合lambda遍历Map集合

```java
maps.forEach((key, value) ->{
        System.out.println(key+"===>"+value);
});
```

Map集合案列-统计投票人数

- 需求：某个班级80名学生，组织秋游，提供A,B,C,D四个景点，每个人选一个，统计哪个景点人最多

- 分析：

  - 将80个学生选择的数据拿到程序中去

  - 定义Map集合用于存储最终统计的结果

  - 遍历80个学生选择的数据，看Map集合中是否存在，不存在存入“数据=1”，存在则其对应值+1

  - ```java
    String[] selects = {"A", "B", "C", "D"};
        StringBuilder sb = new StringBuilder();
        Random random = new Random();
        for (int i = 0; i < 80; i++) {
            sb.append(selects[random.nextInt(selects.length)]);
        }
        Map<Character, Integer> map = new HashMap<>();
        Set<Character> keySet = map.keySet();
        for (int i = 0; i < sb.length(); i++){
            char c = sb.charAt(i);
            if (map.containsKey(c)){
                map.put(c, map.get(c)+1);
            }else {
                map.put(c, 1);
            }
        }
        map.forEach((K, V) -> {
            System.out.println(K+"="+V);
        });
    }
    ```

#### 7.实现类HashMap

- 特点(由键决定)：无序、不重复，无索引
- HashMap和HashSet底层原理一样，都是哈希表结构，只是HashMap的每个元素包含两个值而已，依赖hashCode方法和equals方法保证键的唯一
- 注：**实际上：Set系列集合的底层就是Map实现的，只是Set集合中的元素只要键数据，不要值数据而已**
- 如果键要存储的是自定义对象，需要重写hashCode和equals方法。
- 基于哈希表。增删改查的性能都较好。

#### 8.实现类LinkedHashMap

- 由键决定：有序、不重复、无索引
- 有序指的是保证存储和取出的元素顺序一致
- 原理：底层数据结构是哈希表，只是每个键值对元素又额外多了一个双链表的机制记录存储的顺序

#### 9.实现类TreeMap

- 由键决定特性：不重复、无索引、可排序
- 可排序：按照键数据的大小默认升序排序。只能对键排序
- 注意：TreeMap集合是一定要排序的，可以默认排序，也可以将键按照指定的规则进行排序
- TreeMap跟TreeSet一样底层原理是一样的。

TreeMap集合自定义排序规则有两种

- 类实现Comparable接口，重写比较规则
- 集合自定义Comparator比较器对象，重写比较规则。

#### 10.嵌套使用

```java
Map<String, List<String>> maps = new HashMap<>();
    List<String> selects = new ArrayList<>();
    Collections.addAll(selects, "A","B");;
    maps.put("yyue1",selects);
    List<String> selects1 = new ArrayList<>();
    Collections.addAll(selects1, "A","C");;
    maps.put("yyue2",selects1);
    List<String> selects2 = new ArrayList<>();
    Collections.addAll(selects2, "A","C", "D");;
    maps.put("yyue3",selects2);
    System.out.println(maps);

    Map<String, Integer> infos = new HashMap<>();
    Collection<List<String>> values = maps.values();
    for (List<String> value : values) {  //[A,B]  [A,C]
        for (String s : value) {
            if (infos.containsKey(s)){
                infos.put(s, infos.get(s)+1);
            }else {
                infos.put(s, 1);
            }
        }
    }
    System.out.println(infos);
}
```

### 16.Stream、异常体系、日志框架

#### 1.创建不可变集合

- 不可变集合：不能被修改的集合
- 集合的数据项在创建的时候提供，并且在整个生命周期中都不可改变，否则报错。

为什么要创建不可变集合？

- 如果某个数据不能被修改，把它防御性地拷贝到不可变集合中是一个很好的实践
- 或者当集合对象被不可信的库调用时，不可变形式是安全的。

如何创建不可变集合？

- 在List、Set、Map接口中，都存在of方法，可以创建一个不可变的集合

  - static <E> List<E> of(E...elements)     创建一个具有指定元素的List集合对象  

    - ```java
      List<Double> doubleList = List.of(12.1, 13.2, 14.2);
      ```

  - static <E> Set<E> of(E...elements)     创建一个具有指定元素的Set集合对象

  - static <E> Map<E> of(E...elements)     创建一个具有指定元素的Map集合对象

- 这个集合不能添加、删除、修改

#### 2.Stream流

##### 1.概述

目的：用于简化集合和数组操作的API

- 初体验Stream流

- ```java
  List<String> names = new ArrayList<>();
  Collections.addAll(names, "张三丰","张无忌","周芷若","赵敏","张强");
  //从集合中找出姓张的放入新集合
  List<String> zhangList = new ArrayList<>();
  for (String name : names) {
      if (name.startsWith("张")){
          zhangList.add(name);
      }
  }
  System.out.println(zhangList);
  List<String> zhangThreeList = new ArrayList<>();
  for (String s : zhangList) {
      if (s.length() == 3){
          zhangThreeList.add(s);
      }
  }
  System.out.println(zhangThreeList);
  names.stream().filter(s -> s.startsWith("张")).filter(s -> s.length()==3).forEach(s -> System.out.println(s));
  ```

总结：

1. Stream流的作用是什么，结合了什么技术？
   - 简化集合、数组操作的API，结合了lambda表达式
2. 说说Stream流的思想和使用步骤
   - 先得到集合或者数组的Stream流（即一根传送带）
   - 把元素放上去
   - 然后就用这个stream流简化的API来方便的操作元素

##### 2.Stream流的获取

Stream流的三类方法

- 获取Stream流

  - 创建一条流水线，并把数据放到流水线上准备进行操作

  - ```java
    //Collection集合获取流
    Collection<String> list = new ArrayList<>();
    Stream<String> s = list.stream();
    
    //Map集合获取流
    Map<String, Integer> maps = new HashMap<>();
    Stream<String> keyStream = maps.keySet().stream();//键流
    Stream<Integer> valueStream = maps.values().stream();//值流
    Stream<Map.Entry<String, Integer>> keyAndValueStream = maps.entrySet().stream();//键值对流
    
    //数组获取流
    String[] names = {"111","ddd","aaa"};
    Stream<String> arrayStream = Arrays.stream(names);
    Stream<String> arrayStream2 = Stream.of(names);
    ```

  - 总结

    - 集合获取Stream的方式通过调用stream()方法实现
    - 数组有两种方法获取stream流
      - public static <T> Stream<T> stream(T[] array)   获取当前数组的stream流
      - public static <T> Stream<T> of(T... values)    获取当前数组/可变数据的Stream流

- 中间方法

  - 流水线上的操作。一次操作完毕之后，还可以继续进行其他操作

- 终结方法

  - 一个Stream流只能有一个终结方法，是流水线上的最后一个操作
  - 常见终结操作
    - void forEach(Consumer action)   对此流的每个元素执行遍历操作
    - long count() 返回此流中的元素数
  - 终结方法后流不可以继续使用，非终结方法返回新的流，支持链式编程

##### 3.Stream流的常用API（中间操作方法）

**注：中间方法也成为非终结方法，调用完成后返回新的Stream流可以继续使用，支持链式编程**

- Stream<T> filter(Predicate<? super T> predicate)   用于对流中的数据进行过滤

  - ```java
    //过滤以及计数
    long count = names.stream().filter(s -> s.length() == 3).count();
            System.out.println(count);
    ```

- Stream<T> limit(long maxSize)    获取前几个元素

  - ```java
    names.stream().filter(s->s.startsWith("张")).limit(2).forEach(System.out::println);
    ```

- Stream<T> skip(long n)    跳过前几个元素

  - ```java
    names.stream().skip(2).forEach(System.out::println);
    ```

- Stream<T> distinct()  去除流中重复的元素，依赖（hashCode和equals方法）

- static <T> Stream<T> concat(Stream a, Stream b)    合并a和b两个流为一个流

  - ```java
    //流的合并
    Stream<String> s1 = names.stream().filter(s->s.startsWith("张"));
    Stream<String> s2 = Stream.of("java1", "java2");
    Stream<String> s3 = Stream.concat(s1, s2);
    s3.forEach(System.out::println);
    ```

- map方法

  - ```java
     //加工对集合中的每个数据进行加工
    //        names.stream().map(new Function<String, String>() {
    //            @Override
    //            public String apply(String s) {
    //                return "yyue"+s;
    //            }
    //        });
            //Map加工方法：第一个参数原材料   第二个参数是加工后的结果
            names.stream().map(s -> "yyue" + s).forEach(System.out::println);
            //将每个名字加工成学生类
    //        names.stream().map(s->new Student(s)).forEach(System.out::println);
            names.stream().map(Student::new).forEach(System.out::println);//构造器引用   方法引用
    ```

##### 4.Stream流的综合应用

```java
public class StreamDemo {
    public static double allmoney1;
    public static double allmoney2;
    public static double allmoney;
    public static void main(String[] args) {
        List<Employee> one = new ArrayList<>();
        one.add(new Employee("yyue1", '男', 30000, 25000, null));
        one.add(new Employee("yyue2", '女', 25000, 1000, "顶撞上司"));
        one.add(new Employee("yyue3", '男', 20000, 20000, null));
        one.add(new Employee("yyue4", '男', 20000, 25000, null));
        List<Employee> two = new ArrayList<>();
        two.add(new Employee("yyue5", '男', 15000, 9000, null));
        two.add(new Employee("yyue6", '男', 20000, 10000, null));
        two.add(new Employee("yyue7", '男', 50000, 100000, "被打"));
        two.add(new Employee("yyue8", '女', 3500, 1000, "被打"));
        two.add(new Employee("yyue9", '女', 20000, 0, "被打"));

        //定义一个比较器，比较员工工资,获取工资最高的员工
        Topperformer topperformer = one.stream().max((o1,o2)-> Double.compare(o1.getSalary() + o1.getBonus(), o2.getSalary() + o2.getBonus()))
                .map(e -> new Topperformer(e.getName(), e.getSalary() + e.getBonus())).get();
        System.out.println(topperformer);

        one.stream().sorted((o1,o2)-> Double.compare(o1.getSalary() + o1.getBonus(), o2.getSalary() + o2.getBonus()))
                .skip(1).limit(one.size()-2).forEach(e -> {
                    //求出总和，剩余员工的工资总和
            allmoney1 += (e.getSalary()+e.getBonus());
        });
        System.out.println("开发一部的平均工资是：" + allmoney1/(one.size()-2));
        two.stream().sorted((o1,o2)-> Double.compare(o1.getSalary() + o1.getBonus(), o2.getSalary() + o2.getBonus()))
                .skip(1).limit(two.size()-2).forEach(e -> {
            //求出总和，剩余员工的工资总和
            allmoney2 += (e.getSalary()+e.getBonus());
        });
        System.out.println("开发二部的平均工资是：" + allmoney2/(two.size()-2));

        //合并两个部门
        Stream<Employee> allEmployeee = Stream.concat(one.stream(), two.stream());
        allEmployeee.sorted((o1,o2)-> Double.compare(o1.getSalary() + o1.getBonus(), o2.getSalary() + o2.getBonus()))
                .skip(1).limit(one.size()+two.size()-2).forEach(e -> {
            //求出总和，剩余员工的工资总和
            allmoney += (e.getSalary()+e.getBonus());
        });
        System.out.println("开发部整体的平均工资是：" + allmoney/(one.size()+two.size()-2));
    }
}
```

##### 5.收集Stream流

- 将流收集成List类型

- ```java
  Stream<String> s1 = names.stream().filter(s -> s.startsWith("张"));
  List<String> zhangList = s1.collect(Collectors.toList());
  System.out.println(zhangList);
  ```

- **注：流只能使用一次，意味着收集一次流之后，该流就不存在了。**

- 将流收集成Set类型

- ```java
  Stream<String> s2 = names.stream().filter(s -> s.startsWith("张"));
  Set<String> zhangSet = s2.collect(Collectors.toSet());
  System.out.println(zhangSet);
  ```

- 将流收集成数组类型

- ```java
  Stream<String> s3 = names.stream().filter(s -> s.startsWith("张"));
  String[] arrs = a3.toArray(String[]::new);
  System.out.println("Arrays数组内容：" + Arrays.toString(arrs));
  ```

#### 3.异常处理

##### 1.异常概述、体系

- 异常是程序在编译或者执行的过程中可能出现的问题
- 比如：数组索引越界、空指针异常、日期格式化异常等
- ![](D:\mybatis笔记\images\j47.png)

##### 2.常见运行时异常

- 直接继承自RuntimeException或者其子类，编译阶段不会报错，运行时可能出现的错误。

- 运行时异常示例

  - 数组索引越界异常：ArrayIndexOutOfBoundsException

    - ```java
      int[] arr = {1,2};
      System.out.println(arr[1]);
      System.out.println(arr[2]);
      ```

  - 空指针异常：NullPointerException，直接输出没有问题，但是调用空指针的变量的功能就会报错

    - ```java
      String name = null;
      System.out.println(name.length());
      ```

  - 数字操作异常：ArithmeticException

    - ```java
      int a = 10/0;
      ```

  - 类型转换异常：ClassCastException

    - ```java
      Object o = 21;
      String i = (String) o;
      ```

  - 数字转换异常：NumberFormatException

    - ```Java
      String b ="23abbb";
      Integer c = Integer.valueOf(b);
      System.out.println(c);
      ```

##### 3.常见编译时异常

- 不是RuntimeException或者其子类的异常，编译阶段就会报错，必须处理，否则代码不通过

- 示例：日期解析异常ParseException

  - ```java
    String date = "2015-01-12 10:23:21";
    SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
    Date d = sdf.parse(date);
    System.out.println(d);
    ```

##### 4.异常的默认处理流程

- 默认会在出现异常的代码那里自动的创建一个异常对象：如ArithmeticException
- 异常会从方法中出现的点这里抛出给调用者，调用者最终抛出给JVM虚拟机
- 虚拟机接收到异常对象后，先在控制台直接输出异常栈信息数据
- 直接从当前执行的异常点干掉当前程序
- 后续代码没有机会执行了，因为程序已经死亡

总结：默认异常处理机制：并不好，一旦出现异常，程序立即死亡

##### 5.编译时异常的处理机制

编译时异常的处理形式有三种：

- 出现异常直接抛出去给调用者，调用者也继续抛出去
- 出现异常自己捕获处理，不麻烦别人
- 前两者结合，出现异常直接抛出去给调用者，调用者捕获处理。

处理方式一：throws

- throws：用在方法上，可以将方法内部出现的异常抛出去给本方法的调用者处理。
- 这种方式并不好，发生异常的方法自己不处理异常，如果异常最终抛出去给虚拟机将会引起程序死亡
- 抛出异常格式
  - 方法 throws 异常1,异常2,异常3..{   }
- 规范做法：
  - 方法 throws Exception{      }

处理方式2----try...catch...

- 监视捕获异常，用在方法内部，可以将方法内部出现的异常直接捕获处理

- 这种方式还可以，发生异常的方法自己独立完成异常的处理，程序可以继续往下执行

- 格式

  - ```java
    try{
    //监视可能出现异常的代码
    }catch(异常类型1 变量){
    //处理异常
    }catch(异常类型2 变量){
    //处理异常
    }
    ```

- 建议格式：

  - ```java
    try{
    //可能出现异常的代码
    }catch(Exception e){
    e.printStackTrace();//直接打印异常栈信息
    }
    //Exception可以捕获处理一切异常类信息
    ```

处理方式3--------前两者结合

- 方法直接将异常通过throws抛出去给调用者
- 调用者收到异常后直接捕获处理（try  catch）

##### 6.运行时异常的处理机制

处理形式

- 运行时异常编译阶段不会出错，是运行时才可能出错的，所以编译阶段不处理也可以
- 按照规范建议还是处理：建议在最外层调用处集中捕获处理即可

##### 7.异常处理使代码更稳健的案例

```java
public class Test {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        while (true){
            try {
                System.out.println("请输入合法价格：");
                String priceStr = sc.nextLine();
                double price = Double.valueOf(priceStr);
                if (price > 0){
                    System.out.println("定价:"+price);
                    break;
                }else {
                    System.out.println("价格不能为负数");
                }
            } catch (Exception e) {
                System.out.println("用户输入的数据有问题");
            }
        }
    }
}
```

没加try,catch时，用户乱输入字符串，程序就会崩掉。

加了异常处理之后，出现错误，用户可以继续输入，直到输入正确为止。

##### 8.自定义异常

1. 自定义编译时异常

   - 定义一个异常类继承Exception

   - 重写构造器

   - 在出现异常的地方用throw new自定义对象抛出

   - throw与throws区别

     - throw用在方法内部直接创建一个异常对象，并抛出
     - throws用在方法声明上的，抛出方法内部的异常

   - 例子：自定义一个检测年龄是否合法的异常

   - ```java
     //1.继承Exception
     public class AgeIlleagalException extends Exception {
         //需求：认为年龄小于0岁，大于200岁就是一个异常
         //重写构造器
         public AgeIlleagalException(){
         }
     
         public AgeIlleagalException(String message) {
             super(message);
         }
     }
     ```

   - ```java
     public class ExceptionDemo{
         public static void main(String[] args) {
             try {
                 checkAge(-13);
             } catch (AgeIlleagalException e) {
                 e.printStackTrace();
             }
         }
         public static void checkAge(int age) throws AgeIlleagalException {
             if (age < 0 || age > 200){
                 throw new AgeIlleagalException(age+"是非法的");
             }else {
                 System.out.println("年龄合法。。。");
             }
         }
     }
     ```

2. 自定义运行时异常

   - 定义一个异常类继承RuntimeException
   - 重写构造器
   - 在出现异常的地方用throw new自定义对象抛出
   - 作用：提醒不强烈，编译阶段不报错，运行时才可能出现
   - 将上面继承的编译时异常换成继承运行时异常RuntimeException

#### 4.日志框架

##### 1.日志技术概述

日志优势：

- 可以将系统执行的信息选择性的记录到指定的位置（控制台、文件中、数据库中）
- 可以随时以开关的形式控制是否记录日志，无需修改源代码

##### 2.日志技术体系结构

日志规范是一些接口，提供给日志的实现框架设计的标准。

- Commons Logging简称JCL
- Simple Logging Facade for Java简称slf4j

日志框架是牛人或者第三方公司已经做好的日志记录实现代码，后来者可以直接用

- Log4j、JUL、Logback、其他实现

##### 3.Logback概述

Logback日志框架

- Logback由log4j创始人设计的另一个开源日志组件，性能比log4j要好
- Logback是基于slf4j的日志规范实现的框架
- 主要分为三个技术模块：
  - logback-core：为其他两个模块奠定了基础，必须有
  - logback-classic：是log4j的一个改良版本，同时完整实现了slf4jAPI
  - logback-access模块与tomcat和Jetty等servlet容器集成，以提供HTTP访问日志功能

##### 4.Logback快速入门

- 导入相关依赖
- 核心配置文件logback.xml拷贝到src目录下，springboot项目放在resources目录下
- 在代码中获取日志对象
- 使用日志对象输出日志信息

##### 5.Logback配置详解-输出位置、格式设置

Logback日志系统的特性都是通过核心配置文件logback.xml控制的

- 通过logback.xml中的<append>标签可以设置输出位置和日志信息的详细格式

- 通常可以设置两个日志输出位置：一个是控制台，一个是系统文件

  - 输出到控制台

  - ```xml
    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender"></appender>
    ```

  - 输出到文件

  - ```xml
    <appender name="FILE" class="ch.qos.logback.core.rolling.RollingFileAppender"></appender>
    ```

##### 6.Logback配置详解-日志级别设置

日志级别：

- 级别程度：TRACE<DEBUG<INFO<WARN<ERROR；默认是debug
- 作用：用于控制系统中哪些日志级别是可以输出的，只输出级别不低于设定级别的信息
- ALL和OFF分别是打开全部日志信息，及关闭全部日志信息

### 17.项目实战

### 18.File

1.先要定位文件

- File类可以定位文件：进行删除、获取文本本身信息等操作
- 但是不能读写文件内容

2.读写文件数据

- IO流技术可以对硬盘中的文件进行读写

File类的使用---》方法递归--》字符集--》IO流的作用、分类--》字节流、字符流

#### 1.File类概述

- File类在包java.io.File下、代表操作系统的文件对象(文件、文件夹)
- File类提供了诸如：定位文件，获取文件本身的信息、删除文件、创建文件（文件夹）等功能

File类创建对象

| 方法名称                          | 说明                                                 |
| --------------------------------- | ---------------------------------------------------- |
| File(File parent, String child)   | 根据父路径对应文件对象和子路径名字字符串创建文件对象 |
| File(String pathname)             | 根据文件路径创建文件对象                             |
| File(String parent, String child) | 从父路径名字符串和子路径名字符串创建文件对象         |

- File对象可以定位文件和文件夹

- File封装的对象仅仅是一个路径名，这个路径可以是存在的，也可以是不存在的

- ```java
  //创建File对象
  File file = new File("D:\\picture\\a2.jpg");
  long size = file.length();
  System.out.println(size);
  //File创建对象即支持绝对路径，也支持相对路径
  //相对路径：一般定位模块中的文件
  File file1 = new File("file-io/src/data.txt");
  System.out.println(file1.length());
  ```

#### 2.File类的常用API

- 判断文件类型、获取文件信息

- ```java
  File file1 = new File("file-io/src/data.txt");
          System.out.println(file1.length());
  //        File file2 = new File("D:\\picture");//文件夹的大小拿不到
  //        System.out.println(file2.length());
          //a.获取文件的绝对路径
          System.out.println(file1.getAbsolutePath());
          //b.获取文件定义的时候使用的路径
          System.out.println(file1.getPath());
          //c.获取文件的名称：带后缀
          System.out.println(file1.getName());
          //d.获取文件的大小：字节个数
          System.out.println(file1.length());
          //e.获取文件的最后修改时间
          System.out.println("最后修改时间"+new SimpleDateFormat("yyyy-MM-dd HH:mm:ss").format(file1.lastModified())); 
  ```

- 创建文件、删除文件功能

- ```java
  public class FileDemo02 {
      public static void main(String[] args) throws IOException {
          File file = new File("file-io\\src\\data.txt");
          //a.创建新文件，创建成功返回true，反之，不需要这个，以后文件写出去的时候都会自动创建
          System.out.println(file.createNewFile());//创建失败，因为已经存在
          File file1 = new File("file-io\\src\\data1.txt");
          System.out.println(file1.createNewFile());//创建成功
          //b.mkdir创建一级目录
          File file2 = new File("D:/picture/aaa");
          System.out.println(file2.mkdir());
          //c.mkdirs创建多级目录(重点)
          File file3 = new File("D:/picture/aaa/a/b/c");
          System.out.println(file3.mkdirs());
          //d.删除文件或者空文件夹
          System.out.println(file3.delete()); //占用时也可以删除
          //只能删除空文件夹，不能删除非空文件夹
      }
  }
  ```

- 遍历文件夹

- | 方法名称                  | 说明                                                         |
  | ------------------------- | ------------------------------------------------------------ |
  | public String[] list()    | 获取当前目录下所有的“以及文件名称”到一个字符串数组中去返回   |
  | public File[] listFiles() | 获取当前目录下所有的“一级文件对象”到一个文件对象数组中去返回 |

- listFiles方法注意事项：

  - 当调用者不存在时，返回null
  - 当调用者是一个文件时，返回null
  - 当调用者是一个空文件夹时，返回一个长度为0的数组
  - 当调用者是一个有内容的文件夹时，将里面所有文件和文件夹的路径放在File数组中返回
  - 当调用者是一个有隐藏文件的文件夹时，将里面所有文件和文件夹的路径放在File数组中返回，包含隐藏内容

#### 3.方法递归（用于文件搜索等）

1. 递归形式和特点

   - 直接递归：方法自己调用自己
   - 间接递归：方法调用其他方法，其他方法又回调方法自己
   - 递归如果没有控制好终止，会出现递归死循环，导致栈内存溢出现象

2. 递归的算法流程、核心要素

   - 递归算法三要素大体可以总结为
   - 递归公式:f(n)=f(n-1)*n
   - 递归的终结点：f(1)
   - 递归的方向必须走向终结点

3. 递归常见案例

   1. ```java
      public class RecursionDemo01 {
          public static void main(String[] args) {
              System.out.println(f(1));
              System.out.println(f(2));
              System.out.println(f(3));
              System.out.println(f1(1));
              System.out.println(f1(2));
              System.out.println(f1(3));
          }
          public static int f(int n){
              if (n == 1){
                  return 1;
              }
              return f(n-1)*n;
          }
          public static int f1(int n){
              if (n ==1){
                  return 1;
              }
              return f1(n-1)+n;
          }
      }
      ```

4. 递归的经典问题

   1. ```java
      //猴子吃桃子，第一天吃桃子总数的二分之一，有多吃一个，第二天重复，到十天桃子只剩1个了
      //f(x)为第x天的桃子总数，f(x+1)为第x+1天的桃子总数
      //f(x)-f(x)/2-1 = f(x+1)
      //=> f(x+1)=f(x)/2-1  => f(x)=2(f(x+1)+1)
      public class RecursionDemo {
          public static void main(String[] args) {
              System.out.println(f(1));
          }
          public static int f(int x){
              if (x == 10)
                  return 1;
              return 2 * (f(x+1)+1);
          }
      }
      ```

5. 非规律化递归案例-文件搜索

   1. ```java
      /**
       * 需求：文件搜索，从D盘中搜索出某个文件名称并输出绝对路径，   UML期末作业.docx
       * 分析：
       * 1.先定位出的应该是一级文件对象
       * 2.遍历全部一级文件对象，判断是否是文件
       * 3.如果是文件，判断是否是自己想要的
       * 4.如果是文件夹，需要继续递归进去重复上述过程
       */
      public class RecursionFileDemo {
          public static void main(String[] args) {
              File file = new File("E:/");
              String fileName = "test.doc";
              searchFile(file, fileName);
          }
          //搜索文件夹下的全部文件，然后找到想要的文件
          public static void searchFile(File dir, String fileName){
              if (dir != null && dir.isDirectory()) {
                  File[] files = dir.listFiles();
                  if (files != null && files.length>0){
                      for (File file : files) {
                          if (file.isFile()){
                              if (file.getName().contains(fileName)){
                                  System.out.println("找到"+file.getAbsolutePath());
                              }
                          }else {
                              searchFile(file, fileName);
                          }
                      }
                  }
              }else {
                  System.out.println("您当前搜索的不是文件夹");
              }
          }
      }
      ```

6. 非规律化递归案例-啤酒问题

   - ```java
     /**
      * 啤酒2元一瓶，4个盖子可以换一瓶，2个空瓶可以换一瓶
      * 请问10元钱可以喝多少瓶啤酒，剩余多少空瓶和盖子
      */
     public class RecursionDemo04 {
         //定义一个静态的成员变量用于存储可以买的酒的数量
         public static int totalNumber;//酒瓶总数量
         public static int remainBottleNumber;//记录每次剩余的瓶子个数
         public static int lastCoverNumber;//记录每次剩余的盖子个数
         public static void main(String[] args) {
             buy(10);
             System.out.println("总数："+totalNumber);
             System.out.println("剩余瓶子数："+remainBottleNumber);
             System.out.println("剩余盖子数："+lastCoverNumber);
         }
         public static void buy(int money){
             //看money可以买几瓶九
             int buyNumber = money/2;
             totalNumber += buyNumber;
             //把盖子和瓶子换算成钱
             int coverNumber = buyNumber + lastCoverNumber;
             int bottle = remainBottleNumber + buyNumber;
             //统计可以换算的钱
             int allMoney = 0;
             if (coverNumber >=4){ //盖子换钱
                 allMoney += (coverNumber/4)*2;
             }
             lastCoverNumber = coverNumber %4;
             if (bottle >= 2){
                 allMoney += (bottle/2) * 2;
             }
             remainBottleNumber = bottle % 2;
             if (allMoney >= 2){
                 buy(allMoney);
             }
         }
     }
     ```

#### 4.字符集

1. 字符串常见的字符底层组成是什么样的？
   - 英文和数字等在任何国家的字符集中都占1个字节
   - GBK字符中一个中文字符占2个字节
   - UTF-8编码中一个中文一般占3个字节
2. 编码前的字符集和编码后的字符集要求
   - 必须一致，否则会出现中文字符乱码
   - 英文和数字在任何国家的编码中都不会乱码

```java
//1.编码，把文字转换成字节（使用指定的编码）
String name = "我爱你中国abc";
byte[] bytes = name.getBytes(StandardCharsets.UTF_8);
System.out.println(Arrays.toString(bytes));
```

```java
String name = "我爱你中国abc";
byte[] bytes = name.getBytes("GBK");
```

![](D:\mybatis笔记\images\j48.png)

#### 5.IO流概述

- I表示input，是数据从硬盘文件读入到内存的过程，称之为输入，负责读
- O表示output，是内存程序的数据从内存到写出到硬盘文件的过程，称之为输出，负责写

**按流的方向分**-----》分为输入流和输出流

**按流中的数据最小单位分为**-----》字节流（操作所有类型的文件）和字符流（只能操作纯文本文件）

总结流的四大类

- 字节输入流（InputStream）：以内存为基准，来自磁盘文件/网络中的数据以字节的形式读入到内存中去的流称为字节输入流
- 字节输出流（OutputStream）：以内存为基准，把内存中的数据以字节写出到磁盘文件或者网络中去的流称为字节输出流
- 字符输入流（Reader）：以内存为基准，来自磁盘文件/网络中的数据以字符的形式读入到内存中去的流称为字符输入流
- 字符输出流（Writer）：以内存为基准，把内存中的数据以字符写出到磁盘文件或者网络中去的流称为字符输出流

#### 6.字节流的使用

![](D:\mybatis笔记\images\j49.png)

- 文件字节输入流：每次读取一个字节

  - FileInputStream

  - 构造器FileInputStream(File file),  FileInputStream(String pathname)

  - 方法read():每次读取一个字节返回，没有可读的返回-1，read(byte[] buffer):每次读取一个字节数组返回，没有可读的返回-1

  - ```java
    public static void main(String[] args) throws IOException {
            //1.创建一个文件字节输入流管道与源文件接通
    //        InputStream inputStream = new FileInputStream(new File("file-io\\src\\data.txt"));
            InputStream inputStream = new FileInputStream("file-io\\src\\data.txt");
            int b1 = inputStream.read();
            System.out.println((char) b1);
            int b2 = inputStream.read();
            System.out.println((char) b2);
            int b3 = inputStream.read();
            System.out.println((char) b3);
            int b4 = inputStream.read();
            System.out.println((char) b4);
            int b5 = inputStream.read();
            System.out.println(b5); //读取完毕返回-1
        }
    ```

  - 修改代码------循环读取一个字节

  - ```java
    int b;
    while ((b = inputStream.read()) != -1){
        System.out.print((char) b);
    }
    ```

  - 性能过低并且无法读取中文

- 文件字节输入流：每次读取一个字节数组

  - ```java
    public static void main(String[] args) throws IOException {
            InputStream inputStream = new FileInputStream("file-io\\src\\data.txt");
            byte[] bytes = new byte[3];
            int len1 = inputStream.read(bytes);
            System.out.println("读取了几个字节"+len1);
            String str1 = new String(bytes);
            System.out.println(str1);
    
            int len2 = inputStream.read(bytes);
            System.out.println("读取了几个字节"+len2);
            String str2 = new String(bytes);
            System.out.println(str2);
    
            int len3 = inputStream.read(bytes);
            System.out.println("读取了几个字节"+len3);
    //        String str3 = new String(bytes);
    //        //只读取了一个字节，但是打印出来确实三个字节，因为桶中只有当前的一个字节加上上一个读取的桶中后两个字节，也就是桶没有倒干净
    //        System.out.println(str3);
            String str3 = new String(bytes,0,len3);//读取多少倒多少
            System.out.println(str3);
        }
    ```

  - 循环读取

  - ```java
    int len;
    while ((len = inputStream.read(bytes)) != -1){
        String str = new String(bytes, 0, len);
        System.out.print(str);
    }
    ```

  - 还是解决不了中文乱码问题

- 文件字节输入流：一次读完全部字节

  - ```java
    public static void main(String[] args) throws IOException {
        File file = new File("file-io\\src\\\\data1.txt");
        InputStream inputStream = new FileInputStream(file);
        byte[] bytes = new byte[(int) file.length()];
        int len = inputStream.read(bytes);
        System.out.println("读取了多少个字节"+len);
        System.out.println("文件大小："+file.length());
        System.out.println(new String(bytes));
    }
    ```

  - 官方在jdk1.9之后提出了一个读取全部字节的API readAllBytes()

- 文件字节输出流：写字节数据到文件

  - ```java
    OutputStream outputStream = new FileOutputStream("file-io\\src\\data3.txt"); //每次输出都会先清空，在写入
    //        outputStream.write('a');
    //        outputStream.write(98);
    //        outputStream.write('杨');  //乱码，因为输出为一个字节，而一个中文占三个字节
            byte[] bytes = {'a',98,97,96};
    
            outputStream.write(bytes,0,2);//控制输出字节长度
            outputStream.write("\r\n".getBytes());//胡安行
            byte[] bytes1 = "我是中国人".getBytes();
            outputStream.write(bytes1);
            outputStream.flush();//刷新
            outputStream.close();//关闭
        }
    ```

  - 在输出流中加true就可以追加new FileOutputStream("file-io\\src\\data3.txt"，true);

- 文件拷贝

  - ```java
    public class FileCopyDemo04 {
        public static void main(String[] args) {
            try {
                InputStream inputStream = new FileInputStream("D:\\大三下学期\\数字影像后期合成\\期末作品\\主合成.avi");
                OutputStream outputStream =  new FileOutputStream("D:\\yy\\aa.avi");
                byte[] buffer = new byte[1024];
                int len;
                while((len = inputStream.read(buffer))!=-1){
                    outputStream.write(buffer, 0, len);
                }
                System.out.println("复制完成了！！！");
                outputStream.flush();
                outputStream.close();
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    }
    ```

#### 7.资源释放的方式

- try-catch-finally

  - finally:在异常处理时提供finally块来执行所有清除操作，比如IO流中的释放资源

  - 特点：被finally控制的语句最终一定会执行，除非JVM退出

  - 异常处理标准格式：try...catch...finally

  - ```java
    public class FileCopyDemo04 {
        public static void main(String[] args) {
            InputStream inputStream = null;
            OutputStream outputStream = null;
            try {
                inputStream = new FileInputStream("D:\\大三下学期\\数字影像后期合成\\期末作品\\主合成.avi");
                outputStream =  new FileOutputStream("D:\\yy\\aa.avi");
                byte[] buffer = new byte[1024];
                int len;
                while((len = inputStream.read(buffer))!=-1){
                    outputStream.write(buffer, 0, len);
                }
                System.out.println("复制完成了！！！");
                outputStream.flush();
            } catch (Exception e) {
                e.printStackTrace();
            }finally {
                try {
                    if (inputStream != null){
                        inputStream.close();
                    }
                } catch (IOException e) {
                    e.printStackTrace();
                }
                try {
                    if (outputStream != null){
                        outputStream.close();
                    }
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
    ```

  - 基本做法就是上述的做法：

  - ```
    try{
    	可能出现异常的代码；
    }catch(异常类名 变量名){
    	异常的处理代码;
    }finally{
    	执行所有资源释放操作;
    }
    ```

  - **JDK7改进方案**

  - ```
    try(定义流对象){
    	可能出现异常的代码；
    }catch(异常类名 变量名){
    	异常的处理代码；
    }
    ```

  - ```java
    public class tryCatchAutoClose {
        public static void main(String[] args) {
            try (InputStream inputStream = new FileInputStream("D:\\大三下学期\\数字影像后期合成\\期末作品\\主合成.avi");
                 OutputStream outputStream = new FileOutputStream("D:\\yy\\aa.avi");){
                byte[] buffer = new byte[1024];
                int len;
                while((len = inputStream.read(buffer))!=-1){
                    outputStream.write(buffer, 0, len);
                }
                System.out.println("复制完成了！！！");
                outputStream.flush();
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    }
    ```

  - try()中只能放资源，比如int a = 10；是不可以放的，会报错，因为它不是资源。

  - **资源：都是实现类Closeable/AutoCloseable接口的类对象**

  - **JDK9改进方案：**

  - ```
    定义输入流对象；
    定义输出流对象；
    try(输入流对象; 输出流对象){
    	可能出现异常的代码;
    }catch(异常类名 变量名){
     	异常的处理代码：
    }
    ```

- try-with-resource

#### 8.字符流的使用

字节流读取中文输出可能存在乱码或者内存溢出的问题。

读取中文输出，字符流更合适，最小单位是按照单个字符读取的。

1. 文件字符输入流--一次读取一个字符

   - ```java
     public static void main(String[] args) throws IOException {
         FileReader reader = new FileReader("file-io\\src\\data.txt");
         int code;
         while ((code = reader.read()) != -1){
             System.out.print((char) code);
         }
     }
     ```

2. 文件字符输入流--一次读取一个字符数组

   - ```java
     public class FileReaderDemo02 {
         public static void main(String[] args) throws IOException {
             FileReader reader = new FileReader("file-io\\src\\data1.txt");
             char[] butter = new char[1024];//1k字符
             int len;
             while ((len = reader.read(butter))!=-1){
                 String rs = new String(butter,0,len);
                 System.out.println(rs);
             }
         }
     }
     ```

3. 文件字符输出流

   - 追加数据就是将管道设置为true

```java
public class FileWriterDemo03 {
    public static void main(String[] args) throws IOException {
        FileReader reader = new FileReader("file-io\\src\\data1.txt");
        FileWriter writer = new FileWriter("file-io\\src\\data4.txt");
        char[] butter = new char[1024];
        int len;
        while((len=reader.read(butter))!=-1){
            writer.write(butter,0,len);
        }
        writer.flush();
        writer.close();
    }
}
```

### 19.

#### 1.缓冲流

1. 缓冲流概述

   - 缓冲流也成为高校流、或者高级流，之前学习的字节流可以称为原始流
   - 作用：缓冲流自带缓冲区，可以提高原始字节流、字符流读写数据的性能
   - ![](D:\mybatis笔记\images\j53.png)

2. 字节缓冲流

   1. 性能优化原理

      - 字节缓冲输入流自带8KB缓冲池，以后我们直接从缓冲池读取数据，所以性能较好

      - 字节缓冲输出流自带了8KB缓冲池，数据就直接写入到缓冲池中去，写数据性能极高

      - ```java
        public class CacheInputStream {
            public static void main(String[] args) throws IOException {
                InputStream inputStream = new FileInputStream("file-io\\src\\data1.txt");
                InputStream bufferedInputStream = new BufferedInputStream(inputStream);
                OutputStream outputStream = new FileOutputStream("file-io\\src\\data5.txt");
                OutputStream bufferedOutputStream = new BufferedOutputStream(outputStream);
                int len;
                byte[] buffer = new byte[1024];
                while ((len = bufferedInputStream.read(buffer)) != -1){
                    bufferedOutputStream.write(buffer, 0, len);
                }
                System.out.println("复制完成了");
                inputStream.close();
                outputStream.close();
            }
        }
        ```

3. 字节缓冲流的性能分析

   1. ```java
      public class Test {
          public static void main(String[] args) throws IOException {
      //        testLowOneByte();//5.053s
      //        testLowByte();  //0.006s
      //        testHighOneByte();//0.012s
              testHighByte(); //0.001s
          }
          public static void testLowOneByte() throws IOException {
              InputStream inputStream = null;
              OutputStream outputStream = null;
              try {
                  inputStream = new FileInputStream("D:\\mybatis笔记\\images\\j2.png");
                  outputStream = new FileOutputStream("D:\\mybatis笔记\\images\\j2副本.png");
                  long start = System.currentTimeMillis();
                  int len;
                  while ((len = inputStream.read()) != -1){
                      outputStream.write(len);
                  }
                  long end = System.currentTimeMillis();
                  long time = end - start;
                  System.out.println(time/1000.0);   //5.053s
              } catch (FileNotFoundException e) {
                  e.printStackTrace();
              } catch (IOException e) {
                  e.printStackTrace();
              }finally {
                  inputStream.close();
                  outputStream.close();
              }
          }
          public static void testLowByte() throws IOException {
              InputStream inputStream = null;
              OutputStream outputStream = null;
              try {
                  inputStream = new FileInputStream("D:\\mybatis笔记\\images\\j2.png");
                  outputStream = new FileOutputStream("D:\\mybatis笔记\\images\\j2副本2.png");
                  long start = System.currentTimeMillis();
                  int len;
                  byte[] buffer = new byte[1024];
                  while ((len = inputStream.read(buffer)) != -1){
                      outputStream.write(buffer, 0, len);
                  }
                  long end = System.currentTimeMillis();
                  long time = end - start;
                  System.out.println(time/1000.0);   //5.053s
              } catch (FileNotFoundException e) {
                  e.printStackTrace();
              } catch (IOException e) {
                  e.printStackTrace();
              }finally {
                  inputStream.close();
                  outputStream.close();
              }
          }
          public static void testHighOneByte() throws IOException {
              InputStream inputStream = null;
              OutputStream outputStream = null;
              try {
                  inputStream = new FileInputStream("D:\\mybatis笔记\\images\\j2.png");
                  InputStream bufferedInputStream = new BufferedInputStream(inputStream);
                  outputStream = new FileOutputStream("D:\\mybatis笔记\\images\\j2副本3.png");
                  OutputStream bufferedOutputStream = new BufferedOutputStream(outputStream);
                  long start = System.currentTimeMillis();
                  int len;
                  while ((len = bufferedInputStream.read()) != -1){
                      bufferedOutputStream.write(len);
                  }
                  long end = System.currentTimeMillis();
                  long time = end - start;
                  System.out.println(time/1000.0);   //5.053s
              } catch (FileNotFoundException e) {
                  e.printStackTrace();
              } catch (IOException e) {
                  e.printStackTrace();
              }finally {
                  inputStream.close();
                  outputStream.close();
              }
          }
          public static void testHighByte() throws IOException {
              InputStream inputStream = null;
              OutputStream outputStream = null;
              try {
                  inputStream = new FileInputStream("D:\\mybatis笔记\\images\\j2.png");
                  InputStream bufferedInputStream = new BufferedInputStream(inputStream);
                  outputStream = new FileOutputStream("D:\\mybatis笔记\\images\\j2副本2.png");
                  OutputStream bufferedOutputStream = new BufferedOutputStream(outputStream);
                  long start = System.currentTimeMillis();
                  int len;
                  byte[] buffer = new byte[1024];
                  while ((len = bufferedInputStream.read(buffer)) != -1){
                      bufferedOutputStream.write(buffer, 0, len);
                  }
                  long end = System.currentTimeMillis();
                  long time = end - start;
                  System.out.println(time/1000.0);   //5.053s
              } catch (FileNotFoundException e) {
                  e.printStackTrace();
              } catch (IOException e) {
                  e.printStackTrace();
              }finally {
                  inputStream.close();
                  outputStream.close();
              }
          }
      }
      ```

   2. 建议使用字节缓冲输入流、字节缓冲输出流，结合字节数组的方式，目前来看是性能最优的组合。

4. 字符缓冲流

   - 字符缓冲输入流：BufferedReader

   - 作用：提高字符输入流读取数据的性能，除此之外按照行读取数据的功能

   - ```java
     public static void main(String[] args) throws IOException {
         Reader fr = null;
         try {
             fr = new FileReader("file-io\\src\\data1.txt");
             BufferedReader br = new BufferedReader(fr);
             char[] buffer = new char[1024];
             int len;
             while((len = br.read(buffer)) != -1){
                 String rs = new String(buffer,0, len);
                 System.out.println(rs);
             }
         } catch (FileNotFoundException e) {
             e.printStackTrace();
         } catch (IOException e) {
             fr.close();
         }
     }
     ```

   - 字符缓冲输出流

   - ```java
     public class CacheCharBufferStream {
         public static void main(String[] args) throws IOException {
             Writer fw = new FileWriter("file-io\\src\\data6.txt");
             BufferedWriter bw = new BufferedWriter(fw);
             bw.write(98);
             bw.write('a');
             bw.newLine();//换行
             bw.write('徐');
             bw.write("\r\n");
             bw.flush();
             fw.flush();
             fw.close();
         }
     }
     ```

   - 字符缓冲流为什么提高了操作数据的性能？

     - 字符缓冲流自带8k缓冲区
     - 可以提高原始字符流读写数据的性能
   
5. 出师表案例：每行顺序打乱，读取出师表，排好序，写入文件

   - ```java
     public class Demo {
         public static void main(String[] args) {
             try (
                     //1.创建缓冲字符输入流管道与源文件接通
                     BufferedReader br = new BufferedReader(new FileReader("file-io\\src\\old.txt"));
                     //5.创建缓冲字符输出管道与目标文件接通
                     BufferedWriter bw = new BufferedWriter(new FileWriter("file-io\\src\\new.txt"));
             ){
                 //2.定义一个List集合存放每行内容
                 List<String> data = new ArrayList<>();
                 //3.定义循环，按照行读取文章
                 String line;
                 while ((line = br.readLine()) != null){
                     data.add(line);
                 }
                 System.out.println(data);
                 //4.排序
                 //自定义排序规则
                 List<String> sizes = new ArrayList<>();
                 Collections.addAll(sizes, "一", "二", "三", "四","五", "六", "柒", "八", "九");
                 Collections.sort(data, new Comparator<String>() {
                     @Override
                     public int compare(String o1, String o2) {
                         return sizes.indexOf(o1.substring(0, o1.indexOf("."))) - sizes.indexOf(o2.substring(0, o2.indexOf(".")));
                     }
                 });
                 for (String datum : data) {
                     bw.write(datum);
                     bw.newLine();
                 }
             } catch (FileNotFoundException e) {
                 e.printStackTrace();
             } catch (IOException e) {
                 e.printStackTrace();
             }
         }
     }
     ```

#### 2.转换流

如果代码编码和文件编码不一致，使用字符流直接读取还能不乱码吗？

- 会乱码

如何解决？

- 使用字符输入转换流
- 可以提取文件的原始字节流，原始字节不会存在问题
- 然后把字节流以指定编码转换成字符输入流，这样字符输入流中的字符就不乱码了。

字符输入转换流：InputStreamReader

字符输出转换流：OutputStreamWriter 

- 字符输入转换流：实现读取GBK格式的文件

- ```java
  public static void main(String[] args) {
      //文件GBK D:\yy\test.txt
      //1.提取GBK文件的原始字节流
      try (
              Reader inputStreamReader = new InputStreamReader(new FileInputStream("D:\\yy\\test.txt"), "GBK");
              BufferedReader bufferedReader = new BufferedReader(inputStreamReader);
      ){
          String line;
          while ((line = bufferedReader.readLine())!=null){
              System.out.println(line);
          }
          } catch (FileNotFoundException e) {
          e.printStackTrace();
      } catch (IOException e) {
          e.printStackTrace();
      }
  }
  ```

如果需要控制写出去的字符使用的编码，怎么办？

- 可以把字符以指定编码获取字节后再使用字节输出流写出去
  - 我爱你中国.getBytes(编码)
- 也可以使用字符输出转换流实现

#### 3.序列化对象

![](D:\mybatis笔记\images\java.jpeg)

- 对象序列化

  - 作用:以内存为基准，把内存中的对象存储到磁盘文件中去，称为对象序列化

  - 使用到的流是对象字节输出流：ObjectOutputStream

  - 构造器public ObjectOutputStream(OutputStream out)：把低级字节输出流包装成高级的对象字节输出流

  - ```java
    public class ObjectOutputStreamDemo1 {
        public static void main(String[] args) throws IOException {
            Student s1 = new Student("马嘉祺", "mjq", "123456", 20);
            FileOutputStream outputStream = new FileOutputStream("file-io\\src\\data7.txt");
            ObjectOutputStream objectOutputStream = new ObjectOutputStream(outputStream);
            objectOutputStream.writeObject(s1);
            objectOutputStream.close();
        }
    }
    ```

  - 此时会报错：Exception in thread "main" java.io.NotSerializableException: com.yyue.d8.Student

  - 对象要实现序列化，必须要实现Serializable接口：因为要告诉虚拟机，触发它将数据解析出来，存储到磁盘上。

  - ```java
    public class Student implements Serializable {
        private String name;
        private String loginName;
        private String password;
        private int age;
        //skip
    }
    ```

- 对象反序列化

  - 使用到的流是对象字节输入流：ObjectInputStream

  - 作用：以内存为基准，把存储到磁盘文件中去的对象恢复成内存中的对象，称为对象反序列化

  - 使用到：ObjectInputStream（对象字节输入流）

  - 构造器public ObjectInputStream(InputStream out)：把低级字节输入流包装成高级的对象字节输入流

  - ObjectInputStream序列化方法：readObject()把存储到磁盘文件中去的对象数据恢复成内存中的对象返回

  - ```java
    /**
     * 学会进行对象反序列化：使用对象字节输入流把文件中的对象数据恢复成内存中的Java对象
     */
    public class ObjectInputStreamDemo2 {
        public static void main(String[] args) throws IOException, ClassNotFoundException {
            FileInputStream inputStream = new FileInputStream("file-io\\src\\data7.txt");
            ObjectInputStream objectInputStream = new ObjectInputStream(inputStream);
            Student object = (Student)objectInputStream.readObject();
            System.out.println(object);
            objectInputStream.close();
        }
    }
    ```

  - 在有些情况下，某些属性是不需要序列化的，比如密码，可以在声明属性的时候加上transient

  - 加上之后，反序列化的结果为：Student{name='马嘉祺', loginName='mjq', password='null', age=20}

- ```java
  private static final long serialVersionUID = 1
  ```

  - 序列化的版本号与反序列化版本号必须一致才不会出错，当更新的时候，需要重新序列化。

#### 4.打印流

![](D:\mybatis笔记\images\java4.jpeg)

打印流

- 作用：打印流可以实现方便、高效的打印数据到文件中去，打印流一般是指：PrintStream、PrintWriter两个类
- 可以实现打印什么数据就是什么数据，例如打印整数97写出去就是97，打印boolean的true，写出去就是true

- PrintStream、PrintWriter

  - ![](D:\mybatis笔记\images\java5.jpeg)

  - ![](D:\mybatis笔记\images\java6.jpeg)

  - ```java
      public static void main(String[] args) throws FileNotFoundException {
            PrintStream ps = new PrintStream("file-io\\src\\data8.txt");
    //        PrintStream ps = new PrintStream(new FileOutputStream("file-io\\src\\data8.txt"));
            ps.println(90);
            ps.println("马嘉祺");
            ps.println(true);
            ps.println('a');
            ps.close();
        }
    ```

  - ![](D:\mybatis笔记\images\java7.jpeg)

  - **PrintWriter与PrintStream区别**

    - 打印数据功能上是一模一样的，都是使用方便，性能高效(核心优势)
    - PrintStream继承自字节输出流OutputStream，支持写字节数据的方法
    - PrintWriter继承自字符输出流Writer,支持写字符数据出去。

- 输出语句的重定向

  - ```java
    /**
     * 了解改变输出语句的位置到文件
     */
    public class PrintDemo2 {
        public static void main(String[] args) throws FileNotFoundException {
            System.out.println("锦瑟无端五十弦"); //out对象是PrintStream
            System.out.println("一弦一柱思华年");
            //改变输出语句的位置(重定向)
            PrintStream ps = new PrintStream(new FileOutputStream("file-io\\src\\data8.txt", true));
            System.setOut(ps);
            System.out.println("庄生晓梦迷蝴蝶");
            System.out.println("望帝春心托杜鹃");
        }
    ```

#### 5.Properties

Properties属性集对象

- 其实就是一个Map集合，但是我们一般不会当集合使用，因为HashMap更好

Properties核心作用：

- Properties代表的是一个属性文件，可以把自己对象的键值对信息存入到一个属性文件中去。
- 属性文件：后缀是.properties结尾的文件，里面的内容都是key=value，后续做系统配置信息的。

![](D:\mybatis笔记\images\java8.jpeg)

存入文件中：

```java
public class PropertiesDemo01 {
    public static void main(String[] args) throws IOException {
        //需求：使用Properties把键值对信息存入到属性文件中去
        Properties properties = new Properties();
        properties.setProperty("admin", "123445");
        properties.setProperty("dlei", "0394034");
        properties.setProperty("yyue","102923");
        System.out.println(properties);
        /**
         * 参数一：保存管道，字符输出流管道
         * 参数二：保存注释
         */
        properties.store(new FileWriter("file-io\\src\\users.properties"), "this is users!");
    }
}
```

从文件中取：

```java
public class PropertiesDemo02 {
    public static void main(String[] args) throws IOException {
        Properties properties = new Properties();
        System.out.println(properties);
        properties.load(new FileReader("file-io\\src\\users.properties"));
        System.out.println(properties);
    }
}
```

#### 6.IO框架

commons-io概述

- commons-io是apache开源基金组织提供的一组有关IO操作的类库，可以提高IO功能开发的效率。
- commons-io工具包提供了很多有关io操作的类，有两个主要的类FileUtils，IOUtils

### 20.线程

什么是线程？

- 线程是一个程序内部的一条执行路径
- 我们之前启动程序执行后，main方法的执行其实就是一条单独的执行路径
- 程序中如果只有一条执行路径，那么程序就是单线程的程序。

多线程是什么？

- 多线程是指从软硬件上实现多条执行流程的技术。

#### 1.**线程的创建**(三种方式)

1. 方式一：继承Thread类

   1. ```java
      public static void main(String[] args) {
          Thread thread = new MyThread();
          thread.start();
          for (int i = 0; i < 5; i++) {
              System.out.println("主程序执行输出：" + i);
          }
      }
      static class MyThread extends Thread {
          @Override
          public void run() {
              for (int i = 0; i < 5; i++) {
                  System.out.println("子程序执行输出："+i);
              }
          }
      }
      ```

   2. 为什么不直接调用run方法，而是调用启动线程

      - 直接调用run方法会当成普通方法执行，此时相当于还是单线程执行
      - 只有调用start方法才是启动一个新的线程执行

   3. 把主线程任务放在子线程之前了

      - 这样主线程一直是先跑完的，相当于一个单线程的效果。

   4. 优缺点：

      1. 缺点：扩展性较差，不能再继续继承其他类，不能返回线程执行的结果

2. 方式二：实现Runnable接口

   - ```java
     public static void main(String[] args) {
             Runnable myRunnable = new MyRunnable();
             Thread thread = new Thread(myRunnable);
             thread.start();
             for (int i = 0; i < 5; i++) {
                 System.out.println("主程序执行输出：" + i);
             }
         }
         static class MyRunnable implements Runnable {
             @Override
             public void run() {
                 for (int i = 0; i < 5; i++) {
                     System.out.println("子程序执行输出："+i);
                 }
             }
         }
     ```

   - 优缺点：

     - 优点：线程任务类只是实现接口，可以继承类和实现接口，扩展性强
     - 缺点：编程多一层对象包装，如果线程有执行结果是不可以直接返回的

   - 方式二：简便写法：实现Runnable接口(匿名内部类形式)

     - 可以创建Runnable的匿名内部类对象
     - 交给Thread处理
     - 调用线程对象的start()启动线程

   - ```java
     public static void main(String[] args) {
         Thread thread = new Thread(() -> {
             for (int i = 0; i < 5; i++) {
                 System.out.println("子程序执行输出："+i);
           }
             });
            thread.start();
            for (int i = 0; i < 5; i++) {
                System.out.println("主程序执行输出：" + i);
            }
        }
     ```

3. 方式三：JDK5.0新增：实现Callable接口

   - 利用Callable、FutureTask接口实现

     1. 得到任务对象
        1. 定义类实现Callable接口，重写call方法，封装要做的事情
        2. 用FutureTask把Callable对象封装成线程任务对象
     2. 把线程任务对象交给Thread处理
     3. 调用Thread的start方法启动线程、执行任务

   - ```java
     Callable<String> call = new MyCallable(10);
     FutureTask<String> f1 = new FutureTask<>(call);
     Thread thread = new Thread(f1);
     thread.start();
     try {
         String rs1 = f1.get();
         System.out.println("第一个结果：" + rs1);
     } catch (Exception e) {
         e.printStackTrace();
     }
     
     Callable<String> call2 = new MyCallable(100);
     FutureTask<String> f2 = new FutureTask<>(call2);
     Thread thread2 = new Thread(f2);
     thread2.start();
     try {
         String rs2 = f2.get();
         System.out.println("第二个结果：" + rs2);
     } catch (Exception e) {
         e.printStackTrace();
     }
     ```

   - ```java
     static class MyCallable implements Callable<String> {
         private int n;
         public MyCallable(int n) {
             this.n = n;
         }
         @Override
         public String call() throws Exception {
             int sum = 0;
             for (int i = 0; i < n; i++) {
                 sum +=i;
             }
             return "结果"+sum;
         }
     }
     ```

   - public FutureTask<>(Callable call)   把Callable对象封装成FutureTask对象

   - public V get() throws Exception 获取线程执行call方法返回的结果

   - 方法三优缺点：

     - 优点：线程任务类只是实现接口，可以继续继承类和实现接口，扩展性强
     - 可以在线程执行完毕后去获取线程执行的结果
     - 缺点：编码复杂一点

**Thread常用API说明**

- Thread常用方法：获取线程名称getName()、设置名称setName()、获取当前线程对象currentThread().
- 至于Thread类提供的诸如：yield、join、interrupt、不推荐的方法stop、守护线程、线程优先级等线程的控制方法，在开发中很少使用。

1. 当有很多线程在执行的时候，如何区分这些线程？

   - 此时需要获取线程名称getName()、设置名称setName()、获取当前线程对象currentThread()

   - ```java
     public static void main(String[] args) {
         Thread t1 = new MyThread();
         t1.setName("子线程1号");
         t1.start();
         Thread t2 = new MyThread();
         t2.setName("子线程2号");
         t2.start();
         for (int i = 0; i < 5; i++) {
             System.out.println(Thread.currentThread().getName()+"输出："+i);
         }
     }
     static class MyThread extends Thread {
         @Override
         public void run() {
             for (int i = 0; i < 5; i++) {
                 System.out.println(Thread.currentThread().getName()+"输出："+i);
             }
         }
     }
     ```

   - ```java
     public static void main(String[] args) {
         Thread t1 = new MyThread("子线程1号");
         t1.start();
         Thread t2 = new MyThread("子线程2号");
         t2.start();
         for (int i = 0; i < 5; i++) {
             System.out.println(Thread.currentThread().getName()+"输出："+i);
         }
     }
     static class MyThread extends Thread {
         public MyThread(){}
         public MyThread(String name){ //为当前线程对象设置名称，送给父类的有参数构造器初始化名称
             super(name);
         }
         @Override
         public void run() {
             for (int i = 0; i < 5; i++) {
                 System.out.println(Thread.currentThread().getName()+"输出："+i);
             }
         }
     }
     ```

2. Thread类的线程休眠方法

   - public static void sleep(long time)   ：让当前线程休眠指定的时间后再继续执行，单位为毫秒。

   - ```java
     for (int i = 0; i < 5; i++) {
         System.out.println(Thread.currentThread().getName()+"输出："+i);
         if (i == 3){
             Thread.sleep(3000);
         }
     }
     ```

   - 

#### 2.线程安全问题

- 多个线程同时操作同一个共享资源的时候可能会出现业务安全问题，称为线程安全问题。

取钱模型演示

- 需求：小明和小红是一对夫妻，他们有一个共同的账户，余额是十万元
- 如果小明和小红同时来取钱，而且2人都要去十万元，会出现什么问题？

线程安全出现的原因？

- 存在多线程并发
- 同时访问共享资源
- 存在修改共享资源

出现线程安全问题

- Account

- ```java
  public class Account {
      //账户
      private String cardId;
      private Double money;
  
      public Account() {
      }
  
      public Account(String cardId, Double money) {
          this.cardId = cardId;
          this.money = money;
      }
  
      public String getCardId() {
          return cardId;
      }
  
      public void setCardId(String cardId) {
          this.cardId = cardId;
      }
  
      public Double getMoney() {
          return money;
      }
  
      public void setMoney(Double money) {
          this.money = money;
      }
  
      public void drawMoney(double money) {
          String name = Thread.currentThread().getName();
          if (money <= this.money){
              System.out.println(name + "来取钱,取了"+money);
              this.money -= money;
              System.out.println(name + "取了"+money +"，还剩"+this.money);
          }else {
              System.out.println(name + "来取钱，余额不足！");
          }
      }
  }
  ```

- 线程

- ```java
  public class DrawThread extends Thread{
      private Account account;
      public DrawThread(Account account, String name) {
          super(name);
          this.account = account;
      }
  
      @Override
      public void run() {
          account.drawMoney(100000D);
      }
  }
  ```

- 主函数

- ```java
  public class ThreadDemo {
      public static void main(String[] args) {
          Account account = new Account("cc-000", 100000D);
          new DrawThread(account, "小明").start();
          new DrawThread(account, "小红").start();
      }
  }
  ```

解决线程安全问题：

- 核心思想：加锁，把共享资源进行上锁，每次只能一个线程进入访问完毕后解锁，其他线程才能进来

- 方式一：同步代码块

  - 作用：把出现线程安全问题的核心代码给上锁

  - 原理：每次只能一个线程进入，执行完毕后自动解锁，其他线程才可以进来执行

  - ```java
    synchronized(同步锁对象){
        //操作共享资源的代码（核心代码）
    }
    ```

  - 锁对象要求，理论上：锁对象只要对于当前同时执行的线程来说是同一个对象即可

  - 锁对象用任意唯一的对象好不好呢？不好，会影响其他无关线程的执行

  - 锁对象的规范要求，规范上：建议使用共享资源作为锁对象，对于实例方法建议使用this作为锁对象，对于静态方法建议使用字节码(类名.class)对象作为锁对象

  - ```java
    public void drawMoney(double money) {
        String name = Thread.currentThread().getName();
        synchronized (this) {
            if (money <= this.money){
                System.out.println(name + "来取钱,取了"+money);
                this.money -= money;
                System.out.println(name + "取了"+money +"，还剩"+this.money);
            }else {
                System.out.println(name + "来取钱，余额不足！");
            }
        }
    }
    ```

- 方式二：同步方法 

- 作用：把出现线程安全问题的核心方法给上锁

- 原理：每次只能一个线程进入，执行完毕以后自动解锁，其他线程才可以进来执行

- 格式：

  - ```java
    修饰符 synchronized 返回值类型 方法名称(形参列表) {
    	//操作共享资源的代码
    }
    ```

- 同步方法底层原理

  - 同步方法其实底层也是隐式锁对象的，只是锁的范围是整个方法代码
  - 如果方法是实例方法：同步方法默认用this作为的锁对象，但是代码要高度面向对象！
  - 如果方法是静态方法：同步方法默认用类名.class作为锁对象

- ```java
  public synchronized void drawMoney(double money) {
      String name = Thread.currentThread().getName();
          if (money <= this.money){
              System.out.println(name + "来取钱,取了"+money);
              this.money -= money;
              System.out.println(name + "取了"+money +"，还剩"+this.money);
          }else {
              System.out.println(name + "来取钱，余额不足！");
          }
  }
  ```

- Lock锁

  - 为例更清晰的表达如何加锁和释放锁，JDK5以后提供了一个新的锁对象Lock，更加灵活、方便。
  - Lock实现提供比使用synchronized方法和语句可以获得更广泛的锁定操作
  - Lock是接口不能直接实例化，这里采用它的实现类ReentrantLock来构建Lock锁对象
  - public ReentrantLock()  获得Lock锁的实现类对象
  - void lock()  获得锁    void unlock()  释放锁

- ```java
  private final Lock lock = new ReentrantLock();
  public void drawMoney(double money) {
      String name = Thread.currentThread().getName();
      lock.lock();
      try {
          if (money <= this.money){
              System.out.println(name + "来取钱,取了"+money);
              this.money -= money;
              System.out.println(name + "取了"+money +"，还剩"+this.money);
          }else {
              System.out.println(name + "来取钱，余额不足！");
          }
      }finally {
          lock.unlock();
      }
  }
  ```

#### 3.线程通信

什么是线程通信、如何实现？

- 所谓线程通信就是线程间相互发送数据，线程通信通常通过共享一个数据的方式实现。
- 线程间会根据共享数据的情况决定自己该怎么做，以及通知其他线程该怎么做。

线程通信常见模型：

- 生产者与消费者模型：生产者线程负责生产数据，消费者线程负责消费数据
- 要求：生产者线程生产完数据后，唤醒消费者，然后等待自己；消费者消费完该数据后，唤醒生产者，然后等待自己。

Object类的等待和唤醒方法：

- void wait() ：让当前线程等待并释放所占锁，直到另一个线程调用notify()方法或notifyAll()方法
- void notify() ：唤醒正在等待的单个线程
- void notifyAll() ：唤醒正在等待的所有线程
- **注：**上述方法应该使用当前同步锁对象进行调用

Account:

- ```java
  public class Account {
      //账户
      private String cardId;
      private Double money;
      public Account() {
      }
  
      public Account(String cardId, Double money) {
          this.cardId = cardId;
          this.money = money;
      }
  
      public String getCardId() {
          return cardId;
      }
  
      public void setCardId(String cardId) {
          this.cardId = cardId;
      }
  
      public Double getMoney() {
          return money;
      }
  
      public void setMoney(Double money) {
          this.money = money;
      }
  
      public synchronized void drawMoney(double money) {
          String name = Thread.currentThread().getName();
          try {
              if (this.money >= money) {
                  //线程：可取
                  this.money -= money;
                  System.out.println(name + "来取钱" + money + "成功！余额是："+this.money);
                  //取完钱没钱了，则等待
                  this.notifyAll();
                  this.wait();
              }else {
                  //钱不够，不可取
                  //唤醒别人，等待自己
                  this.notifyAll();
                  this.wait();
              }
          } catch (Exception e) {
              e.printStackTrace();
          }
      }
  
      public synchronized void deposit(double money) throws InterruptedException {
          String name = Thread.currentThread().getName();
          if (this.money == 0 ){
              //没钱
              this.money += money;
              System.out.println(name + "存了" + money +"成功，余额："+this.money);
              this.notifyAll();
              this.wait();
          }else {
              //有钱不存
              this.notifyAll();
              this.wait();
          }
      }
  }
  ```
  
- 小红、小明线程

- ```java
  public class DrawThread extends Thread{
      private Account account;
      public DrawThread(Account account, String name) {
          super(name);
          this.account = account;
      }
  
      @Override
      public void run() {
          while (true) {
              account.drawMoney(100000D);
              try {
                  Thread.sleep(3000);
              } catch (Exception e) {
                  e.printStackTrace();
              }
          }
      }
  }
  ```

- dad1、dad2、dad3线程

- ```java
  public class DepositThread extends Thread{
      private Account account;
      public DepositThread(String name, Account account){
          super(name);
          this.account = account;
      }
      @Override
      public void run() {
          while (true){
              try {
                  account.deposit(100000D);
              } catch (InterruptedException e) {
                  e.printStackTrace();
              }
              try {
                  Thread.sleep(3000);
              } catch (Exception e) {
                  e.printStackTrace();
              }
          }
      }
  }
  ```

- main函数

- ```java
  public class ThreadDemo {
      //目标：了解线程通信的流程
      public static void main(String[] args) {
          Account account = new Account("uuuu-1", 0D);
          new DrawThread(account,"小红").start();
          new DrawThread(account,"小明").start();
          new DepositThread("dad1", account).start();
          new DepositThread("dad2", account).start();
          new DepositThread("dad3", account).start();
      }
  }
  ```

#### 4.线程池【重点】

**线程池概述**

- 什么是线程池？
  - 线程池就是一个可以复用线程的技术

- 不使用线程池的问题？
  - 如果用户每发起一个请求，后台就创建一个新线程来处理，下次新任务来了又要创建新线程，二创建新线程的开销是很大的，这样严重影响系统的性能。

**线程池实现的API、参数说明**

- 谁代表线程池？

  - JDK5.0提供了代表线程池的接口：ExecutorService

- 如何得到线程池对象

  - 方式一：使用ExecutorService的实现类ThreadPoolExecutor自创建一个线程池对象

    - ```java
      ThreadPoolExecutor(int corePoolSize, //指定线程池的线程数量(核心线程)-》不能小于0
                          int maximumPoolSize, //指定线程池可支持的最大线程数-》最大数量>=核心线程数量
                         long keepAliveTime, //指定临时线程的最大存活时间->不能小于0
                         TimeUnit unit, //指定存活时间的单位(秒，分，时，天)
                         BlockingQueue<Runnable> workQueue, //指定任务队列->不能为null
                         ThreadFactory threadFactory, //指定用哪个线程工厂创建线程->不能为null
                         RejectedExecutionHandler handler)//指定线程忙，任务满的时候，新任务来了怎么办？->不能为null
      ```

  - 方式二：使用Executors(线程池的工具类)调用方法返回不同特点的线程池对象

线程池常见面试题

- 临时线程什么时候创建？
  - 新任务提交时发现核心线程都在忙，任务队列也满了，并且还可以创建临时线程，此时才会创建临时线程
- 什么时候会开始拒绝任务？
  - 核心线程和临时线程都在忙，任务队列也满了，新的任务过来的时候才会开始任务拒绝

**线程池处理Runnable任务**

- ```java
  ExecutorService service = new ThreadPoolExecutor(3,
          5, 
          8, 
          TimeUnit.SECONDS,
          new ArrayBlockingQueue<>(6),
          Executors.defaultThreadFactory(), 
          new ThreadPoolExecutor.AbortPolicy());//丢弃任务并抛出RejectExecutionException异常，是默认的策略
  ```

- ```java
  public static void main(String[] args) {
          ExecutorService pool = new ThreadPoolExecutor(3,
                  5,
                  6,
                  TimeUnit.SECONDS,
                  new ArrayBlockingQueue<>(5),
                  Executors.defaultThreadFactory(),
                  new ThreadPoolExecutor.AbortPolicy());
          MyThread target = new MyThread();
          pool.execute(target);
          pool.execute(target);
          pool.execute(target);
          pool.execute(target);
          pool.execute(target);
          pool.execute(target);
          pool.execute(target);
  //        pool.shutdownNow(); //立即关闭，即使任务没有完成，会丢失任务的
          pool.shutdown();//等待任务结束后，再关闭
      }
      static class MyThread implements Runnable {
  
          @Override
          public void run() {
              for (int i = 0; i < 5; i++) {
                  System.out.println(Thread.currentThread().getName() + "helloworld" + i);
              }
              try {
                  System.out.println(Thread.currentThread().getName() + "休眠");
                  Thread.sleep(3000);
              } catch (Exception e) {
                  e.printStackTrace();
              }
          }
      }
  ```

- 常用方法

  - void executor(Runnable command)  执行任务/命令，没有返回值，一般用来执行Runnable任务
  - Future<T> submit(Callable<T> task)  执行任务，返回未来任务对象获取线程结果，一般拿来执行Callable任务
  - void shutdown() 等任务执行完毕后关闭线程池
  - List<Runnable> shutdownNow()  立刻关闭，停止正在执行的任务，并返回队列中未执行的任务

- 对于新任务的拒绝策略分为以下几种

  - ThreadPoolExecutor.AbortPolicy()     丢弃任务并抛出RejectExecutionException异常，是默认的策略
  - ThreadPoolExecutor.DiscardPolicy()   丢弃任务，但是不抛出异常 这是不推荐的做法
  - ThreadPoolExecutor.DiscardOldestPolicy()   抛弃队列中等待最久的任务 然后把当前任务加入队列中
  - ThreadPoolExecutor.CallerRunsPolicy()   由主线程负责调用任务的run()方法从而绕过线程池直接执行

**线程池处理Callable任务**

```java
public static void main(String[] args) throws ExecutionException, InterruptedException {
    ExecutorService pool = new ThreadPoolExecutor(3,
            5,
            6,
            TimeUnit.SECONDS,
            new ArrayBlockingQueue<>(5),
            Executors.defaultThreadFactory(),
            new ThreadPoolExecutor.AbortPolicy());
    Future<String> f1 = pool.submit(new MyCallable(10));
    Future<String> f2 = pool.submit(new MyCallable(100));
    Future<String> f3 = pool.submit(new MyCallable(200));
    Future<String> f4 = pool.submit(new MyCallable(300));
    Future<String> f5 = pool.submit(new MyCallable(300));
    Future<String> f6 = pool.submit(new MyCallable(300));
    Future<String> f7 = pool.submit(new MyCallable(300));
    System.out.println(f1.get());
    System.out.println(f2.get());
    System.out.println(f3.get());
    System.out.println(f4.get());
    System.out.println(f5.get());
    System.out.println(f6.get());
    System.out.println(f7.get());

}
static class MyCallable implements Callable<String> {
    private int n;
    public MyCallable(int n){
        this.n = n;
    }
    @Override
    public String call() throws Exception {
        int sum = 0;
        for (int i = 0; i < n; i++) {
            sum+=i;
        }
        return Thread.currentThread().getName()+"计算1-"+n+"的和，执行结果为：" + sum;
    }
}
```

**Executors工具类实现线程池**

- ![](D:\mybatis笔记\images\j54.png)


- ```java
  //使用Executors的工具方法直接得到一个线程池对象
  public class ThreadDemo3 {
      public static void main(String[] args) {
          //1.创建固定线程数据的线程池
          ExecutorService pool = Executors.newFixedThreadPool(3);
          pool.execute(new ThreadDemo.MyThread());
          pool.execute(new ThreadDemo.MyThread());
          pool.execute(new ThreadDemo.MyThread());
          pool.execute(new ThreadDemo.MyThread());
      }
  }
  ```

- Executors使用可能存在的陷阱

- 大型并发系统环境中使用Executors如果不注意可能会出现系统风险。

- ![](D:\mybatis笔记\images\j55.png)

- ![](D:\mybatis笔记\images\j56.png)

#### 5.补充知识：定时器

定时器是一种控制任务延时调用，或者周期调用的技术

- 作用：闹钟、定时邮件发送

- 实现方式：
- 方式一：Timer
  
- ![](D:\mybatis笔记\images\j57.png)
  
- ```java
  public static void main(String[] args) {
      Timer timer = new Timer();//定时器本身就是一个单线程
      timer.schedule(new TimerTask() {
          @Override
          public void run() {
              System.out.println(Thread.currentThread().getName()+"执行1次~~~");
          }
      }, 3000, 2000);
  }
  ```

Timer定时器的特点和存在的问题

- 1.Timer是单线程，处理多个任务按照顺序执行，存在延时与设置定时器的时间有出入

- 2.可能因为其中的某个任务的异常使Timer线程死掉，从而影响后续任务执行

- ```java
  public static void main(String[] args) {
      Timer timer = new Timer();//定时器本身就是一个单线程
      timer.schedule(new TimerTask() {
          @Override
          public void run() {
              System.out.println(Thread.currentThread().getName()+"执行1次~~~" + new Date());
              try {
                  Thread.sleep(5000);
              } catch (Exception e) {
                  e.printStackTrace();
              }
          }
      }, 0, 2000);
  
      timer.schedule(new TimerTask() {
          @Override
          public void run() {
              System.out.println(Thread.currentThread().getName()+"执行1次~~~" + new Date());
          }
      }, 0, 2000);
  }
  ```

- 由于是单线程，这样就会导致执行第二个的时候时间不在是推迟时间2秒了，而是上面的等待时间5秒

- 方式二：ScheduleExecutorService

- ![](D:\mybatis笔记\images\j58.png)

- ```java
  public static void main(String[] args) {
      ScheduledExecutorService pool = Executors.newScheduledThreadPool(3);
      pool.scheduleAtFixedRate(new Runnable() {
          @Override
          public void run() {
              System.out.println(Thread.currentThread().getName() + "执行AAA， 1次~");
              try {
                  Thread.sleep(10000);
              } catch (InterruptedException e) {
                  e.printStackTrace();
              }
          }
      }, 0, 2, TimeUnit.SECONDS);
      pool.scheduleAtFixedRate(new Runnable() {
          @Override
          public void run() {
              System.out.println(Thread.currentThread().getName() + "执行BBB， 1次~");
          }
      }, 0, 2, TimeUnit.SECONDS);
  }
  ```

- 当某个线程挂掉之后，并不会影响其他线程，其他线程继续执行

- ```java
  public static void main(String[] args) {
      ScheduledExecutorService pool = Executors.newScheduledThreadPool(3);
      pool.scheduleAtFixedRate(new Runnable() {
          @Override
          public void run() {
              System.out.println(Thread.currentThread().getName() + "执行AAA， 1次~");
              System.out.println(10/0);
          }
      }, 0, 2, TimeUnit.SECONDS);
      pool.scheduleAtFixedRate(new Runnable() {
          @Override
          public void run() {
              System.out.println(Thread.currentThread().getName() + "执行BBB， 1次~");
          }
      }, 0, 2, TimeUnit.SECONDS);
  }
  ```

#### 6.补充知识：并发、并行

 并行与并发

- 正在运行的程序(软件)就是一个独立的进行，线程是属于进程的，多个线程其实是并发与并行同时进行的。

并发的理解：

- CPU同时处理线程的数量有限
- CPU会轮询为系统中的每个线程服务，由于CPU切换的速度很快，给我们的感觉就是这些线程咋爱同时执行，这就是并发

并行的理解：

- 在同一时刻上，同时有多个线程在被CPU处理并执行

#### 7.补充知识：线程的生命周期

线程的状态：也就是线程从生到死的过程，以及中间经历的各种状态及状态转换。

Java线程的状态：

- Java总共定义了6种状态
- 6种状态都定义在Thread类的内部枚举类中
- ![](D:\mybatis笔记\images\j59.png)
- ![](D:\mybatis笔记\images\j60.png)

### 21.网络编程

什么是网络编程？

- 网络编程可以让程序与网络上的其他设备中的程序进行数据交互

网络通信基本模式

- 常见的通信模式有如下2种形式：Client-Server(CS)、Browser/Server(BS)
- ![](D:\mybatis笔记\images\j61.png)
- ![](D:\mybatis笔记\images\j62.png)
- ![](D:\mybatis笔记\images\j63.png)

#### 1.网络通信三要素

**三要素**

- IP地址：设备在网络中的地址，是唯一的标识
- 端口：应用程序在设备种唯一的标识
- 协议：数据在网络种传输的规则，常见的协议有UDP协议和TCP协议

IP地址形式：

- 公网地址、私有地址(局域网使用)
- 192.168.开头的就是常见的局域网地址，范围即为192.168.0.0--192.168.255.255，专门为组织机构内部使用

IP常用命令：

- ipconfig：查看本机IP地址
- ping IP地址：检查网络是否连通

特殊IP地址：

- 本机IP：127.0.0.1或者localhost：称为回送地址也可称为本地回环地址，只会寻找当前所在本机

**IP地址操作类-InetAddress**

- InetAddress的使用：此类标识Internet协议（IP）地址
- API如下：
  - InetAddress getLocalHost()   返回本主机的地址对象
  - InetAddress getByName(String host)  得到指定主机的IP地址对象，参数是域名或者IP地址
  - String getHostName()   获取此IP地址的主机名
  - String getHostAddress()  返回IP地址字符串
  - boolean isReachable(int timeout)   在指定毫秒内连通该IP地址对应的主机，连通返回true

**端口号**

- 端口号：标识正在计算机设备上运行的进程(程序)，被规定为一个16位的二进制，范围是0~65535
- 端口类型
  - 周知端口：0~1023，被预先定义的知名应用占用(如，HTTP占用80，FTP占用21)
  - 注册端口：1024~49151，分配给用户进程或某些应用程序。(如Tomcat占用8080，MySql占用3306)
  - 动态端口：49152~65535，之所以称为动态端口，是因为它一般不固定分配某种进程，而是动态分配。
- **注：自己开发的程序选择注册端口，且一个设备中不能出现两个程序的端口号一样，否则出错**

**协议：**

- OSI参考模型  应用层、表示层、会话层、传输层（TCP、UDP）、网络层、数据链路层、物理层
- TCP/IP参考模型   应用层、传输层、网络层、数据链路层+物理
- TCP协议：传输控制协议
  - 使用TCP协议，必须双方先建立连接，它是一种面向连接的可靠通信协议
  - 传输前，采用“三次握手”方式建立连接，所以是可靠的
  - 在连接中可进行大数据量的传输
  - 连接、发送数据都需要确认，且传输完毕后，还需释放已建立的连接，通信效率较低
  - 应用场景：对信息安全要求较高的场景，如文件下载、金融等数据通信 
- UDP协议：用户数据报协议
  - UDP是一种无连接、不可靠传输的协议
  - 将数据源IP、目的地IP和端口封装成数据包，不需要建立连接
  - 每个数据包的大小限制在64KB内
  - 发送不管对方是否准备好，接收方收到也不确认，故是不可靠的
  - 可以广播发送，发送数据结束时无需释放资源，开销小，速度快
  - 通信场景：语言通话，视频会话等

#### 2.UDP通信-快速入门

- DatagramPacket:数据包对象

  - DatagramPacket(byte[] buf, int length, InetAddress address, int port)   创建发送端数据包对象
  - DatagramPacket(byte[] buf, int length)  创建接收端的数据包对象

- DatagramSocket: 发送端和接收端对象

  - DatagramSocket()  创建发送端的Socket对象，系统会随机分配一个端口号
  - DatagramSocket(int port)  创建接收端的Socket对象并指定端口号

- DatagramSocket类成员方法

  - void send(DatagramPacket dp)   发送数据包
  - void receive(DatagramPacket p)  接收数据包

- ```java
  /**
   * 发送端
   */
  public class ClientDemo1 {
      public static void main(String[] args) throws IOException {
          DatagramSocket socket = new DatagramSocket();
          //参数一：封装的发送数据
          //参数二：发送数据的长度
          //参数三：发送的地址
          //参数四：发送的端口号
          byte[] buffer = "数据包".getBytes();
          DatagramPacket packet = new DatagramPacket(buffer,
                  buffer.length,
                  InetAddress.getLocalHost(),
                  8888);
          socket.send(packet);
          socket.close();
      }
  }
  ```

- ```java
  /**
   * 接收端
   */
  public class ServerDemo1 {
      public static void main(String[] args) throws IOException {
          //1.创建接收端对象，注册端口
          DatagramSocket socket = new DatagramSocket(8888);
          //2.创建一个数据包对象接收数据
          byte[] buffer = new byte[1024 * 64];
          DatagramPacket packet = new DatagramPacket(buffer, buffer.length);
          //3.等待接收数据
          socket.receive(packet);
          int len = packet.getLength();
          //4.取出数据
          System.out.println("收到了"+new String(buffer, 0, len));
          socket.close();
      }
  }
  ```

- 多发多收：

  - 客户端

  - ```java
    public class ClientDemo1 {
        public static void main(String[] args) throws IOException {
            DatagramSocket socket = new DatagramSocket();
            //参数一：封装的发送数据
            //参数二：发送数据的长度
            //参数三：发送的地址
            //参数四：发送的端口号
            Scanner sc = new Scanner(System.in);
            while (true) {
                System.out.println("发送：");
                String msg = sc.nextLine();
                if ("exit".equals(msg)){
                    System.out.println("离线成功");
                    socket.close();
                    break;
                }
                byte[] buffer = msg.getBytes();
                DatagramPacket packet = new DatagramPacket(buffer,
                        buffer.length,
                        InetAddress.getLocalHost(),
                        8888);
                socket.send(packet);
            }
        }
    }
    ```

  - 服务端

  - ```java
    public class ServerDemo1 {
        public static void main(String[] args) throws IOException {
            //1.创建接收端对象，注册端口
            DatagramSocket socket = new DatagramSocket(8888);
            //2.创建一个数据包对象接收数据
            byte[] buffer = new byte[1024 * 64];
            DatagramPacket packet = new DatagramPacket(buffer, buffer.length);
            //3.等待接收数据
            while (true) {
                socket.receive(packet);
                int len = packet.getLength();
                //4.取出数据
                System.out.println("收到了，来自"+packet.getSocketAddress()+"的消息，消息为"+new String(buffer, 0, len));
            }
        }
    }
    ```

#### 3.UDP通信-广播、组播

UDP的三种通信方式

- 单播：单台主机与单台主机之间的通信
- 广播：当前主机与所在网络中的所有主机通信
- 组播：当前主机与选定的一组主机的通信

**UDP如何实现广播**

- 使用广播地址：255.255.255.255

- 具体操作

  - 发送端发送的数据包的目的地写的是广播地址、且指定端口
  - 本机所在网段的其他主机的程序只要匹配端口成功即可接收消息。

- ```java
  DatagramPacket packet = new DatagramPacket(buffer,
          buffer.length,
          InetAddress.getByName("255.255.255.255"),
          8888);
  ```

**UDP如何实现组播**

- 使用组播地址：224.0.0.0 ~ 239.255.255.255

- 具体操作：

  - 发送端的数据包的目的地是组播IP(例如：224.0.1.1, 端口:9999)
  - 接收端必须绑定该组播IP(224.0.1.1)，端口还要对应发送端的目的端口9999,这样即可接收该组播消息。
  - DatagramSocket的子类MulticastSocket可以在接收端绑定组播IP

- ```java
  DatagramPacket packet = new DatagramPacket(buffer,
          buffer.length,
          InetAddress.getByName("224.0.1.1"),
          9999);
  socket.send(packet);
  ```

- ```java
  //1.创建接收端对象，注册端口
  MulticastSocket socket = new MulticastSocket(9999);
  //把当前接收端绑定到组中
  socket.joinGroup(InetAddress.getByName("224.0.1.1"));
  ```

#### 4.TCP通信-快速入门

- 编写客户端代码
- 编写服务端代码、原理分析

![](D:\mybatis笔记\images\j64.png)

一发一收：

- ```java
  public class ClientDemo1 {
      public static void main(String[] args) {
          Socket socket = null;
          try {
              //1.创建Socket通信管道请求有服务端的连接
              //参数一：服务端的IP地址
              //参数二：服务端的端口
              socket = new Socket("127.0.0.1", 7777);
              OutputStream os = socket.getOutputStream();
              PrintStream ps = new PrintStream(os);
              ps.println("我是TCP的客户端，我已经与你对接，并发出消息");//print没有换行，所以不是一行
              ps.flush();
          } catch (Exception e) {
              e.printStackTrace();
          }
      }
  }
  ```

- ```java
  public class ServerDemo01 {
      public static void main(String[] args) {
          try {
              System.out.println("服务端启动成功");
              //注册服务端端口
              ServerSocket serverSocket = new ServerSocket(7777);
              //必须调用accept方法，等待接收客户端的Socket连接请求，建立Socket管道通信
              Socket socket = serverSocket.accept();
              InputStream inputStream = socket.getInputStream();
              //把字节输入流包装成缓冲字符输入流进行消息的接收
              BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream));
              String msg;
              if (((msg = reader.readLine()) != null)) { //如果是while循环，则会等客户端发消息，而此时客户端挂了，服务端也会挂掉
                  System.out.println(socket.getRemoteSocketAddress() + "说了："+msg);
              }
          } catch (Exception e) {
              e.printStackTrace();
          }
      }
  }
  ```

总结：

- TCP通信服务端用的代表类？
  - ServerSocket类，注册端口
  - 调用accept()方法阻塞等待接收客户端连接，得到Socket对象
- TCP通信的基本原理
  - 客户端怎么发，服务端就应该怎么接收
  - 客户端如果没有消息，服务端就会进入阻塞等待
  - Socket一方关闭或者出现异常、对方Socket也会失效或者出错

#### 5.TCP通信-多发多收消息

- 多发多收

- ```java
  public class ClientDemo1 {
      public static void main(String[] args) {
          try {
              //1.创建Socket通信管道请求有服务端的连接
              //参数一：服务端的IP地址
              //参数二：服务端的端口
              Socket socket = new Socket("127.0.0.1", 7777);
              OutputStream os = socket.getOutputStream();
              PrintStream ps = new PrintStream(os);
              Scanner sc = new Scanner(System.in);
              while(true){
                  System.out.println("请说：");
                  String msg = sc.nextLine();
                  ps.println(msg);//print没有换行，所以不是一行
                  ps.flush();
              }
          } catch (Exception e) {
              e.printStackTrace();
          }
      }
  }
  ```

- ```java
  public class ServerDemo01 {
      public static void main(String[] args) {
          try {
              System.out.println("服务端启动成功");
              //注册服务端端口
              ServerSocket serverSocket = new ServerSocket(7777);
              //必须调用accept方法，等待接收客户端的Socket连接请求，建立Socket管道通信
              Socket socket = serverSocket.accept();
              InputStream inputStream = socket.getInputStream();
              //把字节输入流包装成缓冲字符输入流进行消息的接收
              BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream));
              String msg;
              while (((msg = reader.readLine()) != null)) { //如果是while循环，则会等客户端发消息，而此时客户端挂了，服务端也会挂掉
                  System.out.println(socket.getRemoteSocketAddress() + "说了："+msg);
              }
          } catch (Exception e) {
              e.printStackTrace();
          }
      }
  }
  ```

- 本案例实现了多发多收，那么是否可以接收多个客户端的消息？（不可以）

  - **因为服务端现在只有一个线程，只能与一个客户端进行通信**

#### 6.TCP通信-同时接受多个客户端消息

- 引入多线程

- ![](D:\mybatis笔记\images\j65.png)

- 客户端不变

- 服务端要创建多线程来处理每个socket管道

- ```java
  public class ServerDemo01 {
      public static void main(String[] args) {
          try {
              System.out.println("服务端启动成功");
              //注册服务端端口
              ServerSocket serverSocket = new ServerSocket(7777);
              while (true){
                  //必须调用accept方法，等待接收客户端的Socket连接请求，建立Socket管道通信
                  Socket socket = serverSocket.accept();
                  new MyThread(socket).start();
              }
          } catch (Exception e) {
              e.printStackTrace();
          }
      }
      static class MyThread extends Thread {
          private Socket socket;
          public MyThread(Socket socket){
              this.socket = socket;
          }
  
          @Override
          public void run() {
              try {
                  InputStream inputStream = socket.getInputStream();
                  //把字节输入流包装成缓冲字符输入流进行消息的接收
                  BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream));
                  String msg;
                  while (((msg = reader.readLine()) != null)) { //如果是while循环，则会等客户端发消息，而此时客户端挂了，服务端也会挂掉
                      System.out.println(socket.getRemoteSocketAddress() + "说了："+msg);
                  }
              } catch (Exception e) {
                  e.printStackTrace();
              }
          }
      }
  }
  ```

#### 7.TCP通信-使用线程池优化

上述的通信架构存在什么问题？

- 客户端与服务端的线程模型是：N-N的关系

- 客户端越多，系统越容易瘫痪

- **引入线程池处理多个客户端消息**

- ![](D:\mybatis笔记\images\j66.png)

- ```java
  /**
   * 使用线程池优化通信
   */
  public class ServerDemo01 {
      private static ExecutorService pool = new ThreadPoolExecutor(
              3,
              5,
              8,
              TimeUnit.SECONDS,
              new ArrayBlockingQueue<>(2),
              Executors.defaultThreadFactory(),
              new ThreadPoolExecutor.AbortPolicy());
      public static void main(String[] args) {
          try {
              System.out.println("服务端启动成功");
              //注册服务端端口
              ServerSocket serverSocket = new ServerSocket(7777);
              while (true){
                  //必须调用accept方法，等待接收客户端的Socket连接请求，建立Socket管道通信
                  Socket socket = serverSocket.accept();
                  System.out.println(socket.getRemoteSocketAddress()+"上线了");
                  pool.execute(new Runnable() {
                      @Override
                      public void run() {
                          try {
                              InputStream inputStream = socket.getInputStream();
                              //把字节输入流包装成缓冲字符输入流进行消息的接收
                              BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream));
                              String msg;
                              while (((msg = reader.readLine()) != null)) { //如果是while循环，则会等客户端发消息，而此时客户端挂了，服务端也会挂掉
                                  System.out.println(socket.getRemoteSocketAddress() + "说了："+msg);
                              }
                          } catch (Exception e) {
                              System.out.println(socket.getRemoteSocketAddress()+"下线了");
                          }
                      }
                  });
              }
          } catch (Exception e) {
              System.out.println();
              e.printStackTrace();
          }
      }
  }
  ```

- 本次使用线程池的优势？

  - 服务端可以复用线程处理多个客户端，避免系统瘫痪
  - 适合客户端通信时长较短的场景

#### 8.TCP通信实战案例-即时通信

什么是即时通信？

- 即时通信，是指一个客户端的消息发出去，其他客户端可以接收到
- 之前我们的消息都是发给服务端的
- 即时通信需要进行端口转发的设计思想
- 服务端需要把在线的Socket管道存储起来
- 一旦收到一个消息要推送给其他管道

客户端：

- ```java
  /**
   * 即时通信：客户端不仅要发消息，还要接收消息
   */
  public class ClientDemo1 {
      public static void main(String[] args) {
          try {
              //1.创建Socket通信管道请求有服务端的连接
              //参数一：服务端的IP地址
              //参数二：服务端的端口
              Socket socket = new Socket("127.0.0.1", 9999);
              new MyThreadReceiveMsg(socket).start();
              OutputStream os = socket.getOutputStream();
              PrintStream ps = new PrintStream(os);
              Scanner sc = new Scanner(System.in);
              while (true) {
                  System.out.println("请说：");
                  String msg = sc.nextLine();
                  ps.println(msg);//print没有换行，所以不是一行
                  ps.flush();
              }
          } catch (Exception e) {
              e.printStackTrace();
          }
      }
      static class MyThreadReceiveMsg extends Thread {
          private Socket socket;
          public MyThreadReceiveMsg(Socket socket) {
              this.socket = socket;
          }
          @Override
          public void run() {
              try {
                  InputStream inputStream = socket.getInputStream();
                  //把字节输入流包装成缓冲字符输入流进行消息的接收
                  BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream));
                  String msg;
                  while (((msg = reader.readLine()) != null)) { //如果是while循环，则会等客户端发消息，而此时客户端挂了，服务端也会挂掉
                      System.out.println("收到：" + msg);
                  }
              } catch (Exception e) {
                  System.out.println("服务端已将您踢出");
              }
  
          }
      }
  }
  ```

服务端：

- ```java
  public class ServerDemo01 {
      public static List<Socket> allOnlineSocket = new ArrayList<>();
      public static void main(String[] args) {
          try {
              System.out.println("服务端启动成功");
              //注册服务端端口
              ServerSocket serverSocket = new ServerSocket(9999);
              while (true){
                  //必须调用accept方法，等待接收客户端的Socket连接请求，建立Socket管道通信
                  Socket socket = serverSocket.accept();
                  System.out.println(socket.getRemoteSocketAddress()+"上线了");
                  allOnlineSocket.add(socket);
                  new ServerReaderThread(socket).start();
              }
          } catch (Exception e) {
              e.printStackTrace();
          }
      }
      static class ServerReaderThread extends Thread {
          private Socket socket;
          public ServerReaderThread(Socket socket){
              this.socket = socket;
          }
              @Override
              public void run() {
                  try {
                      InputStream inputStream = socket.getInputStream();
                      //把字节输入流包装成缓冲字符输入流进行消息的接收
                      BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream));
                      String msg;
                      while (((msg = reader.readLine()) != null)) { //如果是while循环，则会等客户端发消息，而此时客户端挂了，服务端也会挂掉
                          System.out.println(socket.getRemoteSocketAddress() + "发来了："+msg);
                          //将该消息进行端口转发，给全部客户端socket管道
                          for (Socket socket1 : allOnlineSocket) {
                              OutputStream outputStream = socket1.getOutputStream();
                              PrintStream ps = new PrintStream(outputStream);
                              ps.println(msg);
                              ps.flush();
                          }
                      }
                  } catch (Exception e) {
                      System.out.println(socket.getRemoteSocketAddress()+"下线了");
                      allOnlineSocket.remove(socket);
                  }
              }
      }
  }
  ```

#### 9.TCP通信实战案例-模拟BS系统

- 浏览器访问服务端，不需要开发客户端

- ![](D:\mybatis笔记\images\j67.png)

- ![](D:\mybatis笔记\images\j68.png)

- ```java
  public class BSserverDemo {
      private static ExecutorService pool = new ThreadPoolExecutor(
              3,
              5,
              8,
              TimeUnit.SECONDS,
              new ArrayBlockingQueue<>(2),
              Executors.defaultThreadFactory(),
              new ThreadPoolExecutor.AbortPolicy());
  
      public static void main(String[] args) {
          try {
              ServerSocket serverSocket = new ServerSocket(8080);
              while (true) {
                  Socket socket = serverSocket.accept();
                  pool.execute(new ServerReaderRunnable(socket));
              }
          }catch (Exception e ){
              e.printStackTrace();
          }
      }
      static class ServerReaderRunnable implements Runnable {
          private Socket socket;
          public ServerReaderRunnable(Socket socket) {
              this.socket = socket;
          }
          @Override
          public void run() {
              try {
                  OutputStream outputStream = socket.getOutputStream();
                  PrintStream ps = new PrintStream(outputStream);
                  ps.println("HTTP/1.1 200 OK");
                  ps.println("Content-Type:text/html;charset=UTF-8");
                  ps.println();
                  ps.println("<h4>hello，html</h4>");
                  ps.close();
              } catch (IOException e) {
                  e.printStackTrace();
              }
          }
      }
  }
  ```

- 网页访问http://127.0.0.1:8080

### 22.单元测试、反射、注解、动态代理

![](D:\mybatis笔记\images\j69.png)

#### 1.单元测试

1.概述

- 单元测试就是针对最小的功能单元编写测试代码，java程序最小的功能单元是方法，因此，单元测试就是针对java方法的测试，进而检查方法的正确性。
- Junit单元测试框架
  - Junit是使用java语言实现的单元测试框架，它是开源的，Java开发者都应当学习并使用Junit编写单元测试。
  - 几乎所有的IDE工具都集成了Junit
- 优点：可以选择执行哪些测试方法，可以一键执行全部测试方法的测试。
- 测试方法：必须是公共的无参数无返回值的非静态方法 

2.快速入门

- ```java
  //业务方法
  public class UserService {
      public String loginName(String loginName, String password) {
          if ("admin".equals(loginName) && "123456".equals(password)){
              return "登陆成功";
          }else {
              return "用户名或者密码有问题";
          }
      }
      public void selectNames() {
          System.out.println(10/0);
          System.out.println("查询全部用户名称成功~~~");
      }
  }
  ```

- ```java
  public class TestUserService {
      /**
       * 测试方法
       */
      @Test
      public void testLoginName(){
          UserService userService = new UserService();
          String msg = userService.loginName("admin", "123456");
          //进行预期结果的正确性测试，断言
          Assert.assertEquals("您的功能业务可能出现问题","登陆成功",msg);
      }
      @Test
      public void testSelectNames(){
          UserService userService = new UserService();
          userService.selectNames();
      }
  }
  ```

3.常用注解

![](D:\mybatis笔记\images\j70.png)

![](D:\mybatis笔记\images\j71.png)

#### 2.反射

##### 1.概述

- 反射是指对于任何一个Class类，在运行的时候都可以直接得到这个类全部成分
- 在运行时，可以直接得到这个类的构造器对象：Constructor
- 在运行时，可以直接得到这个类的成员变量对象：Field
- 在运行时，可以直接得到这个类的成员方法对象：Method
- 这种运行时动态获取类信息以及动态调用类中成分的能力称为java语言的反射机制

反射的关键：

- **反射的第一步都是先得到编译后的Class类对象，然后就可以得到Class的全部成分**

##### 2.获取类对象

![](D:\mybatis笔记\images\j72.png)

![](D:\mybatis笔记\images\j73.png)

```java
//三种获取类对象的方式
public class Test {
    public static void main(String[] args) throws ClassNotFoundException {
        //方式1：Class类中的一个静态方法：forName(全限名)
        Class c = Class.forName("com.yyue.d21_reflect_class.Student");
        System.out.println(c);
        //2.类名.class
        Class c1 = Student.class;
        System.out.println(c1);
        //3.对象.getClass() 获取对象对应类的Class对象
        Student s1 = new Student();
        System.out.println(s1.getClass());
    }
}
```

##### 3.获取构造器对象

![](D:\mybatis笔记\images\j74.png)

- 四种方式：

- ```java
  public class TestStudent01 {
      /**
       * 1.getConstructors
       * 获取全部的构造器，只能获取public修饰的构造器
       * Constructor[] getConstructors()
       */
      @Test
      public void testGetConstructors() {
          Constructor[] constructors = Student.class.getConstructors();
          for (Constructor constructor : constructors) {
              System.out.println(constructor.getName() + constructor.getParameterCount());
          }
      }
      //2.getDeclaredConstructors()
      //获取全部的构造器，无所谓权限是否可及
      @Test
      public void testGetDeclaredConstructors() {
          Constructor[] constructors = Student.class.getDeclaredConstructors();
          for (Constructor constructor : constructors) {
              System.out.println(constructor.getName() + constructor.getParameterCount());
          }
      }
      //3.getConstructor(Class... parameterTypes)
      //获取某个构造器，只能拿public修饰的某个构造器
      @Test
      public void testGetConstructor() throws NoSuchMethodException {
          Constructor constructor = Student.class.getConstructor();
          Constructor constructor1 = Student.class.getConstructor(String.class, int.class);
          System.out.println(constructor.getName() + constructor.getParameterCount());
          System.out.println(constructor1.getName() + constructor1.getParameterCount());
      }
      //4.getDeclaredConstrucctor
      //获取某个构造器，无所谓权限
      @Test
      public void testGetDeclaredConstructor() throws NoSuchMethodException {
          Constructor constructor = Student.class.getDeclaredConstructor();
          Constructor constructor1 = Student.class.getDeclaredConstructor(String.class, int.class);
          System.out.println(constructor.getName() + constructor.getParameterCount());
          System.out.println(constructor1.getName() + constructor1.getParameterCount());
      }
  }
  ```

- 使用反射技术获取构造器对象并使用

  - 获取构造器的作用依然是初始化一个对象返回

  - 如果非public的构造器，需要打开权限(暴力反射)，然后再创建对象

  - ![](D:\mybatis笔记\images\j75.png)

  - ```java
    @Test
    public void testGetDeclaredConstructor() throws NoSuchMethodException, IllegalAccessException, InvocationTargetException, InstantiationException {
        Constructor constructor = Student.class.getDeclaredConstructor();
        Constructor constructor1 = Student.class.getDeclaredConstructor(String.class, int.class);
        //私有的构造器可以暴力反射
        constructor.setAccessible(true);
        Student s = (Student) constructor.newInstance();
        System.out.println(s);
        Student s1 = (Student) constructor1.newInstance("马嘉祺",20);
        System.out.println(s1);
        System.out.println(constructor.getName() + constructor.getParameterCount());
    }
    ```

##### 4.获取成员变量对象

使用反射技术获取成员变量对象并使用

- 反射的第一步是先得到类对象，然后从对象中获取类的成分对象

- Class类中用于获取成员变量的方法：

  - Field[] getFields    返回所有成员变量对象的数组(只能拿public的)

  - Field[] getDeclaredFields()  返回所有成员变量对象的数组，存在就能拿到

  - Field getField(String name)  返回单个成员变量对象(只能拿public的)

  - Field getDeclaredField(String name)    返回单个成员变量，存在就能拿到

  - ```java
    public class FieldDemo1 {
        /**
         * 1. Field[] getFields    返回所有成员变量对象的数组(只能拿public的)
         * 2. Field[] getDeclaredFields()  返回所有成员变量对象的数组，存在就能拿到
         * 3. Field getField(String name)  返回单个成员变量对象(只能拿public的)
         * 4. Field getDeclaredField(String name)    返回单个成员变量，存在就能拿到
         */
        //1.获取所有成员变量对象
        @Test
        public void testGetFields(){
            Field[] fields = Student.class.getFields();
            for (Field field : fields) {
                System.out.println(field);
            }
        }
        //2.获取所有成员变量对象,全部，无论权限
        @Test
        public void testGetDeclaredFields(){
            Field[] fields = Student.class.getDeclaredFields();
            for (Field field : fields) {
                System.out.println(field);
            }
        }
        @Test
        public void testGetField(){
            try {
                Field field = Student.class.getField("COUNTRY");
                System.out.println(field);
            } catch (NoSuchFieldException e) {
                e.printStackTrace();
            }
        }
        @Test
        public void testGetDeclaredField(){
            try {
                Field field = Student.class.getDeclaredField("name");
                System.out.println(field);
            } catch (NoSuchFieldException e) {
                e.printStackTrace();
            }
        }
    }
    ```

- 使用反射技术获取成员变量对象并使用

  - 获取成员变量的作用依然是在某个对象取值、赋值

  - void set(Object obj, Object value)  赋值

  - Object get(Object obj)   获取值

  - ```java
    /**
     * 目标：反射获取成员变量：取值和赋值
     * Field的方法，给成员变量赋值和取值
     * void set(Object obj, Object value) 给对象注入某个成员变量数据
     * Object get(Object obj) 获取对象的成员变量的值
     * void setAccessible(true) 暴力反射，设置为可以直接访问私有类型的属性
     * Class getType() 获取属性的类型，返回Class对象
     * String getName()  获取属性的名称
     */
    public class FieldDemo2 {
        @Test
        public void setField() throws Exception {
            Field age = Student.class.getDeclaredField("age");
            Student s = new Student();
            age.setAccessible(true);
            //取值
            age.set(s, 18);//s.setAge(18)
            System.out.println(s);
            //赋值
            System.out.println(age.get(s));
        }
    }
    ```

- 如果某成员变量是非public的，需要打开权限(暴力反射)，

  - setAccessible(boolean)

##### 5.获取方法对象

使用反射技术获取方法对象并使用

- 反射的第一步就是先得到类对象，然后从类对象中获取类的成分对象

- Class类中用于获取成员方法的方法

- ![](D:\mybatis笔记\images\j76.png)

- 获取成员方法的作用依然是在某个对象中进行执行此方法

- Method类中用于触发执行的方法：

- ![](D:\mybatis笔记\images\j77.png)

- ```java
  public class MethodDemo01 {
      /**
       * 1.获取类中的所有成员方法对象
       */
      @Test
      public void getDeclaredMethods() {
          Method[] methods = Dog.class.getDeclaredMethods();
          for (Method method : methods) {
              System.out.println(method.getName() + "====>" + method.getReturnType());
          }
      }
  
      /**
       * 2.获取某个方法对象
       */
      @Test
      public void getDeclaredMethod() throws Exception {
          Class dog = Dog.class;
          Method method = dog.getDeclaredMethod("eat");
          Method method1 = dog.getDeclaredMethod("eat", String.class);
          Dog d = new Dog();
          method.setAccessible(true);
          method.invoke(d);
          method1.setAccessible(true);
          Object result = method1.invoke(d, "麦当劳");//有返回值
          System.out.println(result);
      }
  }
  ```

##### 6.反射的作用-绕过编译阶段为集合添加数据

- 反射是作用在运行时的技术，此时集合的泛型将不能产生约束了，此时是可以为集合存入其他任意类型的元素的

- 泛型只是在编译阶段可以约束集合只能操作某种数据类型，在编译称Class文件进入运行阶段的时候，其真实类型都是ArrayList了，泛型相当于被擦除了。

- ```java
  public class ReflectDemo {
      public static void main(String[] args) throws Exception {
          ArrayList<Integer> list1 = new ArrayList<>();
          ArrayList<String> list2 = new ArrayList<>();
          System.out.println(list1.getClass());
          System.out.println(list2.getClass());
          System.out.println("------------------");
          list1.add(22);
          list1.add(23);
          //想加入"字符串"list1.add("马嘉祺");
          Class c = list1.getClass();
          Method method = c.getDeclaredMethod("add", Object.class);
          boolean rs = (boolean)method.invoke(list1, "马嘉祺");
          System.out.println(rs);
          System.out.println(list1);
      }
  }
  ```

- 结果：太牛了，突破泛型的约束，字符串能加到整型集合中

- ```
  class java.util.ArrayList
  class java.util.ArrayList
  ------------------
  true
  [22, 23, 马嘉祺]
  ```

##### 7.反射的作用-通用框架的底层原理

反射做通用框架

需求：给任意一个对象，在不清楚对象字段的情况，可以把对象的字段名称和对应值存储到文件中去

分析：

- 定义一个方法，可以接收任意类的对象

- 每次收到一个对象后，需要解析这个对象的全部成员变量名称

- 这个对象可能是任意的，那么怎么才可以知道这个对象的全部成员变量名称呢？

- 使用反射获取对象的Class类对象，然后获取全部成员变量信息

- 遍历成员变量信息，然后提取成员变量在对象中的具体值

- 存入成员变量名称和值到文件中去

- 一个工具类用来存储任意类型的对象

- ```java
  public class MybatisUtil {
      /**
       * 保存任意类型的对象
       */
      public static void save(Object obj)  {
          try (PrintStream ps = new PrintStream(new FileOutputStream("E:\\projectwork\\javase\\file-io\\src\\data.txt", true))){//直接释放管道资源
              //1.提取这个对象的全部成员变量，只有反射可以解决
              Class c = obj.getClass();
              ps.println("============"+c.getSimpleName() + "============");//获取当前类名
              //2.提取它的全部成员变量
              Field[] fields = c.getDeclaredFields();
              //3.获取成员变量的信息
              for (Field field : fields) {
                  String name = field.getName();//成员变量的名称
                  field.setAccessible(true);
                  String value = field.get(obj) + "";
                  ps.println(name +":" + value);
              }
          } catch (Exception e) {
              e.printStackTrace();
          }
      }
  }
  ```

#### 3.注解

##### 1.概述

- Java注解(annotation)又称Java标注，是JDK5.0引入的一种注释机制
- Java语言中的类、构造器、方法、成员变量、参数等都可以被注解进行标注

##### 2.自定义注解

- 自定义注解--格式

  - 自定义注解就是自己做一个注解来使用

  - ```java
    public @interface 注解名称 {
        public 属性类型 属性名() default 默认值；
    }
    ```

- 特殊属性

  - value属性，如果只有一个value属性的情况下，使用value属性的时候可以省略value名称不写
  - 但是如果有多个属性，且多个属性没有默认值，那么value名称不能省略

- 自定义一个MyBook注解

- ```java
  /**
   * 自定义注解
   */
  public @interface MyBook {
      public String name();
      public String[] authors();
      public double price();
  }
  ```

- 可以添加在类上、方法上、变量上

- ```java
  @MyBook(name = "《精通java》", authors = {"yyue", "zhangzhenyuan"}, price = 100)
  public class AnnotationDemo01 {
      @MyBook(name = "《精通javaSE》", authors = {"yyue", "zhangzhenyuan"}, price = 100)
      private AnnotationDemo01() {
      }
      @MyBook(name = "《精通javaSE1》", authors = {"yyue", "zhangzhenyuan"}, price = 100)
      public static void main(String[] args) {
          @MyBook(name = "《精通javaSE》", authors = {"yyue", "zhangzhenyuan"}, price = 100)
          int age = 21;
      }
  }
  ```

##### 3.元注解

- 元注解：就是注解注解的注解
- 有两个：
  - @Target：约束自定义注解只能在哪些地方使用
  - @Retention：申明注解的生命周期
- ![](D:\mybatis笔记\images\j78.png)

##### 4.注解解析

- 注解的操作中经常需要进行解析，注解的解析就是判断是否存在注解，存在注解就解析出内容

与注解解析相关的接口

- Annotation：注解的顶级接口，注解都是Annotation类型的对象
- AnnotatedElement：该接口定义了与注解解析相关的解析方法
- ![](D:\mybatis笔记\images\j79.png)

解析注解的技巧

- 注解在哪个成份上，就先拿哪个成分对象

- 比如注解作用成员方法，则要获取该成员方法对应的Method对象，再来拿上面的注解

- 比如注解作用在类上，则要该类的Class对象，再来拿上面的注解

- 比如注解作用在成员变量上，则要获得该成员变量对应的Field对象，再来拿上面的注解

- 一个注解类@Book

- ```java
  @Target({ElementType.TYPE, ElementType.METHOD})
  @Retention(RetentionPolicy.RUNTIME)
  public @interface Book {
      String value();
      double price() default 100;
      String[] authors();
  }
  ```

- 一个被注解的类

- ```java
  @Book(value = "《精通java》", price = 19.9, authors = {"yyue", "zhang"})
  public class BookStore {
      @Book(value = "《精通javaSE》", price = 19.9, authors = {"yyue", "zhang"})
      public void read(){
      }
  }
  ```

- 解析注解的类

- ```java
  public class AnnotationDemo02 {
      public static void main(String[] args) throws NoSuchMethodException {
          //解析类上面的注解
          Class c = BookStore.class;
          if (c.isAnnotationPresent(Book.class)){//如果类上存在该注解
              Book book = (Book)c.getDeclaredAnnotation(Book.class);
              System.out.println(book.value());
              System.out.println(book.price());
              System.out.println(Arrays.toString(book.authors()));
          }
          //解析方法上面的注解
          Method read = c.getDeclaredMethod("read");
          if (read.isAnnotationPresent(Book.class)) {
              Book book = (Book) read.getDeclaredAnnotation(Book.class);
              System.out.println(book.value());
              System.out.println(book.price());
              System.out.println(Arrays.toString(book.authors()));
          }
      }
  }
  ```

##### 5.注解的应用场景一：junit框架

模拟Junit框架

- 定义若干个方法，只要加了MyTest注解，就可以在启动时被触发执行

- @MyTest注解

- ```java
  @Target(ElementType.METHOD)
  @Retention(RetentionPolicy.RUNTIME)
  public @interface MyTest {
  }
  ```

- 在类方法上添加@MyTest注解

- ```java
  public class MyTestDemo {
      @MyTest
      public void test1(){
          System.out.println("test1...");
      }
      public void test2(){
          System.out.println("test2...");
      }
      @MyTest
      public void test3(){
          System.out.println("test3...");
      }
  }
  ```

- 解析

- ```java
  public class AnnotationDemo1 {
      public static void main(String[] args) throws InvocationTargetException, IllegalAccessException {
          //解析所有带MyTest注解的方法，让其执行
          //1.获取所有方法
          Class c = MyTestDemo.class;
          MyTestDemo o = new MyTestDemo();
          for (Method method : c.getDeclaredMethods()) {
              //判断是否带有MyTest注解
              if (method.isAnnotationPresent(MyTest.class)) {
                  method.invoke(o);
              }
          }
      }
  }
  ```

#### 4.动态代理













