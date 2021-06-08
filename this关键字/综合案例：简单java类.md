# 综合案例：简单java类

在进行项目的开发与设计的过程中，简单java类都将作为一个重要的部分存在。所谓的简单java类指的是可以描述某一类信息的程序类：描述一个人、描述一本书……并且在这个类之中并没有特别复杂的逻辑操作，只作为一种信息存储的媒介存在

对于简单java类而言，其核心的开发结构如下：

- 类名称一定要有意义，可以明确的描述某一类事物；
- 类之中的所有属性都必须使用private进行封装，同时封装后的属性必须提供有setter、getter方法
- 类之中可以提供有无数多个构造方法，但必须要保留有无参构造方法
- 类中不允许出现任何的输出语句，所有内容的获取必须返回
- 【非必须】可以提供有一个获取对象详细信息的方法，暂时将此方法名称定义为getInfo()

**范例：**定义一个简单java类

```java
class Dept{  // 类名称可以明确描述出某类事物
    private long deptno;
    private String dname;
    private String loc;
    public Dept(){} // 必须提供有无参的构造方法
    public Dept(long deptno,String dname,String loc){
        this.deptno = deptno;
        this.dname = dname;
        this.loc = loc;
    }
    public String getInfo(){
        return "[部门信息]部门编号："+this.deptno+"、部门名称："+this.dname+"、部门位置："+this.loc;
    }
    public void setDeptno(long deptno){
        this.deptno = deptno;
    }
    public void setDname(String dname){
        this.dname = dname;
    }
    public void setLoc(String loc){
        this.loc = loc;
    }
    public long getDeptno(){
        return this.deptno;
    }
    public String getDname(){
        return this.dname;
    }
    public String getLoc(){
        return this.loc;
    }
}

public class JavaDemo {
    public static void main(String args[]){
        Dept dept = new Dept(10,"技术部","北京");
        System.out.println(dept.getInfo());
    }
}
```

这样的简单Java类基本上融合了所有目前接触到的概念，例如：数据类型划分、类的定义、private封装、构造方法、方法定义、对象实例化