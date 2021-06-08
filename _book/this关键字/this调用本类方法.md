# this调用本类方法

除了调用属性之外，this也可以实现方法的调用，但是对于方法的调用就必须考虑构造与普通方法

- 构造方法调用(this())：使用关键字new实例化对象的时候才会调用构造方法
- 普通方法调用(this.方法名称()):实例化对象产生之后就可以调用普通方法

**范例：**调用类中的普通方法

```java
class Person{ // 定义一个类
    private String name;  // 人员的姓名
    private int age;  // 人员的年龄
    // 方法名称与类名称相同，并且无返回值定义
    public Person(String name, int age){ //定义有参构造
        this.setName(name);
        setAge(age);  // 加与不加都表示本类方法
    }
    public void tell(){
        System.out.println("姓名："+ this.name +"、年龄：" + this.age);
    }
    public void setName(String name){
        this.name = name;
    }
    public void setAge(int age){
        this.age = age;
    }
    public String getName(){
        return this.name;
    }
    public int getAge(){
        return this.age;
    }
}
public class JavaDemo {
    public static void main(String args[]){
//        //1、对象初始化准备
        Person per = new Person("王老五",38); // 声明实例化对象
        per.tell();
    }
}
```

除了普通的方法调用之外，还需要进行构造方法的调用，对于构造方法，需要放在构造方法中执行。假设类中一共定义三个构造方法，但是要求不管调用哪个构造方法，都执行一行输出语句“一个新的Person类对象实例化”

**范例：**传统做法实现

```java
class Person{ // 定义一个类
    private String name;  // 人员的姓名
    private int age;  // 人员的年龄
    // 方法名称与类名称相同，并且无返回值定义
    public Person(){
        System.out.println("*** 一个新的Person类对象实例化");
    }
    public Person(String name){
        this.name = name;
        System.out.println("*** 一个新的Person类对象实例化");
    }
    public Person(String name,int age){
        this.name = name;
        this.age = age;
        System.out.println("*** 一个新的Person类对象实例化");
    }

    public void tell(){
        System.out.println("姓名："+ this.name +"、年龄：" + this.age);
    }

}
public class JavaDemo {
    public static void main(String args[]){
//        //1、对象初始化准备
        Person per = new Person("王老五"); // 声明实例化对象
        per.tell();
    }
}
```

要想**评价一个代码的好坏**：

- 代码结构可以重用：提供的是一个中间独立的支持；	
- 目标是：没有重复代码；

对于本类构造方法的互相调用需要注意以下几点重要问题：

- 构造方法必须在实例化新对象时调用，所以“this()”的语句只允许放在构造方法的首行，<font color='red'>在构造方法中可以调用普通方法，而在普通方法中不可以调用构造方法</font>
- 构造方法互相调用时，请保留程序的出口，别形成死循环

**范例**：利用this（）构造进行优化

```java
class Person{ // 定义一个类
    private String name;  // 人员的姓名
    private int age;  // 人员的年龄
    // 方法名称与类名称相同，并且无返回值定义
    public Person(){
        System.out.println("*** 一个新的Person类对象实例化");
    }
    public Person(String name){
        this();  // 调用本类无参构造
        this.name = name;
    }
    public Person(String name,int age){
        this(name);  //调用本类单参构造
        this.age = age;
    }
    public void tell(){
        System.out.println("姓名："+ this.name +"、年龄：" + this.age);
    }
}
public class JavaDemo {
    public static void main(String args[]){
//        //1、对象初始化准备
        Person per = new Person("王老五",15); // 声明实例化对象
        per.tell();
    }
}
```

**构造方法相互调用**

现在要求定义一个描述员工信息的程序类，该类中有：编号、姓名、部门、工资，在这个类中提供有四个构造方法

- 【无参构造】编号定义为1000，姓名定义为无名氏；
- 【单参构造】传递编号，姓名定义为“新员工”，部门定义为“未定”，工资为0
- 【三参构造】传递编号，姓名、部门，工资为2500.00；
- 【四参构造】所有属性全部进行传递

**范例：**进行代码初期实现

```java
class Emp{
    private long empno;  //员工编号
    private String ename;  //员工姓名
    private String dept;  //部门名称
    private double salary;  //基本工资
    public Emp(){
        this.empno = 1000;
        this.ename = "无名氏";
    }
    public Emp(long empno){
        this.empno = empno;
        this.ename = "新员工";
        this.dept = "未定";
    }
    public Emp(long empno,String ename,String dept){
        this.empno = empno;
        this.ename = ename;
        this.dept = dept;
    }
    public Emp(long empno,String ename,String dept,double salary){
        this.empno = empno;
        this.ename = ename;
        this.dept = dept;
        this.salary = salary;
    }
    public String getInfo(){
        return "雇员编号：" + this.empno +
                "、雇员姓名：" + this.ename +
                "、所在部门：" + this.dept +
                "、基本工资：" + this.salary;
    }
}

public class JavaDemo {
    public static void main(String args[]){
        Emp emp = new Emp(7369L,"史密斯","财务部",6500.00);
        System.out.println(emp.getInfo());
    }
}
```

上述有很多的重复代码，所以可以对Emp类进行简化定义。代码的任何位置上都可能有重复，消除重复代码非常重要

**范例：**简化代码

```java
class Emp{
    private long empno;  //员工编号
    private String ename;  //员工姓名
    private String dept;  //部门名称
    private double salary;  //基本工资
    public Emp(){
        this(1000,"无名氏",null,0.0);
    }
    public Emp(long empno){
        this(empno,"新员工","未定",0.0);
    }
    public Emp(long empno,String ename,String dept){
        this(empno,ename,dept,2500.00);
    }
    public Emp(long empno,String ename,String dept,double salary){
        this.empno = empno;
        this.ename = ename;
        this.dept = dept;
        this.salary = salary;
    }
    public String getInfo(){
        return "雇员编号：" + this.empno +
                "、雇员姓名：" + this.ename +
                "、所在部门：" + this.dept +
                "、基本工资：" + this.salary;
    }
}

public class JavaDemo {
    public static void main(String args[]){
        Emp emp = new Emp(7369L,"史密斯","财务部");
        System.out.println(emp.getInfo());
    }
}
```

