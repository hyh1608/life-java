# this关键字

this算是Java中比较复杂的关键字，因为this的使用形式决定了它的灵活性，在程序中使用this可以实现以下三类结构的描述：

- 当前类中的属性：this.属性
- 当前类中的方法（普通方法、构造方法）：this()、this.方法名称()
- 描述当前对象

# this调用本类属性

利用构造方法或者是setter方法都可以进行类中属性的赋值，但是在进行赋值时，之前采用的是如下的定义形式：

```java
class Person{ // 定义一个类
    private String name;  // 人员的姓名
    private int age;  // 人员的年龄
    // 方法名称与类名称相同，并且无返回值定义
    public Person(String n, int a){ //定义有参构造
        name = n; //为类中的属性赋值(初始化）
        age = a; //为类中的属性赋值(初始化）
    }
    public void tell(){
        System.out.println("姓名："+ name +"、年龄：" + age);
    }
    //setter、getter忽略
}
public class JavaDemo {
    public static void main(String args[]){
//        //1、对象初始化准备
        Person per = new Person("王老五",38); // 声明实例化对象
        per.tell();
    }
}
```

此时构造方法定义的过程中存在一点问题：此时构造方法中两个参数的目的是为了类中的name或age属性初始化，但是此时的代码n和a参数名称不好。如果将构造方法中的参数名称修改为name与age则无法进行属性的正确设置。<font color='red'>下面的代码会报错</font>

```java
 public Person(String name, int age){ //定义有参构造
        name = name; //为类中的属性赋值(初始化）
        age = age; //为类中的属性赋值(初始化）
    }
```

在Java程序中“{}”是作为一个结构体的边界符，那么当进行变量（参数、属性都称为变量）使用的时候都会以“{}”作为一个查找边界，所以按照就近取用的原则，此时的构造方法并没有访问类中的属性，此时为了明确类中的属性与参数的区别，往往会在属性前追加一个“this”表示本类属性。

```java
class Person{ // 定义一个类
    private String name;  // 人员的姓名
    private int age;  // 人员的年龄
    // 方法名称与类名称相同，并且无返回值定义
    public Person(String name, int age){ //定义有参构造
        this.name = name; //为类中的属性赋值(初始化）
        this.age = age; //为类中的属性赋值(初始化）
    }
    public void tell(){
        System.out.println("姓名："+ this.name +"、年龄：" + this.age);
    }
    //setter、getter忽略
}
public class JavaDemo {
    public static void main(String args[]){
//        //1、对象初始化准备
        Person per = new Person("王老五",38); // 声明实例化对象
        per.tell();
    }
}
```

在以后所编写的程序代码之中，只要是访问本类中属性时，一定要加上this实现访问

