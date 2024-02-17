# 第一章 Java 学习笔记

这里记录学习 Java Web 开发的笔记，主要模块包括：Java + SpringBoot + MySQL + MyBatis + Redis 。

Java中 JDK8（JDK1.8）、JDK11、JDK17，该怎么选择：https://cloud.tencent.com/developer/article/1977236



## 1.1 前期知识点索引 

这里记录一下个人 Java 生态的课程学习路线：

- Java 基础：https://www.bilibili.com/video/BV12J41137hu
- Java 注解与反射：https://www.bilibili.com/video/BV1p4411P7V3
- Java 多线程：https://www.bilibili.com/video/BV1V4411p7EF
- Java Web（SpringBoot、Maven、Mybatis）：https://www.bilibili.com/video/BV1m84y1w7Tb
- Mybatis-Plus：https://www.bilibili.com/video/BV1Xu411A7tL
- 瑞吉外卖业务开发：https://www.bilibili.com/video/BV13a411q753



### 1.1.1 Java 语法

多态的概念：https://www.liaoxuefeng.com/wiki/1252599548343744/1260455778791232

> `Person p = new Student()` 一个实际类型为 Student，引用类型为 Person 的实例。多态具有一个非常强大的功能，就是允许添加更多类型的子类实现功能扩展，却不需要修改基于父类的代码。



`final`修饰符有多种作用：

- `final`修饰的方法可以阻止被覆写；
- `final`修饰的class可以阻止被继承；
- **`final`修饰的字段必须在创建对象时初始化，随后不可修改。**
- https://www.liaoxuefeng.com/wiki/1252599548343744/1260455778791232



面向抽象编程的本质就是：

- 上层代码只定义规范（例如：`abstract class Person`）；
- 不需要子类就可以实现业务逻辑（正常编译）；
- 具体的业务逻辑由不同的子类实现，调用者并不关心。
- https://www.liaoxuefeng.com/wiki/1252599548343744/1260456371027744



接口类型的定义：

- 如果一个抽象类没有字段，所有方法全部都是抽象方法，就可以把该抽象类改写为接口：`interface`。
- 在接口中，可以定义`default`方法，实现类时可以不必覆写`default`方法。

- `interface`是可以有静态字段的，并且静态字段必须为`final`类型：`public static final int MALE = 1;`

- `interface`定义抽象方法：`public abstract void num();`

- https://www.liaoxuefeng.com/wiki/1252599548343744/1260456790454816



静态字段的定义：

- 在一个`class`中定义的字段，我们称之为实例字段。还有一种字段，是用`static`修饰的字段，称为静态字段.
- 调用实例方法必须通过一个实例变量，而调用静态方法则不需要实例变量，通过类名就可以调用。
- **因为静态方法不属于实例，因此，静态方法内部，无法访问`this`变量，也无法访问实例字段，它只能访问静态字段。**
- https://www.liaoxuefeng.com/wiki/1252599548343744/1260464690677856



输入和输出以及占位符：

- %s、%f、%d 占位符
- 引用类型输出通常使用 `toString`
- https://www.liaoxuefeng.com/wiki/1252599548343744/1255887264020640



字符串核心方法：

- join、split、replace、isBlank、isEmpty、substring、equalsIgnoreCase、equals、indexOf、contains

- 格式化字符串：`s.formatted("cocoon", 12)`、`String.format("%s...%d", "cocoon", 12)`

- 更高效的字符串拼接：StringBuilder（链式拼接）、StringJoiner（已固定分隔符链式拼接）

- https://www.liaoxuefeng.com/wiki/1252599548343744/1260469698963456



日期与时间类：

- 旧版类：https://www.liaoxuefeng.com/wiki/1252599548343744/1303791989162017
- LocalDateTime：https://www.liaoxuefeng.com/wiki/1252599548343744/1303871087444002



java 包与 import：

- 默认自动 import 当前 package 的其他 class
- 一个 Java 程序默认自动引入 `import java.lang.*`
- https://www.liaoxuefeng.com/wiki/1252599548343744/1260467032946976



枚举类 enum：

- 枚举类既是类型又是常量，使用双等于号既会判断类型又会判断变量的值
- 默认定义为字符串，可以通过私有化构造函数给每个枚举常量添加字段
- https://www.liaoxuefeng.com/wiki/1252599548343744/1260473188087424



包装类：

- 想要把`int`基本类型变成一个引用类型，我们可以定义一个`Integer`类，它只包含一个实例字段`int`，这样，`Integer`类就可以视为`int`的包装类
- https://www.liaoxuefeng.com/wiki/1252599548343744/1260473794166400



注解与反射：

- 注解：注解是放在Java源码的类、方法、字段、参数前的一种给程序看的特殊“注释”
- 如何使用注解：https://www.liaoxuefeng.com/wiki/1252599548343744/1265102413966176
- 如何定义注解：https://www.liaoxuefeng.com/wiki/1252599548343744/1265102803921888
- 反射：这种通过`Class`实例（实例变量、`class`静态变量）获取`class`信息的方法称为反射（Reflection）
- 如何获取一个`class`的`Class`实例：https://www.liaoxuefeng.com/wiki/1252599548343744/1264799402020448



### 1.1.2 SpringBoot 语法

JavaWeb 课程：https://www.bilibili.com/video/BV1m84y1w7Tb



Springboot 接口开发三层架构

- controller：控制层，接收前端发送的请求，对请求进行处理，并响应数据
- service：业务逻辑层，处理具体的业务逻辑
- dao：数据访问层（Data Access Object），负责数据访问操作，包括数据的增删改查



数据访问层多态的实现逻辑示例

```java
public interface EmpDao {
    public List<Emp> getEmpDaoList();
}
```

```java
public class EmpDaoInstance implements EmpDao {
    @Override
    public List<Emp> getEmpDaoList() {
        String file = Objects.requireNonNull(this.getClass().getClassLoader().getResource("emp.xml")).getFile();
        System.out.println(file);
        List<Emp> empDaoList = XmlParserUtils.parse(file, Emp.class);
        return empDaoList;
    }
}
```



业务处理层调用 dao 的实例

```java
public class EmpServiceInstance implements EmpService {
    private final EmpDao empDao = new EmpDaoInstance();

    @Override
    public List<Emp> getEmpServiceList() {
        List<Emp> empServiceList = empDao.getEmpDaoList();
        empServiceList.forEach(emp -> {
          ......
        });
        return empServiceList;
    }
}
```



IOC&DI 控制反转与依赖注入

将对象的控制权交给Spring的IOC容器，由IOC容器创建及管理对象。IOC容器创建的对象称为bean对象。在之前的入门案例中，要把某个对象交给IOC容器管理，需要在类上添加一个注解：@Component 。而Spring框架为了更好的标识web应用程序开发当中，bean对象到底归属于哪一层，又提供了@Component的衍生注解：

- @Controller    （标注在控制层类上）
- @Service          （标注在业务层类上）
- @Repository    （标注在数据访问层类上）
- 如果同类型的 bean 对象存在多个，则使用以下三个注解：@Resource、@Qualifier、@Primary

```java
@Repository
public class EmpDaoInstance implements EmpDao
```

```java
@Service
public class EmpServiceInstance implements EmpService {
    @Autowired // 运行时,从IOC容器中获取该类型对象,赋值给该变量
    private EmpDao;

    @Override
    public List<Emp> getEmpServiceList() {
        List<Emp> empServiceList = empDao.getEmpDaoList();
        empServiceList.forEach(emp -> {
          ......
        });
        return empServiceList;
    }
}
```



### 1.1.3 MySQL 常用语法

这里主要介绍 Mysql 里的查询语言的语法。通常被包装为变量 `sqlStr`

参考文档：https://blog.csdn.net/liustreh/article/details/123411958



**数据库操作**

```sql
create database mysql01; //默认创建数据库

create database mysql01 default character set utf8; //创建指定默认字符集为交的数据库

drop database mysql01; //删除数据库

show databases; //查看所有数据库

show create databases; //查看数据库属性
```



**常用数据类型**

```sql
// 创建一个学生表 编号为整型5个字节，名字为变长字符串类型10个字节，年龄不允许为空默认为20
create table student(id int(5),name varchar(10),age int not null default 20);

// 字符串类型
char(0-255) 定长字符串
varchar(0-65535) 变长字符串

// 日期和时间类型
date[日期 年月日] time[时间 时分秒] datetime[年月日 时分秒 YYYY-MM-DD HH:mm:ss]
```



**数据库表操作**

```sql
// 查看表
show tables;

// 查看表结构
desc 表名;

// 快速创建一个表结构相同的表 
create table 新表名 like 旧表名;

// 删除表，如果表结构存在的话
drop table if exits 表名;

// 修改表名
rename table 表名 to 新表名;

// 添加字段（新的列属性）
alter table 表名 add [column]  字段名 类型;

// 修改字段名
alter table 表名 change 旧字段名  新字段名 类型;

// 修改字段类型
alter table 表名 modify 字段 新字段类型;
```



**数据库表的增删改查操作**

1. insert 插入数据

```sql
// 插入全部数据（值的顺序一定要与字段对应）
insert into user values('张三','30','133324','男');

// 插入部分数据
insert into user(name,age,modile) values('小艾',20,'243252');
```



2. update 修改数据

```sql
// 一般更新
update 表名 set 字段名1 = 值1， 字段名2 = 值2，......

// 更新时加入计算
update user1 set age = age+1;

// 部分更新
update 表名 set 字段名1 = 值1，字段名2 = 值2，...where 字段条件
update user1 set sex='女' where name = '张三';
```



3. delete 删除数据

```sql
// 删除全部记录
delete from 表名;

// 按条件删除
delete from 表名 where 字段条件; 
delete from user1 where name = '张三';
delete from user1 where age<23 and name = '小天';

// 快速删除表数据（物理删除）
truncate 表名;
```



4. select 简单查询数据

```sql
// 取出表中的所有数据
select * from 表名;

// 查询指定列
select 字段名1，字段名2，.... from 表名

// 查询指定列带别名
select 字段名1 as  别名 ，字段名2 as 别名，.....
```



**条件查询与运算符**

1. 按条件查询：`where` 

2. 相关运算符：`< ` 小于 `=` 等于 `>` 大于 `>=` 大于等于 `<=` 小于等于  `<>`  或  `!=` 不等于

3. 逻辑运算符： `and (&&)` 与 `or(||)` 或  `not(!)` 非

4. 范围关键字：`between and`

5. `%` 通配符：代表任意长度的任意字符

6. `_` 通配符 代表一个字符长度的任意字符 用法与 `%` 一样，只不过只代表一个字符

```sql
select *from student where math>60 and ehglish>60;

select * from student where math  not in(66,76);

select * from student where math  between 56  and  66；

select * from student where name like '马%';

select * from student where name like '马_';
```



**关键词属性**：即指定字符为一些特殊关键词属性

```sql
// 在字段后面确认主键
create table user2(id int primary key,name varchar(10));

// 在字段后面确认自增
create table user3(id int primary key auto_increment,name  varchar(10));

// 其他关键词
create  table  user5 (
    id  int   primary  key   auto_increment，
    name  varchar(10),
    mobile  varchar(11)  unique,   --此字段值唯一
    sex   varchar(2)  not null     --此字段值唯一
    age  int  default  18
)
```

> 一般将 id 确认为主键和自增



**排序和函数**

1. 排序：`order by [asc] [desc]`， asc 按升排序  desc 降序排序

```sql
// 单列排序
select  *  from  student  order  by  math;        asc 默认可以不写
select  *  from  student  order  by  math  desc;   desc 必须写上

// 多列排序
select  *  from  student  order  by  math  desc, english  desc;
```



### 1.1.4 Maven 项目构建

首先要知道项目的 JDK 环境，然后是项目的 jar 包版本都依赖与 JDK 版本。新建一个 SpringBoot 项目，必须先使用 IDEA 构建框架， 勾选默认的依赖，试试看初始化项目是否跑的起来。然后 IDEA 会根据 `pom.xml` 自动下载项目的依赖。然后在 IDEA 中配置项目的 Maven 运行的 JDK 版本和 Java 的JDK 版本。配置好之后应该就可以跑通了。



### 1.1.5 MyBatis 学习

当构建 SpringBoot 项目时，勾选 MyBatis 依赖必须初始化 `application.properties`  里面的配置才能够启动项目，该配置的作用是链接数据库的。这里推荐下载插件：MyBatisX
```properties
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/springboot
spring.datasource.username=root
spring.datasource.password=2002CZYczy
# 输出SQL语句日志
mybatis.configuration.log-impl=org.apache.ibatis.logging.stdout.StdOutImpl
# 开启mybatis的驼峰命名自动映射开关
mybatis.configuration.map-underscore-to-camel-case=true
```



**数据访问层入门代码**

```java
@Mapper
public interface UserMapper {
    /**
     * 查询所有的员工列表
     * 调用这个函数等于是执行了一个SQL语句，返回值就是该SQL语句的返回值
     * @return List<User>
     */
    @Select("select * from user")
    public List<User> list();

    /**
     * 删除某个员工
     * @param id
     */
    @Delete("delete from emp where id = #{id}")
    public void delete(Integer id);
}
```
```java
@Autowired
private UserMapper userMapper;

@Test
void contextLoads() {
    userMapper.delete(17);
    List<User> userList = userMapper.list();
    userList.forEach(System.out::println);
}
````



**使用注解操作SQL，简单的增删改查**

```java
/**
 * 删除某个员工
 * @param id
 */
@Delete("delete from emp where id = #{id}")
public void delete(Integer id);

/**
 * 导入新员工，导入成功后emp实例获取到一个主键属性id
 * @param emp
 */
@Options(useGeneratedKeys = true, keyProperty = "id")
@Insert("insert into emp(username, name, gender, image, job, entrydate, dept_id, create_time, update_time)" + "values (#{username},#{name},#{gender},#{image},#{job},#{entrydate},#{deptId},#{createTime},#{updateTime})")
public void insert(Emp emp);

/**
 * 更新某个员工的信息
 * @param emp
 */
@Update("update emp set username = #{username}, name = #{name}, gender = #{gender}, image = #{image}," + "job = #{job}, entrydate = #{entrydate}, dept_id = #{deptId},update_time = #{updateTime} where id = #{id}")
public void update(Emp emp);
```

```java
/**
 * 查询某员工信息，已开启mybatis的驼峰命名自动映射开关
 * @param id
 * @return Emp
 */
@Select("select * from emp where id = #{id}")
public Emp selectEmp(Integer id);

/**
 * 查询某员工信息，通过@Results，手动映射结果字段
 * @param id
 * @return
 */
@Results({
        @Result(column = "dept_id", property = "deptId"),
        @Result(column = "create_time", property = "createTime"),
        @Result(column = "update_time", property = "updateTime")
})
@Select("select * from emp where id = #{id}")
public Emp selectEmpV2(Integer id);
```

```java
/**
 * 模糊查询和多条件查询
 * concat 函数是SQL语句的字符串拼接函数
 */
@Select("select * from emp where name like concat('%',#{name},'%') and gender = #{gender} and " +
        "entrydate between #{begin} and #{end} order by update_time desc ")
public List<Emp> obscureList(String name, Short gender, LocalDate begin, LocalDate end);
```



**使用 XML 映射操作 SQL**

1. XML 映射文件的名称与 `Mapper` 接口名称一致，并且将 XML 映射文件和 `Mapper` 接口放置在相同包下
2. XML 映射文件的 `namespace` 属性为 `Mapper` 接口全限定名一致。
3. XML 映射文件中 SQL 语句的 `id` 与 `Mapper` 接口中的方法名一致，并保持返回类型一致。



**动态 SQL**

1. 在 XML 映射中使用动态 SQL，借助 `where`、`if`、`foreach`、`sql`、`include`、`set` 等标签实现
2. https://mybatis.org/mybatis-3/zh_CN/dynamic-sql.html

```java
/**
 * 模糊查询和多条件查询，使用XML映射实现SQL，并且支持动态SQL
 */
public List<Emp> activeObscureList(String name, Short gender, LocalDate begin, LocalDate end);

/**
 * 动态更新某个员工的信息
 * @param emp
 */
public void activeUpdateList(Emp emp);

/**
 * 批量删除员工
 * @param ids
 */
public void batchDelete(Integer[] ids);
```

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.cocoon.mybatislearn.mapper.EmpMapper">
    <!--  定义sql语句常量  -->
    <sql id="commonSelect">
        select * from emp
    </sql>

    <select id="activeObscureList" resultType="com.cocoon.mybatislearn.pojo.Emp">
        <include refid="commonSelect"/>
        -- where标签只会在子元素有内容的情况下才插入where子句，而且会自动去除子句的开头的AND或OR
        <where>
            <if test="name != null">
                name like concat('%',#{name},'%')
            </if>
            <if test="gender != null">
                and gender = #{gender}
            </if>
            <if test="begin != null and end != null">
                and entrydate between #{begin} and #{end}
            </if>
        </where>
        order by update_time desc
    </select>

    <update id="activeUpdateList">
        update emp
        -- 动态地在行首插入set标签，并会删掉额外的逗号（用在update语句中）
        <set>
            <if test="username != null">username = #{username},</if>
            <if test="name != null">name = #{name},</if>
            <if test="gender != null">gender = #{gender},</if>
            <if test="image != null">image = #{image},</if>
            <if test="job != null">job = #{job},</if>
            <if test="entrydate != null">entrydate = #{entrydate},</if>
            <if test="deptId != null">dept_id = #{deptId},</if>
            <if test="updateTime != null">update_time = #{updateTime}</if>
        </set>
        where id = #{id}
    </update>

    <!--
        批量删除员工 (18,19,20)
        collection: 遍历的集合
        item: 遍历出来的元素
        separator: 分隔符
        open: 遍历开始前拼接的SQL片段
        close: 遍历结束后拼接的SQL片段
    -->
    <delete id="batchDelete">
        delete from emp where id in
        <foreach collection="ids" item="id" separator="," open="(" close=")">
            #{id}
        </foreach>
    </delete>
</mapper>
```




## 1.2 后端项目业务笔记

这里主要记录第一次后端项目的编写和构建笔记

- 学习视频：https://www.bilibili.com/video/BV13a411q753
- 参考文档：https://cyborg2077.github.io/2022/09/29/ReggieTakeOut/



### 1.2.1 项目初始化构建

在创建spring boot或者spring cloud项目时，idea默认使用 [https://start.spring.io](https://start.spring.io/) 作为脚手架，创建完成后手动去添加相关的jar包组合。通过 [https://start.aliyun.com](https://start.aliyun.com/) 可以直接勾选ali相关的jar包，快速的引入集成。

首先需要电脑本地下载 JDK 8（该项目需要），另外电脑本地和 IDEA 配置好 Maven，然后开始新建 SpringBoot2 的项目，初始依赖选择 Spring Web、MySQL：

![image-20240209132913031](mark-img/image-20240209132913031.png)

![image-20240209133024686](mark-img/image-20240209133024686.png)

然后在 `pom.xml` 导入以下依赖，项目就直接可以运行了！然后参考课程再配置其他数据库和前端静态资源。

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.20</version>
</dependency>

<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.76</version>
</dependency>

<dependency>
    <groupId>commons-lang</groupId>
    <artifactId>commons-lang</artifactId>
    <version>2.6</version>
</dependency>

<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid</artifactId>
    <version>1.1.16</version>
</dependency>

<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid-spring-boot-starter</artifactId>
    <version>1.1.23</version>
</dependency>

<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatis-plus-boot-starter</artifactId>
    <version>3.4.1</version>
</dependency>
```



配置静态资源映射

```java
public class WebMvcConfig extends WebMvcConfigurationSupport {
    /**
     * 设置前端静态资源映射
     * @param registry
     */
    @Override
    protected void addResourceHandlers(ResourceHandlerRegistry registry) {
        //"classpath:"就是当前项目的"resources"
        //默认“localhost:8080/”->"classpath/static/"
        //现在将路径“localhost:8080/backend/**”映射到文件夹"classpath/backend/"
        log.info("开始进行静态资源映射...");
        registry.addResourceHandler("/backend/**").addResourceLocations("classpath:/backend/");
        registry.addResourceHandler("/front/**").addResourceLocations("classpath:/front/");
    }
}
```



### 1.2.2 构建三层架构步骤



