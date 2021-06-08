# foreach输出

对于数组而言，一般会使用for循环进行输出，但是在传统for循环输出的时候往往都采用了下标的形式进行数组元素的访问

**范例：**传统形式

```java
public class ArrayDemo {
    public static void main(String[] args){
        // 使用数组的动态初始化实现了数组的定义
        int data[] = new int[] {1,2,3,4,5};
        for (int x = 0; x < data.length; x++){
            System.out.println(data[x]);
        }
    }
}
```

从jdk1.5之后为了减轻下标对程序的影响（如果下标处理不当会出现数组越界异常），所以参考了.NET的设计，引入了一个增强型的for循环（foreach），利用foreach的语法结构可以自动获取数组中的每一个元素，避免下标访问。

<font color='red'>foreach语法形式：for (数据类型 变量 ：数组 | 集合){}</font>

**foreach最大的特点在于可以自动将数组中的每一个元素的内容取出保存在变量里面，这样就可以直接通过变量获取数组内容，避免下标的方式获取**

**范例：**使用foreach语法形式输出

```java
public class ArrayDemo {
    public static void main(String[] args){
        // 使用数组的动态初始化实现了数组的定义
        int data[] = new int[] {1,2,3,4,5};
        for (int temp:data){
            System.out.println(temp);
        }
    }
}
```

