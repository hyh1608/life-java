# 声明static方法

static关键字也可以进行方法的定义，static方法的主要特点在于，其可以直接由类名称在没有实例化对象的情况下进行调用。

**范例：**定义static方法

```java
class Person{  // 创建所有同一个国家的类
    private String name;
    private int age;
    private static String country = "中华民国";
    public Person(String name,int age){
        this.name = name;
        this.age = age;
    }
    public static void setCountry(String c){
        country = c;
    }
    // setter、getter略
    public String getInfo(){
        return  "姓名：" + this.name + "、年龄：" + this.age + "、国家："+ this.country;
    }
}

public class JavaDemo {
    public static void main(String args[]){
        Person.setCountry("中华人民共和国"); //用类名称直接调用
        Person per = new Person("zhangsan",10);
        System.out.println(per.getInfo());
    }
}
```

这个时候对于程序而言就有了两种方法：static方法、非static方法，这两个方法在调用上有限制

- static方法只允许调用static属性或static方法；
- 非static方法允许调用static属性或static方法

所有的static定义的属性和方法都可以在没有实例化对象的前提下使用，而所有的非static定义的属性和方法必须要有实例化对象的情况下才可以使用。

> **疑问：**static方法中为什么不能有this
>
> **解释：**所有static方法可以在没有实例化对象的前提下访问，因此setCountry()方法中不能有this，而getInfo()属于非static方法，也使用this

对于之前的方法定义可以得出新的结论：当前定义的方法都是在主类中定义的，并且由主方法直接调用。**static定义和方法只有在回避实例化对象调用并且描述公共属性的情况下才会考虑使用**

```java
public class JavaDemo {
    public static void main(String args[]){
        new JavaDemo().print();
    }
    public void print(){
        System.out.println("www.mldn.cn");
    }
}
```

