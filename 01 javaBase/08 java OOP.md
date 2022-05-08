# 面向对象编程

OOP代表面向对象编程。

## 类和对象

万事万物是对象，鸟、老虎、桌子等等实体都是对象。
类是对象向上抽象出来的模板，或创建对象的“蓝图”。
鸟、老虎我们可以抽象出一个“动物”的模板(类)，这个动物是所有鸟和老虎具有共同特性的模板。

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

## 静态和非静态的区别

静态属性和方法在没创建对象之前就存在，而非静态的需要在创建对象才存在
静态的可以直接通过类名访问，非静态只能通过对象进行访问
所有static修饰的属性和方法都存放在内存的方法区里，而非静态的都存在堆内存中
静态属性是整个类都公用的
静态在类消失后被销毁，非静态在对象销毁后销毁

**使用static的注意事项**

带静态修饰符的方法只能访问静态属性
非静态方法既能访问静态属性也能访问非静态属性
非静态方法不能定义静态变量
静态方法不能使用this关键字
静态方法不能调用非静态方法，反之可以

**父子类中静态和非静态的关系**

对于非静态属性，子类可以继承父类非静态属性
但是当父子类出现相同的非静态属性时，不会发生子类的重写并覆盖父类的非静态属性，而是隐藏父类的非静态属性
对于非静态方法，子类可以继承并重写父类的非静态方法
对于静态属性，子类可以继承父类的静态属性，但是如何和非静态属性一样时，会被隐藏
对于静态方法，子类可以继承父类的静态方法，但是不能重写静态方法，同名时会隐藏父类的
注：静态属性、静态方法、非静态属性都可以被继承和隐藏，但是不可以被重写，非静态方法可以被重写和继承

**静态代码块**
静态代码块只能写在类中方法外，不能写在方法中，它会随着类的加载而优先于各种代码块和构造方法的加载，并且只会
加载一次，如果出现多个静态代码块，会按照书写顺序加载

**静态代码块的作用**

一般情况下，有些代码需要在项目启动的时候就执行，这时候就需要静态代码块，比如一个项目启动需要加载配置文件，或初始化内容等。
静态代码块不能出现在任何方法体内
对于普通方法：普通方法是需要加载类new出一个实例化对象，通过运行这个对象才能运行代码块，而静态方法随着类加载就运行了。
对于静态方法：在类加载时静态方法也加载了，但是必须需要类名或者对象名才可以访问，相比于静态代码块，静态方法是被动运行，而静态代码块是主动运行
静态代码块不能访问普通变量
普通变量只能通过对象调用的，所以普通变量不能放在静态代码块中。

**普通代码块和构造代码块**

静态代码块和构造代码块在声明上少一个static关键字

执行时机：
构造代码块在创建对象时被调用，每次创建对象都会调用一次，且优先于构造函数执行。
注：不是优先于构造函数执行，而是依托于构造函数，如果不创建对象就不会执行构造代码块

普通代码块和构造代码块的区别在于，构造代码块是在类中定于的，而普通代码块是在方法体中定义的，执行顺序和书写顺序一致。

执行顺序：静态代码块>构造代码块>构造函数>普通代码块

## 访问函数

```java
// Create a Main class
public class Main {
 
  // Create a fullThrottle() method
  public void fullThrottle() {
    System.out.println("The car is going as fast as it can!");
  }

  // Create a speed() method and add a parameter
  public void speed(int maxSpeed) {
    System.out.println("Max speed is: " + maxSpeed);
  }

  // Inside main, call the methods on the myCar object
  public static void main(String[] args) {
    Main myCar = new Main();   // Create a myCar object
    myCar.fullThrottle();      // Call the fullThrottle() method
    myCar.speed(200);          // Call the speed() method
  }
}

// The car is going as fast as it can!
// Max speed is: 200
```

1)用class关键字创建了一个自定义的Main类。
2)在Main类中创建了fullThrottle()和speed()方法。
3)fullThrottle()方法和speed()方法在被调用时会打印一些文本。
4)speed()方法接受一个名为maxSpeed的int形参。
5)为了使用Main类及其方法，我们需要创建一个Main类的对象。
6)然后，转到main()方法，你现在知道它是一个运行程序的内置Java方法(main中的任何代码都会被执行)。
7)通过使用new关键字，我们创建了一个名为myCar的对象。
8)然后，我们在myCar对象上调用fullThrottle()和speed()方法
并使用对象的名称(myCar)，后跟一个点(.)
然后是方法的名称(fullThrottle();和速度(200);)。
注意，我们在speed()方法中添加了一个int形参200。

# 构造函数

Java中的构造函数是一种用于初始化对象的特殊方法。创建类的对象时调用构造函数。它可以用来设置对象属性的初始值:

```java
// Create a Main class
public class Main {
  int x;  // Create a class attribute

  // Create a class constructor for the Main class
  public Main() {
    x = 5;  // Set the initial value for the class attribute x
  }

  public static void main(String[] args) {
    Main myObj = new Main(); // Create an object of class Main (This will call the constructor)
    System.out.println(myObj.x); // Print the value of x
  }
}

// Outputs 5
```

构造函数也可以接受参数，用于初始化属性。
下面的示例向构造函数添加了一个int y形参。在构造函数中，我们设置x为y (x=y)。当调用构造函数时，向构造函数(5)传递一个参数，将x的值设置为5:

```java
public class Main {
  int x;

  public Main(int y) {
    x = y;
  }

  public static void main(String[] args) {
    Main myObj = new Main(5);
    System.out.println(myObj.x);
  }
}

// Outputs 5
```

可以多参数：

```java
public class Main {
  int modelYear;
  String modelName;

  public Main(int year, String name) {
    modelYear = year;
    modelName = name;
  }

  public static void main(String[] args) {
    Main myCar = new Main(1969, "Mustang");
    System.out.println(myCar.modelYear + " " + myCar.modelName);
  }
}

// Outputs 1969 Mustang
```

# 修饰符

public关键字是一个访问修饰符，这意味着它用于设置类、属性、方法和构造函数的访问级别。

```java
public class Main
```

我们把修饰语分成两组:

访问修饰符——控制访问级别
非访问修饰符——不控制访问级别，但提供其他功能

## 访问修饰符

对于类，可以使用public或default:

| Modifier  | Description                                            |
| :-------- | :----------------------------------------------------- |
| `public`  | 任何其他类都可以访问这个类                             |
| *default* | 该类只能由同一包中的类访问。当你没有指定修饰语时使用。 |

对于属性、方法和构造函数，可以使用以下方法之一:

| Modifier    | Description                                                  |
| :---------- | :----------------------------------------------------------- |
| `public`    | 所有类都可以访问该代码                                       |
| `private`   | 代码只能在声明的类中访问                                     |
| *default*   | 代码只能在同一个包中访问。当你没有指定修饰语时使用。         |
| `protected` | 代码可以在同一个包和**子类中访问**。你将在继承章节中了解更多关于子类和超类的知识。 |

## 非访问修饰符

对于类，可以使用final或abstract:

| Modifier   | Description                                                  |
| :--------- | :----------------------------------------------------------- |
| `final`    | 这个类不能被其他类继承                                       |
| `abstract` | 这个类成为抽象类，只能用来声明引用，不能用来创建对象，其子类可以继承后用来创建对象。 |

对于属性和方法，可以使用以下方式之一:

| Modifier       | Description                                                  |
| :------------- | :----------------------------------------------------------- |
| `final`        | 属性和方法不能被重写/修改                                    |
| `static`       | 属性和方法属于类，而不是对象                                 |
| `abstract`     | 只能在抽象类中使用，并且只能在方法中使用。该方法没有主体，例如**abstract void run();**。主体由子类提供(继承自)。 |
| `transient`    | 当序列化包含属性和方法的对象时，将跳过它们                   |
| `synchronized` | 方法每次只能由一个线程访问                                   |
| `volatile`     | 属性的值不是线程本地缓存的，而是始终从“主内存”中读取。       |

## final

如果你不想覆盖已有的属性值，可以将属性声明为final:

```java
public class Main {
  final int x = 10;
  final double PI = 3.14;

  public static void main(String[] args) {
    Main myObj = new Main();
    myObj.x = 50; // will generate an error: cannot assign a value to a final variable
    myObj.PI = 25; // will generate an error: cannot assign a value to a final variable
    System.out.println(myObj.x);
  }
}
```

## static

静态方法意味着不需要创建类的对象就可以访问它，与public不同:

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
  public static void main(String[ ] args) {
    myStaticMethod(); // Call the static method
    // myPublicMethod(); This would output an error

    Main myObj = new Main(); // Create an object of Main
    myObj.myPublicMethod(); // Call the public method
  }
}
```

## abstract

一个抽象方法属于一个抽象类，它没有主体。主体由子类提供:

```java
// Code from filename: Main.java
// abstract class
abstract class Main {
  public String fname = "John";
  public int age = 24;
  public abstract void study(); // abstract method
}

// Subclass (inherit from Main)
class Student extends Main {
  public int graduationYear = 2018;
  public void study() { // the body of the abstract method is provided here
    System.out.println("Studying all day long");
  }
}
// End code from filename: Main.java

// Code from filename: Second.java
class Second {
  public static void main(String[] args) {
    // create an object of the Student class (which inherits attributes and methods from Main)
    Student myObj = new Student();

    System.out.println("Name: " + myObj.fname);
    System.out.println("Age: " + myObj.age);
    System.out.println("Graduation Year: " + myObj.graduationYear);
    myObj.study(); // call abstract method  }
}
```