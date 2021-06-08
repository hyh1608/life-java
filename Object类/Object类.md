# Object类

## **Object类的基本概念**

Object类的主要特点是解决参数的统一问题，也就是说使用Object类可以接收所有的数据类型。在Java中只有一个类是不存在继承关系的，这个类就是Object类，也就是说所有的类默认情况下都是Object子类。以下两种类的定义效果完全相同：

```java
Class Person{}   Class Person extends Object{}
```

在Object类设计时考虑了所有继承的问题，所以该类提供无参构造方法，这样所有的类在定义时即便不知道Object类的存在，也不会出现构造方法调用失败的语法错误。

因为Object类是所有类的父类，那么就可以使用Object类接收所有的子类对象

**范例：**观察Object类接收所有子类对象

```java
class Person{ //
    public void print(){
        System.out.println("一个正常的人类行为");
    }
}

public class JavaDemo{
    public static void main(String args[]){
        Object obj = new Person();  // 向上转型
        if (obj instanceof Person){
            Person per = (Person) obj; // 向下转型
            System.out.println("Person对象向下转型执行完毕");
        }
    }
}
```

如果以后一个程序的方法要求可以接收所有类对象时可以利用Object实现处理。需要注意的是，在Java设计的过程中，对于所有的引用数据类型都可以使用Object类进行接收，包括数组也可以。

**范例：**使用Object类接收数组

```java
class Person{ //
    public void print(){
        System.out.println("一个正常的人类行为");
    }
}

public class JavaDemo{
    public static void main(String args[]){
        Object obj = new int[] {1,2,3};  // 向上转型
        if (obj instanceof int[]){
            int[] data = (int[]) obj; // 向下转型
            for (int temp:data){
                System.out.print(temp + "、"); // 1、2、3
            }
        }
    }
}
```

## **取得对象信息toString()**

toString()方法可以获取一个对象的完整信息：public String toString()

**范例：**观察默认的toString()实现

```java
class Person{ //
}

public class JavaDemo{
    public static void main(String args[]){
       Person per = new Person();
       System.out.println(per);
       System.out.println(per.toString());  // Object类继承而来
    }
}
```

在之前进行对象直接输出的时候所调用的就是toString()方法。在以后开发中，对象信息的获得可以覆写此方法。

**范例：**覆写toString()方法

```java
class Person{ //
    private String name;
    private int age;
    public Person(String name,int age){
        this.name = name;
        this.age = age;
    }
    @Override
    public String toString(){
        return "姓名："+this.name+"、年龄："+this.age;
    }
}

public class JavaDemo{
    public static void main(String args[]){
       Person per = new Person("张三",20);
       System.out.println(per); // 姓名：张三、年龄：20
       System.out.println(per.toString());  // 姓名：张三、年龄：20
    }
}
```

在编写简单Java类的过程中只要覆写toString()方法即可

## **对象比较：equals()**

对象比较指的是比较两个对象的内容是否完全相同。若现在有两个Person对象，要想确认两个对象是否一致，但是两个对象本身会有不同的内存地址数值，所以比较应该是通过内容的比较完成

**范例：**对象比较的基础实现

```java
class Person{ //
    private String name;
    private int age;
    public Person(String name,int age){
        this.name = name;
        this.age = age;
    }
    @Override
    public String toString(){
        return "姓名："+this.name+"、年龄："+this.age;
    }
    public String getName(){
        return this.name;
    }
    public int getAge(){
        return this.age;
    }
}

public class JavaDemo{
    public static void main(String args[]){
       Person perA = new Person("张三",20);
       Person perB = new Person("张三",20);
       if (perA.getName().equals(perB.getName()) && perA.getAge() == perB.getAge()){
           System.out.println("是同一个对象");
       }else {
           System.out.println("不是同一个对象");
       }
    }
}
```

可以通过equals()实现对象比较的功能，但是：

- 由于需要进行对象比较时要将每一个属性都进行相等判断，所以在外部要调用大量的getter()方法
- 对象比较应该是类内部所具备的功能，而不应该在外部定义
- 对象比较：**public boolean equals(**[**Object**](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) **obj)，可以接收所有类型，默认情况下只是进行了两个对象的地址判断，也就是说要想正确实现判断处理，必须在子类中覆写此方法，并且进行属性判断。**

```java
public boolean equals(Object obj) { return (this == obj)};
```

Object作为所有类的父类，提供了对象比较操作的支持，对于对象比较的操作实现可以使用equals()方法完成：

**范例：**观察Object类中equals()方法覆写

```java
class Person{ //
    private String name;
    private int age;
    public Person(String name,int age){
        this.name = name;
        this.age = age;
    }
    @Override
    public String toString(){
        return "姓名："+this.name+"、年龄："+this.age;
    }
    public boolean equals(Object obj){
        if (!(obj instanceof Person)){
            return false;
        }
        if (obj == null){//不关心null的比较
            return false;
        }
        if (this == obj){
            return true;
        }
        Person per = (Person) obj;  // 目的是为了获取类中的属性，向下转型
        return this.name.equals(per.name) && this.age == per.age;
    }
}

public class JavaDemo{
    public static void main(String args[]){
       Person perA = new Person("张三",20);
       Person perB = new Person("张三",20);
       System.out.println(perA.equals(perB));
       System.out.println(perA.equals(perA));
    }
}
```

