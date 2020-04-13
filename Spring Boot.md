### [Spring Boot](https://spring.io/) `是对Spring的封装`
> Spring Boot是一个便捷搭建基于Spring工程的脚手架，帮助开发人员快速搭建Spring项目，简化工程的配置，依赖管理简化。

##### 微服务 
```
            Spring Boot（jar包里带tomcat）
                                                =>运行（微服务）
        Spring  --> SpringMVC   --> Tomcat
```
1. Spring Boot零配置        ==>     springMVC 实现去掉xml。
2. Spring Boot的嵌入tomcat  ==>     把tomcat嵌入到项目中，并运行。
3. Spring Boot的工作原理

##### 优势
1. 基于注解开发，简化配置，使用yml或propreties进行简要配置。
2. 每个工程都可以打包成一个jar ，内置了Tomcat可以独立运行。
3. 有强大的启动器，starter

### Spring Boot 项目创建
1. 创建Spring Boot 工程 

2. 添加依赖 `启动依赖：spring-boot-starter-web` 
```xml
	<!-- 继承SpringBoot官方指定的父工程 -->
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.1.6.RELEASE</version>
	</parent>
	<!-- 设置JDK版本 （可选） -->
	<properties>
		<java.version>1.8</java.version>
	</properties>
	<dependencies>
		<!-- 加入Web工程启动器(SpringMVC) -->
		<dependency>
			<!-- 指定groupId和artifactId即可，版本已在父工程中定义 -->
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
	</dependencies>
```
3. 创建启动类 
```java
	@SpringBootApplication	//标记为SpringBoot应用
	public class SpringBootMain {
		public static void main(String[] args) {
			SpringApplication.run(SpringBootMain.class, args);
		}	
	}

```


### Spring Boot 配置文件 
1. application.properties 配置 

2. application.yml （多个）配置
> 必须有一个`application.yml` 多个命名 `application-xxx.yml`

```yml
------------------------- application.yml----------------------------

# 激活配置文件
spring:
  profiles:
    active: onau,topau #配置文件名为 application-onau.yml,application-topau.yml
mybatis:
  mapper-locations: classpath:mapper/**/*.xml  #注意：一定要对应mapper映射xml文件的所在路径
  type-aliases-package: top.au.**.pojo  # 注意：对应实体类的路径

debug: true

logging:
  level:
    root: WARN
    org:
      springframework:
        security: DEBUG
        web: ERROR
        boot:
          autoconfigure: ERROR
    com:
      cq:
        yulin:
          livestock:
            shiro:
              mapper: debug

server:
  port: 8999 # 设置端口
---------------------- application-xxx.yml --------------------------
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/new_sys?serverTimezone=GMT%2B8
    username: root
    password: Zhuoduyi123
	driver-class-name: com.mysql.cj.jdbc.Driver
	
```



### Spring Boot 自动配置原理 
> 了解Spring Boot自动配置流程

1. 在`META-INF\spring.fatories`文件中定义了很多自动配置类；可以根据pom.xml 文件中添加的启动依赖自动配置组件。
2. 修改application 配置文件，修改自动配置组件的默认参数。


### lombok应用 
> 使用Lombok 的注解实现 `pojo类(实体类)`的简化 

1. IDEA 安装Lombok 插件
```xml
	Settings --> Plugins --> Marketplace 
```

2. 添加Lombok 依赖到项目
```xml
	<dependency>
		<groupId>org.projectlombok</groupId>
		<artifactId>lombok</artifactId>
	</dependency>
	-------------------------------------------------
	@Data：提供`getter、setter、hashCode、equals、toString`的方法
	@Getter：提供getter
	@Setter：提供setter
	@SIf4j：自动在bean中提供log变量，`log.debug("日志输出。")`可以输出日志信息

```


### Spring Boot 整合SpringMVC 端口和静态资源
> 修改tomcat的端口和访问项目中的静态资源

1. 修改tomcat端口
>> 查询**Properties，设置配置项（前缀 + 类变量名）到application配置文件中


```yml
 # 设置端口
server:
  port: 80

```


2. 访问项目静态资源 
```java
resources
	|——	static
		|——	itcast.gif
		|——	test.js

	//访问路径
		localhost/test.js
		# 在项目页面中 
		/test.js
```


### Spring Boot 整合SpringMVC 拦截器
> 如果你想要保持Spring Boot的一些默认MVC特征,同时又想自定义一些MVC配置(包括:拦截器，格式化器,视图控制器、消息转换器等等)， 你应该让一个类实现`webMvcConfigurer`，并且添加`@Confi guration`注解,但是千万不要加`@EnablewebMvc`注解。如果你想要自定义`HandlerMapping`、`HandTerAdapter` 、`ExceptionResolver`等组件,你可以创建一个WebMvcRegistrationsAdapter实例来提供以上组件。如果你想要完全自定义SpringMVC,不保留SpringBoot提供的一 切特征，你可以自己定义类并且添加`@Configuration`注解和`@EnabTewebMvc`注解

1. 编写一个实现`HandlerInterceptor`的拦截器
2. 编写配置类实现`webMvcConfigurer`,在该类中添加组件



### Spring Boot 整合连接池 
> 配置Spring Boot自带默认的hikari数据库连接池和使用@Transactional注解进行事务配置 

1. 添加事务相关的启动器依赖, mysq|相关依赖; 
```xml

<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>
<dependency>
	<groupId>mysq1</groupId>
	<artifactId>mysq1-connector-java</artifactId>
	<version>5.1.46</version>
</dependency>


```

2. 编写业务类UserService使用事务注解@Transactional



### Spring Boot 整合Mybatis 

### Spring Boot 整合Redis 

### Spring Boot 项目部署 








##### Spring Boot整合Filtert 
1. 创建一个Filter
```java

/**
 * @Project demo
 * @Description: FirstFilter
 * @Author AU
 * @Explain Filter 拦截器
 * @Date 2020-03-31 11:06
 */
@WebFilter(filterName = "FirstFilter",urlPatterns = "/first")
public class FirstFilter implements Filter {
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        System.out.println("进入 init----------->");
    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        System.out.println("进入 doFilter----------->");
        filterChain.doFilter(servletRequest,servletResponse);
        System.out.println("离开 doFilter----------->");
    }

    @Override
    public void destroy() {
        System.out.println("进入 destroy----------->");
    }
```
2. 修改启动类
```java

@SpringBootApplication
@ServletComponentScan
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

}
```







##### 配置文件占位符 `${}`	
```yml
	# ${} 
	server:
		port: ${random.int(1024,9999)}	# 随机生成 1024 ~ 9999 的整数。 

```

##### bootstrap配置文件
> Spring Boot 的两种上下文对象，`bootsrap、application (bootsrap.yml、application.yml)`




##### 注解 

```java
	1) @SpringBootApplication 
			# @Configuration + @ComponentScan + @EnableAutoConfiguration
					|	# 1. 标记为SpringBoot应用，该类的main方法是SpringBoot应用人口。通过main启动应用。
					|	# 2. 主启动类所在的包和子包会自动扫描，其他不会自动扫码，需要手动扫描。
					|—— 1) @Configuration
					|			# 
					|—— 2) @ComponentScan
					|			# 
					|—— 3) @EnableAutoConfiguration
								# 
	2) 

	3）@RestController
			# @Controller + @ResponseBody结合
					|——	1）@Controller
					|			// 表面为控制器。
					|——	2）@ResponseBody
								# 将java对象转为json格式的数据。

	4) @GetMapping 
	5) @PostMappng
	6) @PutMapping
	7) @DeleteMapping






```
