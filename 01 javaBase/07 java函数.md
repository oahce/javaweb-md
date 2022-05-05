# 函数

方法是一段代码，它只在被调用时运行。
您可以将称为参数的数据传递到方法中。
方法用于执行某些操作，它们也称为函数。
为什么使用方法?重用代码:定义代码一次，然后多次使用。

## 创建函数

必须在类中声明方法。它由方法的名称定义,后面是括号()。
Java提供了一些预先定义的方法,例如System.out.println(),但是您还可以创建自己的方法来执行某些操作:

```java
public class Main {
  static void myMethod() {
    // code to be executed
  }
}
```

myMethod()是该方法的名称。
static表示该方法属于Main类，而不是Main类的对象。
在本教程后面，您将学习更多关于对象以及如何通过对象访问方法的知识。
Void表示该方法没有返回值。

## 调用函数

要在Java中调用一个方法，需要在方法名后面加上两个括号()和一个分号;
在下面的例子中，当myMethod()被调用时，它被用来打印文本(动作):

```java
public class Main {
  static void myMethod() {
    System.out.println("I just got executed!");
  }

  public static void main(String[] args) {
    myMethod();
  }
}

// Outputs "I just got executed!"
```

一个方法也可以被多次调用:

```java
public class Main {
  static void myMethod() {
    System.out.println("I just got executed!");
  }

  public static void main(String[] args) {
    myMethod();
    myMethod();
    myMethod();
  }
}

// I just got executed!
// I just got executed!
// I just got executed!
```

## 传递参数

### 形参和实参

信息可以作为参数传递给方法。参数充当方法中的变量。
参数在方法名之后的圆括号内指定。您可以添加任意多的参数，只需用逗号分隔即可。

形参 ：
形式参数，用于定义方法的时候使用的参数，是用来接收调用者传递的参数的。
形参只有在方法被调用的时候，虚拟机才会分配内存单元，在方法调用结束之后便会释放所分配的内存单元。 
因此,形参只在方法内部有效，所以针对引用对象的改动也无法影响到方法外。

实参 ：
实际参数，用于调用时传递给方法的参数。
实参在传递给别的方法之前是要被预先赋值的。 

> 注意:
> 在值传递调用过程中，只能把实参传递给形参，而不能把形参的值反向作用到实参上。
> 在函数调用过程中，形参的值发生改变，而实参的值不会发生改变。
> 而在引用传递调用的机制中，实际上是将实参引用的地址传递给了形参，所以任何发生在形参上的改变也会发生在实参变量上。


下面的例子有一个方法，它接受一个名为fname的字符串作为参数。当方法被调用时，我们传递一个名字，在方法内部使用它来打印全名:

```java
public class Main {
  static void myMethod(String fname) {
    System.out.println(fname + " Refsnes");
  }

  public static void main(String[] args) {
    String name1 = "Liam";
    myMethod(name1);
    myMethod("Jenny");
    myMethod("Anja");
  }
}
// Liam Refsnes
// Jenny Refsnes
// Anja Refsnes
```

myMethod函数的fname就是形参，name1就是实参。
形参出现在**函数定义**中，在整个函数体内都可以使用，离开该函数则不能使用。
实参出现在**主调函数中，进入被调函数后，实参变量也不能使用**。 
实参可以是常量、变量、表达式、函数等.
无论实参是何种类型的量，在进行函数调用时，它们都必须具有确定的值， 以便把这些值传送给形参。 因此应预先用赋值，输入等办法使实参获得确定值。 

### 多个参数

```java
public class Main {
  static void myMethod(String fname, int age) {
    System.out.println(fname + " is " + age);
  }

  public static void main(String[] args) {
    myMethod("Liam", 5);
    myMethod("Jenny", 8);
    myMethod("Anja", 31);
  }
}

// Liam is 5
// Jenny is 8
// Anja is 31
```

### 返回值

在上面的例子中使用的void关键字表明该方法不应该返回值。
如果你想让方法返回一个值，你可以使用原始数据类型(比如int, char等)而不是void，并在方法内部使用return关键字:

```java
public class Main {
  static int myMethod(int x) {
    return 5 + x;
  }

  public static void main(String[] args) {
    System.out.println(myMethod(3));
  }
}
// Outputs 8 (5 + 3)
```

这个例子返回一个方法的两个参数之和:

```java
public class Main {
  static int myMethod(int x, int y) {
    return x + y;
  }

  public static void main(String[] args) {
    System.out.println(myMethod(5, 3));
  }
}
// Outputs 8 (5 + 3)
```

你也可以将结果存储在一个变量中(推荐，因为它更容易阅读和维护):

```java
public class Main {
  static int myMethod(int x, int y) {
    return x + y;
  }

  public static void main(String[] args) {
    int z = myMethod(5, 3);
    System.out.println(z);
  }
}
// Outputs 8 (5 + 3)
```

## 函数重载

通过方法重载，多个方法可以具有相同的名称和不同的参数:

```java
int myMethod(int x)
float myMethod(float x)
double myMethod(double x, double y)
```

考虑下面的例子，它有两个添加不同类型数字的方法:

```java
static int plusMethodInt(int x, int y) {
  return x + y;
}

static double plusMethodDouble(double x, double y) {
  return x + y;
}

public static void main(String[] args) {
  int myNum1 = plusMethodInt(8, 5);
  double myNum2 = plusMethodDouble(4.3, 6.26);
  System.out.println("int: " + myNum1);
  System.out.println("double: " + myNum2);
}
```

与其定义两个应该做相同事情的方法，不如重载一个方法。
在下面的例子中，我们重载了plusMethod方法，使其同时适用于int和double:

```java
static int plusMethod(int x, int y) {
  return x + y;
}

static double plusMethod(double x, double y) {
  return x + y;
}

public static void main(String[] args) {
  int myNum1 = plusMethod(8, 5);
  double myNum2 = plusMethod(4.3, 6.26);
  System.out.println("int: " + myNum1);
  System.out.println("double: " + myNum2);
```



# 作用域

在Java中，变量只能在创建它们的区域内访问。这叫做作用域。

## 函数的作用域

直接在方法内部声明的变量，可以在声明它们的代码行之后的任何地方使用(方法内部):

```csharp
public class Main {
  public static void main(String[] args) {

    // Code here CANNOT use x

    int x = 100;

    // Code here can use x
    System.out.println(x);
  }
}
```

## 块作用域

代码块指的是花括号{}之间的所有代码。
在代码块中声明的变量只能由声明变量所在行的花括号之间的代码访问:

```csharp
public class Main {
  public static void main(String[] args) {
    // Code here CANNOT use x
    { // This is a block
      // Code here CANNOT use x
      int x = 100;
      // Code here CAN use x
      System.out.println(x);
   } // The block ends here
  // Code here CANNOT use x
  }
}
```

# 函数递归

递归是调用函数本身的技术。这种技术提供了一种将复杂问题分解为更容易解决的简单问题的方法。
递归可能有点难以理解。弄清楚它是如何工作的最好方法就是进行实验。

## 递归举例

两个数字相加很容易，但一组数字相加就复杂多了。
在下面的例子中，递归被用来将一个范围内的数字相加，方法是将其分解为两个数字相加的简单任务:

```csharp
//把10之内的所有整数相加
public class Main {
  public static void main(String[] args) {
    int result = sum(10);
    System.out.println(result);
  }
  public static int sum(int k) {
    if (k > 0) {
      return k + sum(k - 1);
    } else {
      return 0;
    }
  }
}
```

当sum()函数被调用时，它将参数k加到所有小于k的数字的和上，并返回结果。当k = 0时，函数返回0。运行时，程序遵循以下步骤:

```
10 + sum(9)
10 + ( 9 + sum(8) )
10 + ( 9 + ( 8 + sum(7) ) )
...
10 + 9 + 8 + 7 + 6 + 5 + 4 + 3 + 2 + 1 + sum(0)
10 + 9 + 8 + 7 + 6 + 5 + 4 + 3 + 2 + 1 + 0
```

## 停止条件

就像循环会遇到无限循环的问题一样，递归函数也会遇到无限循环的问题。
无限递归是指函数永不停止调用自身。每个递归函数都应该有一个暂停条件，也就是函数停止调用自身的条件。
在前面的示例中，暂停条件是当参数k变为0时。
看到各种不同的例子有助于更好地理解这个概念。

```java
public class Main {
  public static void main(String[] args) {
    int result = sum(5, 10);
    System.out.println(result);
  }
  public static int sum(int start, int end) {
    if (end > start) {
      return end + sum(start, end - 1);
    } else {
      return end;
    }
  }
}
```