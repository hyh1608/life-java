# 数据表与简单Java类映射转换

简单java类是目前面向对象设计的主要分析基础，在实际开发中往往根据数据表的结构来实现简单Java类

在数据库中提供有若干个数据表，每一张实体数据表都可以描述出一些具体的事物概念，例如：雇员信息表、部门信息表。程序类的定义形式与实体表的差别不大，所以实际开发中，数据表与简单Java类之间的基本映射如下：

- 数据实体表设计 = 类的定义
- 表中的字段 = 类的成员属性
- 表的外键关联 = 引用关联
- 表的一行记录 = 类的一个实例化对象
- 表的多行记录 = 对象数组

