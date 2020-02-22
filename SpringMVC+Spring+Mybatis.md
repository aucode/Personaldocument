### SpringMVC + Spring + [MyBatis (SSM)](https://mybatis.org/mybatis-3/zh/index.html)
> [`MyBatis `](https://mybatis.org/mybatis-3/zh/index.html) ORM 框架 （对象关系映射）

```
  表现层 =>   业务层 => 持久层 
SpringMVC(controller) => Spring(con) => MyBatis (dao)
包 调用关系
	controller => service => dao => 

```
#### SSM搭建

#### jar包

- 表现层（SpringMVC的jar包 ）
> SpringMVC的jar + spring-mvc.xml配置文件   

- 业务层（Spring）
> spring-ioc.jar、spring-aop.jar、spring-tx.jar、spring-test.jar + appliationContext.xml 

-持久层 (mybatis)
> mybatis自身核心包 + mysql 驱动连接池 + mybatis-spring 整合包 + 配置文件 （sqlMapconfig.xml + dao包配置文件）

### 单独使用`mybatis ` 

#### 导入必须包

#### 建立数据库和表

#### 建立实体类

#### 建立Mapper接口 
- 创建表接口 

- 创建表接口xml文件 
> 创建 `XxxxMapper.xml `文件； 该文件编写mybatis中的mapper 接口里的方法，为接口里的方法提供一个对应sql语句 
```
public interface TestService {
	User getUserByCodePassword(User u);
}

```


#### 建立sql映射文件 `Mapper.xml 表文件配置`
```

<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
 
<!-- namespace：命名空间，是接口路径 -->
<mapper namespace="test">
	<!-- id:statement的id 或者叫做sql的id 注意必须与接口方法名一致-->
	<!-- parameterType: 声明输入参数的类型 -->
	<!-- resultType:声明输出结果的类型，应该填写pojo的全路径 -->
	<!-- #{}：输入参数的占位符，相当于jdbc的？ -->
 
	<!-- 通过id查询一个用户 -->
	<select id="findUserById" parameterType="integer" resultType="com.itheima.domain.User">
		select * from user where id=#{id};
	</select>
	
	<!-- 通过username 模糊查询用户列表
	    #{}: 占位符
	    ${}：字符串拼接
	 -->
	<select id="findUserByUsername" parameterType="String" resultType="com.itheima.domain.User">
		select * from user where username like '%${value}%';
	</select>
	
	
	<!-- 添加用户 -->
	<insert id="insertUser"  parameterType="com.itheima.domain.User">
	   INSERT INTO user (username,birthday,sex,address) VALUES (#{username},#{birthday},#{sex},#{address});
 
	</insert>
	
	<!-- 更新用户 -->
	<update id="updatetUser" parameterType="com.itheima.domain.User" >
		update user set username=#{username} where id=#{id};
	</update>
	
	<!-- 删除用户 -->
	<delete id="deleteUser" parameterType="integer">
		delete from user where id= #{id};
	</delete>
	
</mapper>

```
#### 建立sqlMapConfig.xml文件 
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration
PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
<!-- 和spring整合后 environments将废除 -->
    <environments default="development">
        <environment id="development">
        <!-- 使用JDBC事务管理，事务控制由mybatis -->
            <transactionManager type="JDBC"/>
            <!-- 数据库连接池，由mybatis -->
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis?characterEncoding=utf-8"/>
                <property name="username" value="root"/>
                <property name="password" value="root"/>
            </dataSource>
        </environment>
    </environments>
    	<mappers>
		<!-- 映射文件的位置 -->
		<mapper resource="com/soft/domain/User.xml" />
	
	</mappers>
</configuration>

```
#### 测试 
```
    @Test 
    public void text(){
        //1.sqlSessionFactoryBuilder(构造器) 
        SqlSessionFactoryBuilder builder = new SqlSessionFactoryBuilder();
        //2.加载sqlMapConfig.xml 文件 
        InputStream is = Resources.getResourceAsStream("sqlMapConfig.xml");

        //3.创建sqlSessionFactory 
        SqlSessionFactory factory = builer.build(is);

        //4.打开 SqlSession 
        SqlSession sqlSession = fatctory.openSession();

        //5.获取Mapper 接口对象 
        UserMapper userMapper = sqlSession.getMapper(user.class);

        //6.设置数据
        User user = new User();
            //调用接口方法
            user.saveUser(user);

        //7.提交事务
        sqlSession.commit();

        //8.关闭资源
        sqlSession.close();

    }

```

### mybatis 整合 Spring 

#### 导包
```
mybatis-spring 
spring-ioc
spring-aop
spring-tx
spring-context

```
####  整合 方法一

#### 编写Mapper 的实现类 （xxxImpl 实现类 与SSH框架类似） 
```
//接口
public interface TestService {
	User saveuser(User u);
}
//实现类
public class CustomerMapperImpl extends SqlSessionDaoSupport implements CustomerMapper{
    public void saveCustomer( Customer customer ){
        SqlSession sqlSession = this. getSqlSession();
        sqlSession.insert("saveuser",user); //sqlSession.insert("xml文件配置的id",user);
        //不需要管理事务    
    }

}




```

#### 编写 applicationContext.xml 在这里配置连接池 （完成可删除sqlMapConfig.xml文件 ）
```
db.properties文件：
jdbc.jdbcUrl=jdbc:mysql:///vb
jdbc.driverClass=com.mysql.jdbc.Driver
jdbc.user=root
jdbc.password=root

applicationContext.xml文件：
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:context="http://www.springframework.org/schema/context"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:aop="http://www.springframework.org/schema/aop"
    xmlns:tx="http://www.springframework.org/schema/tx"
    xsi:schemaLocation="http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd
        http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd
        http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

        <!--读取jdbc. properties -->
        <context: property-placeholder location="classpath:jdbc.properties"/>
        <!--创建DataSource -->
        <bean id= "dataSource" class="org. apache。commons. dbcp. BasicDataSource ">
            <property name="url ”value= "${jdbc.url}"/>
            <property name= "driverClassName”value= "${ jdbc. driverClass}"/>
            <property name= "username" value= "${jdbc. user}"/> 
            <property name= "password" value= "${jdbc. password} "/>
            <property name= "maxActive" value="10"/>
            <property name= "maxIdLe" value="5"/>
        </bean>
        <!-- 创建SqlSessionFactory对象 -->
        <bean id="sqlSessionFactory" class= "org. mybatis. spring. SqLSessionFactoryBean">
            <!--关联连接池-->
            <property name= "dataSource" ref= "dataSource"/>
            <!--加载sq1映射文件-->
            <property name= "mapperlocations”value= "classpath:mapper/*. xmL"/>
        </bean>
        <!--创建CustomerMapperImpl对象， 注入SqlSessionFactory -->
        <bean id= "cus tomerMapper" class= "cn. sm1234. dao. impL. Cus tomerMapperImpl ">
            <!-- 关联sqlSessionFactory -->
            <property name= "sqlSessionFactory”ref= "sqlSessionFactory"/>
        </bean>



</beans>

```
#### 测试 
```
    @Test 
    public void test(){
        //1.加载spring配置
        ApplicationContext ac = new ClassPathXmlApplicationContext(" applicationContext. xml");
        //2.获取对象
        CustomerMapper customerMapper = (CustomerMapper)ac. getBean("customerMapper");
        //3.调用方法
        Customer customer = new Customer();
        customer.setName("小美");
        customer.setGender("女" );
        customer.setTelephone("020-666666") ;
        customer.setAddress("广州体育中心");
        customerMapper.saveCus tomer( customer);


    }

```

####  整合 方法二  applicationContext.xml添加
```
<!--配置Mapper接口-->
<bean id= "cus tomerMapper" class= "org. mybatis. spring . mapper . MapperFactoryBean">
    <!-- 关联Mapper接口-->
    <property name= "mapperInterface”value= "cn. sm1234. dao. CustomerMapper"/>
    <!-- 关联SqlSessionFactory -->
    <property name= "sqlSessionFactory" ref="sqlSessionFactory"/>
</bean>


```


####  整合 方法三 Mapper接口扫码 
```
<!-- Mapper接口的扫描-->
<bean class="org. mybatis. spring. mapper. MapperScannerConfigurer">
<!--配置Mapper接口所在包路径-->
<property name= "basePackage”value= "cn. sm1234. dao"/>
</bean>


```













## Maven搭建项目


### [`Maven 库`](https://mvnrepository.com/) 
> 囊括所有开源的`jar `工具包 
+ 使用 
````
1.解压 apache-maven-3.5.2-bin.zip 和 MavenRepository.rar 
2.进入 apache-maven-3.5.2 => conf => settings.xml 在54行添加  <localRepository>解压出来 MavenRepository 的路径</localRepository>
    例如：
         <localRepository>E:\Maven\MavenRepository</localRepository> 

3.打开 eclipse => window => Maven => user Sttings 在user Sttings点击Browse 选择 apache-maven-3.5.2\conf\settings.xml 
4.创建Maven Project => 打勾 Create a simple project => 1)Group Id (公司名) 2)Artifact id(项目名) 3)Packaging 选择 war 

```` 
##### Maven项目
1) src/main/java 放Java代码
	包：
		dao 
		controller 
		service 
		entity 
		utils 
2) src/main/resources xml放配置文件

##### 1）导入jar包: 在项目的 Pom.xml文件 添加
````
 <dependencies>
  	<dependency>
	    <groupId>org.springframework</groupId>
	    <artifactId>spring-webmvc</artifactId>
	    <version>4.3.14.RELEASE</version>
	</dependency>
  
  	<!-- https://mvnrepository.com/artifact/log4j/log4j -->
	<dependency>
	    <groupId>log4j</groupId>
	    <artifactId>log4j</artifactId>
	    <version>1.2.17</version>
	</dependency>
	<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
	<dependency>
	    <groupId>org.mybatis</groupId>
	    <artifactId>mybatis</artifactId>
	    <version>3.4.1</version>
	</dependency>
	<!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
	<dependency>
	    <groupId>mysql</groupId>
	    <artifactId>mysql-connector-java</artifactId>
	    <version>5.1.39</version>
	</dependency>
	<!-- https://mvnrepository.com/artifact/org.springframework/spring-context -->
	<dependency>
	    <groupId>org.springframework</groupId>
	    <artifactId>spring-context</artifactId>
	    <version>4.3.14.RELEASE</version>
	</dependency>
	<!-- https://mvnrepository.com/artifact/org.springframework/spring-test -->
	<dependency>
	    <groupId>org.springframework</groupId>
	    <artifactId>spring-test</artifactId>
	    <version>4.3.14.RELEASE</version>
	    <scope>test</scope>
	</dependency>
	<!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
	<dependency>
	    <groupId>org.projectlombok</groupId>
	    <artifactId>lombok</artifactId>
	    <version>1.16.20</version>
	    <scope>provided</scope>
	</dependency>
	<!-- https://mvnrepository.com/artifact/junit/junit -->
	<dependency>
	    <groupId>junit</groupId>
	    <artifactId>junit</artifactId>
	    <version>4.12</version>
	    <scope>test</scope>
	</dependency>
	<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
	<dependency>
	    <groupId>org.mybatis</groupId>
	    <artifactId>mybatis-spring</artifactId>
	    <version>1.3.1</version>
	</dependency>
	<!-- https://mvnrepository.com/artifact/com.alibaba/druid -->
	<dependency>
	    <groupId>com.alibaba</groupId>
	    <artifactId>druid</artifactId>
	    <version>1.0.18</version>
	</dependency>
	<!-- https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
	<dependency>
	    <groupId>org.springframework</groupId>
	    <artifactId>spring-jdbc</artifactId>
	    <version>4.3.14.RELEASE</version>
	</dependency>
  </dependencies>
````
##### 2）配置Web.xml文件 
````

  <context-param>
  	<param-name>contextConfigLocation</param-name>
  <!-- applicationContext.xml Spring 的核心配置文件 -->
  	<param-value>classpath:applicationContext.xml</param-value>
  </context-param>
  <listener>
  	<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
  </listener>
  <!-- dispatcherServlet 拦截器开始 -->
  <!-- 只要你发了请求、用了SpringMVC 请求都得经过dispatcherServlet 拦截器 -->
  <servlet>
  	<servlet-name>dispatcherServlet</servlet-name>
  	<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
  	<init-param>
  		<param-name>contextConfigLocation</param-name>
  <!-- SpringMVC.xml SpringMVC 的核心配置文件 -->
  		<param-value>classpath:SpringMVC.xml</param-value>
  	</init-param>
  	<load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
  	<servlet-name>dispatcherServlet</servlet-name>
  	<!-- 地址必须是.do 结尾的才能通过 -->
  	<url-pattern>*.do</url-pattern>
  </servlet-mapping>
   <!-- dispatcherServlet 拦截器结束 -->
  
````
##### 3）Spring 的核心配置文件 `applicationContext.xml ` 
- [`添加约束 `](https://docs.spring.io/spring-framework/docs/current/spring-framework-reference/core.html#beans-annotation-config)
````
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <context:annotation-config/>

</beans>
````

- 配置文件 
````
<!-- 
		扫描包
	 -->
	 <context:component-scan base-package="com.neuedu.service"></context:component-scan>

	<!-- 
		读取配置文件内容
	 -->
	 <context:property-placeholder location="classpath:jdbc.properties"/>

	<!-- 
		创建数据库连接池
	 -->
	 <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
	 	<property name="url" value="${url}"></property>
	 	<property name="username" value="${username1}"></property>
	 	<property name="password" value="${password}"></property>
	 </bean>
	 
	 <!-- 
	 	创建sqlSessionFactory
	  -->
	  <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
	  	<property name="configLocation" value="classpath:SqlMapConfig.xml"></property>
	 	<property name="dataSource" ref="dataSource"></property>
	  </bean>
	 <!-- 
	 	扫描mapper文件
	  -->
	  <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
	  	<property name="basePackage" value="com.neuedu.dao"></property>
	  </bean>
````
##### MyBatis核心配置文件 SqlMapConfig.xml 文件
````
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>

</configuration>
````
##### SpringMVC.xml 
- [`导入约束 `](https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html#mvc-config)
````
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:mvc="http://www.springframework.org/schema/mvc"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/mvc
        https://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <mvc:annotation-driven/>

</beans>
````
- 文件配置
````
<context:component-scan base-package="com.neuedu.controller"></context:component-scan>
	
	<mvc:annotation-driven />
	
	<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
		<property name="prefix" value="WEB-INF/"></property>
		<property name="suffix" value=".jsp"></property>
	</bean>

```` 

##### mybatis 动态代理 

1） mapper 文件存放路径要与接口文一致 

2） mapper 中的namespace 要写接口连接 

3） mapper 中的每一个方法返回值类型和参数类型 必须的接口一致 

````
1. 在src/main/resources 下创建接口一致的包 
2. 再创建与接口名一致的xml (mapper) 文件 


````
##### [`mapper约束文件`](https://mybatis.org/mybatis-3/zh/getting-started.html)
````
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="接口的连接">

	<select id="方法名" resultType="返回值类型" ></select>
	例子：
	<select id="queryAllUser" resultType="top.auread.entity.Users"></select>

</mapper>

````