# 环境准备

## java安装

检查java安装：

```
java -version

java version "11.0.1" 2018-10-16 LTS
Java(TM) SE Runtime Environment 18.9 (build 11.0.1+13-LTS)
Java HotSpot(TM) 64-Bit Server VM 18.9 (build 11.0.1+13-LTS, mixed mode)
```

1. JAVA_HOME: your file path
2. PATH: %JAVA_HOME%\bin   

## 第一个java程序

**新建HelloWorld.java文件**

在Java中，每个应用程序都以一个类名开始，并且这个类必须与文件名匹配。
让我们创建第一个Java文件HelloWorld.java，它可以在任何文本编辑器(如记事本)中完成。
该文件应该包含一个“Hello World”消息，它是用以下代码编写的:

```java
public class HelloWorld {
  public static void main(String[] args) {
    System.out.println("Hello World");
  }
}
```

**在当前文件夹下执行命令**

打开命令提示符(cmd.exe)，导航到你保存文件的目录，输入"javac HelloWorld.java":

```
C:\Users\Your Name>javac HelloWorld.java
C:\Users\Your Name>java HelloWorld
```

输出应该为:

```
Hello World
```



# java变量

变量是存储数据值的容器，在Java中，有不同类型的变量。

## 声明变量

要创建一个变量，你必须指定它的类型并给它赋值:

```java
type variableName = value;
```

其中type是Java类型之一(比如int、String)等， variableName是变量的名称(比如x或name)，等号用于给变量赋值。
要创建一个应该存储文本的变量，请看下面的例子:

```java
//创建一个数据类型为String 名为name的变量，并将其赋值为“John”:
String name = "John";
System.out.println(name);
//要创建一个应该存储数字的变量，请看下面的例子:
int myNum = 15;
System.out.println(myNum);
```

注意，如果你给一个现有的变量赋一个新值，它会覆盖之前的值:

```java
int myNum = 15;
myNum = 20;  // myNum is now 20
System.out.println(myNum);
```

## final定义变量(常量)

如果你不希望别人(或你自己)覆盖现有的值，使用final关键字(这将声明变量为“final”或“constant”，这意味着不可更改和只读):

```java
final int myNum = 15;
myNum = 20;  // will generate an error: cannot assign a value to a final variable
```

其他类型的举例：

```java
int myNum = 5;
float myFloatNum = 5.99f;
char myLetter = 'D';
boolean myBool = true;
String myText = "Hello";
```

## 声明多个变量

```java
int x = 5;
int y = 6;
int z = 50;
System.out.println(x + y + z);
//也可以：
int x = 5, y = 6, z = 50;
System.out.println(x + y + z);
//或者，定义后赋值
int x, y, z;
x = y = z = 50;
System.out.println(x + y + z);
```

## 标识符

所有Java变量都必须用惟一的名称标识，这些惟一名称称为标识符。
标识符可以是短名称(如x和y)或更具描述性的名称(年龄、总和、totalVolume)。
注意:为了创建易于理解和维护的代码，建议使用描述性名称:

```java
// Good
int minutesPerHour = 60;

// OK, but not so easy to understand what m actually is
int m = 60;
```

变量命名的一般规则如下:

- 名称可以由字母、数字、下划线和美元符号组成
- 名字必须以字母开头
- 名称应以小写字母开头，不能包含空格
- 名称也可以以$和_开头(但我们不会在本教程中使用它)
- 名称区分大小写(“myVar”和“myVar”是不同的变量)
- 保留字(如Java关键字，如int或boolean)不能用作名称