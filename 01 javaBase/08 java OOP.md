# 面向对象

OOP代表面向对象编程。
过程式编程是关于编写对数据执行操作的过程或方法，而面向对象编程是关于创建同时包含数据和方法的对象。
面向对象编程与过程编程相比有几个优势:

- OOP更快，更容易执行
- OOP为程序提供了清晰的结构
- OOP有助于保持Java代码DRY“不要重复自己”，并使代码更容易维护、修改和调试
- OOP使得用更少的代码和更短的开发时间创建完全可重用的应用程序成为可能

> 提示:“不要重复你自己”(DRY)原则是关于减少代码的重复。
> 您应该提取出应用程序通用的代码，并将它们放在单个位置，并重用它们，而不是重复它们。

## 类和对象

类和对象是面向对象编程的两个主要方面。
举例：动物是class(类)，猴子、老虎是Object(对象/实例)。
所以，类是对象的模板，对象是类的实例。
当创建单个对象时，它们从类中继承所有变量和方法。

Java是一种面向对象的编程语言。
Java中的一切都与类和对象相关联，还有它的属性和方法。
例如:在现实生活中，汽车是一个对象。汽车有属性，如重量和颜色，和方法，如驱动和刹车。
类类似于对象构造函数，或创建对象的“蓝图”。

## 创建类

创建一个名为“Main”的类，属性包含一个变量 x:

```java
public class Main {
  int x = 5;
}
```

## 创建一个对象

```java
public class Main {
  int x = 5;

  public static void main(String[] args) {
    Main myObj = new Main();
    System.out.println(myObj.x);
  }
}
```

## 创建多个对象

```java
public class Main {
  int x = 5;

  public static void main(String[] args) {
    Main myObj1 = new Main();  // Object 1
    Main myObj2 = new Main();  // Object 2
    System.out.println(myObj1.x);
    System.out.println(myObj2.x);
  }
}
```

## 使用多个对象

您还可以创建一个类的对象，并在另一个类中访问它。这通常用于更好地组织类(一个类拥有所有属性和方法，而另一个类拥有main()方法(要执行的代码))。
请记住，java文件的名称应该与类名称匹配。在这个例子中，我们在同一个目录/文件夹中创建了两个文件:

- Main.java
- Second.java



Main.java：

```java
public class Main {
  int x = 5;
}
```

Second.java：

```java
class Second {
  public static void main(String[] args) {
    Main myObj = new Main();
    System.out.println(myObj.x);
  }
}
```



```
C:\Users\Your Name>javac Main.java
C:\Users\Your Name>javac Second.java

C:\Users\Your Name>java Second
5
```

# 类属性

## 创建类属性

```java
public class Main {
  int x = 5;
  int y = 3;
}
```

## 访问类属性

```java
public class Main {
  int x = 5;

  public static void main(String[] args) {
    Main myObj = new Main();
    System.out.println(myObj.x);
  }
}
```

## 修改类属性

修改属性值

```java
public class Main {
  int x; //其实默认是0 也是覆盖

  public static void main(String[] args) {
    Main myObj = new Main();
    myObj.x = 40;
    System.out.println(myObj.x);
  }
}
```

也可以覆盖：

```java
public class Main {
  int x = 10;

  public static void main(String[] args) {
    Main myObj = new Main();
    myObj.x = 25; // x is now 25
    System.out.println(myObj.x);
  }
}
```

如果你不想被覆盖现有值，可以声明该属性为final:

```java
public class Main {
  final int x = 10;

  public static void main(String[] args) {
    Main myObj = new Main();
    myObj.x = 25; // will generate an error: cannot assign a value to a final variable
    System.out.println(myObj.x);
  }
}
```

## 多个对象

对象复制类的所有信息生成新对象。
如果你创建一个类的多个对象，你可以改变一个对象的属性值，而不影响另一个对象的属性值:

```java
public class Main {
  int x = 5;

  public static void main(String[] args) {
    Main myObj1 = new Main();  // Object 1
    Main myObj2 = new Main();  // Object 2
    myObj2.x = 25;
    System.out.println(myObj1.x);  // Outputs 5
    System.out.println(myObj2.x);  // Outputs 25
  }
}
```

# 类函数

创建类函数：

```java
public class Main {
  static void myMethod() {
    System.out.println("Hello World!");
  }
}
```

myMethod()在被调用时输出一个文本(动作)。
要调用一个方法，需要在方法名后面加上括号()和一个分号;

```java
public class Main {
  static void myMethod() {
    System.out.println("Hello World!");
  }

  public static void main(String[] args) {
    myMethod();
  }
}
```

## static/non-static方法

您经常会看到Java程序具有静态或公共属性和方法。
在上面的例子中，我们创建了一个静态方法，这意味着可以在不创建类的对象的情况下访问它，而不像public，它只能被对象访问:

```java
public class Main {
  // Static method
  static void myStaticMethod() {
    System.out.println("Static methods can be called without creating objects");
  }

  // Public method
  public void myPublicMethod() {
    System.out.println("Public methods must be called by creating objects");
  }

  // Main method
  public static void main(String[] args) {
    myStaticMethod(); // Call the static method
    // myPublicMethod(); This would compile an error

    Main myObj = new Main(); // Create an object of Main
    myObj.myPublicMethod(); // Call the public method on the object
  }
}
```



- 静态属性和方法在没创建对象之前就存在，而非静态的需要在创建对象才存在
- 静态的可以直接通过类名访问，非静态只能通过对象进行访问
- 所有static修饰的属性和方法都存放在内存的方法区里，而非静态的都存在堆内存中
- 静态属性是整个类都公用的
- 静态在类消失后被销毁，非静态在对象销毁后销毁



使用static的注意事项
带静态修饰符的方法只能访问静态属性
非静态方法既能访问静态属性也能访问非静态属性
非静态方法不能定义静态变量
静态方法不能使用this关键字
静态方法不能调用非静态方法，反之可以
3.父子类中静态和非静态的关系
对于非静态属性，子类可以继承父类非静态属性，但是当父子类出现相同的非静态属性时，不会发生子类的重写并覆盖父类的非静态属性，而是隐藏父类的非静态属性
对于非静态方法，子类可以继承并重写父类的非静态方法
对于静态属性，子类可以继承父类的静态属性，但是如何和非静态属性一样时，会被隐藏
对于静态方法，子类可以继承父类的静态方法，但是不能重写静态方法，同名时会隐藏父类的
注：静态属性、静态方法、非静态属性都可以被继承和隐藏，但是不可以被重写，
       非静态方法可以被重写和继承

4.静态代码块
静态代码块只能写在类中方法外，不能写在方法中，它会随着类的加载而优先于各种代码块和构造方法的加载，并且只会
加载一次，如果出现多个静态代码块，会按照书写顺序加载
1
2
静态代码块的作用：
一般情况下，有些代码需要在项目启动的时候就执行，这时候就需要静态代码块，比如一个项目启动需要加载配置文件，或初始化内容等。
静态代码块不能出现在任何方法体内
对于普通方法：普通方法是需要加载类new出一个实例化对象，通过运行这个对象才能运行代码块，而静态方法随着类加载就运行了。
对于静态方法：在类加载时静态方法也加载了，但是必须需要类名或者对象名才可以访问，相比于静态代码块，静态方法是被动运行，而静态代码块是主动运行
静态代码块不能访问普通变量
普通变量只能通过对象调用的，所以普通变量不能放在静态代码块中。
5.普通代码块和构造代码块
静态代码块和构造代码块在声明上少一个static关键字

执行时机：
构造代码块在创建对象时被调用，每次创建对象都会调用一次，且优先于构造函数执行。
注：不是优先于构造函数执行，而是依托于构造函数，如果不创建对象就不会执行构造代码块

普通代码块和构造代码块的区别在于，构造代码块是在类中定于的，而普通代码块是在方法体中定义的，执行顺序和书写顺序一致。

6.执行顺序
           静态代码块>构造代码块>构造函数>普通代码块
————————————————
版权声明：本文为CSDN博主「久治长安」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_43821892/article/details/90054868