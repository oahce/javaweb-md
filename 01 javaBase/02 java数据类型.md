# 数据类型

正如前一章所解释的，Java中的变量必须指定数据类型:

```java
int myNum = 5;               // Integer (whole number)
float myFloatNum = 5.99f;    // Floating point number
char myLetter = 'D';         // Character
boolean myBool = true;       // Boolean
String myText = "Hello";     // String
```

数据类型分为两组:
原始(基本)数据类型：包括byte、short、int、long、float、double、boolean和char
非基本数据类型(引用类型)：如字符串，数组和类(你将在后面的章节中了解更多)

## 1. 原始数据类型

原始数据类型指定变量值的大小和类型，它没有其他方法。
在Java中有八种基本数据类型:

| Data Type | Size    | Description                                                  |
| :-------- | :------ | :----------------------------------------------------------- |
| `byte`    | 1 byte  | Stores whole numbers from -128 to 127                        |
| `short`   | 2 bytes | Stores whole numbers from -32,768 to 32,767                  |
| `int`     | 4 bytes | Stores whole numbers from -2,147,483,648 to 2,147,483,647    |
| `long`    | 8 bytes | Stores whole numbers from -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| `float`   | 4 bytes | Stores fractional numbers. Sufficient for storing 6 to 7 decimal digits |
| `double`  | 8 bytes | Stores fractional numbers. Sufficient for storing 15 decimal digits |
| `boolean` | 1 bit   | Stores true or false values                                  |
| `char`    | 2 bytes | Stores a single character/letter or ASCII values             |

原始数类型分为两类:
整数类型存储整数，正数或负数(如123或-456)，不包含小数。有效的类型有byte、short、int和long。您应该使用哪种类型，取决于数值。
浮点类型表示带有小数部分的数字，其中包含一个或多个小数。有两种类型:float和double。

> 尽管Java中有很多数字类型，但最常用的是int(整数)和double(浮点数)。然而，我们将在您继续阅读时描述它们。

### 整数类型(Integer Types)

#### byte

byte数据类型可以存储从-128到127的整数。当你确定值将在-128和127之间时，可以使用该值代替int或其他整数类型来节省内存:

```java
byte myNum = 100;
System.out.println(myNum);
```

#### short

short数据类型可以存储从-32768到32767的整数:

```java
short myNum = 5000;
System.out.println(myNum);
```

#### int

int数据类型可以存储从-2147483648到2147483647的整数。通常，在本教程中，当我们创建带有数字值的变量时，int数据类型是首选的数据类型。

```java
int myNum = 100000;
System.out.println(myNum);
```

#### long

long数据类型可以存储从-9223372036854775808到9223372036854775807的整数。当int值不够大，无法存储值时使用。注意，你应该以“L”结束值:

```java
long myNum = 15000000000L;
System.out.println(myNum);
```

### 浮点类型

**Floating Point Types**

当您需要一个带小数的数字时，例如9.99或3.14515，您应该使用浮点类型。
float和double数据类型可以存储小数。注意，你应该用"f"表示浮点数，用"d"表示双精度值:

```java
float myNum = 5.75f;
System.out.println(myNum);
double myNum = 19.99d;
System.out.println(myNum);
```

> 使用float还是double?
>
> 浮点值的精度表示该值在小数点后可以有多少位。
> float的精度只有6或7位十进制数字，而double变量的精度约为15位。因此，在大多数计算中使用double比较安全。

### **科学数据**

浮点数也可以是科学数字，用“e”表示10的幂:

```java
float f1 = 35e3f;
double d1 = 12E4d;
System.out.println(f1);
System.out.println(d1);
```

### 布尔类型

布尔数据类型使用boolean关键字声明，只能接受true或false值:

```java
boolean isJavaFun = true;
boolean isFishTasty = false;
System.out.println(isJavaFun);     // Outputs true
System.out.println(isFishTasty);   // Outputs false
```

### char类型

char数据类型用于存储单个字符。字符必须用单引号括起来，比如'A'或'c':

```java
char myGrade = 'B';
System.out.println(myGrade);
```

或者，如果您熟悉ASCII值，您可以使用它们来显示某些字符:

```java
char myVar1 = 65, myVar2 = 66, myVar3 = 67;
System.out.println(myVar1);
System.out.println(myVar2);
System.out.println(myVar3);
```

> 所有ASCII值的列表可以在我们的ASCII表参考中找到。

### 字符串类型(特殊/引用类型)

String数据类型用于存储字符序列(文本)。字符串值必须用双引号括起来:

```java
String greeting = "Hello World";
System.out.println(greeting);
```

> String类型在Java中使用和集成得如此之多，以至于有人把它称为“特殊的第九种类型”。
> Java中的String实际上是非原始(引用)数据类型，因为它引用的是对象。
> String对象具有用于对字符串执行某些操作的方法。
> 如果您还不理解术语“对象”，请不要担心。我们将在后面的章节中学习更多关于字符串和对象的知识。

## 2. 引用类型

**引用(非基本)数据类型**

非基元数据类型称为引用类型，因为它们引用对象。
基本数据类型和非基本数据类型的主要区别是:

- 基本类型在Java中是预定义的(已经定义了)。非原语类型是由程序员创建的，不是由Java定义的(String除外)。
- 非原语类型可用于调用方法来执行某些操作，而原语类型则不能。
- 原始类型总是有一个值，而非原始类型可以为空。
- 原始类型以小写字母开头，而非原始类型以大写字母开头。
- 原始类型的大小取决于数据类型，而非原始类型的大小都相同。

> 非基本类型的例子有字符串、数组、类、接口等。您将在后面的章节中了解更多。

# 类型转换

类型转换是将一种基本数据类型的值赋给另一种类型。
在Java中，有两种类型的类型转换:

- 扩大转换(自动) - 将较小的类型转换为较大的类型byte-> short -> char -> int -> long -> float -> double
- 收缩转换(手动) - 将较大的类型转换为较小的类型double -> float -> long -> int -> char -> short -> byte

## 自动转换(扩大范围)

当将较小范围的类型传递给较大范围的类型时，会自动进行扩展类型转换:

```java
public class Main {
  public static void main(String[] args) {
    int myInt = 9;
    double myDouble = myInt; // Automatic casting: int to double

    System.out.println(myInt);      // Outputs 9
    System.out.println(myDouble);   // Outputs 9.0
  }
}
```

## 手动转换(缩小范围)

缩小范围的类型转换必须手动完成，将类型放在值前的圆括号中:

```java
public class Main {
  public static void main(String[] args) {
    double myDouble = 9.78d;
    int myInt = (int) myDouble; // Manual casting: double to int

    System.out.println(myDouble);   // Outputs 9.78
    System.out.println(myInt);      // Outputs 9
  }
}
```