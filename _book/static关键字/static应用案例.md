# static应用案例

**范例：**编写一个程序类，这个类可以实现实例化对象个数的统计，每一次创建新的实例化对象都可以实现一个统计操作

- 此时可以单独创建一个static属性，因为所有对象对共享同一个static属性，那么在构造方法中实现数据的统计处理

```java
class Book{
    private String title;
    private static int count = 0;
    public Book(String title){
        this.title = title;
        this.count ++;
        System.out.println("第"+this.count+"本书创建完成");
    }
}
public class JavaDemo {
    public static void main(String args[]){
        new Book("java");
        new Book("python");
        new Book("hadoop");
    }
}
```

**范例：**实现属性的自动命名处理

- 如果现在传递了title属性，就用传递的属性内容，而如果没有传递title属性，则自动采用“NOTITLE-编号”的形式进行该属性内容的定义。

```java
class Book{
    private String title;
    private static int count = 0;
    public Book(){
        this("NOTITILE - "+ count++);
    }
    public Book(String title){
        this.title = title;
//        System.out.println("第"+this.count+"本书创建完成");
    }
    public String getTitle(){
        return this.title;
    }
}
public class JavaDemo {
    public static void main(String args[]){
        System.out.println(new Book("java").getTitle()); //java
        System.out.println(new Book("python").getTitle()); //python
        System.out.println(new Book("hadoop").getTitle()); //hadpoop
        System.out.println(new Book().getTitle()); //NOTITILE - 0
        System.out.println(new Book().getTitle()); // NOTITILE - 1
    }
}
```

这样处理的好处是可以避免在没有设置title属性时内容为null的重复问题

