---
title: Springboot
---

##### Spring官网

springboot版本的说明：图中给出的是当前稳定版本，而且是持续更新的，主要抓住GA，通常位置都在第一个，包含有SNAPSHOT的指的是快照也就是不稳定版本。

<img src="C:\Users\69551\AppData\Roaming\Typora\typora-user-images\image-20210425001420606.png" alt="image-20210425001420606" style="zoom:30%;" />

##### 第一个Springboot项目

###### 新建项目

第一步：新建项目，选择Spring Initializr，选择默认即可，默认后面的网址是Spring提供的配置信息网址，IDEA从中提取出来需要配置的东西

<img src="C:\Users\69551\AppData\Roaming\Typora\typora-user-images\image-20210425000437160.png" alt="image-20210425000437160" style="zoom:50%;" />

第二步：为你的项目进行项目配置信息设置。

​	通常来说来说要改的只有组名。介绍一下有哪些东西：

​		（你的工作单位或学习单位，如：com.hbut）；

​		工件指的是项目的名字；

​		类型指你要创建是Maven项目还是Gradle项目，所谓Maven就是帮你把所有的jar包都汇集打包，Gradle暂且不谈；

​		语言就是你的编程语言；

​		打包指的是你的文件将打包成jar文件还是War文件；

​		Java版本就是java语言的版本，通常是8，当然根据实际会有所不同；

​		版本及之后的信息 是 你的项目的基本信息展示：项目版本；项目名称；项目描述；项目的主要文件包（也就是写源码的位置）。

<img src="C:\Users\69551\AppData\Roaming\Typora\typora-user-images\image-20210425000549595.png" alt="image-20210425000549595" style="zoom:50%;" />

第三步：选择你的依赖项，通常来说选择一个Spring Web即可

<img src="C:\Users\69551\AppData\Roaming\Typora\typora-user-images\image-20210425001157339.png" alt="image-20210425001157339" style="zoom:50%;" />

第四步：确认项目文件，以及项目存放的位置。

<img src="C:\Users\69551\AppData\Roaming\Typora\typora-user-images\image-20210425001231571.png" alt="image-20210425001231571" style="zoom:50%;" />

###### 项目目录结构

目录截图如下：

![image-20210425001733735](C:\Users\69551\AppData\Roaming\Typora\typora-user-images\image-20210425001733735.png)

说明：

​	.idea和.mvn：Maven项目的依赖库；

​	src：源码库；分为main和test，分别是主要代码和测试代码；main又分为java和resources，也就是java源码和资源文件，如HelloworldApplication是主要函数入口，使用的是Spring入口；HelloworldApplicationTests则是测试项目的代码；application.properties则是相关配置文件，除了使用.properties作为后缀外有时还使用.yml作为文件后缀。

​	.gitignore等文件则是Maven相关的配置或命令文件，以及一些说明文件

注意：

​	编辑项目时要在HelloworldApplication的同级目录下建包写代码，因为此项目只扫描这个目录下的文件

###### 简单运行

首先创建一个Controller类(controller后面会解释),controller如下:

> 注意:类文件要放在跟启动类同级或者下一目录下

```java
package com.laowang.sptest.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

import java.util.HashMap;

@Controller
public class HelloController {

    @RequestMapping("/")
    @ResponseBody
    public String getHello() {
        return "hello";
    }
}
```

然后在IDEA启动HelloworldApplication文件(这其实是一个Starter),运行后台;

后台运行起来之后,在浏览器中打开localhost:8080/即可打开controller给出的页面:

![运行结果](https://img-blog.csdnimg.cn/20190703090305117.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dqZzgyMDk=,size_16,color_FFFFFF,t_70)

重点说明:

1. 类文件要放在跟启动类同级或者下一目录下,因为springboot默认扫描加载启动类同级或者下级目录的标签类（@RestController，@Service ，@Configuraion，@Component等），假如真需要加载其他目录的标签类，可以通过在启动上配置标签@ComponentScan(具体包)来进行扫描加载。
2. 资源文件默认放到resources下面，templates默认放的是动态文件，比如：html文件，不过要搭配thymeleaf 使用（pom文件中需新加gav）。

总结:

​	springboot主要是通过spring提供的多个starter和一些默认约定，实现项目的快速搭建。

##### application配置文件

###### 文件类型

共有三种格式，分别是：properties；yml；yaml，其中yml和yaml完全等价，所以可视为只有两类

###### 不同文件后缀的差异

properties文件中配置写法是按照key=value方式来写；

yml和yaml文件中配置写法是按照key: value方式来写，其中“ : ”后面必须跟一个空格，这种格式对空格的要求非常的高

###### yaml和yml的用法

在yml中可以声明以下集中配置：

​	属性值：

 ```yaml 
name: qinjiang
 ```

​	对象的两种写法：

``` yaml 
student: 
  name: qinjiang
  age: 3

# 行内写法
student: {name: qinjiang,age: 3}
```

​	数组的两种写法：

``` yaml 
pets: 
  - cat
  - dog
  - pig

# 行内写法
pets: [cat,dog,pig]
```

##### 给属性赋值的几种方法

> ###### 几种注解:
>
> ``` yaml
> @SpingbootApplication
> 	#包含了@Configuration、@EnableAutoConfiguration、@ComponentScan 以及他们的默认属性。
> @Component
> 	#@Component就是把这里的类加入到SpringbootApplication组件里，其实SpringbootApplication也是个组件
> @Controller
> 	# @Controller表示在tomcat启动的时候，把这个类作为一个控制器加载到Spring的Bean工厂，如果不加，就是一个普通的类，和Spring没有半毛钱关系。
> 	# @Controller就是一个注解，当tomcat启动，我们会看到一些JAVA类挥舞着印有@Controller的旗子大喊：
> 	#       " Hey，SpringMVC，I'm  here,please take me to your bean factory!"
> 	#   Controller 可以决定要显示哪一个View。
> 	#   Controller 负责定义和调用Model。
> 	# 作用：
> 	#   控制器接受用户的输入并调用模型和视图去完成用户的需求。当web页面中的超链接和发送HTML表单时，控制器本身不输出任何东西和做任何处理。
> 	#   它只接受请求并决定调用哪个模型构件去处理请求，然后决定用哪个视图来显示模型处理返回的数据。
> @RequestMapping("/映射地址名称<自定义的>")
> 	#@RequestMapping，最终对应的必然是一个方法，方法的功能无非就是进行一些业务的操作，或者返回一个什么东西。
> 	# 我们就是通过这个方法获得了想要的jsp页面，RequestMapping的作用就是提供了一个句柄，让我们可以访问到对应的方法，最终获得我们想要的东西。
> 	# 综上所述，RequestMapping就是一个映射路径。
> 	#
> 	# 作用：
> 	#   @RequestMapping 是一个注解，用来标识 http 请求地址与 Controller 类的方法之间的映射。
> 	#
> 	#方法匹配的完整路径是 Controller 类上 @RequestMapping 注解的 value 值加上方法上的 @RequestMapping 注解的 value 值。
> @ConfigurationProperties
> 	#@ConfigurationProperties用法:
> 	# @ConfigurationProperties(prefix="my")
> @SpringbootTest
> 	#表示测试类
> @Test
> 	#表示测试方法
> @Value("值")
> 	#将使用了本注解的属性赋予"值"
> @Autowired	
> 	#表示自动装配,前面用了@Value的,此处就把value中的值引用过来
> @Qualifier
> 	#表示指定具体的某一对象,与@Autowired连用
> @ConfigurationProperties(prefix="yaml文件中的相应绑定的对象名称(将实体类和配置类绑定起来)")
> 	#使用此注解时,如果没有去官网配置的话,idea会有提示爆红;
> 	#当然也可以通过提示进入官网进行配置:
> 	#	如果当前版本没有这个配置,可以倒退几个版本如2.2.0没有可以进入2.1.9进行查看(在url中进行修改版本)
> 	#其实就是给你一个<dependency>,然后你把这个复制到pom中,其作用就是给你提示,并没有多大用,所以即使没有配置也可以使用;如果配置的话,需要重启一下IDEA,爆红才会消失
> @Validated
> 	# 数据校验
> ```

###### 第一种赋值方式(使用@Value进行数据绑定):

​	通过使用@Value("值")来给pojo类(或者是model类)中的模型对象的属性进行赋值:

``` java
public class Dog{
    @Value("旺财")
	private String name;
    @Value("3")
	private Integer age;
    
    public Dog(){}
    
    //此处省去Getter和Setter以及重写的toString方法
}
```

​	然后通过@Autowired进行对象使用处的属性自动装配:

```java
public class Test{
    public void test{
        @Autowired
        @Qualifier//Qualifier用来表示具体的某一个对象(当需要给多个对象赋值时)
        Dog dog;
        System.out.println(dog);
    }
}
```

###### 第二种赋值方式(使用.yaml文件进行配置):

> 配置->配置绑定->自动装配-> 运行

​	这种方式可以用来进行对其他文件进行配置.

​	使用yaml对属性进行赋值,注意yaml文件必须是application.yaml:

> 这里需要先给出Person类,并加上@ConfigurationProperties(prefix="配置类中的相应名称")
>
> ```java
> 
> /*有关@ConfigurationProperties:
>     @ConfigurationProperties作用：
>     将配置文件中配置的每一个属性的值，映射到这个组件中；
>     告诉SpringBoot将本类中的所有属性和配置文件中相关的配置进行绑定
>     参数 prefix = “person” : 将配置文件中的person下面的所有属性一一对应
> */
> 
> //实体类
> @ConfigurationProperties(prefix="person")
> public class Person{
>     private String name;
>     private Integer age;
>     private boolean happy;
>     private Date birthday;
>     private Map<String,Object> maps;
>     private List<Object> lists;
>     private Dog dog;
>     
>     public Person(){}
>     
>     //此处省去Getter和Setter和toString方法
> }
> ```

​	在类中使用

```yaml
#配置类
#配置类和实体类中如果有属性名称不一致,则会报错
person: 
  name: qinjiang
  age: 3
  happy: false
  birthday: 2019/11/02
  maps: {k1: v1,k2: v2}
  #lists 相当于是数组
  lists: 
    - code
    - music
    - girl
  dog: 
    name: 旺财
    age: 3
```

​	在测试类中仍然需要使用@Autowired进行自动装配:

```java
public class Test{
	@Autowired
    Person person;
    public void test{
        System.out.println(person);
    }
}
```



###### 第三种赋值方式(使用.properties文件进行配置):

> 这种方式有编码的缺陷,可以在 编辑器选项卡->编辑器(editor)->文件编码(file encoding)中,将编码变为utf-8并保存,否则很容易就变成了乱码,因为idea默认的GBK编码(ASCII编码)

​	1. 加载指定的配置文件

```java
//首先在与yaml文件相同的位置新建一个新的.properties文件,文件名随便取都行.
@propertySource(value="classpath:文件名.properties")
//表示指定的配置文件
public class Person(){
    //使用SPEL表达式取出配置文件的值
    @Value("${name}")
    private String name;
    private Integer age;
    //省去部分内容
}
```

​	2. 而在新建的.properties文件中需要写入相应的内容

```properties
name=狂神
```

​	3. 在测试类中仍然需要使用@Autowired进行自动装配

```java
public class Test{
	@Autowired
    Person person;
    public void test{
        System.out.println(person);
    }
}
```

###### 两种注解的区别:

![注解对比](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7KtjyIb9NEaYlz0tCWSiboOYjMibiaov73iaTsiaWEPoArDcAB1Ooibx9uR5JxtacIuicHblEtUI9SrySX2A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

###### 题外话

在yaml文件中还有很多神奇的玩法:

```yaml
#使用Springboot的EL表达式:
person: 
  name: qinjiang${random.uuid} #获得一个id
  age: ${random.int}
    happy: false
  birthday: 2019/11/02
  maps: {k1: v1,k2: v2}
  lists: 
    - code
    - music
    - girl
  dog: 
    name: ${person.hello: hello}_旺财 
    # 如果person中存在hello这个值,就显示这个值,否则显示为后面的默认值hello,并连接上最后的"_旺财"
    age: 3
```

###### 其他内容

1. 松散绑定:在配置类和实体类中可以采用不同的命名规则:实体类中使用 驼峰命名 :firstName,而配置类中使用 横杠命名:first-name
2. JSR303数据校验 :这个就是我们可以在字段是增加一层过滤器验证 ， 可以保证数据的合法性
3. 复杂类型封装:yml中可以封装对象 ， 使用value就不支持

###### JSR303数据校验

> 涉及到的注解:@Validated,在实体类上使用后,将在实体类的属性上开启类型注解如@Email

​	开启@Validated之后,属性均可通过相应的注解进行限制,其源代码在Validation中(一个Maven包)

​	**数据校验的常用参数(注解)**

```txt
@NotNull(message="名字不能为空")
private String userName;
@Max(value=120,message="年龄最大不能查过120")
private int age;
@Email(message="邮箱格式错误")
private String email;
空检查
@Null       验证对象是否为null
@NotNull    验证对象是否不为null, 无法查检长度为0的字符串
@NotBlank   检查约束字符串是不是Null还有被Trim的长度是否大于0,只对字符串,且会去掉前后空格.
@NotEmpty   检查约束元素是否为NULL或者是EMPTY.    Booelan检查@AssertTrue     验证 Boolean 对象是否为 true  @AssertFalse    验证 Boolean 对象是否为 false      
长度检查
@Size(min=, max=) 验证对象（Array,Collection,Map,String）长度是否在给定的范围之内  
@Length(min=, max=) string is between min and max included.
日期检查
@Past       验证 Date 和 Calendar 对象是否在当前时间之前  
@Future     验证 Date 和 Calendar 对象是否在当前时间之后  
@Pattern    验证 String 对象是否符合正则表达式的规则(最常用)
.......等等除此以外，我们还可以自定义一些数据校验规则
```

###### 多环境切换

> profile是Spring对不同环境提供不同配置功能的支持，可以通过激活不同的环境版本，实现快速切换环境；

1. 多配置文件

   1. 配置文件的位置有很多,官方文档中给出的有:

      > file指的是项目文件根目录

      1. 默认情况下的文件位置,并且配置文件的优先级按以下顺序:1最高,4最低
         1. file: ./config/    (项目的根目录中的config目录)
         2. file: ./    (项目的根目录)
         3. classpath: /config/    (类路径目录下的config目录,即src目录中的resource或者java两个目录 中的config目录)
         4. classpath: /    (类路径目录,即src目录中的resource或者java两个目录)

   2. Springboot的多环境配置

      1. spring.profiles.active=test指令,其中"="的前面部分固定,"="后面的内容是指,在你建立了不同的application配置文件之后进行环境选择的
         1. .properties配置文件方式:建立了application-dev.properties和application-test.properties之后,通过上述指令,则会选择执行application-test.properties配置

2. yaml的多文档块

   1. yaml配置文件方式的多环境配置

      1. 通过"---"来实现不同的环境配置:

         ```yaml
         # 第一个是默认环境配置,什么都不写的话就执行第一个
         server:
           port: 8080
         # 要切换环境的话则是通过以下语句,这里使用的是切换到dev版本
         spring:
           profiles:
             active: dev
         ---
         server:
           port: 8081
         spring:
           profiles: dev
         ---
         server:
           port: 8082
         spring:
           profiles: test
         ---
         server:
           port: 8083
         spring:
           profiles: product
         ```

         

3. 配置文件加载位置

4. 拓展:运维小技巧