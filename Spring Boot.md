### Spring Boot `是对Spring的封装`
> Spring Boot是由Pivotal团队提供的全新框架，其设计目的是用来简化新Spring应用的初始**搭建**以及**开发过程**。该框架使用了特定的方式来进行配置，从而使开发人员不再需要定义样板化的配置。

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


##### 搭建项目 
1. 创建Maven 项目 
2. pom.xml导入jar包 
```
<!-- 继承SpringBoot官方指定的父工程 -->
<parent>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-parent</artifactId>
	<version>2.1.6.RELEASE</version>
</parent>

<dependencies>
	<!-- 加入Web开发所需要的场景启动器(SpringMVC) -->
	<dependency>
		<!-- 指定groupId和artifactId即可，版本已在父工程中定义 -->
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-web</artifactId>
	</dependency>
</dependencies>

<!-- Maven构建过程相关配置 -->
<build>
	<!-- 构建过程中所需要用到的插件 -->
	<plugins>
		<!-- 这个插件将SpringBoot应用打包成一个可执行的jar包 -->
		<plugin>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-maven-plugin</artifactId>
		</plugin>
	</plugins>
</build>
```
3. 创建主启动类。
```
/**
 * 主启动类
 * @author Administrator
 *
 */
//标记为SpringBoot应用
@SpringBootApplication
public class SpringBootMain {
	public static void main(String[] args) {
		SpringApplication.run(SpringBootMain.class, args);
	}	
}
```

##### 注解
```
	1）@SpringBootApplication 
			#1. 标记为SpringBoot应用，该类的main方法是SpringBoot应用人口。通过main启动应用。
			#2. 主启动类所在的包和子包会自动扫描，其他不会自动扫码，需要手动扫描。
	2）@RestController
			# @Controller + @ResponseBody结合
					|——	1）@Controller
					|			# 表面为控制器。
					|——	2）@ResponseBody
								# 将java对象转为json格式的数据。











```

