# Java面向对象学习的三条主线

## Java类和类的成员：属性、方法、构造器、代码块、内部类

### 设计类

- 属性：对应类中的成员变量（field  域、字段）
- 方法：对应类中的成员方法（method  函数）
- 创建类的对象：实例化类、类的实例化

### 类和对象的使用

- 创建类，设计类的成员
- 创建类的对象
- 通过对象.属性/对象.方法调用对象的结构

### 如果创建了一个类的多个对象，每个对象都独立拥有一套类的属性（非static）

如果我们修改一个对象属性的值，不影响另外一个对象同属性的值

### 对象的内存解析

- 通常所说的栈是指虚拟机栈
- 堆（heap）的唯一目的就是存放对象实例
- 方法区用于存储已被虚拟机加载的类信息、常量、静态变量、即时编译器编译后的代码等数据

```java
Person p1 = new Person( ) ;
p1.name = "Tom";
p1.isMale = true;
Person p2 = new Person();
System.out.print(p2.name);//null
Person p3= p1;//在堆中和p1共用同一存储空间
p3.age = 10;//此时p1.age = 10
```

### 类中属性的使用

- 成员变量与局部变量：

1. 不同点：

   1）在类中声明的位置不同：属性直接定义在类的{}内；局部变量声明在方法内、方法形参、代码块内、构造器形参、构造器内部的变量

   2）权限修饰符不同：属性可以在声明时指明其权限，使用权限修饰符（常用的权限修饰符：private、public、缺省、protected）；局部变量不可以使用权限修饰符

   3）默认初始化值：类的属性根据其类型都有默认初始化值；局部变量没有默认初始化值，在调用前需要显式赋值，特别地，形参在调用时赋值即可

   4）在内存中加载的位置不同：属性加载在堆中（非static）；局部变量加载在栈空间中

2. 相同点：

   1）定义变量的格式、数据类型

   2）先声明，后使用

   3）变量都有其对应的作用域

### 类中方法的声明和使用

- 方法：描述类应该具有的功能

- 方法的声明：

  权限修饰符 返回值类型 方法名（形参列表）{

  ​				方法体

  }

- 说明：

  1.关于权限修饰符

  2.返回值类型：

  如果方法有返回值，必须在方法声明时指定返回值类型，方法中使用return返回指定类型的变量或常量；如果方法没有返回值，声明时使用void表示，如果使用“return;”表示结束此方法

  3.方法名：属于标识符，“见名知意”

  4.形参列表：可以声明零到多个形参

  5.方法体：方法功能的实现

- return关键词的使用：

  使用在方法体中，用于结束方法、针对有返回值类型的方法，使用“return”数据方法返回所要的值；在return语句后不能声明执行语句

- 方法使用时，可以调用当前类的属性和方法

### 构造器（constructor）的使用

- 构造器的作用：

  1.创建对象

  2.初始化对象的信息

- 说明：

  1.如果没有显式的定义类的构造器的话，则系统默认提供一个空参的构造器

  2.定义构造器的格式：权限修饰符 类名（形参列表）{}

  3.一个类中定义的多个构造器，彼此构成重载

  4.一旦我们显式的定义了类的构造器之后，系统就不再提供默认的空参构造器

  5.一个类中至少有一个构造器

  - 

```java
public class PersonTest{
    public static void main(String[] args){
        //创建类的对象：new + 构造器
        Person p = new Person();
        
        p.eat();
        
        Person p1 = new Person("Tom");
        p1.eat();
    }
    class Person{
        //属性
        String name;
        int age;
        //构造器
        public Person(){
            System.out.println("Person()......")
        }

        public Person(String n){
            name = n;
        }
        
        public Person(String n, int a){
            name = n;
            age = a;
        }
        //方法
        public void eat(){
            System.out.println("人吃饭")；
        }
    }
}    
```

- this的使用：

  1.this可以用来修饰、调用：属性、方法、构造器

  2.this修饰属性和方法：理解为“当前对象”或当前正在创建的对象

  ​	1）在类的方法中，我们可以使用"this.属性"或"this.方法"的方式，调用当前对象属性或方法。但是，
  通常情况下，我们都选择省略"this."。特殊情况下，如果方法的形参和类的属性同名时，我们必须显式
  的使用"this.变量"的方式，表明此变量是属性，而非形参。

  ​	2）在类的构造器中，我们可以使用"this.属性"或"this.方法"的方式，调用当前对象属性或方法。但是
  通常情况下，我们都选择省略"this.“。特殊情况下，如果方法的形参和类的属性同名时，我们必须显式
  的使用"this.变量"的方式，表明此变量是属性，而非形参。

  3.this调用构造器：

  ​	1）我们在类的构造器中，可以显式的使用"this (形参列表) "方式，调用本类中指定的其他构造器
  ​	2）构造器中不能通过"this (形参列表)"方式调用自己
  ​	3）如果一个类中有n个构造器，则最多有n - 1构造器中使用 了"this (形参列表)"（不能形成闭环）

  ​    4）规定，"this (形参列表) "必须声明在当前构造器的首行
  ​    5）构造器内部，最多只能声明一个"this(形参列表)"，用来调用其他的构造器

```java
public class PersonTest {
	public static void main(String[] args) {
		
        Person p1 = new Person();
		
        p1.setAge(1);
		
        System.out.print1n(p1.getAge());
        
        p1.eat();
        
        System.out.println();
        
        Person p2 = new Person("Jerry", 20);
	}
}

class Person{
    
	private String name;
	private int age;
    
    public Person( ){
		this.eat(); 
		//Person初始化时，需要考虑如下的
	}
	public Person(String name){
		this();//调用空参构造器
        this.name = name;
	}
	public Person(int age){
		this.age = age;
	}
	public Person(String name,int age){
        this(age);//调用int构造器
		this.name = name;
		this.age = age;//作用重复了可以去掉
	}

    
	public void setName(String name){
		this.name = name;
	}
    
	public String getName(){
		return name;
	}
	public void setAge(int age){
		this.age = age;
	}
	public int getAge(){
		return age;
	}
    public void eat(){
    System.out.println("人吃饭")；
	}
}
```







