# JDK和JRE有什么区别 #
JDK 的全屏是 Java Development Kit 软件开发工具包,提供了Java的开发环境和运行环境   JRE全屏为Java RunTime Environment. Java运行环境
如果只是想运行程序那么只安装JRE就可以, 如果想开发,编写程序那么需要安装JDK
JDK包含了JRE


# ==与equal的区别 #

考察点分为两个
1 基本类型比较:比较的是值相等, 引用类型比较:比较的是引用地址相等
2 ==比较的是引用类型 , equal本质也是比较的引用类型

说明
对于string 和 integer 等比较equal的时候发现比较的是值类型,那是因为他们重写了equal方法,所以最终比较的是值相等

# 两个对象的Hashcode相等, 则equals也一定为true吗 #

考察点

1 Hashcode代表了什么: 确定该对象在哈希表中的索引位置,应用的地方例如:HashMap,HashTable,HashSet, 通过Hash索引位置我们可以知道该对象在散列表的位置
2 Hash值相等,但是两个键值对也可能不相等--->针对于需要使用散列表的类
3 equals相等那么Hash也一定相等
4 如果不需要散列表那么其实没有区别

        
        //重写hashcode,返回都是1
        judytest judytest1 = new judytest();
        judytest judytest2 =  new judytest();
        System.out.println(judytest1.hashCode());  //1
        System.out.println(judytest2.hashCode());  //1
        System.out.println(judytest1.equals(judytest2)); //false

----------
        //在没有重写的情况下,Hashcode相等,但是equals也不相等
        String str1 = "通话";
        String str2 = "重地";
        System.out.println(str1.hashCode());  //1179395
        System.out.println(str2.hashCode());  //1179395
        System. out. println(str1. equals(str2)); //false


# final在Java中的作用 #       

 考察点:
 1 final可以作用在什么地方? 1类, 方法,修饰符 
 2 被final修饰之后引用还可以改变吗? **不可以改变**
 3 被final修饰的方法是**不可以**被重写的
 4 被final修饰的类是不可以被继承的,因为他**不可以被改变**



# Java中的Math.round(-1.5) #

考察点:
  Math.round()的作用是四舍五入,如果是负数,则取接近最大值的那个数

 `  System.out.println(Math.round(-1.5)); //1`


# String属于基本类型吗 #

考察点:
   基本类型都有哪些? byte:1  char:1 short:2 int:4 floot:4 long:8 double:8 boolean:1

不属于,String 属于引用类型,他是对象

# java中操作字符串有哪些类,他们之间有什么区别 #

 考察点:
  字符串:String
  操作字符串安全与不安全.为什么

1 String, StringBuffer , StringBuilder

2 区别
 A. String 声明的是不可以变对象 , StringBuffer,Stringbuilder是在原有的基础上可以改变. 
 B. StringBuffer 是线程安全的,因为加了synchronized .StringBuilder 声明的是可变对象但是非线程安全的
   `  
    @Override
    synchronized StringBuffer append(AbstractStringBuilder asb) {
        toStringCache = null;
        super.append(asb);
        return this;
    }`
 C. StringBuffer效率没有StringBuilder高

# String str="i" 与String str = new String("i") #

  考察点
  数据存放在JVM什么地方

1 String str 存放在JVM常量池区的一块空间
2 String str = new String() 存储在堆区

       `  
        // 为true的原因是因为在同一块区域常量池, 
        String s1 = "i";
        String s2 = "i";
        String s3 = "i";
        System.out.println(s1==s2);  //true
        System.out.println(s2 == s3);  //true
        System.out.println(s1.equals(s2)); //true
        System.out.println(s2.equals(s3)); //true
        System.out.println("----------------------------------");
        // 为false的原因是因为在堆与不同地址
        String s4 = new String("i");
        String s5 = new String("i");
        String s6 = new String("i");
        System.out.println(s4==s5); //false
        System.out.println(s5 == s6); //false
       `

# 如何将字符串反转 #

 考察点
 StringBuffer和StringBuilder有反转的方法,但是String没有该方法
        `  
        StringBuffer stringBuffer = new StringBuffer("12345678");
        stringBuffer.reverse();
        System.out.println(stringBuffer); //87654321
        `

# String常用方法有哪些 #
  
 考察点
   基本代码书写
    `
     public static void main(String[] args){
        String a = new String("judy");
        System.out.println(a.toUpperCase()); //把小写转换为大写
        System.out.println(a.compareTo("judy1"));//比较大小
        System.out.println(a.substring(1));//从第几位截取字符串
        System.out.println(a.substring(1, 2));//从开始位置到结束位置截取字符串
        System.out.println(a.matches("judy"));// 字符串匹配
        System.out.println(a.replace("judy", "徐靖峰"));
        a.trim(); // 去除空格
        System.out.println(a.split("u"));//分割字符串
    }

    `

# 抽象类必须要有抽象方法吗 #
 考察点
  1什么是抽象类
  2抽象类和抽象方法的区别
  
  A. 抽象类表示抽取公共方法,并且抽象类不可以被实例化,也就是不能被new,抽象类被继承表示的是实现不是重写
  B. 抽象类里面可以包含其他方法,如果该方法被声明为抽象方法,那么它的类也必须是抽象类,否则编译都通不过

 
# 抽象类和普通类的区别 #

  1 抽象类里面可以有抽象方法
  2 普通类可以被实例化,但是抽象类不可以被实例化

# 抽象类能使用final修饰吗 #
  
  考察点
  1被final修饰的类是否可以改变,是否可以继承
  
  A. 抽象类不可以被final修饰,编译都通不过, 因为被final修饰之后就不可以改变了, 但是抽象类必须被继承,实现


# 接口和抽象类有什么区别 #
   
   考察点
   1 什么是接口, 什么是抽象类
   2 接口用在什么场景, 抽象类用在什么场景
   3 语法区别

   A. 接口表示规范 , 抽象类表示公共提取的方法
   B. 接口应用定义模块之间的通信规则,规范, 抽象类主要是在代码重用
   C. 接口没有构造方法,但是抽象类有构造方法, 接口没有静态方法,抽象类有静态方法,访问修饰符,接口只能是public,抽象类都可以
   D. 接口使用implements, 抽象类是extends ,接口是可以多个类实现, 只能继承一个抽象类



   
 


   
  

  



 




 
  