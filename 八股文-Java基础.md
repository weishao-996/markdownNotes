---
title: 面试-Java基础
date: 2022-09-06 11:11:45
tags: 
- 面试
category_bar: [面试]
categories:
- [面试]

---

# **基本概念与常识**

## 什么是字节码?采用字节码的好处是什么?

- 在 Java 中，JVM 可以理解的代码就叫做字节码（**即扩展名为 .class 的文件**）。
- 在一定程度上解决了传统解释型语言执行效率低的问题，同时又保留了解释型语言**可移植**的特点。
- 由于字节码并不针对一种特定的机器，因此，Java 程序无须重新编译便可在多种不同操作系统的计算机上运行。 

![image-20230909200711855](https://static.weishao996.top/article/20230909200712.png)

 **JIT（just-in-time compilation） 编译器，JIT 属于运行时编译**。当 JIT 编译器完成第一次编译后，其会将字节码对应的机器码保存下来，下次可以直接使用。而我们知道，机器码的运行效率肯定是高于 Java 解释器的。这也解释了我们为什么经常会说 **Java 是编译与解释共存的语言** 。HotSpot 采用了惰性评估(Lazy Evaluation)的做法，根据二八定律，消耗大部分系统资源的只有那一小部分的代码（**热点代码**），而这也就是 **JIT 所需要编译的部分**。JVM 会根据代码每次被执行的情况收集信息并相应地做出一些优化，因此执行的次数越多，它的速度就越快。

**JDK 9** 引入了一种新的**编译模式 AOT**(Ahead of Time Compilation)，它是直接将字节码编译成机器码，这样就避免了 JIT 预热等各方面的开销。JDK 支持**分层编译和 AOT 协作使用**。但是 ，AOT 编译器的编译质量是肯定比不上 JIT 编译器的。



## 一次编写、到处运行

JVM（Java虚拟机）是Java跨平台的关键。

在程序运行前，Java**源代码（.java）**需要经过编译器编译成**字节码（.class）**。在程序运行时，JVM负责将字节码翻译成特定平台下的机器码并运行，也就是说，只要在不同的平台上安装对应的JVM，就可以运行字节码文件。

同一份Java源代码在不同的平台上运行，它不需要做任何的改变，并且只需要编译一次。而编译好的字节码，是通过JVM这个中间的“桥梁”实现跨平台的，JVM是与平台相关的软件，它能将统一的字节码翻译成该平台的机器码。

**注意事项**

1. 编译的结果是生成字节码、不是机器码，字节码不能直接运行，必须通过JVM翻译成机器码才能运行；

2. 跨平台的是Java程序、而不是JVM，JVM是用C/C++开发的软件，不同平台下需要安装不同版本的JVM。

   

## Oracle JDK vs OpenJDK

1. **OpenJDK 是一个参考模型并且是完全开源的**，而 Oracle JDK 是 OpenJDK 的一个实现，并不是完全开源的；
2. **Oracle JDK 比 OpenJDK 更稳定。**OpenJDK 和 Oracle JDK 的代码几乎相同，但 Oracle JDK 有更多的类和一些错误修复。因此，如果您想开发企业/商业软件，我建议您选择 Oracle JDK，因为它经过了彻底的测试和稳定。某些情况下，有些人提到在使用 OpenJDK 可能会遇到了许多应用程序崩溃的问题，但是，只需切换到 Oracle JDK 就可以解决问题；
3. 在响应性和 JVM 性能方面，**Oracle JDK 与 OpenJDK 相比提供了更好的性能**；
4. Oracle JDK 不会为即将发布的版本提供长期支持，用户每次都必须通过更新到最新版本获得支持来获取最新版本；
5. Oracle JDK 使用 BCL/OTN 协议获得许可，而 OpenJDK 根据 GPL v2 许可获得许可。



## Java 和 C++的区别?

都是面向对象的语言，都支持**封装、继承和多态**

Java 不提供**指针**来直接访问内存，程序内存更加安全

Java 的类是**单继承**的，C++ 支持多**重继承**；虽然 Java 的类不可以多继承，但是接口可以多继承。

Java 有**自动内存管理垃圾回收机制(GC)**，不需要程序员手动释放无用内存。

C ++同时**支持方法重载和操作符重载**，但是 **Java 只支持方法重载**（操作符重载增加了复杂性，这与 Java 最初的设计思想不符）。



## 为什么说 Java 语言“编译与解释并存”？

- **编译型** ：编译型语言 

​		将源代码一次性翻译成可被该平台执行的机器码。一般情况下，编译语言的执行速度比较快，开发效率比较低。常见的编译性语言有 C、C++、Go、Rust 等等。

- **解释型** ：解释型语言

​		通过解释器 (opens new window)一句一句的将代码解释（interpret）为机器代码后再执行。解释型语言开发效率比较快，执行速度比较慢。常见的解释性语言有 Python、JavaScript、PHP 等等。

![image-20231213230452140](https://static.weishao996.top/article/20231213230452.png)

**为什么说 Java 语言“编译与解释并存”？**

这是因为 Java 语言既具有编译型语言的特征，也具有解释型语言的特征。因为 Java 程序要经过**先编译，后解释**两个步骤，由 Java 编写的程序需要先经过**编译步骤，生成字节码（.class 文件）**，这种字节码必须由 **Java 解释器**来解释执行。



## JVM vs JDK vs JRE

- **JVM**

**Java 虚拟机（JVM）**是运行 Java 字节码的虚拟机。

JVM 有针对不同系统的特定实现（Windows，Linux，macOS），目的是使用相同的字节码，它们都会给出相同的结果。字节码和不同系统的 JVM 实现是 Java 语言“一次编译，随处可以运行”的关键所在。

- **JRE**

**Java 运行时环境**

它是运行已编译 Java 程序所需的所有内容的集合，包括 **Java 虚拟机（JVM），Java 类库，java 命令和其他的一些基础构件**。但是，它不能用于创建新程序。

- **JDK**

JDK 是 Java Development Kit 缩写，它是功能齐全的 Java SDK。**它拥有 JRE 所拥有的一切，还有编译器（javac）和工具（如 javadoc 和 jdb）**。它能够创建和编译程序。



## JAVA语言的特点

- 简单易学、有丰富的类库 
- 面向对象（Java最重要的特性，让程序耦合度更低，内聚性更高） 封装，继承，多态
- 与平台无关性（JVM是Java跨平台使用的根本） 
- 可靠安全
- 支持多线程
- 支持网络编程
- 编译与解释并存



## 线程、程序、进程

要说线程，必须得先说说进程。

- **进程：进程是代码在数据集合上的一次运行活动，是系统进行资源分配和调度的基本单位。**
- **线程：线程是进程的一个执行路径，一个进程中至少有一个线程，进程中的多个线程共享进程的资源。**

​		操作系统在分配资源时是把资源分配给进程的， 但是 CPU 资源比较特殊，它是被分配到线程的，因为真正要占用CPU运行的是线程，所以也说线程是 CPU分配的基本单位。比如在Java中，当我们启动 main 函数其实就启动了一个JVM进程，而 main 函数在的线程就是这个进程中的一个线程，也称主线程。一个进程中有多个线程，多个线程共用进程的堆和方法区资源，但是每个线程有自己的程序计数器和栈。

**程序**是含有**指令和数据的文件**，被存储在磁盘或其他的数据存储设备中，也就是说程序是静态的代码。



# **基本语法**

## 隐式类型转换

`+= `操作符会进行`隐式自动类型转换`,此处`a+=b`隐式的**将加操作的结果类型强制转换为持有结果的类** 型,而`a=a+b`则不会自动进行类型转换.如：

```java
byte a = 127;
byte b = 127;
b = a + b; // 报编译错误:cannot convert from int to byte
b += a;
```

以下代码是否有错,有的话怎么改？

```java
short s1= 1;
s1 = s1 + 1;
```

有错误.`short`类型在进行运算时会自动提升为`int`类型,也就是说` s1+1` 的运算结果是`int`类型,而`s1`是 `short`类型,此时编译器会报错

正确写法：

```java
short s1= 1;
s1 += 1;
```

`+=`操作符会对右边的表达式结果强转匹配左边的数据类型,所以没错.

在Java语言中，当参与运算的两个数是`byte`、`short`或`int`类型时，他们首先会被转化成`int`类型，然后在进行计算。然后把计算的结果赋值给用来存储结果的变量。如果用来存储结果变量的类型是byte或者short，这意味着需要把int类型转化成byte或者short类型。a+=b和a = a+b的区别就在于`a+=b会隐式的把运算结果转换为a的类型`。而a = a+b不会把a+b运算结果的类型隐式转换为a的类型。



## 使用过可变长参数吗？

从 Java5 开始，Java 支持定义可变长参数，所谓可变长参数就是允许在调用方法时传入不定长度的参数。就比如下面的这个 `printVariable` 方法就可以接受 0 个或者多个参数。

```java
public static void method1(String... args) {
   //......
}
```

另外，可变参数只能作为函数的**最后一个参数**，但其前面可以有也可以没有任何其他参数。

```java
public static void method2(String arg1, String... args) {
   //......
}
```

**遇到方法重载的情况怎么办呢？会优先匹配固定参数还是可变参数的方法呢？**

答案是会**优先匹配固定参数**的方法，因为固定参数的方法匹配度更高。

我们通过下面这个例子来证明一下。

```java
/**
 *
 **/
public class VariableLengthArgument {
    public static void printVariable(String... args) {
        for (String s : args) {
            System.out.println(s);
        }
    }
    public static void printVariable(String arg1, String arg2) {
        System.out.println(arg1 + arg2);
    }
    public static void main(String[] args) {
        printVariable("a", "b");
        printVariable("a", "b", "c", "d");
    }
}
```

```java
ab
a
b
c
d
```

另外，Java 的可变参数**编译后实际会被转换成一个数组**，我们看编译后生成的 `class`文件就可以看出来了。

```java
public class VariableLengthArgument {
    public static void printVariable(String... args) {
        String[] var1 = args;
        int var2 = args.length;
        for(int var3 = 0; var3 < var2; ++var3) {
            String s = var1[var3];
            System.out.println(s);
        }
    }
    // ......
}
```



## 重载和重写的区别

### **重载**

发生在同一个类中（或者父类和子类之间），方法名必须相同，参数类型不同、个数不同、顺序不同，方法返回值和访问修饰符可以不同。


```java
StringBuilder sb = new StringBuilder();
StringBuilder sb2 = new StringBuilder("HelloWorld");
```

编译器必须挑选出具体执行哪个方法，它通过用各个方法给出的参数类型与特定方法调用所使用的值类型进行匹配来挑选出相应的方法。 如果编译器找不到匹配的参数， 就会产生编译时错误， 因为根本不存在匹配， 或者没有一个比其他的更好(这个过程被称为重载解析(overloading resolution))。**Java 允许重载任何方法， 而不只是构造器方法**。

综上：**重载就是同一个类中多个同名方法根据不同的传参来执行不同的逻辑处理。**

### **重写**

重写发生在运行期，是子类对父类的允许访问的方法的实现过程进行重新编写。

**方法名、参数列表必须相同，子类方法返回值类型应比父类方法返回值类型更小或相等，抛出的异常范围小于等于父类，访问修饰符范围大于等于父类。**

如果父类方法访问修饰符为 **`private/final/static`** 则子类就**不能重写该方法**，但是被 `static` 修饰的方法能够被再次声明。

**构造方法无法被重写**

综上：**重写就是子类对父类方法的重新改造，外部样子不能改变，内部逻辑可以改变**。

> 重载就是同样的一个方法能够根据输入数据的不同，做出不同的处理。
>
> 重写就是当子类继承自父类的相同方法，输入数据一样，但要做出有别于父类的响应时，你就要覆盖父类方法

![image-20220906114511133](https://static.weishao996.top/article/20230909000551.png)

**方法的重写要遵循“两同两小一大”**（以下内容摘录自《疯狂 Java 讲义》：

- “两同”即方法名相同、形参列表相同；
- “两小”指的是子类方法返回值类型应比父类方法返回值类型更小或相等，子类方法声明抛出的异常类应比父类方法声明抛出的异常类更小或相等；
- “一大”指的是子类方法的访问权限应比父类方法的访问权限更大或相等。

⭐️ 关于 **重写的返回值类型** 这里需要额外多说明一下，上面的表述不太清晰准确：**如果方法的返回类型是 void 和基本数据类型，则返回值重写时不可修改。但是如果方法的返回值是引用类型，重写时是可以返回该引用类型的子类的**。

```java
public class Hero {
    public String name() {
        return "超级英雄";
    }
}
public class SuperMan extends Hero{
    @Override
    public String name() {
        return "超人";
    }
    public Hero hero() {
        return new Hero();
    }
}
public class SuperSuperMan extends SuperMan {
    public String name() {
        return "超级超级英雄";
    }
    @Override
    public SuperMan hero() {
        return new SuperMan();
    }
}
```

## == 和 equals()

### == 

对于基本类型和引用类型的作用效果是不同的：

- 对于**基本数据类型**来说，`==` 比较的是**值**。
- 对于**引用数据类型**来说，`==` 比较的是对象的**内存地址**。

因为 **Java 只有值传递**，所以，对于 == 来说，不管是比较基本数据类型，还是引用数据类型的变量，其本质比较的都是值，只是引用类型变量存的值是对象的地址。两边的操作数必须是**同一类型**的（可以是 **父子类之间**）才能编译通过。

### equals()

 不能用于判断基本数据类型的变量，**只能用来判断两个对象是否相等**。`equals()`方法存在于`Object`类中，而`Object`类是所有类的直接或间接父类。

`Object` 类 `equals()` 方法：

```java
public boolean equals(Object obj) {
     return (this == obj);
}
```

`equals()` 方法存在两种使用情况：

- **类没有覆盖 `equals()`方法** ：通过`equals()`比较该类的两个对象时，**等价于通过“==”比较**这两个对象，使用的默认是 `Object`类`equals()`方法。
- **类覆盖了 `equals()`方法** ：一般我们都覆盖 `equals()`方法来**比较两个对象中的属性是否相等**；若它们的属性相等，则返回 true(即，认为这两个对象相等)。

举个例子（这里只是为了举例。实际上，你按照下面这种写法的话，像 IDEA 这种比较智能的 IDE 都会提示你将 `==` 换成 `equals()` ）：

```java
String a = new String("ab"); // a 为一个引用
String b = new String("ab"); // b为另一个引用,对象的内容一样
String aa = "ab"; // 放在常量池中
String bb = "ab"; // 从常量池中查找
System.out.println(aa == bb);// true
System.out.println(a == b);// false
System.out.println(a.equals(b));// true
System.out.println(42 == 42.0);// true
```

`String` 中的 `equals` 方法是被重写过的，因为 `Object` 的 `equals` 方法是比较的对象的内存地址，而 `String` 的 `equals` 方法比较的是对象的值。

当创建 `String` 类型的对象时，虚拟机会在常量池中查找有没有已经存在的值和要创建的值相同的对象，如果有就把它赋给当前引用。如果没有就在常量池中重新创建一个 `String` 对象。

`String`类`equals()`方法：

```java
public boolean equals(Object anObject) {
    if (this == anObject) {
        return true;
    }
    if (anObject instanceof String) {
        String anotherString = (String)anObject;
        int n = value.length;
        if (n == anotherString.value.length) {
            char v1[] = value;
            char v2[] = anotherString.value;
            int i = 0;
            while (n-- != 0) {
                if (v1[i] != v2[i])
                    return false;
                i++;
            }
            return true;
        }
    }
    return false;
}
```

## hashCode() 与 equals()

### **hashCode() 有什么用？**

`hashCode()` 的作用是**获取哈希码**（`int` 整数），也称为**散列码**。这个哈希码的作用是确定该对象在哈希表中的**索引位置**。

`hashCode()`定义在 JDK 的 `Object` 类中，这就意味着 Java 中的任何类都包含有 `hashCode()` 函数。另外需要注意的是： `Object` 的 `hashCode()` 方法是**本地方法**，也就是用 C 语言或 C++ 实现的，**该方法通常用来将对象的内存地址转换为整数**之后返回。

```java
public native int hashCode();
```

散列表存储的是键值对(key-value)，它的特点是：**能根据“键”快速的检索出对应的“值”。这其中就利用到了散列码！（可以快速找到所需要的对象）**

### **为什么要有 hashCode？**

当你把对象加入 `HashSet` 时，`HashSet` 会先计算对象的 `hashCode` 值来判断对象加入的位置，同时也会与其他已经加入的对象的 `hashCode` 值作比较，如果没有相符的 `hashCode`，`HashSet` 会假设对象没有重复出现。但是如果发现有相同 `hashCode` 值的对象，这时会调用 **equals**() 方法来检查 `hashCode` 相等的对象是否真的相同。如果两者相同，`HashSet` 就不会让其加入操作成功。如果不同的话，就会重新散列到其他位置。。这样我们就大大减少了 `equals` 的次数，相应就大大提高了执行速度。

其实， `hashCode()` 和 `equals()`都是用于比较两个对象是否相等。 

### **那为什么 JDK 还要同时提供这两个方法呢？**

是因为在一些容器（比如 `HashMap`、`HashSet`）中，有了 `hashCode()` 之后，判断元素是否在对应容器中的效率会更高（参考添加元素进`HastSet`的过程）！

我们在前面也提到了添加元素进`HastSet`的过程，如果 `HashSet` 在对比的时候，同样的 `hashCode` 有多个对象，它会继续使用 `equals()` 来判断是否真的相同。也就是说 **`hashCode`** **帮助我们大大缩小了查找成本**。

### **那为什么不只提供 `hashCode()` 方法呢？**

这是因为两个对象的**`hashCode` **值相等并不代表两个对象就相等。

### **那为什么两个对象有相同的 `hashCode` 值，它们也不一定是相等的？**

因为 `hashCode()` 所使用的哈希算法也许刚好会让多个对象传回相同的哈希值。越糟糕的哈希算法越容易碰撞，但这也与数据值域分布的特性有关（所谓哈希碰撞也就是指的是不同的对象得到相同的 `hashCode` )。

总结下来就是 ：

- 如果两个对象的`hashCode` 值相等，那这两个对象不一定相等（哈希碰撞）。
- 如果两个对象的`hashCode` 值相等并且`equals()`方法返回 `true`，我们才认为这两个对象相等。
- 如果两个对象的`hashCode` 值不相等，我们就可以直接认为这两个对象不相等。

### 为什么重写 equals() 时必须重写 hashCode() 方法？

因为两个相等的对象的 `hashCode` 值必须是相等。也就是说如果 `equals` 方法判断两个对象是相等的，那这两个对象的 `hashCode` 值也要相等。

如果重写 `equals()` 时没有重写 `hashCode()` 方法的话就可能**会导致** **`equals`** **方法判断是相等的两个对象，`hashCode`** 值却不相等。例子：**可能会造成再HashSet中存在两个相等的元素，但是他们的哈希值不同**。

**思考** ：重写 `equals()` 时没有重写 `hashCode()` 方法的话，使用 `HashMap` 可能会出现什么问题。

**总结** ：

- `equals` 方法判断两个对象是相等的，那这两个对象的 `hashCode` 值也要相等。
- 两个对象有相同的 `hashCode` 值，他们也不一定是相等的（哈希碰撞）。

**拓展**

**Hashcode冲突：**

产生hash冲突时,两个不相等的对象就会有相同的 hashcode 值.当hash冲突产生时,一般 有以下几种方式来处理:

- **拉链法**:每个哈希表节点都有一个next指针,多个哈希表节点可以用next指针构成一个单向链 表，被分配到同一个索引上的多个节点可以用这个单向链表进行存储. 
- **开放定址法**:一旦发生了冲突,就去寻找下一个空的散列地址,只要散列表足够大,空的散列地址总 能找到,并将记录存入
- **再哈希**:又叫双哈希法,有多个不同的Hash函数.当发生冲突时,使用第二个,第三个….等哈希函数 计算地址,直到无冲突.

## 成员变量和局部变量的区别

Java中的变量分为成员变量和局部变量，它们的区别如下：

**成员变量：**

1. 成员变量是在类的范围里定义的变量；
2. 成员变量**有默认初始值**；
3. 未被static修饰的成员变量也叫实例变量，它存储于对象所在的堆内存中，生命周期与对象相同；
4. 被static修饰的成员变量也叫类变量，它存储于方法区中，生命周期与当前类相同。

**局部变量：**

1. 局部变量是在方法里定义的变量；
2. 局部变量没有默认初始值；
3. 局部变量存储于栈内存中，作用的范围结束，变量空间会自动的释放。

**注意事项**Java中没有真正的全局变量，面试官应该是出于其他语言的习惯说全局变量的，他的本意应该是指成员变量。

## 静态方法为什么不能调用非静态成员?

这个需要结合 JVM 的相关知识，主要原因如下：

1. **静态方法**是属于类的，在**类加载**的时候就会分配内存，可以通过类名直接访问。而**非静态成员**属于实例对象，只有在对象实例化之后才存在，需要通过类的**实例对象去访问**。
2. 在类的非静态成员不存在的时候静态成员就已经存在了，此时调用在内存中还不存在的非静态成员，属于非法操作。

### 静态方法和实例方法有何不同？

**1、调用方式**

在外部调用静态方法时，可以使用 `类名.方法名` 的方式，也可以使用 `对象.方法名` 的方式，而实例方法只有后面这种方式。也就是说，**调用静态方法可以无需创建对象** 。

不过，需要注意的是一般不建议使用 `对象.方法名` 的方式来调用静态方法。这种方式非常容易造成混淆，静态方法不属于类的某个对象而是属于这个类。

因此，一般建议使用 `类名.方法名` 的方式来调用静态方法。

```java
public class Person {
    public void method() {
      //......
    }
    public static void staicMethod(){
      //......
    }
    public static void main(String[] args) {
        Person person = new Person();
        // 调用实例方法
        person.method();
        // 调用静态方法
        Person.staicMethod()
    }
}
```

**2、访问类成员是否存在限制**

**静态方法**在访问本类的成员时，**只允许访问静态成员（即静态成员变量和静态方法）**，不允许访问实例成员（即实例成员变量和实例方法），而实例方法不存在这个限制。

## 什么是方法的返回值?方法有哪几种类型？

#### 什么是方法的返回值?方法有哪几种类型？

**方法的返回值** 是指我们获取到的某个方法体中的代码执行后产生的结果！（前提是该方法可能产生结果）。返回值的作用是接收出结果，使得它可以用于其他的操作！

我们可以按照方法的返回值和参数类型将方法分为下面这几种：

- **1.无参数无返回值的方法**
- **2.有参数无返回值的方法**
- **3.有返回值无参数的方法**
- **4.有返回值有参数的方法**

## continue、break 和 return 的区别是什么？

在循环结构中，当循环条件不满足或者循环次数达到要求时，循环会正常结束。但是，有时候可能需要在循环的过程中，当发生了某种条件之后 ，提前终止循环，这就需要用到下面几个关键词：

1. **continue** ：指跳出当前的这一次循环，继续下一次循环。
2. **break** ：指跳出整个循环体，继续执行循环下面的语句。

`return` 用于跳出所在方法，结束该方法的运行。return 一般有两种用法：

1. **return**; ：直接使用 return 结束方法执行，用于没有返回值函数的方法
2. **return value**; ：return 一个特定值，用于有返回值函数的方法

```java
public static void main(String[] args) {
        boolean flag = false;
        for (int i = 0; i <= 3; i++) {
            if (i == 0) {
                System.out.println("0");
            } else if (i == 1) {
                System.out.println("1");
                continue;
            } else if (i == 2) {
                System.out.println("2");
                flag = true;
            } else if (i == 3) {
                System.out.println("3");
                break;
            } else if (i == 4) {
                System.out.println("4");
            }
            System.out.println("xixi");
        }
        if (flag) {
            System.out.println("haha");
            return;
        }
        System.out.println("heihei");
    }

```

运行结果：

```java
0
xixi
1
2
xixi
3
haha
```

## 自增自减运算符

在写代码的过程中，常见的一种情况是需要某个整数类型变量增加 1 或减少 1，Java 提供了一种特殊的运算符，用于这种表达式，叫做自增运算符（++)和自减运算符（--）。

++ 和 -- 运算符可以放在变量之前，也可以放在变量之后，当运算符放在变量之前时(前缀)，先自增/减，再赋值；当运算符放在变量之后时(后缀)，先赋值，再自增/减。例如，当 `b = ++a` 时，先自增（自己增加 1），再赋值（赋值给 b）；当 `b = a++` 时，先赋值(赋值给 b)，再自增（自己增加 1）。也就是，++a 输出的是 a+1 的值，a++输出的是 a 值。用一句口诀就是：“**符号在前就先加/减，符号在后就后加/减**”。

## 注释有哪几种？注释越多越好吗？

Java 中的注释有三种：

1. **单行注释**
2. **多行注释**
3. **文档注释**。

在我们编写代码的时候，如果代码量比较少，我们自己或者团队其他成员还可以很轻易地看懂代码，但是当项目结构一旦复杂起来，我们就需要用到注释了。注释并不会执行(编译器在编译代码之前会把代码中的所有注释抹掉,字节码中不保留注释)，是我们程序员写给自己看的，注释是你的代码说明书，能够帮助看代码的人快速地理清代码之间的逻辑关系。因此，在写程序的时候随手加上注释是一个非常好的习惯。

## 字符型常量和字符串常量的区别?

- **形式** : 字符常量是单引号引起的一个字符，字符串常量是双引号引起的 0 个或若干个字符
- **含义** : 字符常量相当于一个整型值( ASCII 值),可以参加表达式运算; 字符串常量代表一个地址值(该字符串在内存中存放位置)
- **占内存大小** ： 字符常量只占 2 个字节; 字符串常量占若干个字节 (**注意： `char` 在 Java 中占两个字节)**

## instanceof 关键字

instanceof 严格来说是Java中的一个**双目运算符**，用来**测试一个对象是否为一个类的实例**，用法为：

```java
boolean result = obj instanceof Class
```

其中 obj 为一个对象，Class 表示一个类或者一个接口，**当 obj 为 Class 的对象，或者是其直接 或间接子类，或者是其接口的实现类，结果result 都返回 true，否则返回false**。 注意：编译器会检查 obj 是否能转换成右边的class类型，如果不能转换则直接报错，如果不能 确定类型，则通过编译，具体看运行时定。

```java
int i = 0;
System.out.println(i instanceof Integer);//编译不通过 i必须是引用类型，不能是基本类型
System.out.println(i instanceof Object);//编译不通过
```

```java
Integer integer = new Integer(1);
System.out.println(integer instanceof Integer);//true
```

```java
//false ,在 JavaSE规范 中对 instanceof 运算符的规定就是：如果 obj 为 null，那么将返
//回 false。
System.out.println(null instanceof Object);
```

# **基本数据类型**

## Java 中的几种基本数据类型了解么？

**Java 中有 8 种基本数据类型**，分别为：

1. 6 种数字类型：
   - 4 种整数型：**byte、short、int、long**
   - 2 种浮点型：**float、double**
2. 1 种字符类型：**char**
3. 1 种布尔型：**boolean**。

这 8 种基本数据类型的默认值以及所占空间的大小如下：

![image-20220906180157973](https://static.weishao996.top/article/20230909000605.png)

虽然定义了boolean这种数据类型，但是只对它提供了非常有限的支持。在Java虚拟机中没有 任何供boolean值专用的字节码指令，Java语言表达式所操作的boolean值，在编译之后都使用Java 虚拟机中的**int**数据类型来代替，而boolean数组将会被编码成Java虚拟机的byte数组，每个元素 boolean元素占8位。这样我们可以得出boolean类型占了单独使用是4个字节，在数组中又是1个字 节。使用int的原因是，对于当下32位的处理器（CPU）来说，一次处理数据是32位（这里不是指的 是32/64位系统，而是指CPU硬件层面），具有**高效存取**的特点。

另外，Java 的每种基本类型所占存储空间的大小不会像其他大多数语言那样随机器硬件架构的变化而变化。这种所占存储空间大小的不变性是 Java 程序比用其他大多数语言编写的程序更具可移植性的原因之一（《Java 编程思想》2.2 节有提到）。

**注意：**

1. Java 里使用 `long` 类型的数据一定要在数值后面加上 **L**，否则将作为整型解析。
2. `char a = 'h'`char :单引号，`String a = "hello"` :双引号。

这八种基本类型都有对应的包装类分别为：**`Byte`、`Short`、`Integer`、`Long`、`Float`、`Double`、`Character`、`Boolean` 。**

**包装类型不赋值就是** **`Null`** **，而基本类型有默认值且不是** **`Null`**。

另外，这个问题建议还可以先从 JVM 层面来分析。

**基本数据类型**直接存放在 Java 虚拟机栈中的**局部变量表**中，而**包装类型**属于对象类型，我们知道对象实例都存在于**堆**中。相比于对象类型， 基本数据类型占用的空间非常小。

引用类型就是对一个对象的引用，根据引用对象类型的不同，可以将引用类型分为3类，即数组、类、接口类型。引用类型本质上就是通过指针，指向堆中对象所持有的内存空间，只是Java语言不再沿用指针这个说法而已。

## int和Integer有什么区别，二者在做==运算时会得到什么结果

int是基本数据类型，Integer是int的包装类。二者在做==运算时，Integer会**自动拆箱**为int类型，然后再进行比较。届时，如果两个int值相等则返回true，否则就返回false。

## 如何对Integer和Double类型判断相等？

Integer、Double不能直接进行比较，这包括：

- 不能用==进行直接比较，因为它们是不同的数据类型；
- 不能转为字符串进行比较，因为转为字符串后，浮点值带小数点，整数值不带，这样它们永远都不相等；
- 不能使用compareTo方法进行比较，虽然它们都有compareTo方法，但该方法只能对相同类型进行比较。

整数、浮点类型的包装类，都继承于Number类型，而Number类型分别定义了将数字转换为byte、short、int、long、float、double的方法。所以，可以**将Integer、Double先转为转换为相同的基本数据类（如double）**，然后使用==进行比较。 

**示例代码**

```
Integer i = 100;
Double d = 100.00;
System.out.println(i.doubleValue() == d.doubleValue());
```

## 为啥要有包装类？

**参考答案**

Java语言是面向对象的语言，其设计理念是“**一切皆对象**”。但8种基本数据类型却出现了例外，它们不具备对象的特性。正是为了解决这个问题，Java为每个基本数据类型都定义了一个对应的引用类型，这就是包装类。

**扩展阅读**

Java之所以提供8种基本数据类型，主要是为了照顾程序员的传统习惯。这8种基本数据类型的确带来了一定的方便性，但在某些时候也会受到一些制约。比如，所有的引用类型的变量都继承于Object类，都可以当做Object类型的变量使用，但基本数据类型却不可以。如果某个方法需要Object类型的参数，但实际传入的值却是数字的话，就需要做特殊的处理了。有了包装类，这种问题就可以得以简化。

## 自动装箱与拆箱

**什么是自动拆装箱？**

- **装箱**：将基本类型用它们对应的引用类型包装起来；
- **拆箱**：将包装类型转换为基本数据类型；

```java
Integer i = 10;  //装箱
int n = i;   //拆箱
```

```java
   L1
    LINENUMBER 8 L1
    ALOAD 0
    BIPUSH 10
    INVOKESTATIC java/lang/Integer.valueOf (I)Ljava/lang/Integer;
    PUTFIELD AutoBoxTest.i : Ljava/lang/Integer;
   L2
    LINENUMBER 9 L2
    ALOAD 0
    ALOAD 0
    GETFIELD AutoBoxTest.i : Ljava/lang/Integer;
    INVOKEVIRTUAL java/lang/Integer.intValue ()I
    PUTFIELD AutoBoxTest.n : I
    RETURN
```

从字节码中，我们发现装箱其实就是调用了 包装类的`valueOf()`方法，拆箱其实就是调用了 **`xxxValue()`**方法。

因此，

- `Integer i = 10` 等价于 `Integer i = Integer.valueOf(10)`
- `int n = i` 等价于 `int n = i.intValue()`;

注意：**如果频繁拆装箱的话，也会严重影响系统的性能。我们应该尽量避免不必要的拆装箱操作。**

```java
private static long sum() {
    // 应该使用 long 而不是 Long
    Long sum = 0L;
    for (long i = 0; i <= Integer.MAX_VALUE; i++)
        sum += i;
    return sum;
}
```

在Java SE5之前，如果要生成一个数值为10的Integer对象，必须这样进行：

```java
Integer i = new Integer(10);
```

而在从Java SE5开始就提供了自动装箱的特性，如果要生成一个数值为10的Integer对象，只需要 这样就可以了：

```java
Integer i = 10;
```

试题1： 以下代码会输出什么？

```java
public class Main {
 public static void main(String[] args) {
 
 Integer i1 = 100;
 Integer i2 = 100;
 Integer i3 = 200;
 Integer i4 = 200;
 
 System.out.println(i1==i2);
 System.out.println(i3==i4);
 }
}
```

运行结果：

```java
true
false
```

为什么会出现这样的结果？输出结果表明i1和i2指向的是同一个对象，而i3和i4指向的是不同的对 象。此时只需一看源码便知究竟，下面这段代码是Integer的valueOf方法的具体实现：

```java
public static Integer valueOf(int i) {
 if(i >= -128 && i <= IntegerCache.high)
 return IntegerCache.cache[i + 128];
 else
 return new Integer(i);
 }
```

其中**IntegerCache类**的实现为：

```java
private static class IntegerCache {
 static final int high;
 static final Integer cache[];
 static {
 final int low = -128;
 // high value may be configured by property
 int h = 127;
 if (integerCacheHighPropValue != null) {
 // Use Long.decode here to avoid invoking methods that
 // require Integer's autoboxing cache to be initialized
 int i = Long.decode(integerCacheHighPropValue).intValue();
 i = Math.max(i, 127);
 // Maximum array size is Integer.MAX_VALUE
 h = Math.min(i, Integer.MAX_VALUE - -low);
 }
 high = h;
 cache = new Integer[(high - low) + 1];
 int j = low;
 for(int k = 0; k < cache.length; k++)
 cache[k] = new Integer(j++);
 }
 private IntegerCache() {}
 }
```

从这2段代码可以看出，在通过**valueOf方法**创建Integer对象的时候，如果数值在**[-128,127]**之间， 便返回指向**IntegerCache.cache**中已经存在的对象的引用；否则创建一个新的Integer对象。 上面的代码中i1和i2的数值为100，因此会直接从cache中取已经存在的对象，所以i1和i2指向的是 同一个对象，而i3和i4则是分别指向不同的对象。

**面试题2：以下代码输出什么**

```java
public class Main {
 public static void main(String[] args) {
 
 Double i1 = 100.0;
 Double i2 = 100.0;
 Double i3 = 200.0;
 Double i4 = 200.0;
 
 System.out.println(i1==i2);
 System.out.println(i3==i4);
 }
}
```

运行结果：

```java
false
false
```

原因： 在某个范围内的整型数值的个数是有限的，而浮点数却不是。

## 包装类型的常量池技术了解么？

Java 基本类型的包装类的大部分都实现了**常量池技术**。

**Byte,Short,Integer,Long** 这 4 种包装类默认创建了数值 **[-128，127]** 的相应类型的**缓存数据**，**Character** 创建了数值在 **[0,127]** 范围的缓存数据，**Boolean** 直接返回 **True or False**。

**Integer 缓存源码：**

```java
public static Integer valueOf(int i) {
    if (i >= IntegerCache.low && i <= IntegerCache.high)
        return IntegerCache.cache[i + (-IntegerCache.low)];
    return new Integer(i);
}
private static class IntegerCache {
    static final int low = -128;
    static final int high;
    static {
        // high value may be configured by property
        int h = 127;
    }
}
```

**`Character` 缓存源码:**

```java
public static Character valueOf(char c) {
    if (c <= 127) { // must cache
      return CharacterCache.cache[(int)c];
    }
    return new Character(c);
}
private static class CharacterCache {
    private CharacterCache(){}
    static final Character cache[] = new Character[127 + 1];
    static {
        for (int i = 0; i < cache.length; i++)
            cache[i] = new Character((char)i);
    }
}
```

**`Boolean` 缓存源码：**

```java
public static Boolean valueOf(boolean b) {
    return (b ? TRUE : FALSE);
}
```

如果超出对应范围仍然会去创建新的对象，缓存的范围区间的大小只是在性能和资源之间的权衡。

两种浮点数类型的包装类 **Float,Double**并没有实现常量池技术。

```java
Integer i1 = 33;
Integer i2 = 33;
System.out.println(i1 == i2);// 输出 true
Float i11 = 333f;
Float i22 = 333f;
System.out.println(i11 == i22);// 输出 false
Double i3 = 1.2;
Double i4 = 1.2;
System.out.println(i3 == i4);// 输出 false
```

下面我们来看一下问题。下面的代码的输出结果是 `true` 还是 `flase` 呢？

```java
Integer i1 = 40;
Integer i2 = new Integer(40);
System.out.println(i1==i2);
```

`Integer i1=40` 这一行代码会发生装箱，也就是说这行代码等价于 `Integer i1=Integer.valueOf(40)` 。因此，`i1` 直接使用的是常量池中的对象。而**`Integer i2 = new Integer(40)`** **会直接创建新的对象**。 因此，答案是 `false` 。

记住：**所有整型包装类对象之间值的比较，全部使用 equals 方法比较**。

![image-20220906174815320](https://static.weishao996.top/article/20230909000615.png)

缓存池

**new Integer(123) 与 Integer.valueOf(123)** 的区别在于:

- new Integer(123) 每次都会新建一个对象
- Integer.valueOf(123) 会使用缓存池中的对象，多次调用会取得同一个对象的引用。

```java
Integer x = new Integer(123);
Integer y = new Integer(123);
System.out.println(x == y);    // false
Integer z = Integer.valueOf(123);
Integer k = Integer.valueOf(123);
System.out.println(z == k);   // true
```

valueOf() 方法的实现比较简单，就是先判断值是否在缓存池中，如果在的话就直接返回缓存池的内容。

```java
public static Integer valueOf(int i) {
    if (i >= IntegerCache.low && i <= IntegerCache.high)
        return IntegerCache.cache[i + (-IntegerCache.low)];
    return new Integer(i);
}
```

编译器会**在缓冲池范围内的基本类型**自动装箱过程调用 valueOf() 方法，因此多个 Integer 实例使用自动装箱来创建并且值相同，那么就会引用相同的对象。

```java
Integer m = 123;
Integer n = 123;
System.out.println(m == n); // true
```

基本类型对应的缓冲池如下:

- boolean values true and false
- all byte values
- short values between -128 and 127
- int values between -128 and 127
- char in the range \u0000 to \u007F

在使用这些基本类型对应的包装类型时，就可以直接使用缓冲池中的对象。

如果在缓冲池之外：

```java
Integer m = 323;
Integer n = 323;
System.out.println(m == n); // false
```

# **面向对象基础**

## 面向对象和面向过程

**面向过程**：是**分析解决问题的步骤**，然后用函数把这些步骤一步一步地实现，然后在使用的时候一 一调用则可。性能较高，所以单片机、嵌入式开发等一般采用面向过程开发

**面向对象**：**是把构成问题的事务分解成各个对象**，而建立对象的目的也不是为了完成一个个步骤， 而是为了描述某个事物在解决整个问题的过程中所发生的行为。面向对象有封装、继承、多态的特 性，所以易维护、易复用、易扩展。可以设计出低耦合的系统。 但是性能上来说，比面向过程要低。

## 面向对象三大特征

### **封装**

**封装是指把一个对象的状态信息（也就是属性）隐藏在对象内部，不允许外部对象直接访问对象的内部信息。但是可以提供一些可以被外界访问的方法来操作属性**。就好像我们看不到挂在墙上的空调的内部的零件信息（也就是属性），但是可以通过遥控器（方法）来控制空调。如果属性不想被外界访问，我们大可不必提供方法给外界访问。但是如果一个类没有提供给外界访问的方法，那么这个类也没有什么意义了。就好像如果没有空调遥控器，那么我们就无法操控空凋制冷，空调本身就没有意义了（当然现在还有很多其他方法 ，这里只是为了举例子）。

 **封装的目的**

封装是面向对象编程语言对客观世界的模拟，在客观世界里，对象的状态信息都被隐藏在对象内部，外界无法直接操作和修改。对一个类或对象实现良好的封装，可以实现以下目的：

- **隐藏类的实现细节；**
- **让使用者只能通过事先预定的方法来访问数据，从而可以在该方法里加入控制逻辑，限制对成员变量的不合理访问；**

- **可进行数据检查，从而有利于保证对象信息的完整性；**
- **便于修改，提高代码的可维护性。**

 为了实现良好的封装，需要从两个方面考虑：

- **将对象的成员变量和实现细节隐藏起来，不允许外部直接访问；**
- **把方法暴露出来，让方法来控制对这些成员变量进行安全的访问和操作。**

封装实际上有两个方面的含义：把该隐藏的隐藏起来，把该暴露的暴露出来。这两个方面都需要通过使用Java提供的访问控制符来实现。

### **继承**

不同类型的对象，相互之间经常有一定数量的共同点。例如，小明同学、小红同学、小李同学，都共享学生的特性（班级、学号等）。同时，每一个对象还定义了额外的特性使得他们与众不同。例如小明的数学比较好，小红的性格惹人喜爱；小李的力气比较大。**继承是使用已存在的类的定义作为基础建立新类的技术，新类的定义可以增加新的数据或新的功能，也可以用父类的功能，但不能选择性地继承父类**。通过使用继承，可以快速地创建新的类，可以提高代码的重用，程序的可维护性，节省大量创建新类的时间 ，提高我们的开发效率。

**关于继承如下 3 点请记住：**

1. 子类拥有父类对象所有的属性和方法（包括私有属性和私有方法），但是父类中的私有属性和方法子类是无法访问，**只是拥有**。
2. 子类可以拥有自己属性和方法，即子类可以对父类进行扩展。
3. 子类可以用自己的方式实现父类的方法。

### **多态**

多态，顾名思义，表示一个对象具有多种的状态，具体表现为**父类的引用指向子类的实例。**

**多态的特点:**

- 对象类型和引用类型之间具有继承（类）/实现（接口）的关系；
- 引用类型变量发出的方法调用的到底是哪个类中的方法，必须在程序运行期间才能确定；
- 多态不能调用“只在子类存在但在父类不存在”的方法；
- 如果子类重写了父类的方法，真正执行的是子类覆盖的方法，如果子类没有覆盖父类的方法，执行的是父类的方法。

Java中的多态是怎么实现的

多态的实现离不开继承，在设计程序时，我们可以将参数的类型定义为父类型。在调用程序时，则可以根据实际情况，传入该父类型的某个子类型的实例，这样就实现了多态。对于父类型，可以有三种形式，即**普通的类、抽象类、接口**。对于子类型，则要根据它自身的特征，重写父类的某些方法，或实现抽象类/接口的某些抽象方法。

抽象也是面向对象的重要部分，抽象就是忽略一个主题中与当前目标无关的那些方面，以便更充分地注意与当前目标有关的方面。抽象并不打算了解全部问题，而只是考虑部分问题。例如，需要考察Person对象时，不可能在程序中把Person的所有细节都定义出来，通常只能定义Person的部分数据、部分行为特征，而这些数据、行为特征是软件系统所关心的部分。

## final用法

final也是很多面试喜欢问的地方,但我觉得这个问题很无聊,通常能回答下以下5点就不错了: 

- **被final修饰的类不可以被继承** 

- **被final修饰的方法不可以被重写** 

- **被final修饰的变量不可以被改变.如果修饰引用,那么表示引用不可变,引用指向的内容可变.** 

- **被final修饰的方法,JVM会尝试将其内联,以提高运行效率** 

- **被final修饰的常量,在编译阶段会存入常量池中.** 

对final域的读和写更像是普通的变量访问，编译器和处理器要遵守两个重排序规则：

- 在构造函数内对一个final域的写入，与随后把这个被构造对象的引用赋值给一个引用变量，这两个操作之间不能重排序。
- 初次读一个包含final域的对象的引用，与随后初次读这个final域，这两个操作之间不能重排序。

下面，我们通过一些示例性的代码来分别说明这两个规则：

```java
public class FinalExample {
    int i;                            //普通变量
    final int j;                      //final变量
    static FinalExample obj;

    public void FinalExample () {     //构造函数
        i = 1;                        //写普通域
        j = 2;                        //写final域
    }
    public static void writer () {    //写线程A执行
        obj = new FinalExample ();
    }
    public static void reader () {       //读线程B执行
        FinalExample object = obj;       //读对象引用
        int a = object.i;                //读普通域
        int b = object.j;                //读final域
    }
}
```

这里假设一个线程A执行writer ()方法，随后另一个线程B执行reader ()方法，注意两者的调用先后关系！

下面我们通过这两个线程的交互来说明这两个规则。

### **写final域的重排序规则**

写final域的重排序规则禁止把final域的写重排序到构造函数之外。这个规则的实现包含下面2个方面：

- JMM禁止编译器把final域的写重排序到构造函数之外。
- 编译器会在final域的写之后，构造函数return之前，插入一个StoreStore屏障。这个屏障禁止处理器把final域的写重排序到构造函数之外。

现在让我们分析writer ()方法。writer ()方法只包含一行代码：finalExample = new FinalExample ()。这行代码包含两个步骤：

- 构造一个FinalExample类型的对象；
- 把这个对象的引用赋值给引用变量obj。

假设线程B读对象引用与读对象的成员域之间没有重排序（马上会说明为什么需要这个假设），下图是一种可能的执行时序：

![img](https://static.weishao996.top/article/20230909000625.jpg)

在上图中，写普通域的操作被编译器重排序到了构造函数之外，读线程B错误的读取了普通变量i初始化之前的值。而写final域的操作，被写final域的重排序规则“限定”在了构造函数之内，读线程B正确的读取了final变量初始化之后的值。

写final域的重排序规则可以确保：在对象引用为任意线程可见之前，对象的final域已经被正确初始化过了，而普通域不具有这个保障。以上图为例，在读线程B“看到”对象引用obj时，很可能obj对象还没有构造完成（对普通域i的写操作被重排序到构造函数外，此时初始值2还没有写入普通域i）。

总结一下：也就是对象初始化final变量和普通变量，然后将初始化的对象引用赋值给其它变量前，final变量可以保证已经被初始化，但是普通变量不能保证，可能会导致读取的普通变量是一个空值，或者说是未初始化的值，导致异常。

### **读final域的重排序规则**

读final域的重排序规则如下：

- 在一个线程中，初次读对象引用与初次读该对象包含的final域，JMM禁止处理器重排序这两个操作（注意，这个规则仅仅针对处理器）。编译器会在读final域操作的前面插入一个LoadLoad屏障。

reader()方法包含三个操作：

1. 初次读引用变量obj;
2. 初次读引用变量obj指向对象的普通域j。
3. 初次读引用变量obj指向对象的final域i。

现在我们假设写线程A没有发生任何重排序，同时程序在不遵守间接依赖的处理器上执行，下面是一种可能的执行时序：

![preview](https://static.weishao996.top/article/20230909000631.jpg)

在上图中，读对象的普通域的操作被处理器重排序到读对象引用之前。读普通域时，该域还没有被写线程A写入，这是一个错误的读取操作。而读final域的重排序规则会把读对象final域的操作“限定”在读对象引用之后，此时该final域已经被A线程初始化过了，这是一个正确的读取操作。

总结一下：**在读一个对象的final变量之前，一定会先读包含这个final域的对象的引用，所以不用担心读到对象的final变量，会因为重排除导致读到的是一个未初始化的值，但是对象的普通变量就不能这样保证**。

对读和写finlal域，整体总结一下：**写final域的重排序规则会要求译编器在final域的写之后，构造函数return之前，插入一个StoreStore障屏。读final域的重排序规则要求编译器在读final域的操作前面插入一个LoadLoad屏障**。

### **如果final域是引用类型**

上面我们看到的final域是基础数据类型，下面让我们看看如果final域是引用类型，将会有什么效果？请看下列示例代码：

```java
public class FinalReferenceExample {
  final int[] intArray;                     //final是引用类型
  static FinalReferenceExample obj;
  public FinalReferenceExample () {        //构造函数
      intArray = new int[1];              //1
      intArray[0] = 1;                   //2
  }
  public static void writerOne () {          //写线程A执行
      obj = new FinalReferenceExample ();  //3
  }
  public static void writerTwo () {          //写线程B执行
      obj.intArray[0] = 2;                 //4
  }
  public static void reader () {              //读线程C执行
      if (obj != null) {                    //5
          int temp1 = obj.intArray[0];       //6
      }
  }
}
```

![preview](https://static.weishao996.top/article/20230909000637.jpg)

在上图中，1是对final域的写入，2是对这个final域引用的对象的成员域的写入，3是把被构造的对象的引用赋值给某个引用变量。这里除了前面提到的1不能和3重排序外，2和3也不能重排序。

JMM可以确保读线程C至少能看到写线程A在构造函数中对final引用对象的成员域的写入。即C至少能看到数组下标0的值为1。而写线程B对数组元素的写入，读线程C可能看的到，也可能看不到。JMM不保证线程B的写入对读线程C可见，因为写线程B和读线程C之间存在数据竞争，此时的执行结果不可预知。

如果想要确保读线程C看到写线程B对数组元素的写入，写线程B和读线程C之间需要使用同步原语（lock或volatile）来确保内存可见性。

> 总结一下：如果final域为引用类型，这个其实和非引用类型禁止重排序的规则基本一样。上面的示例，writerTwo()和reader()同时对一个数据进行操作，存在竞争关系，也很好理解，我换一个非引用类型，也一样存在并发，解决方案就是加锁。

### **为什么final引用不能从构造函数内“逸出”**

前面我们提到过，写final域的重排序规则可以确保：在引用变量为任意线程可见之前，该引用变量指向的对象的final域已经在构造函数中被正确初始化过了。其实要得到这个效果，还需要一个保证：

> 在构造函数内部，不能让这个被构造对象的引用为其他线程可见，也就是对象引用不能在构造函数中“逸出”。

为了说明问题，让我们来看下面示例代码：

```java
public class FinalReferenceEscapeExample {
  final int i;
  static FinalReferenceEscapeExample obj;
  public FinalReferenceEscapeExample () {
      i = 1;                              //1写final域
      obj = this;                          //2 this引用在此“逸出”
  }
  public static void writer() {
      new FinalReferenceEscapeExample ();
  }
  public static void reader {
      if (obj != null) {                     //3
          int temp = obj.i;                 //4
      }
  }
}
```

假设一个线程A执行writer()方法，另一个线程B执行reader()方法。这里的操作2使得对象还未完成构造前就为线程B可见。即使这里的操作2是构造函数的最后一步，且即使在程序中操作2排在操作1后面，执行read()方法的线程仍然可能无法看到final域被初始化后的值，因为这里的操作1和操作2之间可能被重排序。实际的执行时序可能如下图所示：

![img](https://static.weishao996.top/article/20230909000642.jpg)

从上图我们可以看出：在构造函数返回前，被构造对象的引用不能为其他线程可见，因为此时的final域可能还没有被初始化。在构造函数返回后，任意线程都将保证能看到final域正确初始化之后的值。

## static用法

所有的人都知道static关键字这两个基本的用法:**静态变量和静态方法**.也就是被static所修饰的变量/ 方法都属于类的静态资源,**类实例所共享**.

除了静态变量和静态方法之外,static也用于**静态块**,多用于初始化操作:

```java
public calss PreCache{
 static{
 //执行相关操作
 }
}
```

此外static也多用于修饰内部类,此时称之为**静态内部类**.

最后一种用法就是静态导包,即 **import static** .import static是在JDK 1.5之后引入的新特性,可以用 来指定导入某个类中的静态资源,并且不需要使用类名,可以直接使用资源名,比如:

```java
import static java.lang.Math.*;
public class Test{
 public static void main(String[] args){
 //System.out.println(Math.sin(20));传统做法
 System.out.println(sin(20));
 }
}
```

在Java类里只能包含成员变量、方法、构造器、初始化块、内部类（包括接口、枚举）5种成员，而static可以修饰**成员变量、方法、初始化块、内部类**（包括接口、枚举），以static修饰的成员就是类成员。类成员属于整个类，而不属于单个对象。

对static关键字而言，有一条非常重要的规则：**类成员（包括成员变量、方法、初始化块、内部类和内部枚举）不能访问实例成员（包括成员变量、方法、初始化块、内部类和内部枚举）**。因为类成员是属于类的，类成员的作用域比实例成员的作用域更大，完全可能出现类成员已经初始化完成，但实例成员还不曾初始化的情况，如果允许类成员访问实例成员将会引起大量错误。 

**static修饰的类能不能被继承**

**static修饰的类可以被继承。**

如果使用static来修饰一个内部类，则这个内部类就属于外部类本身，而不属于外部类的某个对象。因此使用static修饰的内部类被称为**类内部类**，有的地方也称为**静态内部类**。

static关键字的作用是把类的成员变成类相关，而不是实例相关，即static修饰的成员属于整个类，而不属于单个对象。外部类的上一级程序单元是包，所以不可使用static修饰；而内部类的上一级程序单元是外部类，使用static修饰可以将内部类变成外部类相关，而不是外部类实例相关。因此static关键字不可修饰外部类，但可修饰内部类。

静态内部类需满足如下规则：

1. 静态内部类可以包含静态成员，也可以包含非静态成员；

2. 静态内部类不能访问外部类的实例成员，只能访问它的静态成员；

3. 外部类的所有方法、初始化块都能访问其内部定义的静态内部类；

4. 在外部类的外部，也可以实例化静态内部类，语法如下：

    

   ```java
   外部类.内部类 变量名 = new 外部类.内部类构造方法();
   ```

## Java访问权限

Java语言为我们提供了三种访问修饰符，即private、protected、public，在使用这些修饰符修饰目标时，一共可以形成四种访问权限，即**private、default、protected、public**，注意在不加任何修饰符时为default访问权限。

在**修饰成员变量/成员方法**时，该成员的四种访问权限的含义如下：

- private：该成员可以被该类**内部成员**访问；
- default：该成员可以被该类**内部成员**访问，也可以被**同一包下其他的类**访问；
- protected：该成员可以被该类**内部成员**访问，也可以被**同一包下其他的类**访问，还可以被**它的子类**访问；
- public：该成员可以被**任意包下，任意类的成员**进行访问。

在**修饰类**时，该类只有两种访问权限，对应的访问权限的含义如下：

- default：该类可以被**同一包下其他的类**访问；
- public：该类可以被**任意包下，任意的类**所访问。

## 一个Java文件里可以有多个类

1. 一个java文件里可以有多个类，但最多只能有一个被**public**修饰的类；
2. 如果这个java文件中包含**public**修饰的类，则这个类的名称必须和java文件名一致。

## 深拷贝和浅拷贝

- **浅拷贝**：浅拷贝会在堆上创建一个新的对象（区别于引用拷贝的一点），不过，如果原对象内部的属性是引用类型的话，浅拷贝会直接复制内部对象的引用地址，也就是说拷贝对象和原对象共用同一个内部对象。
- **深拷贝** ：深拷贝会**完全复制整个对象**，包括这个对象所包含的内部对象。

### **浅拷贝**

浅拷贝的示例代码如下，我们这里实现了 `Cloneable` 接口，并重写了 `clone()` 方法。`clone()` 方法的实现很简单，直接调用的是父类 `Object` 的 `clone()` 方法。

```java
public class Address implements Cloneable{
    private String name;
    // 省略构造函数、Getter&Setter方法
    @Override
    public Address clone() {
        try {
            return (Address) super.clone();
        } catch (CloneNotSupportedException e) {
            throw new AssertionError();
        }
    }
}

public class Person implements Cloneable {
    private Address address;
    // 省略构造函数、Getter&Setter方法
    @Override
    public Person clone() {
        try {
            Person person = (Person) super.clone();
            return person;
        } catch (CloneNotSupportedException e) {
            throw new AssertionError();
        }
    }
}

```

测试 ：

```java
Person person1 = new Person(new Address("武汉"));
Person person1Copy = person1.clone();
// true
System.out.println(person1.getAddress() == person1Copy.getAddress());
```

从输出结构就可以看出， `person1` 的克隆对象和 `person1` 使用的仍然是同一个 `Address` 对象。

### **深拷贝**

这里我们简单对 `Person` 类的 `clone()` 方法进行修改，连带着要把 `Person` 对象内部的 `Address` 对象一起复制。

```java
@Override
public Person clone() {
    try {
        Person person = (Person) super.clone();
        person.setAddress(person.getAddress().clone());
        return person;
    } catch (CloneNotSupportedException e) {
        throw new AssertionError();
    }
}
```

测试 ：

```java
Person person1 = new Person(new Address("武汉"));
Person person1Copy = person1.clone();
// false
System.out.println(person1.getAddress() == person1Copy.getAddress());
```

从输出结构就可以看出， `person1` 的克隆对象和 `person1` 包含的 `Address` 对象已经是不同的了。

**那什么是引用拷贝呢？** 简单来说，**引用拷贝就是两个不同的引用指向同一个对象。**

![image-20220906211832053](https://static.weishao996.top/article/20230909000650.png)

![image-20220906211847040](https://static.weishao996.top/article/20230909000654.png)

![image-20220906211856438](https://static.weishao996.top/article/20230909000658.png)

## 接口和抽象类

从**设计目的**上来说，二者有如下的区别：

接口体现的是一种**规范**。对于接口的实现者而言，**接口规定了实现者必须向外提供哪些服务**；对于接口的调用者而言，**接口规定了调用者可以调用哪些服务**，以及如何调用这些服务。当在一个程序中使用接口时，**接口是多个模块间的耦合标准**；当在多个应用程序之间使用接口时，**接口是多个程序之间的通信标准**。

抽象类体现的是一种**模板式设计**。抽象类作为多个子类的抽象父类，可以被当成系统实现过程中的中间产品，这个中间产品已经实现了系统的部分功能，但这个产品依然不能当成最终产品，必须有更进一步的完善，这种完善可能有几种不同方式。

从使用方式上来说，二者有如下的**区别**：

- 接口里只能包含抽象方法、静态方法、默认方法和私有方法，不能为普通方法提供方法实现；抽象类则完全可以包含普通方法。
- 接口里只能定义静态常量，不能定义普通成员变量；抽象类里则既可以定义普通成员变量，也可以定义静态常量。
- 接口里不包含构造器；抽象类里可以包含构造器，抽象类里的构造器并不是用于创建对象，而是让其子类调用这些构造器来完成属于抽象类的初始化操作。
- 接口里不能包含初始化块；但抽象类则完全可以包含初始化块。
- 一个类最多只能有一个直接父类，包括抽象类；但一个类可以直接实现多个接口，通过实现多个接口可以弥补Java单继承的不足。

扩展阅读

接口和抽象类很像，它们都具有如下**共同的特征**：

- 接口和抽象类都**不能被实例化**，它们都位于继承树的顶端，用于被其他类实现和继承。
- 接口和抽象类都可以包含抽象方法，实现接口或继承抽象类的普通子类都必须实现这些抽象方法。

**面向接口编程**

接口体现的是一种规范和实现分离的设计哲学，充分利用接口可以极好地**降低程序各模块之间的耦合**，从而提高系统的可扩展性和可维护性。基于这种原则，很多软件架构设计理论都倡导“面向接口”编程，而不是面向实现类编程，希望通过面向接口编程来降低程序的耦合。



## 构造器

### 构造方法有哪些特点？是否可被 override?

构造方法特点如下：

- 名字与类名相同。
- 没有返回值，但不能用 void 声明构造函数。
- 生成类的对象时自动执行，无需调用。

**构造方法不能被 override（重写）,但是可以 overload（重载）**,所以你可以看到**一个类中有多个构造函数**的情况。

构造方法不能重写。因为构造方法需要和类保持同名，而重写的要求是子类方法要和父类方法保持同名。如果允许重写构造方法的话，那么子类中将会存在与类名不同的构造方法，这与构造方法的要求是矛盾的。

**Constructor(构造器)**不能被继承，所以不能被**override(重写)**，但是可以被**overloading(重载)**。构造器就是构造方法，能够被重载（同类中不同参数列表的构造器），不能够被重写（子类使用super方法可以调用）。

### 如果一个类没有声明构造方法，该程序能正确执行吗?

如果一个类没有声明构造方法，也可以执行！因为一个类即使没有声明构造方法也会有**默认的不带参数的构造方法**。如果我们自己添加了类的构造方法（无论是否有参），Java 就不会再添加默认的无参数的构造方法了，这时候，就不能直接 new 一个对象而不传递参数了，所以我们一直在不知不觉地使用构造方法，这也是为什么我们**在创建对象的时候后面要加一个括号（因为要调用无参的构造方法）**。**如果我们重载了有参的构造方法，记得都要把无参的构造方法也写出来**（无论是否用到），因为这可以帮助我们在创建对象的时候少踩坑。

## Java创建对象

### 创建一个对象用什么运算符?对象实体与对象引用有何不同

new 运算符，new 创建对象实例（对象实例在堆内存中），对象引用指向对象实例（对象引用存放在栈内存中）。

### Java创建对象方式

java中提供了以下四种创建对象的方式:

- **new创建新对象** 

```java
User user=new User();
```

- **通过反射机制** 

使用 newInstance()，但是得处理两个异常 InstantiationException、 IllegalAccessException：

```java
User user=User.class.newInstance();
Object object=(Object)Class.forName("java.lang.Object").newInstance()
```

- **采用clone机制** 
- **通过序列化机制** 

调用 ObjectInputStream 类的 readObject() 方法。 我们反序列化一个对象，JVM 会给我们创建一个单独的对象。JVM 创建对象并不会调用任何构造函 数。一个对象实现了 Serializable 接口，就可以把对象写入到文件中，并通过读取文件来创建对 象。

# **JAVA常见对象**

## String

### **String、StringBuffer、StringBuilder 的区别？String 为什么是不可变的?**

#### **可变性**

简单的来说：`String` 类中使用 **final** **关键字**修饰字符数组来保存字符串

```java
public final class String implements java.io.Serializable, Comparable<String>, CharSequence {
    private final char value[];
	//...
}
```

 **我们知道被** `final` **关键字修饰的类不能被继承，修饰的方法不能被重写，修饰的变量是基本数据类型则值不能改变，修饰的变量是引用类型则不能再指向其他对象**。因此，`final` 关键字修饰的数组保存字符串并不是 `String` 不可变的根本原因，因为这个数组保存的字符串是可变的（`final` 修饰引用类型变量的情况）。

`String` 真正不可变有下面几点原因：

1. **保存字符串的数组被 final 修饰且为私有的，并且`String` 类没有提供/暴露修改这个字符串的方法。**
2. **`String` 类被 `final` 修饰导致其不能被继承，进而避免了子类破坏 `String` 不可变。**

在 Java 9 之后，`String` 、`StringBuilder` 与 `StringBuffer` 的实现改用 **byte 数组**存储字符串。

**StringBuilder**与 **StringBuffer**都继承自 `AbstractStringBuilder` 类，在 `AbstractStringBuilder` 中也是使用字符数组保存字符串，不过没有使用 `final` 和 `private` 关键字修饰，最关键的是这个 `AbstractStringBuilder` 类还提供了很多**修改字符串的方法**比如 `append` 方法。

#### **线程安全性**

**String中的对象是不可变的，也就可以理解为常量，线程安全**。AbstractStringBuilder 是 `StringBuilder` 与 `StringBuffer` 的公共父类，定义了一些字符串的基本操作，如 `expandCapacity`、`append`、`insert`、`indexOf` 等公共方法。StringBuffer 对方法加了同步锁或者对调用的方法加了同步锁，**StringBuffer 是线程安全的**，内部使用 synchronized 进行同步，所以是线程安全的。**StringBuilder 并没有对方法进行加同步锁，所以是非线程安全的**。

#### **性能**

**每次对 `String` 类型进行改变的时候，都会生成一个新的 `String` 对象，然后将指针指向新的 `String` 对象。`StringBuffer` 每次都会对 `StringBuffer` 对象本身进行操作，而不是生成新的对象并改变对象引用。相同情况下使用 `StringBuilder` 相比使用 `StringBuffer` 仅能获得 10%~15% 左右的性能提升，但却要冒多线程不安全的风险。** 

**对于三者使用的总结：**

- 操作少量的数据: 适用 String
- 单线程操作字符串缓冲区下操作大量数据: 适用 StringBuilder
- 多线程操作字符串缓冲区下操作大量数据: 适用 StringBuffer

### 字符串拼接用“+” 还是 StringBuilder?

Java 语言本身并不支持运算符重载，“+”和“+=”是专门为 String 类重载过的运算符，也是 Java 中仅有的两个重载过的元素符。

![image-20220906221904219](https://static.weishao996.top/article/20230909000707.png)

不过，在循环内使用**“+”**进行字符串的拼接的话，**存在比较明显的缺陷：编译器不会创建单个 StringBuilder** **以复用，会导致创建过多的 StringBuilder 对象**。

```java
String[] arr = {"he", "llo", "world"};
String s = "";
for (int i = 0; i < arr.length; i++) {
    s += arr[i];
}
System.out.println(s);
```

`StringBuilder` 对象是在循环内部被创建的，这意味着**每循环一次就会创建一个** **`StringBuilder`** 对象。

![image-20220906222043648](https://static.weishao996.top/article/20230909000737.png)

如果直接使用 `StringBuilder` 对象进行字符串拼接的话，就不会存在这个问题了。

### String#equals() 和 Object#equals() 有何区别？

`String` 中的 `equals` 方法是被重写过的，比较的是 String 字符串的值是否相等。 `Object` 的 `equals` 方法是比较的对象的内存地址。

### 字符串常量池的作用了解吗？

**字符串常量池** 是 JVM 为了提升性能和减少内存消耗针对字符串（String 类）专门开辟的一块区域，主要目的是为了避免字符串的重复创建。

```java
String aa = "ab"; // 放在常量池中
String bb = "ab"; // 从常量池中查找
System.out.println(aa==bb);// true
```

**JDK1.7 之前**运行时常量池逻辑包含字符串常量池存放在**方法区**。**JDK1.7** 的时候，字符串常量池被从方法区拿到了**堆中**。

### String类有哪些方法？

String类是Java最常用的API，它包含了大量处理字符串的方法，比较常用的有：

- char charAt(int index)：返回指定索引处的字符；
- String substring(int beginIndex, int endIndex)：从此字符串中截取出一部分子字符串；
- String[] split(String regex)：以指定的规则将此字符串分割成数组；
- String trim()：删除字符串前导和后置的空格；
- int indexOf(String str)：返回子串在此字符串首次出现的索引；
- int lastIndexOf(String str)：返回子串在此字符串最后出现的索引；
- boolean startsWith(String prefix)：判断此字符串是否以指定的前缀开头；
- boolean endsWith(String suffix)：判断此字符串是否以指定的后缀结尾；
- String toUpperCase()：将此字符串中所有的字符大写；
- String toLowerCase()：将此字符串中所有的字符小写；
- String replaceFirst(String regex, String replacement)：用指定字符串替换第一个匹配的子串；
- String replaceAll(String regex, String replacement)：用指定字符串替换所有的匹配的子串

### String可以被继承吗？

在Java中，String类被设计为不可变类，主要表现在它保存字符串的成员变量是final的。

- Java 9之前字符串采用char[]数组来保存字符，即 private final char[] value；
- Java 9做了改进，采用byte[]数组来保存字符，即 private final byte[] value；

之所以要把String类设计为不可变类，主要是出于安全和性能的考虑，可归纳为如下4点。

- 由于字符串无论在任何 Java 系统中都广泛使用，会用来存储敏感信息，如账号，密码，网络路径，文件处理等场景里，保证字符串 String 类的安全性就尤为重要了，如果字符串是可变的，容易被篡改，那我们就无法保证使用字符串进行操作时，它是安全的，很有可能出现 SQL 注入，访问危险文件等操作。
- 在多线程中，只有不变的对象和值是线程安全的，可以在多个线程中共享数据。由于 String 天然的不可变，当一个线程”修改“了字符串的值，只会产生一个新的字符串对象，不会对其他线程的访问产生副作用，访问的都是同样的字符串数据，不需要任何同步操作。
- 字符串作为基础的数据结构，大量地应用在一些集合容器之中，尤其是一些散列集合，在散列集合中，存放元素都要根据对象的 hashCode() 方法来确定元素的位置。由于字符串 hashcode 属性不会变更，保证了唯一性，使得类似 HashMap，HashSet 等容器才能实现相应的缓存功能。由于 String 的不可变，避免重复计算 hashcode，只要使用缓存的 hashcode 即可，这样一来大大提高了在散列集合中使用 String 对象的性能。
- 当字符串不可变时，字符串常量池才有意义。字符串常量池的出现，可以减少创建相同字面量的字符串，让不同的引用指向池中同一个字符串，为运行时节约很多的堆内存。若字符串可变，字符串常量池失去意义，基于常量池的 String.intern() 方法也失效，每次创建新的字符串将在堆内开辟出新的空间，占据更多的内存。

因为要保证String类的不可变，那么将这个类定义为final的就很容易理解了。如果没有final修饰，那么就会存在String的子类，这些子类可以重写String类的方法，强行改变字符串的值，这便违背了String类设计的初衷。 

### 使用字符串时，new和""推荐使用哪种方式

先看看 "hello" 和 new String("hello") 的区别：

- 当Java程序直接使用 "hello" 的字符串直接量时，JVM将会使用**常量池**来管理这个字符串；
- 当使用 new String("hello") 时，JVM会先使用常量池来管理 "hello" 直接量，再调用String类的构造器来创建一个**新的String对象**，新创建的String对象被保存在**堆内存**中。

显然，采用new的方式会多创建一个对象出来，会占用更多的内存，所以一般建议使用**直接量的方式**创建字符串。 

### 字符串拼接

拼接字符串有很多种方式，其中最常用的有4种，下面列举了这4种方式各自适合的场景。

1. \+ 运算符：如果拼接的都是字符串直接量，则适合使用 + 运算符实现拼接；
2. StringBuilder：如果拼接的字符串中包含变量，并不要求线程安全，则适合使用StringBuilder；
3. StringBuffer：如果拼接的字符串中包含变量，并且要求线程安全，则适合使用StringBuffer；
4. String类的concat方法：如果只是对两个字符串进行拼接，并且包含变量，则适合使用concat方法；

**用 + 运算符拼接字符串时：**

- 如果拼接的都是**字符串直接量**，则在编译时**编译器会将其直接优化为一个完整的字符串**，和你直接写一个完整的字符串是一样的，所以效率非常的高。
- 如果拼接的字符串中**包含变量**，则在编译时编译器采用StringBuilder对其进行优化，即自动创建**StringBuilder**实例并调用其**append()**方法，将这些字符串拼接在一起，效率也很高。但如果这个拼接操作是在**循环中**进行的，那么**每次循环编译器都会创建一个StringBuilder实例**，再去拼接字符串，相当于执行了 new StringBuilder().append(str)，所以此时效率很低。

**采用StringBuilder/StringBuffer拼接字符串时：**

- StringBuilder/StringBuffer都有字符串缓冲区，缓冲区的容量在创建对象时确定，并且**默认为16**。当拼接的字符串超过缓冲区的容量时，会触发缓冲区的**扩容机制，即缓冲区加倍**。
- 缓冲区频繁的扩容会降低拼接的性能，所以如果能提前预估最终字符串的长度，则建议在创建可变字符串对象时，放弃使用默认的容量，**可以指定缓冲区的容量为预估的字符串的长度**。

**采用String类的concat方法拼接字符串时：**

- concat方法的拼接逻辑是，先创建一个足以容纳待拼接的两个字符串的字节数组，然后先后将两个字符串拼到这个数组里，最后将此数组转换为字符串。
- 在拼接大量字符串的时候，concat方法的效率低于StringBuilder。但是只拼接2个字符串时，concat方法的效率要优于StringBuilder。并且这种拼接方式代码简洁，**所以只拼2个字符串时建议优先选择concat方法**。

### String a = "abc"; ，说一下这个过程会创建什么，放在哪里？

JVM会使用常量池来管理字符串直接量。在执行这句话时，JVM会先检查常量池中是否已经存有"abc"，若没有则将"abc"存入常量池，否则就复用常量池中已有的"abc"，将其引用赋值给变量a。

### new String("abc") 是去了哪里，仅仅是在堆里面吗？

在执行这句话时，JVM会先使用常量池来管理字符串直接量，即**将"abc"存入常量池**。然后再创建一个新的String对象，这个对象会被保存在**堆内存**中。并且，堆中对象的数据会**指向常量池中的直接量**。

### string不可变的好处

**1. 可以缓存 hash 值**

因为 String 的 hash 值经常被使用，例如 String 用做 HashMap 的 key。不可变的特性可以使得 hash 值也不可变，因此只需要进行一次计算。

**2. String Pool 的需要**

如果一个 String 对象已经被创建过了，那么就会从 String Pool 中取得引用。只有 String 是不可变的，才可能使用 String Pool。

![image-20220906223127273](https://static.weishao996.top/article/20230909000744.png)

**3. 安全性**

String 经常作为参数，String 不可变性可以保证参数不可变。例如在作为网络连接参数的情况下如果 String 是可变的，那么在网络连接过程中，String 被改变，改变 String 对象的那一方以为现在连接的是其它主机，而实际情况却不一定是。

**4. 线程安全**

String 不可变性天生具备线程安全，可以在多个线程中安全地使用。

### String.intern()

使用 **String.intern()** 可以保证相同内容的字符串变量引用同一的内存对象。

下面示例中，s1 和 s2 采用 new String() 的方式新建了两个不同对象，而 s3 是通过 s1.intern() 方法取得一个对象引用。intern() 首先把 s1 引用的对象放到 String Pool(字符串常量池)中，然后返回这个对象引用。因此 s3 和 s1 引用的是同一个字符串常量池的对象。

```java
String s1 = new String("aaa");
String s2 = new String("aaa");
System.out.println(s1 == s2);           // false
String s3 = s1.intern();
System.out.println(s1.intern() == s3);  // true
```

如果是采用 "bbb" 这种使用双引号的形式创建字符串实例，会自动地将新建的对象放入 String Pool 中。

```java
String s4 = "bbb";
String s5 = "bbb";
System.out.println(s4 == s5);  // true
```

在 Java 7 之前，字符串常量池被放在运行时常量池中，它属于永久代。而在 Java 7，字符串常量池被移到 Native Method 中。这是因为永久代的空间有限，在大量使用字符串的场景下会导致 OutOfMemoryError 错误。

## Object

### Object 类的常见方法有哪些？

Object 类是一个特殊的类，是所有类的父类。它主要提供了以下 11 个方法：

```java
public final native Class<?> getClass()//native方法，用于返回当前运行时对象的Class对象，使用了final关键字修饰，故不允许子类重写。

public native int hashCode() //native方法，用于返回对象的哈希码，主要使用在哈希表中，比如JDK中的HashMap。
public boolean equals(Object obj)//用于比较2个对象的内存地址是否相等，String类对该方法进行了重写用户比较字符串的值是否相等。

protected native Object clone() throws CloneNotSupportedException//naitive方法，用于创建并返回当前对象的一份拷贝。一般情况下，对于任何对象 x，表达式 x.clone() != x 为true，x.clone().getClass() == x.getClass() 为true。Object本身没有实现Cloneable接口，所以不重写clone方法并且进行调用的话会发生CloneNotSupportedException异常。

public String toString()//返回类的名字@实例的哈希码的16进制的字符串。建议Object所有的子类都重写这个方法。

public final native void notify()//native方法，并且不能重写。唤醒一个在此对象监视器上等待的线程(监视器相当于就是锁的概念)。如果有多个线程在等待只会任意唤醒一个。

public final native void notifyAll()//native方法，并且不能重写。跟notify一样，唯一的区别就是会唤醒在此对象监视器上等待的所有线程，而不是一个线程。

public final native void wait(long timeout) throws InterruptedException//native方法，并且不能重写。暂停线程的执行。注意：sleep方法没有释放锁，而wait方法释放了锁 。timeout是等待时间。

public final void wait(long timeout, int nanos) throws InterruptedException//多了nanos参数，这个参数表示额外时间（以毫微秒为单位，范围是 0-999999）。 所以超时的时间还需要加上nanos毫秒。

public final void wait() throws InterruptedException//跟之前的2个wait方法一样，只不过该方法一直等待，没有超时时间这个概念

protected void finalize() throws Throwable { }//实例被垃圾回收器回收的时候触发的操作

```

# **泛型**

## Java 泛型了解么？

**Java 泛型（generics）** 是 JDK 5 中引入的一个新特性, 泛型提供了编译时类型安全检测机制，该机制允许程序员在编译时检测到非法的类型。泛型的本质是参数化类型，也就是说所操作的数据类型被指定为一个参数。

Java 的泛型是伪泛型，这是因为 Java 在运行期间，所有的泛型信息都会被擦掉，这也就是通常所说类型擦除 。

```java
List<Integer> list = new ArrayList<>();
list.add(12);
//这里直接添加会报错
list.add("a");
Class<? extends List> clazz = list.getClass();
Method add = clazz.getDeclaredMethod("add", Object.class);
//但是通过反射添加是可以的
//这就说明在运行期间所有的泛型信息都会被擦掉
add.invoke(list, "kl");
System.out.println(list);

```

泛型一般有三种使用方式: **泛型类、泛型接口、泛型方法**。

**1.泛型类**：

```java
//此处T可以随便写为任意标识，常见的如T、E、K、V等形式的参数常用于表示泛型
//在实例化泛型类时，必须指定T的具体类型
public class Generic<T> {
    private T key;
    public Generic(T key) {
        this.key = key;
    }
    public T getKey() {
        return key;
    }
}
```

如何实例化泛型类：

```java
Generic<Integer> genericInteger = new Generic<Integer>(123456);
```

**2.泛型接口** ：

```java
public interface Generator<T> {
    public T method();
}
```

实现泛型接口，不指定类型：

```java
class GeneratorImpl<T> implements Generator<T>{
    @Override
    public T method() {
        return null;
    }
}
```

实现泛型接口，指定类型：

```java
class GeneratorImpl implements Generator<String>{
    @Override
    public String method() {
        return "hello";
    }
}
```

**3.泛型方法** ：

```java
public static <E> void printArray(E[] inputArray) {
    for (E element : inputArray) {
        System.out.printf("%s ", element);
    }
    System.out.println();
}
```

使用：

```java
// 创建不同类型数组： Integer, Double 和 Character
Integer[] intArray = { 1, 2, 3 };
String[] stringArray = { "Hello", "World" };
printArray(intArray);
printArray(stringArray);
```

## 泛型擦除

### **一、各种语言中的编译器是如何处理泛型的**

通常情况下，一个编译器处理泛型有两种方式：

1.**Code specialization**。在实例化一个泛型类或泛型方法时都产生一份新的目标代码（字节码or二进制代码）。例如，针对一个泛型List，可能需要 针对String，Integer，Float产生三份目标代码。

2**.Code sharing**。对每个泛型类只生成唯一的一份目标代码；该泛型类的所有实例都映射到这份目标代码上，在需要的时候执行类型检查和类型转换。

C++ 中的模板（template）是典型的Code specialization实现。C++ 编译器会为每一个泛型类实例生成一份执行代码。执行代码中Integer List和String List是两种不同的类型。这样会导致**代码膨胀**（code bloat）。 C#里面泛型无论在程序源码中、编译后的IL中（Intermediate Language，中间语言，这时候泛型是一个占位符）或是运行期的CLR中都是切实存在的，List<Integer>与List<String>就是两个不同的类型，它们在系统运行期生成，有自己的虚方法表和类型数据，这种实现称为类型膨胀，基于这种方法实现的泛型被称为**真实泛型**。 Java语言中的泛型则不一样，它只在程序源码中存在，在编译后的字节码文件中，就已经被替换为原来的原生类型（Raw Type，也称为裸类型）了，并且在相应的地方插入了强制转型代码，因此对于运行期的Java语言来说，ArrayList<Integer>与ArrayList<String>就是同一个类。**所以说泛型技术实际上是Java语言的一颗语法糖，Java语言中的泛型实现方法称为类型擦除，基于这种方法实现的泛型被称为伪泛型**。

C++和C#是使用Code specialization的处理机制，前面提到，他有一个缺点，那就是**会导致代码膨胀**。另外一个弊端是在引用类型系统中，浪费空间，因为引用类型集合中元素本质上都是一个指针。没必要为每个类型都产生一份执行代码。而这也是Java编译器中采用Code sharing方式处理泛型的主要原因。

Java编译器通过Code sharing方式为每个泛型类型创建唯一的字节码表示，并且将该泛型类型的实例都映射到这个唯一的字节码表示上。将多种泛型类形实例映射到唯一的字节码表示是通过类型擦除（type erasure）实现的。

### **二、什么是类型擦除**

前面我们多次提到这个词：**类型擦除**（type erasure），那么到底什么是类型擦除呢？

类型擦除指的是通过类型参数合并，将泛型类型实例关联到**同一份字节码**上。编译器只为泛型类型生成一份字节码，并将其实例关联到这份字节码上。类型擦除的关键在于从泛型类型中清除类型参数的相关信息，并且再必要的时候添加类型检查和类型转换的方法。 类型擦除可以简单的理解为将泛型java代码转换为普通java代码，只不过编译器更直接点，将泛型java代码直接转换成普通java字节码。 类型擦除的主要过程如下： **1.将所有的泛型参数用其最左边界（最顶级的父类型）类型替换。（这部分内容可以看：Java泛型中extends和super的理解） 2.移除所有的类型参数。**

### **三、Java编译器处理泛型的过程**

**code 1:**

```java
public static void main(String[] args) {  
    Map<String, String> map = new HashMap<String, String>();  
    map.put("name", "hollis");  
    map.put("age", "22");  
    System.out.println(map.get("name"));  
    System.out.println(map.get("age"));  
}  
```

**反编译后的code 1:**

```java
public static void main(String[] args) {  
    Map map = new HashMap();  
    map.put("name", "hollis");  
    map.put("age", "22"); 
    System.out.println((String) map.get("name"));  
    System.out.println((String) map.get("age"));  
}  
```

**code 2:**

```java
interface Comparable<A> {
    public int compareTo(A that);
}

public final class NumericValue implements Comparable<NumericValue> {
    private byte value;

    public NumericValue(byte value) {
        this.value = value;
    }

    public byte getValue() {
        return value;
    }

    public int compareTo(NumericValue that) {
        return this.value - that.value;
    }
}

```

**反编译后的code 2:**

```java
 interface Comparable {
  public int compareTo( Object that);
} 

public final class NumericValue
    implements Comparable
{
    public NumericValue(byte value)
    {
        this.value = value;
    }
    public byte getValue()
    {
        return value;
    }
    public int compareTo(NumericValue that)
    {
        return value - that.value;
    }
    public volatile int compareTo(Object obj)
    {
        return compareTo((NumericValue)obj);
    }
    private byte value;
}

```

**code 3:**

```java
public class Collections {
    public static <A extends Comparable<A>> A max(Collection<A> xs) {
        Iterator<A> xi = xs.iterator();
        A w = xi.next();
        while (xi.hasNext()) {
            A x = xi.next();
            if (w.compareTo(x) < 0)
                w = x;
        }
        return w;
    }
}
```

**反编译后的code 3:**

```java
public class Collections
{
    public Collections()
    {
    }
    public static Comparable max(Collection xs)
    {
        Iterator xi = xs.iterator();
        Comparable w = (Comparable)xi.next();
        while(xi.hasNext())
        {
            Comparable x = (Comparable)xi.next();
            if(w.compareTo(x) < 0)
                w = x;
        }
        return w;
    }
}

```

## 泛型通配符

E - Element (在集合中使用，因为集合中存放的是元素)

T - Type（Java 类）

K - Key（键）

V - Value（值）

N - Number（数值类型）

？ - 表示不确定的java类型（无限制通配符类型）

S、U、V - 2nd、3rd、4th types

Object - 是所有类的根类，任何类的对象都可以设置给该Object引用变量，使用的时候可能需要类型强制转换，但是用使用了泛型T、E等这些标识符后，在实际用之前类型就已经确定了，不需要再进行类型强制转换。

## 你的项目中哪里用到了泛型？

- 可用于定义通用返回结果 **CommonResult<T>** 通过参数 T 可根据具体的返回类型动态指定结果的数据类型

- 定义 Excel 处理类 **ExcelUtil<T>** 用于动态指定 Excel 导出的数据类型

- 用于构建集合工具类。参考 Collections 中的 sort, binarySearch 方法

## List<? super T>和List<? extends T>

- ? 是类型通配符，List<?> 可以表示各种泛型List的父类，意思是**元素类型未知的List**；
- List<? super T> 用于设定类型通配符的下限，此处 ? 代表一个未知的类型，但它必须是**T的父类型**；
- List<? extends T> 用于设定类型通配符的上限，此处 ? 代表一个未知的类型，但它必须是**T的子类型**。

**扩展阅读**

在Java的早期设计中，允许把Integer[]数组赋值给Number[]变量，此时如果试图把一个Double对象保存到该Number[]数组中，编译可以通过，但在运行时抛出ArrayStoreException异常。这显然是一种不安全的设计，因此Java在泛型设计时进行了改进，它不再允许把 List<Integer> 对象赋值给 List<Number> 变量。

数组和泛型有所不同，假设Foo是Bar的一个子类型（子类或者子接口），那么Foo[]依然是Bar[]的子类型，但G<Foo> 不是 G<Bar> 的子类型。Foo[]自动向上转型为Bar[]的方式被称为型变，也就是说，Java的数组支持型变，但Java集合并不支持型变。Java泛型的设计原则是，只要代码在编译时没有出现警告，就不会遇到运行时ClassCastException异常。

# **反射**

## 反射的定义、优缺点及应用场景

### 何为反射？

Java 的反射（reflection）机制是指在程序的运行状态中，可以构造任意一个类的对象，可以了解任意一个对象所属的类，可以了解任意一个类的成员变量和方法，可以调用任意一个对象的属性和方法。这种动态获取程序信息以及动态调用对象的功能称为 Java 语言的反射机制。反射被视为动态语言的关键。

### 反射机制优缺点

**优点** ： 可以让咱们的代码更加灵活、为各种框架提供**开箱即用**的功能提供了便利

**缺点** ：让我们在运行时有了分析操作类的能力，这同样也增加了安全问题。比如可以**无视泛型参数的安全检查**（泛型参数的安全检查发生在编译时）。另外，反射的性能也要稍差点，不过，对于框架来说实际是影响不大的。使用反射 性能较低，需要解析字节码，将内存中的对象进行解析

解决方案： 

1、通过setAccessible(true) 关闭JDK的安全检查来提升反射速度； 

2、多次创建一个类的实例时，有缓存会快很多 

3、 ReflectASM工具类，通过字节码生成的方式加快反射速度 2）相对不安全，破坏了封装性（因为通 过反射可以获得私有方法和属性）

### 反射的应用场景

像咱们平时大部分时候都是在写业务代码，很少会接触到直接使用反射机制的场景。

但是，这并不代表反射没有用。相反，正是因为反射，你才能这么轻松地使用各种框架。像 **Spring/Spring Boot、MyBatis** 等等框架中都大量使用了反射机制。

**这些框架中也大量使用了动态代理，而动态代理的实现也依赖反射。**

比如下面是通过 JDK 实现动态代理的示例代码，其中就使用了反射类 `Method` 来调用指定的方法。

```java
public class DebugInvocationHandler implements InvocationHandler {
    /**
     * 代理类中的真实对象
     */
    private final Object target;
    public DebugInvocationHandler(Object target) {
        this.target = target;
    }
    public Object invoke(Object proxy, Method method, Object[] args) throws InvocationTargetException, IllegalAccessException {
        System.out.println("before method " + method.getName());
        Object result = method.invoke(target, args);
        System.out.println("after method " + method.getName());
        return result;
    }
}
```

另外，像 Java 中的一大利器 **注解** 的实现也用到了反射。

为什么你使用 Spring 的时候 ，一个`@Component`注解就声明了一个类为 Spring Bean 呢？为什么你通过一个 `@Value`注解就读取到配置文件中的值呢？究竟是怎么起作用的呢？

这些都是因为你可以基于反射分析类，然后获取到类/属性/方法/方法的参数上的注解。你获取到注解之后，就可以做进一步的处理。

## 过反射获取Class对象的方法

- **类名.class**：即通过一个 Class 的静态变量 class 获取，实例如下

```java
Class cls = ImoocStudent.class;
```

- **对象.getClass ()**：前提是有该类的对象实例，该方法由 java.lang.Object 类提供，实例如下：

```java
ImoocStudent imoocStudent = new ImoocStudent("小慕");
Class imoocStudent.getClass();
```

- **Class.forName (“包名.类名”)**：如果知道一个类的完整包名，可以通过 Class 类的静态方法 forName() 获得 Class 对象，实例如下：

```java
class cls = Class.forName("java.util.ArrayList");
```

- 通过类加载器**xxxClassLoader.loadClass()**传入类路径获取:

```java
Class clazz = ClassLoader.loadClass("cn.javaguide.TargetObject");
```

**实现Java反射的类：**

- 1）**Class**：表示正在运行的Java应用程序中的类和接口 注意： 所有获取对象的信息都需要Class类 来实现。 
- 2）**Field**：提供有关类和接口的属性信息，以及对它的动态访问权限。 
- 3）**Constructor**： 提供关于类的单个构造方法的信息以及它的访问权限 
- 4）**Method**：提供类或接口中某个方法的信息

**反射的一些基本操作**

1. **创建一个我们要使用反射操作的类**

```java
package cn.javaguide;

public class TargetObject {
    private String value;

    public TargetObject() {
        value = "JavaGuide";
    }

    public void publicMethod(String s) {
        System.out.println("I love " + s);
    }

    private void privateMethod() {
        System.out.println("value is " + value);
    }
}
```

2.使用反射操作这个类的方法以及参数

```java
package cn.javaguide;

import java.lang.reflect.Field;
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;

public class Main {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, IllegalAccessException, InstantiationException, InvocationTargetException, NoSuchFieldException {
        /**
         * 获取 TargetObject 类的 Class 对象并且创建 TargetObject 类实例
         */
        Class<?> tagetClass = Class.forName("cn.javaguide.TargetObject");
        TargetObject targetObject = (TargetObject) tagetClass.newInstance();
        /**
         * 获取 TargetObject 类中定义的所有方法
         */
        Method[] methods = targetClass.getDeclaredMethods();
        for (Method method : methods) {
            System.out.println(method.getName());
        }

        /**
         * 获取指定方法并调用
         */
        Method publicMethod = targetClass.getDeclaredMethod("publicMethod",
                String.class);

        publicMethod.invoke(targetObject, "JavaGuide");

        /**
         * 获取指定参数并对参数进行修改
         */
        Field field = targetClass.getDeclaredField("value");
        //为了对类中的参数进行修改我们取消安全检查
        field.setAccessible(true);
        field.set(targetObject, "JavaGuide");

        /**
         * 调用 private 方法
         */
        Method privateMethod = targetClass.getDeclaredMethod("privateMethod");
        //为了调用private方法我们取消安全检查
        privateMethod.setAccessible(true);
        privateMethod.invoke(targetObject);
    }
}


```

输出内容：

```java
publicMethod
privateMethod
I love JavaGuide
value is JavaGuide
```

**注意** : 有读者提到上面代码运行会抛出 ClassNotFoundException 异常,具体原因是你没有下面把这段代码的包名替换成自己创建的 TargetObject 所在的包 。

```java
Class<?> targetClass = Class.forName("cn.javaguide.TargetObject");
```

# 注解

`Annontation` （注解） 是Java5 开始引入的新特性，可以看作是一种特殊的注释，主要用于修饰类、方法或者变量。

注解本质是一个继承了**`Annotation`** 的特殊接口：

```java
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.SOURCE)
public @interface Override {

}

public interface Override extends Annotation{
    
}
```

注解只有被解析之后才会生效，常见的解析方法有两种：

- **编译期直接扫描** ：编译器在编译 Java 代码的时候扫描对应的注解并处理，比如某个方法使用**@Override** 注解，编译器在编译的时候就会检测当前的方法是否重写了父类对应的方法。
- **运行期通过反射处理** ：像框架中自带的注解(比如 Spring 框架的 **@Value**、**@Component**)都是通过反射来进行处理的。

JDK 提供了很多内置的注解（比如 **@Override**、**@Deprecated**），同时，我们还可以自定义注解。

# I/O

## Java 中 IO 流分为几种?

Java 中 IO 流分为几种?

- 按照流的流向分，可以分为**输入流和输出流**；

- 按照操作单元划分，可以划分为**字节流和字符流**；

- 按照流的角色划分为**节点流和处理流**。

Java IO 流共涉及 40 多个类，这些类看上去很杂乱，但实际上很有规则，而且彼此之间存在非常紧密的联系， Java IO 流的 40 多个类都是从如下 4 个抽象类基类中派生出来的。

- **InputStream/Reader**: 所有的输入流的基类，前者是**字节输入流**，后者是**字符输入流**。
- **OutputStream/Writer**: 所有输出流的基类，前者是**字节输出流**，后者是**字符输出流**。

## 既然有了字节流,为什么还要有字符流?

问题本质想问：**不管是文件读写还是网络发送接收，信息的最小存储单元都是字节，那为什么 I/O 流操作要分为字节流操作和字符流操作呢？**

回答：字符流是由 Java 虚拟机将字节转换得到的，问题就出在这个过程还算是非常耗时，并且，如果我们不知道编码类型就很容易出现乱码问题。所以， I/O 流就干脆提供了一个直接操作字符的接口，方便我们平时对字符进行流操作。如果**音频文件、图片**等媒体文件用**字节流**比较好，如果涉及到**字符**的话使用**字符流**比较好。

## BIO、NIO、AIO？

![image-20220907210051326](https://static.weishao996.top/article/20230909000758.png)

**BIO** (blocking I/O) ： 就是传统的IO，同步阻塞，服务器实现模式为一个连接一个线程，即 **客
户端有连接请求时服务器端就需要启动一个线程进行处理** ，如果这个连接不做任何事情会造
成不必要的线程开销，可以通过连接池机制改善(实现多个客户连接服务器)。

![image-20220907210209850](https://static.weishao996.top/article/20230909000808.png)

BIO方式适用于连接数目比较小且固定的架构，这种方式对服务器资源要求比较高，并发局限于应用中，JDK1.4 以前的唯一选择，程序简单易理解。

**NIO** ：全称 java non-blocking IO，是指 JDK 提供的新 API。从JDK1.4开始，Java 提供了一系列改进的输入/输出的新特性，被统称为NIO(即New IO)。

NIO是 **同步非阻塞** 的，服务器端用一个线程处理多个连接，客户端发送的连接请求会注册到多路复用器上，多路复用器轮询到连接有IO请求就进行处理：

![image-20220907210351648](https://static.weishao996.top/article/20230909000812.png)

NIO的数据是面向 **缓冲区Buffer** 的，必须从Buffer中读取或写入。

所以完整的NIO示意图：

![image-20220907210423184](https://static.weishao996.top/article/20230909000816.png)

可以看出，NIO的运行机制：

- 每个Channel对应一个Buffer。
- Selector对应一个线程，一个线程对应多个Channel。
- Selector会根据不同的事件，在各个通道上切换。
- Buffer是内存块，底层是数据。

**AIO** ：JDK 7 引入了 Asynchronous I/O，是 **异步不阻塞** 的 IO。在进行 I/O 编程中，常用到两种模式：Reactor 和 Proactor。Java 的 NIO 就是 Reactor，当有事件触发时，服务器端得到通知，进行相应的处理，完成后才通知服务端程序启动线程去处理，一般适用于连接数较多且连接时间较长的应用。

## IO模型详解

### 何为 I/O?

I/O（**I**nput/**O**utpu） 即**输入／输出** 。

**我们先从计算机结构的角度来解读一下 I/O。**

根据冯.诺依曼结构，计算机结构分为 5 大部分：**运算器、控制器、存储器、输入设备、输出设备**。

![image-20220907211415038](https://static.weishao996.top/article/20230909000821.png)

输入设备（比如键盘）和输出设备（比如显示器）都属于外部设备。网卡、硬盘这种既可以属于输入设备，也可以属于输出设备。

输入设备向计算机输入数据，输出设备接收计算机输出的数据。

**从计算机结构的视角来看的话， I/O 描述了计算机系统与外部设备之间通信的过程。**

**我们再先从应用程序的角度来解读一下 I/O。**

根据大学里学到的操作系统相关的知识：为了保证操作系统的稳定性和安全性，一个进程的地址空间划分为 **用户空间（User space）** 和 **内核空间（Kernel space ）** 。

像我们平常运行的应用程序都是运行在用户空间，只有内核空间才能进行系统态级别的资源有关的操作，比如文件管理、进程通信、内存管理等等。也就是说，我们想要进行 IO 操作，一定是要依赖内核空间的能力。

并且，用户空间的程序不能直接访问内核空间。

当想要执行 IO 操作时，由于没有执行这些操作的权限，只能发起系统调用请求操作系统帮忙完成。

因此，用户进程想要执行 IO 操作的话，必须通过 **系统调用** 来间接访问内核空间。

我们在平常开发过程中接触最多的就是 **磁盘 IO（读写文件）** 和 **网络 IO（网络请求和响应）**。

**从应用程序的视角来看的话，我们的应用程序对操作系统的内核发起 IO 调用（系统调用），操作系统负责的内核执行具体的 IO 操作。也就是说，我们的应用程序实际上只是发起了 IO 操作的调用而已，具体 IO 的执行是由操作系统的内核来完成的。**

当应用程序发起 I/O 调用后，会经历两个步骤：

1. **内核等待 I/O 设备准备好数据**
2. **内核将数据从内核空间拷贝到用户空间。**

### 有哪些常见的 IO 模型?

UNIX 系统下， IO 模型一共有 5 种： **同步阻塞 I/O**、**同步非阻塞 I/O**、**I/O 多路复用**、**信号驱动 I/O** 和**异步 I/O**。

### Java 中 3 种常见 IO 模型

### **BIO (Blocking I/O)**

**BIO 属于**同步阻塞 IO 模型 **。**

同步阻塞 IO 模型中，应用程序发起 read 调用后，会一直阻塞，直到内核把数据拷贝到用户空间。

![image-20220907211637713](https://static.weishao996.top/article/20230909000827.png)

在客户端连接数量不高的情况下，是没问题的。但是，当面对十万甚至百万级连接的时候，传统的 BIO 模型是无能为力的。因此，我们需要一种更高效的 I/O 处理模型来应对更高的并发量。

### **NIO (Non-blocking/New I/O)**

Java 中的 NIO 于 Java 1.4 中引入，对应 `java.nio` 包，提供了 `Channel` , `Selector`，`Buffer` 等抽象。NIO 中的 N 可以理解为 Non-blocking，不单纯是 New。它是支持面向缓冲的，基于通道的 I/O 操作方法。 对于高负载、高并发的（网络）应用，应使用 NIO 。

**Java 中的 NIO 可以看作是 I/O 多路复用模型**。也有很多人认为，Java 中的 NIO 属于同步非阻塞 IO 模型。

跟着我的思路往下看看，相信你会得到答案！

我们先来看看 **同步非阻塞 IO 模型**。

![image-20220907211733470](https://static.weishao996.top/article/20230909000831.png)

同步非阻塞 IO 模型中，应用程序会一直发起 **read** 调用，等待数据**从内核空间拷贝到用户空间**的这段时间里，线程依然是阻塞的，直到在内核把数据拷贝到用户空间。

相比于同步阻塞 IO 模型，同步非阻塞 IO 模型确实有了很大改进。**通过轮询操作，避免了一直阻塞。**

但是，这种 IO 模型同样存在问题：**应用程序不断进行 I/O 系统调用轮询数据是否已经准备好的过程是十分消耗 CPU 资源的**。

这个时候，**I/O 多路复用模型** 就上场了。

![image-20220907211839332](https://static.weishao996.top/article/20230909000836.png)

IO 多路复用模型中，线程首先发起 select 调用，询问内核数据是否准备就绪，等内核把数据准备好了，用户线程再发起 read 调用。read 调用的过程（数据从内核空间 -> 用户空间）还是阻塞的。

目前支持 IO 多路复用的系统调用，有 select，epoll 等等。select 系统调用，目前几乎在所有的操作系统上都有支持。

- **select 调用** ：内核提供的系统调用，它支持一次查询多个系统调用的可用状态。几乎所有的操作系统都支持。
- **epoll 调用** ：linux 2.6 内核，属于 select 调用的增强版本，优化了 IO 的执行效率。

**IO 多路复用模型，通过减少无效的系统调用，减少了对 CPU 资源的消耗。**

Java 中的 NIO ，有一个非常重要的**选择器 ( Selector )** 的概念，也可以被称为 **多路复用器**。通过它，只需要一个线程便可以管理多个客户端连接。当客户端数据到了之后，才会为其服务。

![image-20220907212117819](https://static.weishao996.top/article/20230909000858.png)

### AIO (Asynchronous I/O)

AIO 也就是 NIO 2。Java 7 中引入了 NIO 的改进版 NIO 2,它是**异步 IO 模型**。

异步 IO 是基于**事件和回调机制**实现的，也就是应用操作之后会直接返回，不会堵塞在那里，当后台处理完成，操作系统会通知相应的线程进行后续的操作。

![image-20220907212236794](https://static.weishao996.top/article/20230909000903.png)

目前来说 AIO 的应用还不是很广泛。Netty 之前也尝试使用过 AIO，不过又放弃了。这是因为，Netty 使用了 AIO 之后，在 Linux 系统上的性能并没有多少提升。

最后，来一张图，简单总结一下 Java 中的 BIO、NIO、AIO。

![image-20220907212354609](https://static.weishao996.top/article/20230909000908.png)



## 获取用键盘输入常用的两种方法

方法 1：通过 `Scanner`

```java
Scanner input = new Scanner(System.in);
String s  = input.nextLine();
input.close();
```

方法 2：通过 `BufferedReader`

```java
BufferedReader input = new BufferedReader(new InputStreamReader(System.in));
String s = input.readLine();
```

## IO流用到了什么设计模式？

其实，Java的IO流体系还用到了一个设计模式—— **装饰器模式** 。

![image-20220907212756379](https://static.weishao996.top/article/20230909000913.png)

# **序列化**

### 什么是序列化?什么是反序列化?

如果我们需要**持久化 Java 对象**比如将 Java 对象保存在文件中，或者在网络传输 Java 对象，这些场景都需要用到序列化。

简单来说：

- **序列化：** **将数据结构或对象转换成二进制字节流的过程**
- **反序列化：将在序列化过程中所生成的二进制字节流转换成数据结构或者对象的过程**

对于 Java 这种面向对象编程语言来说，我们序列化的都是对象（Object）也就是实例化后的类(Class)，但是在 C++这种半面向对象的语言中，struct(结构体)定义的是数据结构类型，而 class 对应的是对象类型。

维基百科是如是介绍序列化的：

序列化（serialization）在计算机科学的数据处理中，是指将数据结构或对象状态转换成可取用格式（例如存成文件，存于缓冲，或经由网络中发送），以留待后续在相同或另一台计算机环境中，能恢复原先状态的过程。依照序列化格式重新获取字节的结果时，可以利用它来产生与原始对象相同语义的副本。对于许多对象，像是使用大量引用的复杂对象，这种序列化重建的过程并不容易。面向对象中的对象序列化，并不概括之前原始对象所关系的函数。这种过程也称为对象编组（marshalling）。从一系列字节提取数据结构的反向操作，是反序列化（也称为解编组、deserialization、unmarshalling）。 

综上：**序列化的主要目的是通过网络传输对象或者说是将对象存储到文件系统、数据库、内存中**。

![image-20220907212950852](https://static.weishao996.top/article/20230909000920.png)

### Java 序列化中如果有些字段不想进行序列化，怎么办？

对于不想进行序列化的变量，使用 **transient** 关键字修饰。

transient 关键字的作用是：**阻止实例中那些用此关键字修饰的的变量序列化；当对象被反序列化时，被 transient 修饰的变量值不会被持久化和恢复。**

关于 transient 还有几点注意：

- transient 只能**修饰变量，**不能修饰类和方法。
- transient 修饰的变量，在反序列化后变量值将会被置成类型的默认值。例如，如果是修饰 int 类型，那么反序列后结果就是 0。
- static 变量因为不属于任何对象(Object)，所以无论有没有 transient 关键字修饰，均不会被序列化。

### Serializable接口有什么用？

这个接口只是一个标记，没有具体的作用，但是如果不实现这个接又，在有些序列化场景会报错，所以一般建议，创建的JavaBean类都实现 Serializable。

### serialVersionUID 又有什么用？

```java
private static final long serialVersionUID = 1L;
```

serialVersionUID 就是起验证作用。

我们经常会看到这样的代码，这个 ID 其实就是用来验证序列化的对象和反序列化对应的对象ID 是否一致。

这个 ID 的数字其实不重要，无论是 1L 还是 IDE自动生成的，只要序列化时候对象的serialVersionUID 和反序列化时候对象的 serialVersionUID 一致的话就行。

如果没有显示指定 serialVersionUID ，则编译器会根据类的相关信息自动生成一个，可以认为是一个指纹。

所以如果你没有定义一个 serialVersionUID， 结果序列化一个对象之后，在反序列化之前把对象的类的结构改了，比如增加了一个成员变量，则此时的反序列化会失败。

因为类的结构变了，所以 serialVersionUID 就不一致。

### Java 序列化不包含静态变量？

序列化的时候是不包含静态变量的。

### 说说有几种序列化方式？

Java序列化方式有很多，常见的有三种：

![image-20220907213807214](https://static.weishao996.top/article/20230909000925.png)

- Java对象流列化 ：Java原生序列化方法即通过Java原生流(InputStream和OutputStream之间的转化)的方式进行转化，一般是对象输出流 ObjectOutputStream 和对象输入流ObjectInputStream 。
- Json序列化：这个可能是我们最常用的序列化方式，Json序列化的选择很多，一般会使用jackson包，通过ObjectMapper类来进行一些操作，比如将对象转化为byte数组或者将json串转化为对象。
- ProtoBuff序列化：ProtocolBuffer是一种轻便高效的结构化数据存储格式，ProtoBuff序列化对象可以很大程度上将其压缩，可以大大减少数据传输大小，提高系统性能。

# **异常**

## Java的异常机制

**关于异常处理：**

在Java中，处理异常的语句由**try、catch、finally**三部分组成。其中，**try块用于包裹业务代码，catch块用于捕获并处理某个类型的异常，finally块则用于回收资源**。当业务代码发生异常时，系统会创建一个异常对象，然后由JVM寻找可以处理这个异常的catch块，并将异常对象交给这个catch块处理。若业务代码打开了某项资源，则可以在finally块中关闭这项资源，因为无论是否发生异常，finally块一定会执行。

**关于抛出异常：**

当程序出现错误时，系统会自动抛出异常。除此以外，Java也允许程序主动抛出异常。当业务代码中，判断某项错误的条件成立时，可以使用**throw**关键字向外抛出异常。在这种情况下，如果当前方法不知道该如何处理这个异常，可以在方法签名上通过**throws**关键字声明抛出异常，则该异常将交给JVM处理。

**关于异常跟踪栈：**

程序运行时，经常会发生一系列方法调用，从而形成方法调用栈。异常机制会导致异常在这些方法之间传播，而异常传播的顺序与方法的调用相反。异常从发生异常的方法向外传播，首先传给该方法的调用者，再传给上层调用者，以此类推。最终会传到main方法，若依然没有得到处理，则JVM会终止程序，并打印异常跟踪栈的信息

## Excption与Error

![image-20220907214913794](https://static.weishao996.top/article/20230909000931.png)

在 Java 中，所有的异常都有一个共同的祖先 `java.lang` 包中的 **`Throwable`** **类**。`Throwable` 类有两个重要的子类:

- **Exception**: 程序本身可以处理的异常，可以通过 catch来进行捕获。**Exception**又可以分为 **Checked Exception (受检查异常，必须处理)**和 **Unchecked Exception (不受检查异常，可以不处理)。**

  - **Unchecked Exception**：

    - **NullPointerException：空指针异常；**  

    - **ArithmeticException：算数异常；**  

    - **ArrayIndexOutOfBoundsException：数组下标越界异常；**  

    - **ClassCastException：类型转换异常。**

  - **Checked Exception**：
    - **IOException：IO 异常**
    - **SQLException：SQL 异常**

- **Error** ：Error属于程序无法处理的错误，我们没办法通过 `catch` 来进行捕获 。

  - **Java 虚拟机运行错误（Virtual MachineError）**
  - **虚拟机内存不够错误(`OutOfMemoryError`)**
  - **类定义错误（NoClassDefFoundError）** 


## Throwable 类常用方法有哪些？

- `String getMessage()`: 返回异常发生时的简要描述
- `String toString()`: 返回异常发生时的详细信息
- `String getLocalizedMessage()`: 返回异常对象的本地化信息。使用 `Throwable` 的子类覆盖这个方法，可以生成本地化信息。如果子类没有覆盖该方法，则该方法返回的信息与 `getMessage()`返回的结果相同
- `void printStackTrace()`: 在控制台上打印 `Throwable` 对象封装的异常信息

## **说说你平时是怎么处理 Java 异常的？**

**try-catch-finally**

1. **捕获异常**

   将业务代码包裹在try块内部，当业务代码中发生任何异常时，系统都会为此异常创建一个异常对象。创建异常对象之后，JVM会在try块之后寻找可以处理它的catch块，并将异常对象交给这个catch块处理。

2. **处理异常**

   在catch块中处理异常时，应该先记录日志，便于以后追溯这个异常。然后根据异常的类型、结合当前的业务情况，进行相应的处理。比如，给变量赋予一个默认值、直接返回空值、向外抛出一个新的业务异常交给调用者处理，等等。

3. **回收资源**

   如果业务代码打开了某个资源，比如数据库连接、网络连接、磁盘文件等，则需要在这段业务代码执行完毕后关闭这项资源。并且，无论是否发生异常，都要尝试关闭这项资源。将关闭资源的代码写在finally块内，可以满足这种需求，即无论是否发生异常，finally块内的代码总会被执行。

其中 try 块是必须的， 阿里内部资料 catch 和 finally 至少存在一个标准异常处理流程

![image-20220907220715855](https://static.weishao996.top/article/20230909000938.png)

抛出异常→捕获异常→捕获成功（当 catch 的异常类型与抛出的异常类型匹配时，捕获成功） →异常被处理，程序继续运行 抛出异常→捕获异常→捕获失败（当 catch 的异常类型与抛出异 常类型不匹配时，捕获失败）→异常未被处理，程序中断运行。

在开发过程中会使用到自定义异常，在通常情况下，程序很少会自己抛出异常，因为异常的类名通常也包含了该异常的有用信息，所以在选择抛出异常的时候，应该选择合适的异常类，从而可以明确地描述该异常情况，所以这时候往往都是自定义异常。 自定义异常通常是通过继承 java.lang.Exception 类，如果想自定义 Runtime 异常的话，可以继承 java.lang.RuntimeException类，实现一个无参构造和一个带字符串参数的有参构造方法。 在业务代码里，可以针对性的使用自定义异常。比如说：该用户不具备某某权限、余额不足等。

## **try catch finally，try里有return，finally还执行么？**

执行，并且finally的执行早于try里面的return

结论：

- 1、不管有木有出现异常，finally块中代码都会执行； 
- 2、当try和catch中有return时，finally仍然会执行； 
- 3、finally是在return后面的表达式运算后执行的（此时并没有返回运算后的值，而是先把要返回的 值保存起来，管finally中的代码怎么样，返回的值都不会改变，任然是之前保存的值），所以函数 返回值是在finally执行前确定的； 
- 4、finally中最好不要包含return，否则程序会提前退出，返回值不是try或catch中保存的返回值。

**注意事项**

如果在try块或catch块中使用 System.exit(1); 来退出虚拟机，则finally块将失去执行的机会。但是我们在实际的开发中，重来都不会这样做，所以尽管存在这种导致finally块无法执行的可能，也只是一种可能而已。

## 如何使用 try-with-resources 代替try-catch-finally？

**适用范围（资源的定义）：** 任何实现 `java.lang.AutoCloseable`或者 `java.io.Closeable` 的对象

**关闭资源和 finally 块的执行顺序：** 在 `try-with-resources` 语句中，任何 catch 或 finally 块在声明的资源关闭后运行

《Effective Java》中明确指出：

面对必须要关闭的资源，我们总是应该优先使用 `try-with-resources` 而不是`try-finally`。随之产生的代码更简短，更清晰，产生的异常对我们也更有用。`try-with-resources`语句让我们更容易编写必须要关闭的资源的代码，若采用`try-finally`则几乎做不到这点。 

Java 中类似于`InputStream`、`OutputStream` 、`Scanner` 、`PrintWriter`等的资源都需要我们调用`close()`方法来手动关闭，一般情况下我们都是通过`try-catch-finally`语句来实现这个需求，如下：

```java
//读取文本文件的内容
Scanner scanner = null;
try {
    scanner = new Scanner(new File("D://read.txt"));
    while (scanner.hasNext()) {
        System.out.println(scanner.nextLine());
    }
} catch (FileNotFoundException e) {
    e.printStackTrace();
} finally {
    if (scanner != null) {
        scanner.close();
    }
}

```

使用 Java 7 之后的 `try-with-resources` 语句改造上面的代码:

```java
try (Scanner scanner = new Scanner(new File("test.txt"))) {
    while (scanner.hasNext()) {
        System.out.println(scanner.nextLine());
    }
} catch (FileNotFoundException fnfe) {
    fnfe.printStackTrace();
}

```

当然多个资源需要关闭的时候，使用 `try-with-resources` 实现起来也非常简单，如果你还是用`try-catch-finally`可能会带来很多问题。

通过使用分号分隔，可以在`try-with-resources`块中声明多个资源。

```java
try (BufferedInputStream bin = new BufferedInputStream(new FileInputStream(new File("test.txt")));
             BufferedOutputStream bout = new BufferedOutputStream(new FileOutputStream(new File("out.txt")))) {
            int b;
            while ((b = bin.read()) != -1) {
                bout.write(b);
            }
        }
        catch (IOException e) {
            e.printStackTrace();
        }

```

# **动态代理**

## 代理模式

代理模式是一种比较好理解的设计模式。简单来说就是 **我们使用代理对象来代替对真实对象(real object)的访问，这样就可以在不修改原目标对象的前提下，提供额外的功能操作，扩展目标对象的功能。**

**代理模式的主要作用是**扩展目标对象的功能**，比如说在目标对象的某个方法执行前后你可以增加一些自定义的操作。**

**举个例子：你找了小红来帮你问话，小红就可以看作是代理你的代理对象，代理的行为（方法）是问话。**

![image-20220907221423842](https://static.weishao996.top/article/20230909000946.png)

代理模式有静态代理和动态代理两种实现方式，我们 先来看一下静态代理模式的实现。

##  静态代理

**静态代理中，我们对目标对象的每个方法的增强都是手动完成的（\*后面会具体演示代码\*），非常不灵活（\*比如接口一旦新增加方法，目标对象和代理对象都要进行修改\*）且麻烦(\*需要对每个目标类都单独写一个代理类\*)。** 实际应用场景非常非常少，日常开发几乎看不到使用静态代理的场景。

上面我们是从实现和应用角度来说的静态代理，从 JVM 层面来说， **静态代理在编译时就将接口、实现类、代理类这些都变成了一个个实际的 class 文件。**

**静态代理实现步骤:**

- **定义一个接口及其实现类；**
- **创建一个代理类同样实现这个接口**
- **将目标对象注入进代理类，然后在代理类的对应方法调用目标类中的对应方法。这样的话，我们就可以通过代理类屏蔽对目标对象的访问，并且可以在目标方法执行前后做一些自己想做的事情。**

下面通过代码展示！

**1.定义发送短信的接口**

```java
public interface SmsService {
    String send(String message);
}
```

**2.实现发送短信的接口**

```java
public class SmsServiceImpl implements SmsService {
    public String send(String message) {
        System.out.println("send message:" + message);
        return message;
    }
}
```

**3.创建代理类并同样实现发送短信的接口**

```java
public class SmsProxy implements SmsService {
    private final SmsService smsService;
    public SmsProxy(SmsService smsService) {
        this.smsService = smsService;
    }
    @Override
    public String send(String message) {
        //调用方法之前，我们可以添加自己的操作
        System.out.println("before method send()");
        smsService.send(message);
        //调用方法之后，我们同样可以添加自己的操作
        System.out.println("after method send()");
        return null;
    }
}
```

**4.实际使用**

```java
public class Main {
    public static void main(String[] args) {
        SmsService smsService = new SmsServiceImpl();
        SmsProxy smsProxy = new SmsProxy(smsService);
        smsProxy.send("java");
    }
}
```

运行上述代码之后，控制台打印出：

```
before method send()
send message:java
after method send()
```

可以输出结果看出，我们已经增加了 `SmsServiceImpl` 的`send()`方法。

## 动态代理

相比于静态代理来说，动态代理更加灵活。我们不需要针对每个目标类都单独创建一个代理类，并且也不需要我们必须实现接口，我们可以直接代理实现类( *CGLIB 动态代理机制*)。

**从 JVM 角度来说，动态代理是在运行时动态生成类字节码，并加载到 JVM 中的。**

**说到动态代理，Spring AOP、RPC 框架应该是两个不得不提的，它们的实现都依赖了动态代理。**

**动态代理在我们日常开发中使用的相对较少，但是在框架中的几乎是必用的一门技术。学会了动态代理之后，对于我们理解和学习各种框架的原理也非常有帮助。**

**就 Java 来说，动态代理的实现方式有很多种，比如 JDK 动态代理、CGLIB 动态代理等等。**

guide-rpc-framework[ ](https://github.com/Snailclimb/guide-rpc-framework) (opens new window) 使用的是 JDK 动态代理，我们先来看看 JDK 动态代理的使用。


另外，虽然 guide-rpc-framework[ ](https://github.com/Snailclimb/guide-rpc-framework) (opens new window) 没有用到 CGLIB 动态代理，我们这里还是简单介绍一下其使用以及和JDK 动态代理的对比。

###  JDK 动态代理机制

####  介绍 

**在 Java 动态代理机制中 `InvocationHandler` 接口和 `Proxy` 类是核心。**

`Proxy` 类中使用频率最高的方法是：`newProxyInstance()` ，这个方法主要用来生成一个代理对象。

```java
    public static Object newProxyInstance(ClassLoader loader,
                                          Class<?>[] interfaces,
                                          InvocationHandler h)
        throws IllegalArgumentException
    {
        ......
    }
```

这个方法一共有 3 个参数：

- **loader** :类加载器，用于加载代理对象。
- **interfaces** : 被代理类实现的一些接口；
- **h** : 实现了 `InvocationHandler` 接口的对象；

**要实现动态代理的话，还必须需要实现`InvocationHandler` 来自定义处理逻辑。 当我们的动态代理对象调用一个方法时，这个方法的调用就会被转发到实现`InvocationHandler` 接口类的 `invoke` 方法来调用。**

```java
public interface InvocationHandler {
    /**
     * 当你使用代理对象调用方法的时候实际会调用到这个方法
     */
    public Object invoke(Object proxy, Method method, Object[] args)
        throws Throwable;
}
```

**invoke()方法有下面三个参数： **

- **proxy:动态生成的代理类** 
- **method : 与代理类对象调用的方法相对应** 

- **args : 当前 method 方法的参数**

也就是说：你通过`Proxy` 类的 `newProxyInstance()` 创建的代理对象在调用方法的时候，实际会调用到实现`InvocationHandler` 接口的类的 `invoke()`方法。你可以在 `invoke()` 方法中自定义处理逻辑，比如在方法执行前后做什么事情。 


#### JDK 动态代理类使用步骤

- **定义一个接口及其实现类；**
- **自定义** **`InvocationHandler`** **并重写**`invoke`**方法，在** **`invoke`** **方法中我们会调用原生方法（被代理类的方法）并自定义一些处理逻辑；**
- **通过** **`Proxy.newProxyInstance(ClassLoader loader,Class<?>[] interfaces,InvocationHandler h)`** **方法创建代理对象；**

#### 代码示例

这样说可能会有点空洞和难以理解，我上个例子，大家感受一下吧！

**1.定义发送短信的接口**

```java
public interface SmsService {
    String send(String message);
}
```

**2.实现发送短信的接口**

```java
public class SmsServiceImpl implements SmsService {
    public String send(String message) {
        System.out.println("send message:" + message);
        return message;
    }
}
```

**3.定义一个 JDK 动态代理类**

```java
import java.lang.reflect.InvocationHandler;
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;
/**
 * @author shuang.kou
 * @createTime 2020年05月11日 11:23:00
 */
public class DebugInvocationHandler implements InvocationHandler {
    /**
     * 代理类中的真实对象
     */
    private final Object target;
    public DebugInvocationHandler(Object target) {
        this.target = target;
    }
    public Object invoke(Object proxy, Method method, Object[] args) throws InvocationTargetException, IllegalAccessException {
        //调用方法之前，我们可以添加自己的操作
        System.out.println("before method " + method.getName());
        Object result = method.invoke(target, args);
        //调用方法之后，我们同样可以添加自己的操作
        System.out.println("after method " + method.getName());
        return result;
    }
}
```

`invoke()` 方法: 当我们的动态代理对象调用原生方法的时候，最终实际上调用到的是 `invoke()` 方法，然后 `invoke()` 方法代替我们去调用了被代理对象的原生方法。

**4.获取代理对象的工厂类**

```java
public class JdkProxyFactory {
    public static Object getProxy(Object target) {
        return Proxy.newProxyInstance(
                target.getClass().getClassLoader(), // 目标类的类加载
                target.getClass().getInterfaces(),  // 代理需要实现的接口，可指定多个
                new DebugInvocationHandler(target)   // 代理对象对应的自定义 InvocationHandler
        );
    }
}
```

`getProxy()` ：主要通过`Proxy.newProxyInstance（）`方法获取某个类的代理对象

**5.实际使用**

```java
SmsService smsService = (SmsService) JdkProxyFactory.getProxy(new SmsServiceImpl());
smsService.send("java");
```

运行上述代码之后，控制台打印出：

```java
before method send
send message:java
after method send
```

###  CGLIB 动态代理机制

#### 介绍

**JDK 动态代理有一个最致命的问题是其只能代理实现了接口的类。**

**为了解决这个问题，我们可以用 CGLIB 动态代理机制来避免。**

CGLIB[ ](https://github.com/cglib/cglib) (opens new window)(Code Generation Library)是一个基于ASM[ ](http://www.baeldung.com/java-asm) (opens new window)的字节码生成库，它允许我们在运行时对字节码进行修改和动态生成。CGLIB 通过继承方式实现代理。很多知名的开源框架都使用到了CGLIB[ ](https://github.com/cglib/cglib) (opens new window)， 例如 Spring 中的 AOP 模块中：如果目标对象实现了接口，则默认采用 JDK 动态代理，否则采用 CGLIB 动态代理。

**在 CGLIB 动态代理机制中** `MethodInterceptor` **接口和** `Enhancer` **类是核心。**

你需要自定义 `MethodInterceptor` 并重写 `intercept` 方法，`intercept` 用于拦截增强被代理类的方法。

```java
public interface MethodInterceptor extends Callback{
    // 拦截被代理类中的方法
    public Object intercept(Object obj, java.lang.reflect.Method method, Object[] args,MethodProxy proxy) throws Throwable;
}
```

1. **obj** :被代理的对象（需要增强的对象）
2. **method** :被拦截的方法（需要增强的方法）
3. **args** :方法入参
4. **proxy** :用于调用原始方法

你可以通过 `Enhancer`类来动态获取被代理类，当代理类调用方法的时候，实际调用的是 `MethodInterceptor` 中的 `intercept` 方法。

####  CGLIB 动态代理类使用步骤

- **定义一个类；**

- **自定义** **`MethodInterceptor`** **并重写** **`intercept`** **方法，**`intercept` **用于拦截增强被代理类的方法，和 JDK 动态代理中的** **`invoke`** 方法类似；
- **通过** **`Enhancer`** **类的** **`create()`**创建代理类；

#### 代码示例

不同于 JDK 动态代理不需要额外的依赖。CGLIB[ ](https://github.com/cglib/cglib) (opens new window)(*Code Generation Library*) 实际是属于一个开源项目，如果你要使用它的话，需要手动添加相关依赖。

```xml
<dependency>
  <groupId>cglib</groupId>
  <artifactId>cglib</artifactId>
  <version>3.3.0</version>
</dependency>
```

**1.实现一个使用阿里云发送短信的类**

```java
package github.javaguide.dynamicProxy.cglibDynamicProxy;
public class AliSmsService {
    public String send(String message) {
        System.out.println("send message:" + message);
        return message;
    }
}
```

**2.自定义 `MethodInterceptor`（方法拦截器）**

```java
import net.sf.cglib.proxy.MethodInterceptor;
import net.sf.cglib.proxy.MethodProxy;
import java.lang.reflect.Method;
/**
 * 自定义MethodInterceptor
 */
public class DebugMethodInterceptor implements MethodInterceptor {
    /**
     * @param o           代理对象（增强的对象）
     * @param method      被拦截的方法（需要增强的方法）
     * @param args        方法入参
     * @param methodProxy 用于调用原始方法
     */
    @Override
    public Object intercept(Object o, Method method, Object[] args, MethodProxy methodProxy) throws Throwable {
        //调用方法之前，我们可以添加自己的操作
        System.out.println("before method " + method.getName());
        Object object = methodProxy.invokeSuper(o, args);
        //调用方法之后，我们同样可以添加自己的操作
        System.out.println("after method " + method.getName());
        return object;
    }
}
```

**3.获取代理类**

```java
import net.sf.cglib.proxy.Enhancer;
public class CglibProxyFactory {
    public static Object getProxy(Class<?> clazz) {
        // 创建动态代理增强类
        Enhancer enhancer = new Enhancer();
        // 设置类加载器
        enhancer.setClassLoader(clazz.getClassLoader());
        // 设置被代理类
        enhancer.setSuperclass(clazz);
        // 设置方法拦截器
        enhancer.setCallback(new DebugMethodInterceptor());
        // 创建代理类
        return enhancer.create();
    }
}
```

**4.实际使用**

```java
AliSmsService aliSmsService = (AliSmsService) CglibProxyFactory.getProxy(AliSmsService.class);
aliSmsService.send("java");
```

运行上述代码之后，控制台打印出：

```java
before method send
send message:java
after method send
```

###  JDK 动态代理和 CGLIB 动态代理对比

**JDK 动态代理只能代理实现了接口的类或者直接代理接口，而 CGLIB 可以代理未实现任何接口的类**。 另外， CGLIB 动态代理是通过生成一个被代理类的子类来拦截被代理类的方法调用，因此不能代理声明为 final 类型的类和方法。

就二者的效率来说，大部分情况都是 JDK 动态代理更优秀，随着 JDK 版本的升级，这个优势更加明显。

## 静态代理和动态代理的对比

**灵活性** ：动态代理更加灵活，不需要必须实现接口，可以直接代理实现类，并且可以不需要针对每个目标类都创建一个代理类。另外，静态代理中，接口一旦新增加方法，目标对象和代理对象都要进行修改，这是非常麻烦的！

**JVM 层面** ：静态代理在编译时就将接口、实现类、代理类这些都变成了一个个实际的 class 文件。而动态代理是在运行时动态生成类字节码，并加载到 JVM 中的。