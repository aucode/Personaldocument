## Java 面试笔记 

### 包装类型
> 每一个基本数据类型都会有一个包装类型： boolean --> Boolean ：int integer
>> 装箱 ：把基本数据类型转成包装类型 => int --> integer :例子 integer i = 1(int);
>> 拆箱 ：把包装类型转成基本数据类型 => integer i = 1; int j = i; 

### 内存 
> 整个内存分为栈和堆 

### Java中提供了3个类String、StringBuilder、StringBuffer来表示、操作字符串。
> String 是内容不可变的字符串。
>> String 底层使用了一个不可变的字符数组（ final char[] ）。
> StringBuilder、StringBuffer 是内容可变的字符串。
>> StringBuilder、StringBuffer 底层使用了一个可变的字符数组（ 没有使用 final 修饰 ）
>>> 拼接字符串不能用String拼接，只能用StringBuilder、StringBuffer拼接

### 字节流和字符流。
>字节流 ：传递时二进制字节。
>>字符流 ：传递是字符。

### 数据库
> 关系型数据库 ： mysql oracle sqlServer。
> 非关系型 ： redis.....

### 事务 
> 同步 一起成功、一起失败。






#### Java跨平台原理 ？
1. java 通过跨平台在不同操作系统上运行。
2. Java 程序试运行在虚拟机上，与操作系统无关。所以只需要安装对应的虚拟机即可。
3. 所以我们开发程序，只需要按照接口（Java API）开发即可。

#### 搭建Java开发环境的步骤 ？
1. 安装JDK 
2. 安装IDE 
3. web服务器（Tomcat）
>> 下载我们所需要的版本的JDK、Tomcat、Eclipse，配置环境变量JAVA_HOME。 

#### Java中有几种基本数据类型、分别是什么？
1. 8种 
3. byte、short、int（4个字节、23位）、long，float、double，char，Boolean（1位）。

#### 面向对象的特征有哪些方面（原则：抽象问题要举例说明）？
> 四大基本特征：封装、抽象、继承、多态。
1. 封装 : 人的姓名、身高等属性封装成类.... ；并提供一个方法来操作。 
2. 抽象 ：（把现实生活中的对象抽象成类）把一个人抽象成一个类。
3. 继承 ： 遗产继承（我的都给你了）。
4. 多态 ： 例子：Object obj = new Cat();

#### 有了基本数据类型，为什么还有包装类型？
> Java是面向对象的语言，而基本数据类型，不具备面向对象的特征。

#### ==和equals的区别？
1. == 判断两个变量值是否相等。
> 基本数据类型直接比较值，引用类型比较内存地址。

2. equals 判断两个对象是否一样。


#### 讲下Java中的集合？
> Java中的集合分为value，key-value 即【Collection、Map】两种。
>> 存储value值的：List 和 Set。
>>> List 是`有序的可以重复的`。Set是`无序的、不可重复`。根据equals 和hashcode 判断
>> 存储key-value值的：Map

#### ArrayList 和 LinkedList 的区别和使用场景。
> ArrayList（数组有索引查询快，插入删除慢） 底层使用数组、LinkedList（查询效率低，插入、删除效率高） 底层使用链表。
>> 使用场景 ：ArrayList（常用）用查询多，插入、删除少。LinkedList 用在查询少，插入删除多。

#### HashMap和HashTable的区别。
> HashMap 和 HashTable 都是存储key-value 数据。
>> HashMap 是可以把 null 作为 key 或 value 存储的，而HashTable 不可以。
>>> HashMap 是线程不安全的，所以效率高。而 HashTable 是线程安全，所以效率低。 
>>> 保证效率和线程安全 ConcurrentHashMap。

#### 实现一个拷贝文件的类使用字节流还是字符流。
> 拷贝不确定是字符（文字），还是字节（图片、声音）时考虑通用型用字节流。 

#### 线程的实现方式 怎么启动线程怎么区分
1. 线程的实现方式。
>> 1. 继承Thread 类（start启动，扩展性不强、Java单继承）
>> 2. 实现Runnable 接口 
>>> 区分 ：线程.setName("设置线程名"); 区分不同线程。


#### 线程并发库和线程池的作用？
> JDK5 添加DougLea 线程并发库 
>> Executors 四个静态方法创建线程池 
>>> 1. 
>>> 2. newFixndThreadPool 指定最大线程并发数。
>>> 3. 
>>> 4. 
> 线程池的作用。
>> 限制线程数量，不会导致线程过的导致运行慢或崩溃。



#### 什么是设计模式和常用的设计模式 
> 设计模式 ：经过前人无数的实践，在设计过程中可以反复使用的设计方法。
>> 常用的设计模式 
>>> 1. 单例模式 
>>>> 饱汉模式（一出来就创建）
>>>> 饥汉模式（需要时创建）

>> 2. 工厂模式（Spring IOC）
>> 3. 代理模式（Spring AOP：动态代理）
>> 4. 包装模式


#### http 的 get post请求的区别？
> 都是HTTP请求方式，get 一般时查找信息， post一般时更新资源信息。
>> get 会在地址显示处理、会限制传输数据大小，post 不会显示出来，不会限制传输数据大小（更安全）


#### Servlet的理解？ 
> Java Servlet（动态网络语言） 是Java编写的服务的程序。都要实现Servlet 接口，运行在服务端。
>> HttpServlet 重写了 doGet 和 doPost 方法完成响应。

#### Servlet的生命周期？
> 1. Servlet 生命周期（5个） ：加载、实例化、初始化、处理请求、服务结束。生命周期由javax.servlet.Servlet 接口的 init、servlet、destroy 实现。
>> Servlet 启动时，加载servlet 生命周期就开始。然后调用 init 完成初始化。请求到达时运行servlet 方法，服务器关闭时调用 destroy 方法。
>>> 生命周期 ：加载servlet 类 ==> 实例化servlet ==> 并调用 init 完成初始化 ==> 运行servlet 响应请求（调用doXXX ）方法 ==> destroy 方法（服务器关闭）


#### forward和redirect的区别？
> 1. forward 容器控制权转向（服务端跳转、原来请求、效率高），浏览器地址栏不会变化。redirect 是完全跳转（页面跳转、新请求）

#### JSP和Servlet的相同点和不同点？
> JSP（编译成类，并继承HttpServlet类） 是Servlet 的扩展。
>> Servlet类通过 Writer 输出 HTML 代码 

#### JSP 内置对象和四大作用域和页面传值？
> 1. 9个内置对象 
>> request、response、session、out ....

> 2. 四大作用域 
>> request、response、session、pageContext。jstl取值。

#### Session和Cookie的区别？
> 都是绘画跟踪对象，Session（占内存）服务端记录信息，Cookie（不安全）客户端记录信息。但是Session依赖 Cookie 。

#### mvc模式和mvc各部分的实现？
> m（model）JavaBean ，：v（view） ：html、jsp ，c（Servlet） ：Servlet、Action，==>例子：jsp + Servlet + javabean。

#### 关系型数据库的`三范式（遵守的规范）`?
> 1. 列数的不可分割（不可重复）。
> 2. 主键唯一。
> 3. 外键。

#### 事务的四大特征？
> 1. 原子性 :   事务内操作要么成功、要么失败
> 2. 一致性 ：回滚
> 3. 隔离性 : 一个事务开始、不能受其他事务干扰
> 4. 持久性/持续性 : 开始后不能终止。

#### mysql数据库默认最大连接数？
> 数据库只能支持一定的数目同时连接。100

#### mysql和oracle的分页语句（着重说思路）
> 分页 不可能完全显示数据
>> 1. mysql
>>> 使用limit 关键字分页，limit offset，size； 从多少索引多少位。
>> 2. oracle 忘记了 嵌套查询。

#### 触发器的使用场景？
> 触发器（效率高）需要有触发条件，当条件满足后做什么操作。
```
    # 定义触发器 （）
    create trigger [触发器名] after [操作之后] [做什么]

```

#### 存储过程的优点？
> 只在创建时编译一次，减少客户机和服务器网络传输，可重复使用，安全性高。
```
CREATE PROCEDURE ShowStuScore[存储过程名]([参数])
    BEGIN

       SELECT * FROM tb_students_score;[操作]

    END;
# 调用
    call ShowStuScore[存储过程名]([参数]);
```

#### jdbc调用存储过程？
> 1. 加载驱动 
> 2. 获取连接 
> 3. 调用存储过程、设置参数 
> 4. 执行 
> 5. 释放连接 

#### 常用SQL 语句？


#### 简单说一下你对jdbc的理解？
> jdbc ==> java database connection [Java数据库连接]，每个数据库系统支持的命令是不一样的。
>> 对于开发，需要导入对于的数据库驱动包[jar]，调用接口就行。

#### 写一个jdbc的访问oracle的列子？
> 1. 加载驱动 （oracle.jdbc.driver.OracleDriver，com.mysql.jdbc.Driver..[驱动名称]）
> 2. 获取连接 （DriverManager.getConnection("[数据库url]","[用户名]","[命名]")）
> 4. 执行 （executeQuery("select * from t_user");[执行数据库命令]）
> 5. 释放连接 （close();）

#### jdbc中preparedStatement比Statement的
> 1. preparedStatement预编译（快，可读好），preparedStatement 可以防止SQL注入攻击。

#### 数据库连接池的作用？
> 限制数据库数量，不会导致数据库连接过的导致运行慢或崩溃。
> 不用每次都创建、销毁，节约资源。
> 响应时间更快。

#### bootstrap的是什么？
> 是一个UI框架。别人帮写好的页面。模态框、表单

#### 什么是框架？
> Framework，

#### 简单说一下对mvc框架的理解？
> 常用mvc框架Struts2 、SpringMVC

#### struts2的执行流程或者struts2的原理？
1. 浏览器发送请求经过过滤器，到底struts核心过滤器==> 通过ActionMapper判断是否需要某个Action处理

#### Struts2的拦截器是什么？你都用它干什么？
> 1. 拦截器时Action 调用的对象，在调用Action 方法前后写逻辑代码。
>> 通过动态配置在Action 方法前后写逻辑代码。
>>> 使用场景 ：
>>>> 1. 登录在Action 前判断是否已经登录。
>>>> 2. 用户权限操作
>>>> 3. 日志

#### Spring MVC的执行流程 
```
    发送请求 => Strpng 核心控制器[Servlet DispatcherServlet] => 对url解析 获取 Handler 

    => 执行Handler => ViewResolver渲染返回试图。

```

#### SpringMVC和Struts2的不同 
> 核心控制器 ：Spring （基于方法设计，理论快，好管理，对于Ajax请求直接返回JSON数据） => Servlet ，Struts2 （基于对象设计，配置多，对于Ajax请求返回JSON数据要插件） => Filter 

#### 简单介绍一下Spring或者Spring的两大核心 
> 1. Spring 对管理JavaBean 生命周期核轻量级容器。
> 2. Spring的两大核心
>> 1. IOC 控制器反转 ;控制器在Spring（Spring 注入dao ）
>> 2. AOP 面向切面编程 ：做事务处理（自动管理）


#### AOP是什么？都用它做什么？ 
> 动态代理模式在方法前后、异常后加入逻辑


#### Spring事务的传播特性和隔离级别？ 
> 多个事务存在该怎么处理。

#### ORM是什么？ORM框架是什么？ 
> 1. 对象关系映射（Object Relational Mapped，[ORM]）
>> ORM框架: Hibernate、Mybatis 
>>> ORM框架 : 解决Java面向对象和关系型数据库不匹配


#### mybatis和hibernate有什么不同 
> 都是ORM框架，不用关注数据库连接的底层操作。
>> hibernate（功能强大） 全自动生成 简单 sql 语句执行返回Java结果。
>> mybatis（可以处理 复杂的语句） sql 于Java代码分离，可以将结果自动封装成实体类对象。


#### hibernate对象状态及其转换 
> 1. 临时状态 ： 刚刚new 出来没有实例化。
> 2. 持久化状态 ：被实例化，加入到了session 中，而session是没有关闭持久化对象的。
> 3. 游离状态 ：被实例，不在session 中

#### hibernate的缓存 
> why ???
>> 提高访问速度，访问数据库 => 读取缓存（内存）
1. 一级缓存 ：session（内置，在事务范围内有效） 缓存 
2. 二级缓存 ：sessionFactory  缓存（在引用启动到结束，需要开启）


#### webService的使用场景 
> webService 是一个SOA（面向服务）架构。不依赖于语言、平台。可以实现不同语言的相互调用。
>> 1. 异构系统（不同系统）的整合，2. 不同客户端的整合。


#### activiti的简单介绍？ 
> 是一个业务管理（BPM）和工作流程系统。适用于开发任意和系统管理员。
>> 主要是用在办公自动化（OA），线下流程放到线上。（请假流程）



#### 如果查询和定位慢查询？
> 开启mysql 数据库时开启慢查询。并且把执行慢的语句写到日志中，通过查看日志找到慢查询语句。使用explain 慢查询语句，分析。 

#### 数据库优化之数据库表设计遵循范式 
> 数据库表要遵循范式（准规） ：
>> 1. 原子性不可分割。 
>> 2. 记录的唯一性， 主键 
>> 3. 不要冗余数据，外键 

#### 选择合适的数据库引擎 
> **InnoDB存储引擎**（对事务要求高，保存重要的数据，数据不能出错）、**MyISAM存储引擎**（不支持事务，添加查询为主）、MEMORY存储引擎（不需要入库、查询、修改频繁）。


##### 选择合适的索引 
> 索引[Index]
>> 普通索引（可以重复）、唯一索引（不可重复，用户名、身份证、Email、tel...）、主键索引（主键唯一值）、全文索引（对表的文本域，char、text）。
>>> 使用技巧（作用空间，影响添、删、改） ：一般在查询[where]时用。

#### SQL 优化。

##### 数据库优化之分表 
> 当表数据多，字段值非常多，不怎么查找[抽查出来、通过外键关联]，时使用水平（按行）分表、垂直（按列）发表

##### 数据库的读写分离 （主从数据库）
> 一台数据库支持的并发连接数[同时连接]是有限的，一条服务器满足不了要求。
>> 把读写分离 : 所有改变数据的都往**主数据库**里写。


##### 数据库优化之缓存 
> 在持久层（dao）和数据库之间添加一个缓存屋，使用redis 来缓存。

#### sql语句优化小技巧 
> 1. 多次提交变成一次，


#### 有没有使用过redis、redis的使用场景、redis存储对象的方式 
> 是key -value 数据库，放在内存[快]。

