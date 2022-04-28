# Java框架

## Spring

### 1、Spring简介

* Spring框架是以interface21框架为基础，经过重新设计，并不断丰富内涵后的框架。

* Spring是以使现有技术更加容易使用，整合现有技术框架为理念。

* 学习JAVA的三套件：SSM。即SpringMVC+Spring+Mybatis

  Github地址：https://github.com/spring-projects/spring-framework

  官网地址：https://repo.spring.io/webapp/#/artifacts/browse/tree/General/libs-release-local/org/springframework/spring/5.2.8.RELEASE/spring-5.2.8.RELEASE-dist.zip

  官方文档地址：https://spring.io/projects/spring-framework

```xml
<!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.2.9.RELEASE</version>
</dependency>

```

```xml
<!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>5.2.9.RELEASE</version>
</dependency>

```

#### 1.1、Spring框架的优点

* Spring是一个轻量级的非入侵式的框架
* 控制反转（IOC），面向切面编程（AOP）
* 支持事务的处理，对框架整合的支持

### 2、Spring的组成

![img](http://image.it168.com/cms/2007-10-31/Image/2007103193225.jpg)

* Spring Core核心容器：核心容器提供 Spring 框架的基本功能。核心容器的主要组件是 BeanFactory，它是工厂模式的实现。BeanFactory 使用控制反转 （IOC） 模式将应用程序的配置和依赖性规范与实际的应用程序代码分开。 

* Spring Context Spring 上下文：Spring 上下文是一个配置文件，向 Spring 框架提供上下文信息。Spring 上下文包括企业服务，例如 JNDI、EJB、电子邮件、国际化、校验和调度功能。 

* Spring AOP：通过配置管理特性，Spring AOP 模块直接将面向方面的编程功能集成到了 Spring 框架中。所以，可以很容易地使 Spring 框架管理的任何对象支持 AOP。Spring AOP 模块为基于 Spring 的应用程序中的对象提供了事务管理服务。通过使用 Spring AOP，不用依赖 EJB 组件，就可以将声明性事务管理集成到应用程序中。

* Spring DAO：JDBC DAO 抽象层提供了有意义的异常层次结构，可用该结构来管理异常处理和不同数据库供应商抛出的错误消息。异常层次结构简化了错误处理，并且极大地降低了需要编写的异常代码数量（例如打开和关闭连接）。Spring DAO 的面向 JDBC 的异常遵从通用的 DAO 异常层次结构。 

* Spring ORM：Spring 框架插入了若干个 ORM 框架，从而提供了 ORM 的对象关系工具，其中包括 JDO、Hibernate 和 iBatis SQL Map。所有这些都遵从 Spring 的通用事务和 DAO 异常层次结构。 

* Spring Web 模块：Web 上下文模块建立在应用程序上下文模块之上，为基于 Web 的应用程序提供了上下文。所以，Spring 框架支持与 Jakarta Struts 的集成。Web 模块还简化了处理多部分请求以及将请求参数绑定到域对象的工作。 

* Spring MVC 框架：MVC 框架是一个全功能的构建 Web 应用程序的 MVC 实现。通过策略接口，MVC 框架变成为高度可配置的，MVC 容纳了大量视图技术，其中包括 JSP、Velocity、Tiles、iText 和 POI。 

Spring 框架的功能可以用在任何 J2EE [服务器](http://product.it168.com/files/0402search.shtml)中，大多数功能也适用于不受管理的环境。Spring 的核心要点是：支持不绑定到特定 J2EE 服务的可重用业务和数据访问对象。毫无疑问，这样的对象可以在不同 J2EE 环境 （Web 或 EJB）、独立应用程序、测试环境之间重用

#### 2.1、Spring:the source for modern java

Spring Boot(Build Anything)->Spring Cloud(Coordinate Anything)->Spring Cloud Data Flow(Connect Anything)

* Spring Boot
  * 一个快速开发的脚手架
  * 基与Spring Boot 可以快速开发单个微服务
  * 约定大于配置
  * 需要掌握Spring和SpringMVC

* Spring Cloud
  
  * Spring Cloud是基于Spring Boot实现的
  
* Spring Cloud Data Flow

  * Spring Cloud Data Flow 是基于原生云对 Spring XD 的重新设计，该项目目标是简化大数据应用的开发。

    Spring Cloud Data Flow 简化了专注于数据流处理的应用程序的开发和部署。它的体系结构包含的主要概念有：应用程序、Data Flow Server 和运行时环境。

    Spring Cloud Data Flow 为基于微服务的分布式流处理和批处理数据通道提供了一系列模型和最佳实践。

### 3、IOC理论

* 传统的业务实现

  1.UserDao 接口

  ```java
public interface UserDao{
  	void getuser();
} 
  ```

  2.UserDaoImpl 实现类

  ```java
public class UserDaoimpl implements UserDao{
  	public void getuser(){
  		System.out.println("默认获取用户信息");
  	}
  }
  ```
  
  3.UserService 业务接口
  
  ```java
  public interface UserService{
  	void getUser();
  }
  ```
  
  4.UserServiceImpl 业务实现类
  
  ```java
  public class UserServiceimpl implements UserService{
  	private UserDao userdao; //= new UserDaoimpl();//UserDaoMysqlimpl();
      public void setUserDao(UserDao userdao){
          this.userdao = userdao;
      }
          
  	public void getUser(){
  		userdao.getUser();//业务层调Dao层
  	}
  }
  ```
  
  用户实际调用的是业务层，是不会接触Dao层的，用户调用的只有业务层的方法
  
  ```java
  public static void main(String[] args){
  	UserService uservice = new UserServiceimpl();
  	((UserServiceimpl)userservice).setUserDao(new UserDaoimpl())
  	userservice.getUser();
  	
  }
  ```
  
  如果这时需要新增一个连接，比如加一个mysql层，
  
  ```java
  public class UserDaoMysqlimpl implements UserDao{
  	public void getUser(){
  		System.out.println("mysql")
  	}
  }
  ```
  
  这时候就必须要去UserServiceimpl中去修改userdao对象,这样就是在原有代码上进行了修改，用户的需求可能会影响我们原来的代码，会破坏程序的完整性，如果我们在UserServiceimpl中加一个set接口,就可以动态实现值的注入.当没有这个set接口时，程序是主动new对象，控制权在程序员手上，如果用set接口，程序就不再具有主动性，对象是被动注入的，这就是控制反转的思想，它从本质上解决了问题，我们不再需要去管理对象的创建了，系统耦合性大大降低

* IOC本质

  IOC(Inversion of Control,控制反转)是一种通过描述(XML或注解)并通过第三方去实现生产或获取特定对象的方式。这是一种设计思想，在Spring中实现控制反转的是IOC容器，其实现方法有依赖注入(Dependency injection)等方法

* 我们采用XML方式配置Bean的时候，Bean的定义信息是和实现分离的，而采用注解的方式将两者合为一体，Bean的定义信息直接以注释的形式定义在实现类中，从而达到零配置的目的

  ```java
  /*hello对象是由Spring来创建的
  对象的属性是由Spring容器来设置的
  在xml文件中使用Spring来创建对象，在Spring里称作Bean，这个Bean就是Spring容器，
  spring容器来设置属性的核心是set方法
            一个bean相当与帮你new了一个对象
  bean的id是bean的唯一标识符，相当于对象名，class相当于要new的对象的类，它的值是要new的类的全路径
  bean的id在所有的bean容器中是唯一的，这个东西是bean的名称
  id：   确定该Bean的唯一标识，容器对该Bean的管理、访问，以及该Bean的依赖关系，都通
         过该属性完成。Bean的id属性在Spring容器中应该是唯一的；(字母开头，字母数字组成)
  class：指定该Bean的实现类，而不是接口，通常情况下Spring会直接使用new关键字创建该
         Bean的实例，因此，这里必须提供Bean的实现类的类名。
  name:  可以指定别名
         property相当于给对象中的属性设一个值
  */
  
  //其它的一些属性以及其对应的属性类型和默认值以及说明
  /*
  abstract	Boolean	false	指明该Bean作为父类，spring容器不会为该类创建对象
  autowire-candidate	Boolean	true	指明该Bean是否作为自动装配的候选Bean
  autowire	String	no	指明该Bean是否采用自动装配及采用自动装配的规则
  depends-on	String	——	显示指明该Bean依赖的其他Bean(确保依赖Bean先实例化)
  destroy-method	String	——	指明该Bean默认的回收方法
  factory-bean	String	——	工厂方法创建对象时，指定工厂Bean
  factory-method	String	——	工厂方法创建对象时，指定工厂Bean中创建对象的方法
  init-method	String	——	指明该Bean默认的初始化方法
  lazy-init	Boolean	false	指明该Bean的延迟初始化行为(只对单例模式起作用)
  name	String	——	指明该Bean的别名alias，可以有多个，可以其他Bean重名
  parent	String	——	指明该bean需要继承的父类Bean
  primary	Boolean	false	自动装配若候选Bean不止一个，则此属性为true的Bean当选
  scope	String	singleton	指明该Bean的作用域
  */
  ```

* IOC创建对象的方式

  在配置文件加载的时候，容器(bean)中管理的对象就已经初始化了

  * 使用无参构造方法创建对象(默认情况)

  * 使用有参构造方法创建对象

    * 可以通过参数的下标值来给对应参数赋值

      使用<constructor-arg>标签，在其中使用index属性指定对应下标的参数

    * 可以通过参数的类型来给对应参数赋值

      使用<constructor-arg>标签，在其中使用type属性指定对应类型的参数，不过当有多个类型相同的参数时就不好用了

    * 可以通过引用其他的bean或者直接引用参数名给参数赋值

      使用<constructor-arg>标签，在其中使用name标签指定对应的参数

* 配置Bean的依赖关系

  Spring有两种依赖注入方式(设值注入和构造注入)，但不管哪种注入，都需要为参数传入参数值，而java类的成员变量可以是各种数据类型，除了基本类型、字符串类型、还可以是其他java实例，也可以是java集合、数组等，Spring允许通过如下元素为setter方法、构造器参数指定参数值：

  - value：指定参数值是基本类型及其包装、字符串类型；
  
  - ref：指定参数值是容器中的另一个Bean实例；
  
  - bean：指定参数值是一个嵌套Bean实例；
  
  - list、set、map及props：指定参数值是集合。
  
    **Spring配置说明**
  
* bean:就是创建bean容器，其中的属性说明：
    * id：bean的唯一标识符，也就是对象名
  * class：bean对象对应的全限定名：包名+类名，即全路径
    * name：设置别名，并且可以设置多个别名，可以通过这些别名来访问bean对象
* alias:就是设置别名，设置了别名就可以通过这个别名来访问对象
  
* import：一般用于团队开发，它可以将多个配置文件导入合并成一个，就是当有多个XML配置文件的时候，可以在一个XML文件里面使用<import>标签以及resource属性来导入XML文件，导入进来的多个XML文件就可以通过该XML文件进行同时加载
  
* 依赖注入

  * 构造器注入(即上面的IOC创建对象方式)

  * 通过set方法注入(重点使用)

    * 依赖：bean对象的创建依赖于容器
    * 注入：bean对象中的所有属性由容器来注入
    * 对于不同类型参数的注入：
      * String类型：直接用<propery>标签中的value属性来设置参数值
      * 引用类型：用<propery>标签中的ref属性来指定引用的bean
      * 数组类型：用<propery><propery/>标签中的<array>标签中的<value><value/>标签来设置参数，参数写在value标签中
      * List类型：用<propery><propery/>标签中<list>标签中的<value><value/>标签来设置参数，参数写在value标签中
      * Map类型：用<propery><propery/>标签中的<map>标签中的<entry/>标签中的key属性和value属性来设置参数值
      * Set类型：用<propery><propery/>标签中的<set>标签中的<value><value/>标签来设置参数，参数写在value标签中
      * Porperties类型：要设置为空的画可以用<propery/>标签中的value属性设置为空串，或在<propery><propery/>标签中写一个<null/>，如果不设置为空的话就可以在<propery><propery/>标签中的<props></props>标签中的<prop></prop>来设置，用其中的key属性设置key值，value值写在标签中

  * 第三方注入

    * p命名空间注入(这个东西对应set注入)

      要在XML文件头新增一个东东：

      ```xml
      xmlns:p="http://www.springframework.org/schema/p"
      <!--然后使用p命名空间来注入参数-->
      <bean id="user" class="....." p:要实例化对象中的参数名="参数值"/>
      ```

      c命名空间注入(这个东西对应构造器注入，要在类里面写上有参构造)

      要做XML文件头新增一个东东：

      ```xml
      xmlns:c="http://www.springframework.org/schema/c"
      <!--使用c命名空间来注入参数-->
      <bean id="user" class=".,...." c:要实例化对象中的参数名="参数值>
      ```

* Bean的作用域

  * singleton：单例模式，即容器只会创建一个Bean实例，容器每次返回的都是同一个Bean实例，这个是默认模式，可以在bean里面加上scope属性，其值就是作用域

    ```
    <bean id=".." class=".." scope="singleton">
    ```

    

  * prototype:原型模式，即容器可以创建多个Bean实例，容器每次返回的都是一个新的Bean实例

  * request:该模式进队HTTP请求产生作用，在该模式下时，每次HTTP请求都会创建与一个新的Bean实例，仅适用于WebApplicationContext环境

  * session:该模式仅用于HTTP Session，同一个Session共享一个Bean实例，不同的Session使用不同的实例，仅适用于WebApplicationContext环境

  * application

  * websocket

  * application与websocket合称为globalSession，一般用于Portlet应用环境，仅适用于WebApplicationContext环境

* Bean的自动装配

  对象的各个参数值手动设置是手动装配，Spring可以实现Bean的自动依赖，可以在上下文中自动寻找，并自动给bean装配属性，Spring有三种装配方式：

  * 在XML中显示的配置

  * 在JAVA中显示配置

  * 隐式的自动装配(常用)

    在bean中有一个autowire属性，这个东西就是做自动装配的，属性值是装配的方式

    ```
    <bean id=".." class="....." autowire="..">
    装配方式有：
    byName：会自动在容器上下文中查找和自己对象set方法后的值对应的bean的id，用这个的话就得给bean设置id，且每一个bean的id要跟set后的值一致
    byType：会自动在容器上下文中查找和自己对象类型对应的bean，用这个的话每个bean的class要保证唯一
    ```

* 使用注解实现自动装配

  上述的自动装配在我们写多了就会容易忘，所以我们得用新版的注解来进行自动装配，jdk1.5，Spring2.5版本以上就支持注解了

  要使用注解也要在XML中导入约束(只是在原有的基础上多了一点东东)

  ```xml
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
  ```

  加上了这个约束后，我们就可以不用再在配置文件里写大量的参数赋值了，我们直接在写类的时候直接在写上变量时或者set方法上(我们甚至可以不写set方法，因为注解是使用反射进行实现的)加上@Autowired，就可以实现自动装配，不过这个是像byName那样的，id要与对应变量名一样

  注意：

  ```xml
  @Nullable 这个东西可以标记字段，说明这个字段可以为null值
  @Autowired后面可以跟属性required，如果这个属性的值标记为false了，就说明这个字段可以为null值
  @Qualifier后面可以跟属性value，默认为空值，可以自己设置。当bean中有多个id不一样的时候，可以用这个来增加自动装配的范围
  @Resource这个是java原生的注解，比Spring的注解更好用(估计),它的实现跟上面差不多，不过它整合了byName与byType的功能，都不符合才会报错，也可以通过设置name让它能匹配更多的变量名
  ```

* 使用注解开发(在SpringBoot中会很常用)

  * 在使用注解时，要确定aop的包已经导入了，不然用不了
  * 使用注解前，要确定注解约束都已经设置完毕
  * 使用注解开发可以实现少配置开发
    * @Component:组件，这个东西在类里面头部直接写上，说明这个类被Spring管理了，然后在配置文件中写上<context:Conponent-scan base-package="包">，这个表示要扫描的包，即哪个包下的带这个注解的类会被Spring托管，然后可以直接不用写bean
    * @Value(属性值):可以直接给参数赋值
    * @Component的衍生注解：Web开发中，会有MVC三层架构分层，会有以下功能相似的注解，功能都与@Component一样
      * Dao:@Repository
      * Service:@Service
      * controller:@Controller
    * @Scope(模式值)：该注解可以设置bean的作用域
  * 注解的使用
    * 一般bean还是要写在XML文件中，方便我们管理
    * 注解只用来实现值的注入

* 使用JavaConfig实现配置

  完全使用java的方式来配置Spring，使用这种方法可以直接不适用XML文件来配置，在Spring4之后，都推荐使用JavaConfig来实现配置了

  * 可以在一个Java的类里面来配置，我们在这个类的头上加上@Configuration,这个类就会变成配置类，这个配置类也会被Spring托管，这个类就相当于XML配置文件
  * 在配置类中，可以使用@ComponentScan("要扫描的包")来指定哪些包下带有@Component注解的类会被Spring托管
  * 在配置类中，可以使用@Bean来设置要返回要注入到Bean容器中更多对象
  * 在配置类中，可以使用@Import来引入其它的配置类，这个就相当于XML配置文件中的import标签

### 4.代理模式

这是SpringAOP的底层实现

#### 4.1代理模式的分类

编码原则：少用继承，用组合

* 代理模式的好处：
  * 使真实角色的操作更加纯粹，不用操作公共业务
  * 公共业务可以交给代理角色，实现业务分工
  * 公共业务发生扩展的时候，方便集中管理
* 代理模式的缺点：
  * 一个真实角色会产生一个代理角色，代码量会增加一倍，效率降低，这个缺点可以使用动态代理(反射)解决

##### 4.1.1静态代理

代理模式呢，就好比一个人要租房，这个人要找房东才能完成租房这件事，但是房东只想把房子租给你收钱，不想弄什么合同什么乱七八糟的事，所以这个人会找不到房东，这个时候就有一个中介可以帮房东完成这些事，这个人只要找这个中介就可以租到房，这就是代理模式。在代理模式中，有这样的一些角色：

* 抽象角色：一般使用接口或抽象类来解决，即真实角色和代理角色要实现的事

* 真实角色：被代理的角色，即类似上面例子的房东角色

* 代理角色：代理真实角色，代理真实角色后，会做一些附属操作(一般是真实角色做不到的事)，即上面例子的中介

* 客户：访问代理角色，就是上面例子的要租房的人

  ```java
  //要实现的事情
  public interface chuzu{
  	void zufang();
  }
  ```

  

  ```java
  //房东
  public class fangdong implements chuzu{
      
  	public void zufang(){
  		System.out.println("把房子租出去");
  	}
  }
  ```

  ```java
  //中介类
  public class zhongjie implements chuzu{
  	pravate fangdong fd;
  	public void setfd(fangdong fd){
          this.fd = fd;
      }
      public void zufang(){
          log("1");
          fd.zufang();
      }
      //扩展的业务
      public void iog(String meg){
          System.out.println("use"+meg+"method");
      }
  }
  ```

  ```java
  //客户
  public static void main(String[] args){
      fangdong fd = new fangdong();
      zhongjie zj = new zhongjie();
      zj.setfd(fd);
      zj.zufang;
  }
  ```

* AOP实现机制：

  

  即不改动原来的代码，在业务层使用代理来添加新的功能

##### 4.1.2动态代理

* 动态代理和静态代理的角色一样
* 动态代理的代理类是动态生成的
* 动态代理分为两大类
  * 基于接口（JDK动态代理）的动态代理
  * 基于类的动态代理
  * 基于java字节码（javassist）实现

* 要了解JDK中的两个类：

  * Proxy:代理类

    * 这个东西提供了创建动态代理类和实例的静态方法，它也是由这些方法创建的所有动态代理类的超类

  * InvocationHandler:调用处理程序

    * 这个东西是一由代理实例的调用处理程序实现的接口，每个代理实例都有一个关联的调用处理程序，当在代理实例上调用方法时，方法调用将被编码并分派到其调用处理程序的invoke方法

    * 这个接口里面只有一个方法：invoke方法，其内容如下：

      ```java
      Object invoke(Object proxy,方法 method,Object[] args)
      	throw Throwable
      其中：
      proxy - 调用该方法的代理实例 
      method -所述方法对应于调用代理实例上的接口方法的实例。 方法对象的声明类将是该方法声明的接口，它可以是代理类继承该方法的代理接口的超级接口。 
      args -包含的方法调用传递代理实例的参数值的对象的阵列，或null如果接口方法没有参数。 原始类型的参数包含在适当的原始包装器类的实例中，例如java.lang.Integer或java.lang.Boolean 
      Throwable - 从代理实例上的方法调用抛出的异常。 异常类型必须可以分配给接口方法的throws子句中声明的任何异常类型java.lang.RuntimeException检查的异常类型java.lang.RuntimeException或java.lang.Error 。 如果检查的异常是由这种方法是不分配给任何的中声明的异常类型throws接口方法的子句，则一个UndeclaredThrowableException包含有由该方法抛出的异常将通过在方法调用抛出代理实例。 
      ```

* 动态代理的好处：

  * 一个动态代理类代理的是一个接口，一般就是对应的一类业务
  * 一个动态代理类可以代理多个类，只需要实现同一个接口即可

### 5.AOP

AOP(Aspect Oriented Programming)，面向切面编程，是通过预编译方式和运行期间动态代理实现程序功能的同一维护的一种结束。AOP是OOP的延续，是软件开发的一个热点，也是Spring框架中的一个重要内容，是函数时编程的一种衍生范型。利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑个部分之间的耦合性降低，提高程序的可复用性，提高开发效率

**缺少图片**

上图中的名词解释：

* 横切关注点：跨越应用程序多个模块的方法或功能。即与我们业务逻辑无关，但我们需要关注的部分，如日志，安全，缓存，事务等
* 切面(Aspect)：横切关注点被模块化的特殊对象，它是一个类
* 通知(Adice):切面必须完成的工作，它是切面类中的一个方法
* 目标(Target):被通知的对象(被代理的对象)
* 代理(Proxy):向目标对象应用通知之后创建的对象(生成的代理类)
* 切入点(PointCut):切面通知执行的”地点“的定义
* 连接点(JoinPoint):与切入点匹配的执行点

#### 5.1AOP在Spring中的作用

* 提供声明式事务：允许用户自定义切面

* SpringAOP中，通过Advice定义横切逻辑，Spring中支持5中类型的Advice：

  * MthodBeforeAdvice：目标方法实施前增强

  * AfterReturningAdvice：目标方法实施后增强
  
  * ThrowsAdvice 异常抛出增强
  
  * IntroductionAdvice 引介增强，为目标类添加新的属性和方法。可以构建组合对象来实现多继承
  
  * MethodInterceptor 方法拦截器，环绕增强，在方法的前后实施操作
  
  即AOP在不改变原有代码的情况下拓展业务

#### 5.2 AOP的实现：

##### 方式1：使用原生Spring API接口(即使用bean配置)

实现AOP需要导入一个包，在Pom文件里写上

```xml
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-aop -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-aop</artifactId>
            <version>5.2.9.RELEASE</version>
        </dependency>

        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjweaver</artifactId>
            <version>1.9.6</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/aspectj/aspectjrt -->
        <dependency>
            <groupId>aspectj</groupId>
            <artifactId>aspectjrt</artifactId>
            <version>1.5.4</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/org.aspectj/aspectjrt -->
        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjrt</artifactId>
            <version>1.9.6</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/org.springframework/spring-aspects -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-aspects</artifactId>
            <version>5.2.9.RELEASE</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/org.aspectj/aspectjtools -->
        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjtools</artifactId>
            <version>1.9.6</version>
        </dependency>

```

然后要写Log类来实现Advice接口，配置Spring容器(Bean)，注意要引入aop约束，然后要对aop进行配置

```xml
<aop:config>
<!--切入点--><!--expression:表达式，execution(要执行的位置),这个要执行的位置要精确到哪个类下的多少个方法,类名.*(..)表示这个类下的所有方法-->
    <aop:pointcut id="切入点id" expression="execution(* com.文件名.包名.类名.*(..))">
        <!--执行环绕增加--><!--表示要将哪个类插入到哪个插入点下-->
        <aop:advisor adv-ref="log" pointcut-ref="pointcut"/><!--将log类插入到pointcut这个插入点中-->
        <aop:advisor adv-ref="after-log" pointcut="pointcut">
    </aop:pointcut>  
</aop:config>
```

这个方法有时候会报错，因为API找不到之类的错误，处理很麻烦

##### 方式2：使用自定义类

将需要中间插入的方法写在一个类中，比如：

```java
public class div{
	public void before(){
		System.out.println("before the method do");
	}
	public void after(){
		System.out.println("after the method done");
	}
}
```

这个类中的两个方法是我们想要在业务方法执行前后执行的方法，我们可以在配置文件中这样定义：

```XML
<bean id = "div" class = "....要插入方法所在的类"/>
<aop:conifg>
	<!--引用自定义的切面，ref表示要引用的类-->
	<aop:aspect ref="div">
		<aop:pointcut id="设置切入点id" erxpression="execution(这里写上要将切面插入的切入点的具体位置，有时要准确到某个方法，不过一般写的是所有方法)">
		<!--后面就可以设置切入点前后要执行的方法了-->
		<aop:before method = "方法名" pointcut-ref="切入点id"/>
		<aop:after method = "方法名" pointcut-ref="切入点id"/>
	</aop:aspect>
</aop:config>
```

##### 方式3：使用注解实现

在一个类前使用@Aspect可以将这个类标注为切面，比如这样：

```java
@Aspect
puvlic class div{
	//然后可以在这个类里面写上切面要执行的方法，并且指定切入点，指定切入点使用@Before,@After等
	@Before("execution("切入点位置")")//要在后面跟上切入点位置
	public void before(){
		System.out.println("before method doing");
	}
	@After("execution("切入点位置")")
	public void after(){
		System.out.println("after method done");
	}
	@Around("execution("切入点位置")")//这个是环绕增强，我们可以给定一个参数，表示我们要获取处理切入的点
	public void around(ProceedingJoinPoint jp){
		System.out.println("before around");
		Object proceed = jp.proceed(); //执行方法
		System.out.println("after around");
		
	}
}
```

这个方法也要像之前使用注解注入时一样，要开启注解，并且要在xml文件中配置bean或者直接在类上加注解@Component

### 6.整合Mybatis

步骤：

* 导入相关jar包
  * junit
  * mybatis
  * mysql
  * spring
  * spring-jdbc
  * aop织入
  * mybatis-spring 这个包是专门用来整合spring和mybatis的
* 编写配置文件
* 测试

##### 6.1 Mybatis大致

MyBatis 是一款优秀的持久层框架，它支持定制化 SQL、存储过程以及高级映射。MyBatis 避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集。MyBatis 可以使用简单的 XML 或注解来配置和映射原生信息，将接口和 Java 的 POJOs(Plain Ordinary Java Object,普通的 Java对象)映射成数据库中的记录。

* 编写实体类

  ```java
  @Data
  public class User{
  	private int id;
      private String name;
      private String pud;
  }
  ```

* 编写核心配置文件

  在src下的resources目录下创建Mybatis的著配置文件，其主要作用是提供连接数据库用的驱动，数据名称，编码方式，账号密码等。

  ```xml
  <!--mybatisfonfig.xml-->
  <?xml version="1.0" encoding="UTF-8"?>
  <!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "http://mybatis.org/dtd/mybatis-3-config.dtd">
  <configuration>
  
      <!-- 别名 -->
      <typeAliases>
          <package name="pojo"/><!--这里的别名是某个包名-->
      </typeAliases>
      <!-- 数据库环境 -->
      <environments default="development">
          <environment id="development">
              <transactionManager type="JDBC"/>
              <dataSource type="POOLED">
                  <property name="driver" value="com.mysql.jdbc.Driver"/>
                  <property name="url" value="jdbc:mysql://localhost:3306/mybatis?characterEncoding=UTF-8"/>
                  <property name="username" value="root"/>
                  <property name="password" value="root"/>
              </dataSource>
          </environment>
      </environments>
      <!-- 映射文件 -->
      <mappers>
          <mapper class = "到下面的接口即UserMapper"/>
      </mappers>
  
  </configuration>
  <!--有时候xml文件会加载不出来，一般是maven的静态资源加载问题，要在pom配置文件里加上<bulid>来解决-->
  ```

* 编写接口

  ```java
  //一般都是在上面别名的包的同级目录下新建一个mapper包，这个接口就写在里面
  public interface UserMapper{
  	public List<User> selectUser();
  }
  ```

* 编写Mapper.xml

  ```xml
  <!--这个配置文件也是写在mapper包下的-->
  <?xml version="1.0" encoding="UTF-8"?>
  <!DOCTYPE mapper
          PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
          "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
  
  <mapper namespace="..到上面的接口处即UserMapper">
      <select id="selectUser" resultType="user">
          select * from  mybatic.user;
      </select>
  </mapper>
  ```

* 测试

  ```java
  import org.apache.ibatis.io.Resources;
  import org.apache.ibatis.session.SqlSession;
  import org.apache.ibatis.session.SqlSessionFactory;
  import org.apache.ibatis.session.SqlSessionFactoryBuilder;
  import pojo.Student;
  
  import java.io.IOException;
  import java.io.InputStream;
  import java.util.List;
  
  public class TestMyBatis {
  
      public static void main(String[] args) throws IOException {
          // 根据 mybatisconfig.xml 配置的信息得到 sqlSessionFactory
          String resource = "mybatisconfig.xml";
          InputStream inputStream = Resources.getResourceAsStream(resource);
          SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
          // 然后根据 sqlSessionFactory 得到 session
          SqlSession session = sqlSessionFactory.openSession(true);
          
          
          
          UserMapper mapper = session.getMapper(UserMapper.class);
         
          List<User> userList = session.mapper.selectUser();
          for (User user : userList) {
              System.out.println(user);
          }
  
      }
  }
  ```

##### 6.2 整合Spring和Mybatis

当使用的Mybatis版本在3.5以上，Spring版本在5.0以上时，要使用Spring-Mybais2.0版本的jar，不然就用1.3版本的

步骤：

* 编写数据源配置
* 在配置文件中配置sqlSessionFactory和sqlSessionTemplate对象
* 给接口添加实现类
* 将写的实现类注入到Spring中
* 测试

* 然后我们就要开始配置spring的xml文件了

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xmlns:context="http://www.springframework.org/schema/context"
      xsi:schemaLocation="http://www.springframework.org/schema/beans
          https://www.springframework.org/schema/beans/spring-beans.xsd
          http://www.springframework.org/schema/context
          https://www.springframework.org/schema/context/spring-context.xsd">
  
      <!--配置数据资源DataSource：使用Spring数据源替换mybatis的配置 c3p0，dbcp druid，用spring提供的jdbc--><!--这些东西就是一些关于数据库的配置-->
      <bean id = "dataSource" class="DriMangerDataSource(这个东西是从依赖里导入的)">
      	 <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
           <property name="url" value="jdbc:mysql://localhost:3306/mybatis?characterEncoding=UTF-8"/>
           <property name="username" value="root"/>
           <property name="password" value="root"/>
      </bean>
      <!--配置sqlSessionFactory-->
  	<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
    		<property name="dataSource" ref="dataSource" />
    		<!--还要绑定mybatis配置文件-->
    		<property name="configLocation" value="calsspath:上面(6.1中)那个mybatis的配置文件的位置">
          <property name="mapperLocations" value="calsspath:mapper目录下的所有xml文件" >
  	</bean>
  	<!--配置sqlSession-->
  	<bean id="sqlSession" class="...SqlSessionTemplate">
  		<!--要通过构造器给它注入，以为它没有set方法-->
  		<constructor-arg index="0" ref="sqlSessionFactory">
  	</bean>
  	<!--以上两个配置是固定写法-->
      <bean id="userMapper" class="6.1中的UserMapper接口的实现类的位置">
          <property name="sqlSession" ref="sqlSession"/>
      </bean>
  </beans>
  ```

  ```java
  //6.1中的UserMapper接口的实现类
  public class UserMapperImpl impliments UserMapper{
  	private SqlSeesionTemplate sqlSession;//我们原来的所有操作都用sqlSession来执行，现在用												SqlSessionTemplate
  	public void setSqlSession(SqlSessionTemplate sqlSession){//用来注入的set方法
  		this sqlSession = sqlSession;
  	}
  	public List<User> selectUser(){
  		return sqlSession.各种方法(查找，删除，修改，增加等等方法);
  	}
  }
  ```

  测试：

  ```java
  public static void main(String[] args){
  	ApplictionContext context = new ClassPathXmlApplicationContext("spring的xml文件");
  	UserMapper userMapper = context.getBean("userMapper",UserMapper.class);
  	for(User user:userMapper.selectUser()){
  		System.out.println(user);
  	}
  }
  ```

  我们甚至可以使用一个整体的xml文件来对上面的文件进行整合，使上面的配置文件固定

### 7.声明式事务

* 把一组业务当成一个业务来做，要么都成功、要么都失败
* 事务在项目开发中是十分重要的，设计到数据的一致性问题
* 要确保完整性和一致性

##### 7.1事务的ACID

* 原子性
* 一致性
* 隔离性
  * 多个业务操作统一资源时，要防止数据损坏
* 持久性
  * 事务一旦提交，数据都不会再被影响了

##### 7.2 Spring中的事务管理

* 声明式事务：AOP

  * 配置声明式事务：在Spring的配置文件中添加：

    ```xml
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
      <constructor-arg ref="dataSource" />
    </bean>
    ```

    传入的 `DataSource` 可以是任何能够与 Spring 兼容的 JDBC `DataSource`。包括连接池和通过 JNDI 查找获得的 `DataSource`。

    注意：为事务管理器指定的 `DataSource` **必须**和用来创建 `SqlSessionFactoryBean` 的是同一个数据源，否则事务管理器就无法工作了。

  * 然后结合AOP，实现事务的织入

    ```XML
    <!--首先要配置事务的类（通知）-->
    <tx:advice id="txAdvice" transcaction-manger="transactionManager">
    	<!--给哪些方法配置事务-->
    	<!--配置业务的传播特性，就是在指定方法后的配置，默认是选择REQUIRED，即如果当前没有事务，就新建一个事务-->
    	<tx:attributes>
    		<tx:method name="方法名" />
    	</tx:attributes>
    </tx:advice>
    <!--配置事务切入-->
    <aop:config>
    	<aop:pointcut id="txPointCut" expression="execution("..")"/>
    	<aop:advisor advice-ref="txAdvice" pointcut="txPointCut"/>
    </aop:config>
    ```

    

* 编程式事务：在代码中操作，因为会改变原有代码，不推荐使用这个方式

* 配置事务的原因：
  * 如果不配置事务，可能存在数据提交不一致的情况
  * 如果我们不在Spring中去配置声明式事务，我们就需要在代码中手动配置事务
  * 事务在项目开发中十分重要

## SpringMVC

SpringMVC的执行流程：

![MVC执行流程](C:\Users\qj176\Pictures\Camera Roll\MVC执行流程.PNG)

- ###  DispatcherServlet：前端控制器

​      **用户请求到达前端控制器，它就相当于mvc模式中的c，dispatcherServlet是整个流程控制的中心，**

​      **由它调用其它组件处理用户的请求，dispatcherServlet的存在降低了组件之间的耦合性。**

 

- ### HandlerMapping：处理器映射器

　　　**HandlerMapping负责根据用户请求url找到Handler即处理器，springmvc提供了不同的映射器实现不同的映射方式，**

　　  **例如：配置文件方式，实现接口方式，注解方式等。**

 

- ###  Handler：处理器

　　 **Handler 是继DispatcherServlet前端控制器的后端控制器，在DispatcherServlet的控制下Handler对具体的用户请求进行处理。**

​    **由于Handler涉及到具体的用户业务请求，所以一般情况需要程序员根据业务需求开发Handler。**

 

- ### HandlAdapter：处理器适配器

　　**通过HandlerAdapter对处理器进行执行，这是适配器模式的应用，通过扩展适配器可以对更多类型的处理器进行执行。**

 

- ### ViewResolver：视图解析器

　　**View Resolver负责将处理结果生成View视图，View Resolver首先根据逻辑视图名解析成物理视图名即具体的页面地址，**

　　**再生成View视图对象，最后对View进行渲染将处理结果通过页面展示给用户。**

 

- ### View：视图

　　**springmvc框架提供了很多的View视图类型的支持，包括：jstlView、freemarkerView、pdfView等。我们最常用的视图就是jsp。**

　　**一般情况下需要通过页面标签或页面模版技术将模型数据通过页面展示给用户，需要由程序员根据业务需求开发具体的页面。**

### MVC的发展

* Model 1时代：

  早期的web开发中，采用的基本都是Model 1

  * Model 1分为两层：视图层和模型层

  * Model 1的优点：架构简单，适合小项目开发

  * Model 1的缺点：JSP职责不是单一的，职责国多，不利于维护

* Moderl 2时代：

  Model 2把一个项目分为3部分：视图层，模型层，控制层

  1.客户端发送请求

  2.Servlet接收请求数据，调用对应业务逻辑方法

  3。业务处理完毕，返回更新后的数据给Servlet

  4.Servlet转向到JSP，由JSP来渲染页面

  5.响应给前端更新后的页面

  其中：

  * Controller的职责：
    * 获取表单数据
    * 调用业务逻辑
    * 转向指定页面
  * Model的职责：
    * 业务逻辑
    * 保存数据的状态
  * View的职责：
    * 显示页面

### 1.Servlet回顾

使用Maven创建工程时，要导入这些包：

* junit
* springframework
* servlet.api
* servlet.jstl
* servlet.jsp

```xml
<!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api -->
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>4.0.1</version>
    <scope>provided</scope>
</dependency>
<!-- https://mvnrepository.com/artifact/javax.servlet.jsp.jstl/jstl -->
<dependency>
    <groupId>javax.servlet.jsp.jstl</groupId>
    <artifactId>jstl</artifactId>
    <version>1.2</version>
</dependency>
<!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.2.9.RELEASE</version>
</dependency>
<!-- https://mvnrepository.com/artifact/junit/junit -->
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.13.1</version>
    <scope>test</scope>
</dependency>
<!-- https://mvnrepository.com/artifact/javax.servlet.jsp/javax.servlet.jsp-api -->
<dependency>
    <groupId>javax.servlet.jsp</groupId>
    <artifactId>javax.servlet.jsp-api</artifactId>
    <version>2.3.3</version>
    <scope>provided</scope>
</dependency>

```

可以不通过模板创建web项目，可以只通过普通maven项目来变成web项目，只需要右键模块添加框架支持，选择webapplication即可

编写一个Servlet

```java
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class HelloServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //1.获取前端参数
        String method = req.getParameter("method");
        if(method.equals("add")){
            req.getSession().setAttribute("msg","执行了add方法");
        }
        if(method.equals("delete")){
            req.getSession().setAttribute("msg","执行了delete方法");
        }
        //2.调用业务层

        //3.视图转发或重定向
        req.getRequestDispatcher("/WEB-INF/jsp/test.jsp").forward(req,resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req,resp);
        //1.获取前端参数

        //2.调用业务层

        //3.视图转发或重定向

    }
}
```

JSP页面

```jsp
<!--test.jsp-->
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>

    ${msg}

</body>
</html>

```

```jsp
<!--from.jsp-->
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<form action="/hello" method="post">
    <input type="text" name="method">
    <input type="submit">
</form>
</body>
</html>
```

在web.xml中配置Servlet

```xml
    <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>com.qin.Servlet.HelloServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
```

就可以实现一个简单的请求

MVC框架要完成的事：

* 将url映射到java类或java类的方法
* 封装用户提交的数据
* 处理请求，即调用相关的业务处理
* 封装响应数据
* 将响应的数据进行渲染,由jsp或html页面显示数据

我们的全栈知识：后台，前端，数据库，运维

MVVM：跟MVC相关的一个框架，VM是ViewModel。

### 2.SpringMVC入门

* SpringMVC的特点：
  * 轻量级
  * 高效，基于请求响应的MVC框架
  * 与Spring兼容性好，无缝结合
  * 约定大于配置
  * 功能强大，拥有RESTFUL，数据验证，格式化，本地化，主题等功能
  * 简洁灵活

* 以前的Spring的Web框架围绕DispatcherServlet设计，这个东东这作用是将请求分发到不同的处理器。

  SpringMVC与其它MVC框架一样，以请求为驱动，围绕一个中心Servlet分派请求及提供其它功能，DispatcherServlet这个东东本质也是一个Servlet(继承自HttpServlet基类)

* SpringMVC的运行原理在1中了

* 搭建一个SpringMVC：

  * 使用Maven来创建，先创建一个空Maven，再添加Web支持，然后导入SpringMVC的所有依赖

  * 配置web.xml，配置DispatcherServlet

    ```xml
     <?xml version="1.0" encoding="UTF-8"?>
    <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee 				 http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
             version="4.0">  
        <!--注册DispatcherServlet-->
        <servlet>
            <servlet-name>springmvc</servlet-name>
            <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
            <!--DispatcherServlet必须要关联一个spring的配置文件-->
            <init-param>
                <param-name>contextConfigLocation</param-name>
                <param-value>classpath:springmvc.xml</param-value>
            </init-param>
            <!--启动级别-->
            <load-on-startup>1</load-on-startup>
            
        </servlet>
        <!--/表示匹配所有的请求(不包括jsp)-->
        <!--/*表示匹配所有的请求(包括jsp)-->
        <servlet-mapping>
            <servlet-name>springmvc</servlet-name>
            <url-pattern>/</url-pattern>
        </servlet-mapping>
    </web-app>    
    ```

    关联的spring配置文件的内容：

    ```xml
    sping的配置写法...
    <!--配置一个处理器映射器-->
    <!--对于这个BeanNameUrlHandlerMapping处理器-->
    <!--配置一个处理器适配器-->
    <!--上面这两个可以自动配置-->
    <!--配置一个视图解析器，这个是必配置的，不可省略，以后可能会用到Thymeleof Freemarker-->
    <bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping"/>
    <bean class="org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter"/>
    <!--视图解析器：DispatcherServlet给它的ModelAndView
    1.获取ModelAndView的数据
    2.解析ModelAndView的视图名字
    3.拼接视图名字，找到对应的视图，即拼接前缀和后缀
    4.将数据渲染到视图上
    -->
    
    <bean calss="org.springframework.web.servlet.view.InternalResourceViewResolver" id="InternalResourceViewResolver">
    	<!--前缀-->
    	<property name="prefix" value="/WEB-INF/jsp/"/>
        <!--后缀-->
    	<property name="suffix" value=".jsp"/>
    <!--对于这个BeanNameUrlHandlerMapping处理器是要指定一个bean的，才能找得到-->
    </bean>
    <!--Handler-->
    <bean id="/hello" class="com.qin.controller.HelloController"/>
    ```
    
    控制器类文件：
    
    ```java
    import org.springframework.web.servlet.ModelAndView;
    import org.springframework.web.servlet.mvc.Controller;
    
    import javax.servlet.http.HttpServletRequest;
    import javax.servlet.http.HttpServletResponse;
    //导入Controller接口
    public class HelloController implements Controller {
    
        @Override
        public ModelAndView handleRequest(HttpServletRequest request, HttpServletResponse response) throws Exception {
            //ModelAndView类，模型视图类
            ModelAndView mv = new ModelAndView();
            //封装对象，放在模型和视图类的对象中
            mv.addObject("msg","HelloSpringMVC");
            //封装要跳转的视图，放在模型视图类对象中
          mv.setViewName("hello");//WEB-INF/jsp/hello.jsp
            return mv;
      }
    }
    ```
    
    写一个响应的jsp页面
    
    ```jsp
    <%@ page contentType="text/html;charset=UTF-8" language="java" %>
    <html>
    <head>
        <title>Title</title>
    </head>
    <body>
    
        ${msg}
    
    </body>
    </html>
    ```

* SpringMVC运行的原理分析

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190805214843612.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzMwNjQwMw==,size_16,color_FFFFFF,t_70)

图为SpringMVC的一个较完整的流程图，实线表示SpringMVC框架提供的技术，不需要开发者实现，虚线表示需要开发者实现。

1. DispatcherServlet表示前置控制器，是整个SpringMVC的控制中心。用户发出请求，DispatcherServlet接收请求并拦截请求。

   我们假设请求的url为: `http://localhost:8080/SpringMVC/hello`

   如上url拆分成三部分：`http://localhost:8080服务器域名`

   SpringMVC部署在服务器上的web站点

   hello表示控制器

   通过分析，如上url表示为：请求位于服务器localhost:8080上的SpringMVC站 点的hello控制器。

2. HandlerMapping为处理器映射。DispatcherServlet调用HandlerMapping,HandlerMapping根据请求url查找Handler。

3. HandlerExecution表示具体的Handler,其主要作用是根据url查找控制器，如上url被查找控制器为：hello。

4. HandlerExecution将解析后的信息传递给DispatcherServlet,如解析控制器映射等。

5. HandlerAdapter表示处理器适配器，其按照特定的规则去执行Handler。

6. Handler让具体的Controller执行。

7. Controller将具体的执行信息返回给HandlerAdapter,如ModelAndView。

8. HandlerAdapter将视图逻辑名或模型传递给DispatcherServlet。

9. DispatcherServlet调用视图解析器(ViewResolver)来解析HandlerAdapter传递的逻辑视图名。

10. 视图解析器将解析的逻辑视图名传给DispatcherServlet。

11. DispatcherServlet根据视图解析器解析的视图结果，调用具体的视图。

12. 最终视图呈现给用户。

### 3.SpringMVC的注解开发

实际开发中，我们不会像上面那样操作，那样还是很麻烦的，上面的部分是用于理解SpringMVC的原理的，实际过程中我们用的注解多。

步骤：

* 给创建好的Maven项目添加web支持，以及对应的jar依赖

* 在web.xml中进行配置

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
           version="4.0">
  
  
  
      <!--固定写法，不需要再改了-->
      <servlet>
          <servlet-name>springmvc</servlet-name>
          <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
          <init-param>
              <param-name>contextConfigLocation</param-name>
              <param-value>classpath:springmvc.xml</param-value>
          </init-param>
      </servlet>
      <servlet-mapping>
          <servlet-name>springmvc</servlet-name>
          <url-pattern>/</url-pattern>
      </servlet-mapping>
  </web-app>
  ```

  绑定的spring配置文件

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:context="http://www.springframework.org/schema/context"
         xmlns:mvc="http://www.springframework.org/schema/mvc"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
          https://www.springframework.org/schema/beans/spring-beans.xsd
          http://www.springframework.org/schema/context
          https://www.springframework.org/schema/context/spring-context.xsd
          http://www.springframework.org/schema/mvc
          https://www.springframework.org/schema/mvc/spring-mvc.xsd">
  
      <!--自动扫描包，让指定包下的注解生效，由IOC容器统一管理-->
      <context:component-scan base-package="com.qin.controller"/>
      <!--让SpringMVC不处理静态资源,即.css,.js,.html等等资源-->
      <mvc:default-servlet-handler/>
      <!--
      支持mvc注解驱动
          在spring中一般采用@RequestMapping注解来完成映射关系
          要是@RequestMapping注解生效，必须像上下文中注册DefoultAnnotationHandlerMapping和一个AnnotationMethodHandlerAdapter实例
          这两个实例分别在类级别和方法级别处理
          而annotation-driven配置帮助我们自动完成上面两个实例的注入
      -->
      <mvc:annotation-driven/>
      <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver" id="internalResourceViewResolver">
          <property name="prefix" value="/WEB-INF/jsp/"/>
          <property name="suffix" value=".jsp"/>
      </bean>
  
  </beans>
  ```

  controller类

  ```java
  import org.springframework.stereotype.Controller;
  import org.springframework.ui.Model;
  import org.springframework.web.bind.annotation.RequestMapping;
  
  @Controller//自动装配，不再需要再实现接口
  //@RequestMapping("/hello")//这个注解可以在类上实现，相当于下面的所有的@RequestMapping所带的的会先经过这里的，最后拼接出来的是/localhost:8080/hello/hello
  public class controller {
      @RequestMapping("/hello")//这个注解是为了映射请求路径
      public String hello(Model model){//model参数是为了把Action中的数据携带到视图中
  
          //还得封装数据
          model.addAttribute("msg","Hello mvc");
          return "hello"; //会被视图解析器处理，返回的是视图的名称，被配置文件拼接后形成一个完整的路径
      }
  
  }
  
  ```

  响应的界面

  ```jsp
  <%@ page contentType="text/html;charset=UTF-8" language="java" %>
  <html>
  <head>
      <title>Title</title>
  </head>
  <body>
  ${msg}
  </body>
  </html>
  
  ```

* SpringMVC数据处理

  处理提交上来的数据

  * 提交的域名称和处理方法的参数名一致

    ```
    //比如请求一个：http://localhost:8080/hello?name=qin
    //就这样处理
    @RequestMapping("/hello")
    public String hello(String name){
    	System.out.prinltn(name);
    	return "hello";
    }
    ```

    

  * 提交的域名称和处理方法的参数名不一致

    ```java
    //比如请求一个：http://localhost:8080/hello?username=qin
    //就这样处理
    //在上面代码的头上添加一个@RequestParams("提交的域名称")，然后在处理方法的参数名前也加上这个注解
    ```

  * 提交的是一个对象

    ```java
    //要求提交的表单域和对象的属性名一致，参数使用对象即可
    //这有一个实体类：
    @Data
    @AllArgsConstructor
    @NoAllArgsConstructor
    public class User{
        private int id;
        private String name;
        private int age;
    }
    //请求的url：http://localhost:8080/hello?id=1&name=qin&age=1
    //处理
    @GetMapping("/hello")
    public String test2(User user){
        //可以通过User对象对具体数据进行操作
        return "test";
    }
    //当传递的参数是对象的话，前端传递参数名和对象名要一致，不然获取的就是null
    ```

  数据显示到前端

  * 通过ModelAndView

    ```java
    //就是要return 一个ModelAndView对象的那个方法
    ```

  * 通过ModelMap

    ```java
    //就是通过在方法参数里加一个ModelMap对象，然后通过这个对象的addAttribute方法来回显数据，不过这个是比Model功能更多的
    ```

  * 通过Model

    ```java
    //就是通过在方法参数里加一个Model对象，然后通过这个对象的addAttribute方法来回显数据
    ```

    

* SpringMVC结果跳转方式

  * 重定向和转发

    ModelAndView对象可以根据view的名称和视图解析器跳到指定的位置((视图解析器前缀)view名字(视图解析器后缀))

    * 我们可以通过设置ServletAPI，就可以不需要设置视图解析器

      * 通过HttpServletResponse进行输出
      * 通过HttpServletResponse实现重定向
      * 通过HttpServletResponse实现转发
      * 不过不推荐使用这种方式，这样就会变成像Servlet开发那这样了

    * 通过SpringMVC实现转发和重定向

      * 不用视图解析器的方法：

        ```java
        @Controller//自动装配，不再需要再实现接口
        public class controller {  
            @RequestMapping("/hello")
            public String test1(){
                //转发
                return "/WEB-INF/index.jsp";//没有视图解析器我们得写上全路径
            }
            @RequestMapping("/hello")
            public String test2(){
                //转发
                return "forward:/WEB-INF/index.jsp";
            }
            @RequestMapping("/hello")
            public String test3(){
                //重定向
                return "redirect:/index.do";//index.do为另一个请求
            }
        
        
        }
        ```

      * 有视图解析器的方法：

        ```java
        @Controller//自动装配，不再需要再实现接口
        public class controller {  
            @RequestMapping("/hello")
            public String test1(){
                //转发
                return "/index.jsp";//有视图解析器我们就不用写上全路径
            }
            @RequestMapping("/hello")
            public String test2(){
                //转发
                return "forward:/index.jsp";
            }
            @RequestMapping("/hello")
            public String test3(){
                //重定向
                //return "redirect:/index.do";//index.do为另一个请求
            	return "redirect:index.jsp"
            }
        
        
        }
        ```

        

* SpringMVC的Controller和RestFul风格

  * Controller控制器负责提供访问应用程序的行为，通常通过接口定义或注解定义，这两个方式上面都有实现

  * 控制器负责解析用户的请求并将其转换为一个模型

  * 在SpirngMVC中一个控制器类可以包含很多个方法

  * 配置Controller的方式有很多种

  * @RequestMapping注解用于映射url到控制器类或一个特定的处理程序方法，可用于类或方法上，用于类上的时候表示类中所有响应请求的方法都是以该地址作为父路径，常用在有多个方法返回的是同名页面的情况下

  * RestFul风格：

    这个是一个资源定位与资源操作的风格，不是标准也不是协议，只是一种风格，基于这个风格上设计的软件可以更简洁，更有层次，保密性更加好，更易于实现缓存等机制

    功能：

    * 资源：互联网所有的事物都可以抽象为资源
    * 资源操作：使用POST,GET,DELETE,PUT(增删改查)等方法对资源进行操作

    * 我们可以用@PathVariable注解，写在方法参数前，让方法参数的值对应绑定到一个URL模板变量上 ，然后再在映射的url上加上/{变量名}就可以使用/变量值直接进行请求
    * 对于方法上的@RequestMapping注解，使用这种风格的时候，可以变成@对应的方法Mapping{请求名/变量名/..}这样的样子

* 乱码问题

  有时候提交表单会出现乱码的情况，比如提交中文的时候，这种时候我们一般使用过滤器来解决

  ```java
  //实现servlet*下的Filter接口，重写其中的方法
  import javax.servlet.*;
  import java.io.IOException;
  
  public class encodingFilter implements Filter {
  
  
      @Override
      public void init(FilterConfig filterConfig) throws ServletException {
  
      }
  
      @Override
      public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
          request.setCharacterEncoding("utf-8");
          response.setCharacterEncoding("utf-8");
          chain.doFilter(request,response);
      }
  
      @Override
      public void destroy() {
  
      }
  }
  //记得去web.xml中配置
  ```

  有可能不同的请求方式也会有影响，我们就可以直接用SpringMVC给我们提供的过滤器，直接在web.xml中配置就行，但是这种方法在极端情况下对get请求的支持又不友好，就只能去服务器端设置编码了

  ```xml
  <!--SpringMVC自带的过滤器-->
      <filter>
          <filter-name>encoding</filter-name>
          <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
          <init-param>
              <param-name>encoding</param-name>
              <param-value>utf-8</param-value>
          </init-param>
      </filter>
      <filter-mapping>
          <filter-name>encoding</filter-name>
          <url-pattern>/</url-pattern>
      </filter-mapping>
  ```

### 4.JSON

JSON(JavaScript Object Notation,JS对象标记)是一种轻量级的数据交换格式，目前使用十分广泛

JSON采用完全独立于编程语言的文本格式来存储和表示数据

简洁和清晰的层次结构使得JSON成为理想的数据交换语言

JSON易于人阅读和编写，也易于机器解析和生成，并有效提升网络传输效率

前后端分离：后端部署后端，并提供接口与数据，前端独立部署，负责渲染后端的数据，在他们两个之间，需要有一个传输数据的媒介，这个媒介需要前后端的人员都能看的懂，这就是JSON

在js中，一切都是对象，任意js支持的类型都可以通过JSON来表示，如字符串，数字，对象，数组等：

对象表示为键值对，大括号保存对象，方括号保存数组

JSON是JS对象的字符串表示法，它用文本表示一个JS对象的信息，本质是一个字符串

JSON字符串和JS对象是可以互相转换的，

​	使用JSON.parse()方法可以将JSON对象转换为JS对象

```js
var obj = JSON.parse('("a":"hello","b":"world")');
//可以得到{a:"hello",b:"world"}
```

​	使用JSON.stringify()方法可以将JS对象转换为JOSN字符串

```js
var obj = JSON.parse('("a":"hello","b":"world")');
var json = JSON.stringify(obj);
//json就是一个字符串'{"a":"hello","b":"world"}'
```

#### Controller返回JSON数据

我们后台的数据回传给前端时很多时候都要返回字符串数据，有很多第三方的包支持这个功能

* jackson，很好用的一个JSON解析工具，我们就用这个就OK了，从maven导入支持包：

  ```xml
  <!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-databind -->
  <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-databind</artifactId>
      <version>2.12.0-rc1</version>
  </dependency>
  
  ```

* 使用方法：

  * 先导入上面的包
  * 配置web.xml
  * 添加web.xml中配置的处理器对应的spring配置文件(配置视图解析器)
  * 然后就可以写controller里的东西了
  * 有时候会有乱码，我们可以在绑定的spring配置文件里添加以下的乱码统一解决
  
* Fastjson，阿里开发的一个JSON解析工具，也需要导入包

  ```
   <!-- https://mvnrepository.com/artifact/com.alibaba/fastjson -->
          <dependency>
              <groupId>com.alibaba</groupId>
              <artifactId>fastjson</artifactId>
              <version>1.2.74</version>
          </dependency>
  ```

  * fastjson有三个主要的类
    * JSONObject代表json对象，实现Map接口，对应json对象，通过各种形式的get()方法可以和获取json对象中的数据
    * JSONArray代表json对象数组
    * JSON代表JSONObject与JSONArray的转换

* ```java
  import com.alibaba.fastjson.JSON;
  import com.fasterxml.jackson.core.JsonProcessingException;
  import com.fasterxml.jackson.databind.ObjectMapper;
  import com.qin.User.User;
  import org.springframework.stereotype.Controller;
  import org.springframework.web.bind.annotation.RequestMapping;
  import org.springframework.web.bind.annotation.ResponseBody;
  
  import javax.xml.crypto.Data;
  import java.text.SimpleDateFormat;
  import java.util.ArrayList;
  import java.util.Date;
  import java.util.List;
  
  @Controller
  public class Controller1 {
  
      @RequestMapping("/qingqiu1")
      @ResponseBody
      public String test() throws JsonProcessingException {
          ObjectMapper objectMapper = new ObjectMapper();
          User user = new User("qin",18,"nan");
          String string = objectMapper.writeValueAsString(user);
          return string;
      }
      @RequestMapping("/qingqiu2")
      @ResponseBody
      public String josn3() throws JsonProcessingException {
          ObjectMapper mapper = new ObjectMapper();
          Date date = new Date();
          SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd:mm:ss");
          return mapper.writeValueAsString(simpleDateFormat.format(date));
  
      }
      @RequestMapping("qingqiu3")
      @ResponseBody
      public String josn4(){
          List<User> userList = new ArrayList<User>();
          User user1 = new User("a",18,"a");
          User user2 = new User("b",18,"b");
          User user3 = new User("c",18,"c");
          User user4 = new User("d",18,"d");
          User user5 = new User("e",18,"e");
          userList.add(user1);
          userList.add(user2);
          userList.add(user3);
          userList.add(user4);
          userList.add(user5);
          String string = JSON.toJSONString(userList);
          return string;
      }
  }
  ```

### 5.SSM框架整合

我们来进行一个SSM框架的整合项目，首先新建一个Maven项目，然后将以下包以及静态资源导出问题解决

```xml
<!--在pom.xml中添加的内容-->
<!--junit,数据库驱动，连接池，servlet,jsp,mybatis,mybatis-spring,spring,spring-mvc-->
<dependencies>
<!--junit-->
<!-- https://mvnrepository.com/artifact/junit/junit -->
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.13.1</version>
    <scope>test</scope>
</dependency>

    
    <!-- spring -->
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.2.9.RELEASE</version>
</dependency>
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>5.2.9.RELEASE</version>
</dependency>


<!--数据库驱动-->
<!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.22</version>
</dependency>
    
    
<!--servlet-JSP-->
<!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api -->
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>3.1.0</version>
    <scope>provided</scope>
</dependency>
<!-- https://mvnrepository.com/artifact/javax.servlet.jsp/jsp-api -->
<dependency>
    <groupId>javax.servlet.jsp</groupId>
    <artifactId>jsp-api</artifactId>
    <version>2.2</version>
    <scope>provided</scope>
</dependency>

<!-- https://mvnrepository.com/artifact/javax.servlet/jstl -->
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>jstl</artifactId>
    <version>1.2</version>
</dependency>
<!--mybatis-->
   <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.3</version>
</dependency>
<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis-spring</artifactId>
    <version>2.0.5</version>
</dependency>
<!--连接池-->
    <!-- https://mvnrepository.com/artifact/com.mchange/c3p0 -->
<dependency>
    <groupId>com.mchange</groupId>
    <artifactId>c3p0</artifactId>
    <version>0.9.5.2</version>
</dependency>

<!--静态资源导出问题-->
<build>
    <resources>
    	<resoure>
        	<directory>src/main/java</directory>
            <includes>
            	<include>**/*.properties</include>
                <include>**/*.xml</include>
            </includes>
            <filtering>false</filtering>
        </resoure>
        <resoure>
        	<directory>src/main/resources</directory>
            <includes>
            	<include>**/*.properties</include>
                <include>**/*.xml</include>                
            </includes>
            <filtering>false</filtering>
        </resoure>
    </resources>
</build>

  </dependencies>
```

导入jar包后进行数据库的连接，完成数据库连接后，建立项目结构文件包：在java代码文件夹下创建自己的com包，在里面建立Dao(持久层代码包)，Service(业务层代码包)，Controller(视图控制层代码包)，还有个用户代码包，然后在资源文件夹下建立spring和mybatis的配置文件以及数据库的配置文件database.properties,如果MySQL版本是8.0以上的话注意配置

用户代码包相当于是跟数据库的连接层，Dao与Service相当于MVC的Model

我们先进行Mybatis层的操作：

```
<!--spring-mybatis配置文件(mybatis-config.xml)-->
<!--mybatis-fonfig.xml-->
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>

   <!--配置数据源，交给Spring完成-->
   <!--别名-->
   <typeAliases>
   		<package name="用户代码包的路径"/>
   </typeAliases>
	
	 <mappers>
   	<mapper class="实现接口的配置文件的路径">
   </mappers>
</configuration>
<!--有时候xml文件会加载不出来，一般是maven的静态资源加载问题，要在pom配置文件里加上<bulid>来解决-->
```

```
<!--spring配置文件(applicationContext.xml)-->
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

  

</beans>
```

```properties
<!--数据库配置文件(database.properties)-->
jdbc.driver=com.mysql.cj.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3307/ssmbuild?userSSL=true&useUnicode=true&characterEncoding=utf8
jdbc.username=数据库用户名
jdbc.password=数据库密码
在MySQL版本为8.0以上的时候，要在url上加上这一句：&serverTimezone=Asia/某个地方
```

在用户代码包下建立一个实体类，类名跟数据库的表名跟数据库一样

```
/*比如在数据库中有一个books的表，里面有bookID,bookName,bookCounts,detail四个表单项，我们就要建立以下这个实体类*/
public calss Books{
	private int bookID;
	private String bookName;
	private int bokkCounts;
	private String detail;
	//然后写构造方法(使用lombok的@Data,@All构造，@No构造来实现)
}
```

有了用户实体类，我们就需要在Dao包下建立一个接口来实现对用户实体类数据的操作

```
public interface BookMapper{
	//增删改查操作
	int addBook(Books books);
	int deleteBookById(int id);
	int updateBook(Books books);
	Books queryBookById(int id);
}
```

有了这个接口，我们就可以在接口下通过配置文件来实现接口(这是Mybatis中的东东)

```
<!--BookMapper.xml(Mybatis映射文件，最好与接口同名)-->
<!--这个文件是要在Mybatis的配置文件中spring-mybatis配置文件(mybatis-config.xml)去注册的-->
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper
	PUBLIC "-//mybatis.org//DTD Config 3.0//EN" 
	"http://mybatis.org/dtd/mybatis-3-config.dtd">
	<!--一个mapper标签对应一个接口,其中的各种标签对应接口的方法-->
<mapper namespace="上面接口的路径">
	<insert id="addBook" parameter="Books">
		insert into ssmbuild.books(bookNmae,bookCounts,detail)
		values(#{bookName},#{bookCounts},#{detail})
	</insert>
	<delete id="deleteBookById" parameterType="int">
		delete form ssmbuild.books where bookID=#{bookId}<!--这里可以在上面的接口的参数处加一个@Param("bookId")-->
	</delete>
	<update id="updateBook" parameterType="Books">
		update ssmbuild.books set bookName=#{bookName},
		bookCounts=#{bookCounts},detail=#{detail} where bookID=#{bookID};
	</update>
	<select id="queryBookById" resultType="Books">
		select * from ssmbuild.books where bookID = #{bookId};
	</select>
</mapper>
```

完成了对数据的操作的Dao层后，就可以写业务层了

在Service包下也建立一个实现业务(此处业务与数据操作意义，都是增删改查)的接口

```
//BookService接口
public interface BookService{
	//增删改查操作
	int addBook(Books books);
	int deleteBookById(int id);
	int updateBook(Books books);
	Books queryBookById(int id);
}
```

然后要有实现这个业务的实现类(业务层调持久层)

```
public calss BookServiceImpl implements BookService{
	//组合Dao层
	private BookMapper bookeMapper;
	public void serBookMapper(BookMapper bookMapper){
		this bookMapper = bookMapper;
	}
	//重写方法
	public int addBook(Books books){
		//可以在调用Dao的上下实现其它的事务，不过用Spring的AOP实现更加方便
		return bookMpper.addBook(books);//调用Dao
	}
	...
	
}
```

以上Mybatis层就整合完了，然后整合Spring层：

首先进行Dao的Spring配置：

Spring整合Dao：

在资源文件夹下建立一个spring-dao.xml

```
<!--spring-dao.xml-->
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

   <!--1.关联数据库配置文件-->
   <context:propery-placeholder location="数据库配置文件的路径">
   <!--2.连接池,连接池有好多，这里列举一些
   dbcp:这个是半自动化操作，不能自动连接，得手动配置
   c3p0:自动化操作，可以自动加载配置文件，并且可以自动设置到对象中
   druid:SpringBoot里用的
   hikari:
   -->
   <!--固定写法-->
   <bean id="dataSourse" class="c3p0下的ComboPooledDataSourse">
   		<propery name="driverClass" value="$(jdbc.driver)"/>
   		<propery name="jdbcUrl" value="$(jdbc.url)"/>
   		<propery name="user" value="$(jdbc.username)"/>
   		<propery name="password" value=$(jdbc.password)/>
   		<!--还可以有很多数据源的配置，比如超时配置，最大连接数等-->
   </bean>
   <!--3.sqlSessionFactory-->
   <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
   		<propery name="dataSource" ref="dataSoure"/>
   		<!--绑定mybatis的配置文件-->
   		<propery name="configlocation" value="classpath:mybatis-config.xml"/>
   <bean/>
   
   <!--可以在这里配置Dao接口扫描包，动态实现Dao接口注入Spring容器-->
	<bean class="org.mybatis.spring.MapperScannerConfigurer">
		<!--注入sqlSessionFactory-->
		<propery name="sqlSessionFactoryBeanName" value="sqlSessionFactory"/>
		<!--扫描的Dao包-->
		<propery name="basePackage" value="Dao包的路径"/>
	<bean/>
</beans>
```

Spring还要整合Service层(事务)：

还要在资源文件夹下新建一个spring-service.xml

```
<!--spring-service.xml-->
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

   <!--1.扫描Service下的包下的注解-->
   <context:component-scan base-package="service层的包路径"/>
   <!--2.将所有的业务类注入到Spring中，通过bean配置或注解
   bean的id尽量与类名一致
   -->
   <bean id="BookServiceImpl" class="BookServiceImpl所在的路径">
   		<propery name="bookMapper" ref="bookMapper"/>
   <bean/>
   <!--写完上面那些可以在applicationContext.xml中用<import>整合起来-->
   <!--3.声明式事务，如果需要AOP横切织入的话，记得加jar包-->
   <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
   		<!--注入数据源-->
   		<propery name="dataSource" ref="dataSource"/>
   	</bean>
   	<!--4.AOP事务支持-->
</beans>
```

上面我们就把Spring也整合了，接下来整合SpringMVC，在上面的配置基础上，我们引入web支持，将这个项目变成一个web项目，然后在web.xml中进行配置

```
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee 			 http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">



    <!--1.配置DispatchServlet-->
    <servlet>
        <servlet-name>springmvc</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <!--绑定springmvc.xml-->
            <param-value>classpath:springmvc.xml</param-value>
        </init-param>
        <load-on-startup>1<load-on-startup/>
    </servlet>
    <servlet-mapping>
        <servlet-name>springmvc</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
    
    <!--乱码过滤-->
    <filter>
        <filter-name>encodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>utf-8</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>encodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
    <!--配置Session-->
    <session-config>
    	<session-timeout>1<session-timeout/>
    <session-config/>
</web-app>
```

绑定的spring-mvc.xml文件

```
<!--spring-mvc.xml-->
<!--spring-dao.xml-->
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/mvc
        https://www.springframework.org/schema/mvc/spring-mvc.xsd">
	
	<!--1注解驱动-->
	<mvc:annotation-driven/>
	<!--2静态资源过滤-->
	<mvc:default-servlet-handler/>
	<!--3扫描包-->
	<context:component-scan base-package="controller包所在的路径"
	<!--4视图解析器-->
  	<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver" id="internalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/jsp/"/>
        <property name="suffix" value=".jsp"/>
    </bean>
</beans>
```

这样就把三个框架整合完了

整合mybatis后的情况：

![mybatiszhenghe](C:\Users\CHIYODAMOMO\Pictures\Saved Pictures\mybatiszhenghe.PNG)

整合spring后的情况：

![spring](C:\Users\CHIYODAMOMO\Pictures\Saved Pictures\spring.PNG)

整合springMVC后的情况：

![springmvc](C:\Users\CHIYODAMOMO\Pictures\Saved Pictures\springmvc.PNG)

### 6.SpringSMV AJAX

AJAX(Asynchronous JavaScript and XML)，即异步JavaScript和XML，这个东东是一种无序重新加载整个网页的情况下，更新部分网页的技术，它不是一种新的编程语言，只是用于创建更好更快以及交互性更强的Web应用程序的技术，纯JS原生实现AJAX很少用，JQuery提供的更加容易学习和使用，还能避免重复造轮子

AJAX的核心是XMLHttpRequest对象(XHR),XHR为向服务器发送请求和解析服务器响应提供了接口，能够以异步的方式从服务器获取新数据

* JQuery提供了多个与AJAX有关的方法
* 通过JQuery的AJAX方法，我们可以使用Http Get和Post从服务器上请求文本，html，Jsp，Json，XML等，同时可以把这些外部数据直接载入网页的被选元素中
* JQuery的本质还是XMLHttpRequest，只是对它进行了封装，更方便调用





#### 实战小项目

需求：基于SSM框架，写一个网站，管理宿舍信息的

网站要求：1.有登录退出功能

​					2.区分管理员权限与普通权限

​					3.管理员权限登录后可以实现普通人员信息的增删改查

​						普通权限登录后只能查看信息

完成以上三条即可





## MybatisPlus









## SpringSecurity

SpringSecurity是一个用于Web安全(身份认证和权限控制以及访问控制)的框架.

安全性对于我们的Web项目来说,是应该在设计之初就要考虑到的,它虽然不是功能性模块,但是它非常重要,低安全性的网站会导致大量漏洞的出现,进而导致用户信息或网站信息泄漏而且容易受到攻击.

对于权限来说,一般有这些:

* 功能权限
* 访问权限
* 菜单权限
* 等等

对于权限控制来说,我们可以使用原生代码,也就是做拦截器,过滤器来完成,但是这样做会产生大量原生代码,导致我们的项目比较复杂.

SpringSecurity是针对Spring项目的安全框架,它是SpringBoot底层安全模块默认的选择.它可以实现强大的Web安全控制,对于这个模块,我们只需要引入spring-boot-starter-security模块进行一些配置就可以实现强大的安全管理.

常用的一些类:

* WebSecurityConfigurerAdapter: 自定义安全策略(这个类使用了适配器模式)
* AuthenticationManagerBuilder: 自定义认证策略(这个类使用了建造者模式)
* @EnableWebSecurity: 开启WebSecurity模式(在Spring中很多开启功能都是这个格式,@Enable啥啥)

SpringSecurity的两个目标是"认证(Authentication)"和"授权(Authorization)"(访问控制),认证与授权这两个概念是通用的,并不只在SpringSecurity中存在.

SpringSecurity包导入后,我们会发现它包含了SpringAOP和SpringWeb包.说明它是通过横切的方式进行安全校验的.

### SpringSecurity的使用

我们可以通过Java配置类来进行SpringSecurity的配置,首先引入上述的包后,我们可以新建一个config包,在里面新建一个SecurityConfig类:

```Java
//对于这个配置类,它需要继承WebSecurityConfigurerAdapter类,并要在头上添加@EnableWebSecurity注解,表示开启web安全模式.
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter{
	
    //重写configure(HttpSecurity http)方法
    //授权
    @Override
    protected void configure(HttpSecurity http) throws Exception{
        //对于这个http参数,它是通过链式编程的形式来进行各种权限的直接配置.
        http.authorizeRequests().antMatchers("/").permitAll()
            .antMatchers("/level1").hasRole("vip1")
            .antMatchers("/level2").hasRole("vip2")
            .antMatchers("/level3").hasRole("vip3");
        //这样我们就简单配置好了一个能够拦截路径为/,路径为level1/2/3的请求,并且路径为/的任何人都可以访问,路径为level1的只能由用户vip1访问这样的权限控制器.
        //我们还可以通过它设置无权限时自动跳到的页面
        http.formLogin();//表示没有权限就去登录页面,也可以在上面的hasRole后加上.and().formLogin(),继续加上.loginPage("路径")就可以指定登录页面了,最好还要加上usernameParameter("提交的input的name属性值")和passwordParameter(),以及loginProcessingUrl("要授权的页面").
        
        http.csrf().disable();
        http.logout();//表示开启注销功能.相当于我们在前端有个注销按钮,点那个就应该走这个功能.它默认的话会有一个页面,并且注销后它默认跳到登录界面.我们还可以通过注销来清空Cookie,使用.deleteCookies("cookie")就行了,还可以用.logoutUrl("路径")来指定注销后跳的页面.
        //对于这个注销有一个问题,它默认启动了一个跨域请求攻击防止机制,这个机制会导致我们通过get请求进行的注销操作报404
        
        http.rememberMe();//开启记住我功能,也就是个Cookie功能.它默认能保存两周.加上.rememberMeParameter("前端的那个复选框的name值")来设置自定义的记住我按钮.
    }
    
    //重写参数为AuthenticationManagerBuilder类型的configure方法
    //认证
    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception{
        //认证用户,inMemoryAuthentication表示从内存中获取
        auth.inMemoryAuthentication().passwordEncoder(new BCryptPasswordEncodEncoder())
            .withUser("用户名").password("密码").roles("用户权限");//可以通过.and()继续添加用户权限
        //正常来讲,用户名和密码这些应该是从数据库里去读的.并且密码是需要被加密的.
        //建inMemoryAuthentication改成jdbAuthentication().dataSource(数据源).withDefaultSchema()就可以切换成从数据库中查找了.
        //在SpringSecutiry5.0+以上的版本中新增了很多加密方式,在获取后加上.passwordEncoder(new BCryptPasswordEncodEncoder())就是一种它自带的加密方式.其实我们也可也用JDK中提供的MD5加密方式.
        
    }
}
```

Thymeleaf模板引擎是可以跟SpringSecurity进行整合的,整合后,在Thymeleaf中就可以进行一些SpringSecurity的操作了,我们只需要引入thymeleaf-extras-springsecurity依赖就可以集成他俩了.

```HTML
<!--比如这样,我们在前端验证是否登录,如果登录了就显示注销,没登陆就显示登录-->
<div>
    <div sec:authorize="isAuthenticated()"><!--这调用了一个是否认证的方法,这个sec的命令需要导入它相关的命名空间.-->
        <a class="item" th:href="@{/toLogout}">
    	<i class="address card icon"></i>注销
    </a>
    </div>
    <div sec:authorize="!isAuthenticated()">.
    <a class="item" th:href="@{/toLogin}"> 
    	<i class="sign-out icon"></i>登录
    </a>
    </div>  
    
</div>
```



## Vue

Vue是一套用于构建用户界面的渐进式JS框架,它核心库只关心视图层,它的核心思想是Soc(关注点分离原则).对于我们的网络应用,不是只有视图层的,还有网络通信,数据处理等东西.

#### LESS

这个玩意是一门CSS预处理语言,它扩展了CSS,增加了变量,Mixin,函数等特性,使得CSS更容易维护与扩展,它基于Node.js,可以运行在浏览器或者Node上.

#### 常见的JS框架

* JQuery : 最常见的了
* Angular : Google收购的JS框架,由Java程序员开发,在前端引入了MVC模块化开发理念,由TypeScript语言开发.
* React : Facebook的一个前端框架,它提出了一个虚拟DOM的概念,能够减少真实DOM操作,提高性能,它基于JSX语言开发.
* Vue :  渐进式JS框架,就算逐步实现新特性,如模块化,路由,状态管理等新特性,它综合了模块化开发与虚拟DOM的优点.
* Axios : 前端通信框架,Vue是为了处理DOM的,它并不具备通信能力,除了AJAX通信外,这个框架也可以与服务器进行交互.

#### 常见的UI框架

* Ant-Design : 阿里的一个基于React的UI框架
* ElementUI,iview,ice : 饿了么的一个基于Vue的框架
* Bootstrap : 
* AmazeUI :



#### MVVM: 前后端数据双向绑定

* model : 表示模型层,这里表示js对象
* view : 视图层,这里表示DOM
* viewmodel : 连接视图与数据的中间件,Vue就算MVVM中的VM层实现者,在MVVM框架中是不允许数据与视图的直接通信的,只能通过VM层来进行通信,而VM就是定义了一个Observer观察者,
* VM能够观察数据变化,并对视图对于的内容进行更新
* VM能够监听视图变化,并能够通知数据改变

Vue其实就是MVVM框架的一个实现者,核心是实现了DOM的监听与数据绑定

MVVM的好处

* 低耦合 : 视图可以独立于模型层变化和修改,一个VM可以绑定到不同的视图上,当视图变化的时候,模型可以不变,当模型变化的时候,视图也可以不变
* 可复用 : 可以把视图逻辑放在VM中,让VM绑定的视图都可以复用这个逻辑
* 独立开发 : 开发人员可以专注于业务逻辑和数据的开发(在VM中进行),设计人员可以专注于页面设计
* 可测试 : 界面来说都是比较难测试的,因为需要数据和视图的交互,而现在测试可以针对VM来进行.



#### 第一个Vue程序

IDEA可以下载VUE插件

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.21/dist/vue.js"></script>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <div id="app">
        {{message}}
    </div>
</body>
<script>
    var vm = new Vue({
        el: "#app",
        data: {
            message: "hello vue"
        }
    });
</script>
</html>
```



#### Vue语法

在Vue中,所有以v-为前缀的东西都是Vue指令,表示它们是Vue提供的特殊属性,它们能够渲染DOM的一些行为.

##### 判断-循环

v-if 与 v-else : Vue提供的判断指令

v-for : Vue提供的循环指令

```html
<div id="app3">
        <span v-if="ok">
            Yes
        </span>
        <span v-else>
            No
        </span>
    </div>
<script>
var vm3 = new Vue(
        {
            el: "#app3",
            data: {
                ok: true
            }
        }
    )
</script>
```





## SpringBoot

Spring是通过一下四个关键策略来简化Java开发的:

* 基于POJO的轻量级和最小侵入性编程
* 通过IOC,依赖注入和面向接口实现轻耦合
* 通过基于切面(AOP)和惯例进行声明式编程
* 通过切面和模板减少样式代码

而SpringBoot是一个JavaWeb的开发框架,类似于SpringMVC,对比于其他的Web框架,它可以迅速的开发Web应用,几行代码就可以开发一个http接口.而所有的计数框架发展都遵循这样的规律:从一个复杂的应用场景,衍生出一种规范框架,人们只需要对它进行各种配置而不需要自己来实现,这时强大的配置成为了优势;发展到一定程度后,人们根据实际需求,选取框架中的实用功能和设计精华,重构出一个轻量级框架;再然后为了提高开发效率,原来的复杂配置会成为麻烦,于是提倡"约定大于配置"的思想,进而衍生出一些一站式解决方案.这也就是Java的大型应用->J2EE->Spring->SpringBoot的发展过程.

SpringBoot是不提供Spring的核心特性和扩展功能的,它是用来和Spring一起,快速的开发新一代基于Spring框架的应用程序,它并不是用来代替Spring的.它同Spring一样,"约定大于配置"的思想贯彻始终,它会帮我们配置很多的东西,多数SpringBoot应用只需要很少的Spring配置,而且它还继承了大量常用的第三方库的配置,比如Redis,MongoDB,Jpa等等,这些第三方库几乎可以零配置的开箱即用.它就是很多框架的集合体.

SpringBoot的优点:

* 开箱即用,提供各种默认配置简化项目设置
* 内嵌容器简化Web项目
* 没有冗余代码生成和XML配置的要求



















### 微服务

这是一个架构风格,就像MVC,MVVM架构一样.

微服务就是把原来的业务变成了一个个模块,即把原来的一个应用拆分成一系列小服务的组合,它们通过http的方式进行互通.

* 单体应用架构
  * 一个应用中的所有应用服务都封装在一个应用中,无论什么EPR,CRM或者其他什么系统,都把数据库访问,Web访问等各个功能放到一个war包内,就是单体应用架构
  * 单体应用架构的好处是已于开发和调试,方便部署,而且扩展的时候只需要将war包赋值,放到多个服务器上,做好负载均衡就行
  * 单体应用架构的缺点是修改的时候,需要停掉整个服务,重新打包,重新部署,如果是大型应用的话,这样会导致维护和开发难度上天

* 微服务架构
  * 微服务架构就是把每个功能独立出来,独立出来的功能元素进行动态组合,需要的才被拿来组合,这里就不像单体应用架构那样需要扩展的时候要复制整个应用,而是只复制功能元素.
  * 好处:
    * 节省资源的调用
    * 每个功能元素的服务都是可替换的可独立升级的软件代码
    * 每个服务足够内聚,足够小,代码容易理解,能够聚焦一个指定业务功能或需求
    * 开发简单,开发效率高,一个服务就实现一个功能
    * 开发成本小,只需要一个小团队就可以开发微服务
    * 微服务耦合度小,是有功能意义的服务,无论在开发阶段还是部署阶段都是独立的
    * 微服务可以无视语言限制
    * 容易与第三方集成,微服务有容易且灵活的方式集成自动部署,通过持续集成工具如Jenkins,Hudson,Bamboo等
    * 微服务容易宝贝一个开发者理解,修改和维护.小团队可以更加关注自己的成果而无需通过合作体现价值
    * 微服务允许融合最新技术
    * 微服务只是业务逻辑代码,不会与视图等混合
    * 每个微服务有自己的存储能力,可以有自己的数据库,也可以用统一的数据库
  * 缺点
    * 开发人员要处理分布式系统的复杂问题
    * 多服务运维难度与压力增大
    * 系统部署依赖问题
    * 服务间通信成本问题
    * 数据一致性问题
    * 系统集成测试成本
    * 性能问题

##### 第一个SpringBoot程序

在IDEA中new spring initializr项目(官网直连)项目,选择项目的名字等东西,最后选择boot版本,选择依赖,就可以完成一个springboot项目了

一个springboot项目的项目结构:

![springboot项目结构](C:\Users\qj176\Pictures\springboot项目结构.PNG)

首先这个Springbootstudy01Application是程序的主入口,不能碰也不能改

然后是resources文件中的appilcation.properties文件,这是一个springboot的核心配置文件

还要Springbootstudy01ApplicationTests是单元测试

我们要写自己的代码的时候,就需要在Springbootstudy01Application的同级目录下建立各种包,比如dao那些的

我们现在新建一个controller包,在里面新建一个HelloWorldConteroller类:

![第一个springboot程序](C:\Users\qj176\Pictures\第一个springboot程序.PNG)

然后运行项目,打开浏览器,输入http://localhost:8080/hello,就可以看到hello字符串显示在网页上.

详解:

* 这个主类:Springbootstudy01Application头上的SpringBootApplication注解表明这个类本身就是一个Spring的组件

* SpringBoot项目的pom.xml具体:

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
      
      
      <!--这个parent表示有个父项目,表示继承一个项目-->
      <parent>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter-parent</artifactId>
          <version>2.5.0</version>
          <relativePath/> <!-- lookup parent from repository -->
      </parent>
      
      <groupId>com.qin</groupId>
      <artifactId>springbootstudy01</artifactId>
      <version>0.0.1-SNAPSHOT</version>
      <name>springbootstudy01</name>
      <description>Demo project for Spring Boot</description>
      
      <properties>
          <java.version>1.8</java.version>
      </properties>
      
      <dependencies>
          <!--引入的依赖:Sping Web依赖,帮我们干了tomcat的配置,dispatchservlet.xml
  		实现Http接口(该依赖中包含springmvc),使用tomact作为默认的嵌入式容器
  		-->
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-web</artifactId>
          </dependency>
  		<!--单元测试组件-->
          <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-test</artifactId>
              <scope>test</scope>
          </dependency>
          
          <!--所有的springboot的依赖都用spring-boot-start作为前缀-->
      </dependencies>
  
      <!--打jar包-->
      <build>
          <plugins>
              <plugin>
                  <groupId>org.springframework.boot</groupId>
                  <artifactId>spring-boot-maven-plugin</artifactId>
              </plugin>
          </plugins>
      </build>
  
  </project>
  ```

#### SpringBoot自动装配原理

springboot项目中的pom.xml里:

- spring-boot-dependencies:整个项目的核心依赖在父工程中
- 我们在写或引入springboot的依赖的时候,不需要明确写版本号就是因为父工程中有版本仓库了
- spring-boot-stater前缀的东西都是启动器
  * 它就是springboot的启动场景
  * springboot会将所有的功能场景,都变成启动器
  * 我们要使用什么功能,就找到对应的启动器就行了

主程序:

* @SpringBootApplication:用来配置

  * 标注这个类是一个springboot的应用

  * 进入这个注解,会发现它有这些注解:

    * @SpringBootConfigration
    * @EnableAutoConfigration
    * @ComponentScan
    * @ConfigurationPropertiesScan

  * 两个@C的注解都是用来扫描包的

  * @SpringBootConfigration

    * SpringBoot的配置,点进去我们会看到
    * 里面有@Configration注解,表示是一个spring的配置类
    * @Conponent 表示是一个spring组件

  * @EnableAutoConfigration

    * 自动配置,点进去,出来四个元注解还有@AutoConfigurationPackage

    * @AutoConfigurationPackage表示自动配置包,点进去我们会发现它导入了一个选择器:

      @Import(AutoConfigurationPackages.Registrar.class),用来自动配置包注册

    * 还有一个@Improt(AutoConfigurationImportSelector.class)

  它所有的操作都是为了

  原理图:

  ![springboot自动装配原理](C:\Users\qj176\Pictures\springboot自动装配原理.PNG)

  主要的过程:

  * SpringBoot启动时:从类路径:META-INF/spring.factories获取指定的值
  * 把所有需要导入的组件,以类名返回,这些组件就会被添加到容器中
  * 获取到的自动装配的类导入容器,自动配置生效,帮我们完成配置,即帮我们做了以前那些spring的一堆配置
  * 整合javaEE,解决方案和自动配置的东西都在spring-boot-autoconfigure-版本号.RELEASE.jar这个包下
  * 容器中存在很多以AutoConfiguration结尾的文件,它们都有@Bean的注解,就是这些类给容器中导入了场景需要的所有组件并自动配置,这些也就是我们之前在spring中的java配置形式,
  * 至此我们就不用手写配置文件了

* SpringApplication.run(Springboot01HelloWorldApplication.class,args):用来启动

  启动流程图:

  ![springboot启动流程](C:\Users\qj176\Pictures\springboot启动流程.png)

  * SpringApplication类

    这个类主要做四个事

    * 推断应用的类型是普通的项目还是Web项目
    * 查找并加载所有可以用初始化器,设置到initializers属性中
    * 找出所有的应用程序监听器,设置到listeners属性中
    * 推断并设置mian方法的定义类,找到运行的主类

* 对于SpringBoot的理解

  * 自动装配
  * run()方法



#### SpringBoot配置

对于springboot的配置,它有一个默认的properties文件,里面的配置可以在官方文档查看

但是官方其实不推荐properties文件来配置,最好用yaml文件或者yml来配置,不过配置文件的名字是定死了的,都是application.啥啥啥,yml跟properties文件差不多的.

YAML其实仍是一个标记语言,以前我们用XML文件来配置,我们来看看两个文件的区别:

```yaml
#yaml的:
键: 值
#除了这个它还可以存对象,比如这样
student:
 name: ...
 age: ...
#或者这样
student: {name: ...,age: ...}
#还可以存数组/集合
pets:
 - a
 - b
 - c
#或者
pets: [a,b,c]
```

```xml
<!--xml的-->
<值></值>
```

YAML对空格要求严格.符号后面都要跟一个空格

YAML强大的地方在于它可以注入到我们的配置类中

YAML文件它是可以给我们的实体类赋值的

```java
//在启动类的同级下新建包:pojo
//其中有两个类:
//Dog.class
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

@Component
public class Dog {
    //第一种属性赋值:@Value注解
    @Value("旺财")
    private String name;
    @Value("2")
    private Integer age;

    public Dog() {
    }

    public Dog(String name, Integer age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

}


//application.yaml
#第二种属性赋值方式
#而且yaml里面这些值可以有占位符:Spring的EL表达式 比如↓
cat:
  happy: kuaile 或者写个${ramdon.int}
  name: maomao
  age: 3
  b: false
  map: {K: k,O: o}
  list:
    - code
    - mamda
    - mmd
  dog:
    name: wangcai
    age: 3
//Cat.java
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.stereotype.Component;

import java.util.List;
import java.util.Map;

@Component//注册组件
@ConfigurationProperties(prefix = "cat")//该注解可以绑定yaml文件里面的对象,然后给类属性进行自动装配

public class Cat {
    private String happy;
    private String name;
    private Integer age;
    private Boolean b;
    private Map<String,Object> map;
    private List<String> list;
    private Dog dog;

    @Override
    public String toString() {
        return "Cat{" +
                "happy='" + happy + '\'' +
                ", name='" + name + '\'' +
                ", age=" + age +
                ", b=" + b +
                ", map=" + map +
                ", list=" + list +
                ", dog=" + dog +
                '}';
    }

    public Boolean getB() {
        return b;
    }

    public void setB(Boolean b) {
        this.b = b;
    }

    public Map<String, Object> getMap() {
        return map;
    }

    public void setMap(Map<String, Object> map) {
        this.map = map;
    }

    public List<String> getList() {
        return list;
    }

    public void setList(List<String> list) {
        this.list = list;
    }

    public Dog getDog() {
        return dog;
    }

    public void setDog(Dog dog) {
        this.dog = dog;
    }

    public Cat(String happy, String name, Integer age, Boolean b, Map<String, Object> map, List<String> list, Dog dog) {
        this.happy = happy;
        this.name = name;
        this.age = age;
        this.b = b;
        this.map = map;
        this.list = list;
        this.dog = dog;
    }

    public Cat() {
    }

    public Cat(String happy, String name, Integer age) {
        this.happy = happy;
        this.name = name;
        this.age = age;
    }

    public String getHappy() {
        return happy;
    }

    public void setHappy(String happy) {
        this.happy = happy;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }
}

```

```java
//给个测试:
//Springbootsstudy01ApplictionTests.java

import com.qin.springbootstudy01.pojo.Cat;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
class Springbootstudy01ApplicationTests {

    @Autowired
    Cat cat;
    @Test
    void contextLoads() {
        System.out.println(cat);
    }

}
//启动后就可以看见输出了猫
```

这个@ConfigurationProperties注解如果不配置一下它会报红,但是没啥影响.

使用yaml文件进行数据存储的关键就是这个@ConfigurationProperties注解,它可以将yaml配置文件中的数据映射到组件中对应的位置.只有这个组件是容器中的组件,才可以使用这个注解进行yaml数据配置



对于ymal文件与proprties文件,ymal文件更加的强大.

对于@ConfigurationProperties注解和@Value注解,前者可以批量注入配置文件中的属性,而后者只能一个个指定.前者支持松散语法,后者不支持,前者并不支持SpirngEL,但后者支持,前者支持JSR303数据校验,后者不支持,前者还支持复杂类型封装,而后者不支持.

松散绑定:比如我们在类里面写的属性名是firstName,而配置文件里可以写成first-name,springboot照样可以识别并装配.这就是松散绑定,Value必须就严格对应才行



综上来看.ymal与@ConfigurationProperties注解比原来的sping注入强大的多



#### JSR303校验

给字段增加过滤器验证,保证数据的合法性.

有个注解:@Validated,这个注解就是做数据校验的

JSR303校验是通过很多的注解来实现的.

![JSR303](C:\Users\qj176\Pictures\JSR303.webp)

最常用的是最后那个正则表达式的,因为通过这个就可以验证所有格式的数据了

#### 多环境配置及配置文件的位置

配置文件可以从src文件同级目录下的config文件夹下加载,或者直接在src文件同级目录下直接加载,还可以放在src里面的resources文件夹下,还能放在resources文件夹下的config文件夹下.这些是官方推荐放的位置,不过放哪看自己.

用yaml文件的话,它可以在一个yaml文件里面配很多的环境只需要用---来隔开.比如:

```yaml
server:
	port:8080
spring:
	active:dev#使用dev环境
---
server:
	port:8081
spring:
	profiles:dev #这个是环境的名称
```

#### SpringBoot自动配置原理再理解

大致内容在上面的自动装配里面

* 咱写的配置文件与spring.factories的联系
  * 在spring.factories文件下的那些路径对应的类里面,它们都有一个@Comfiguration注解,表示的是它是一个配置类,还有一个@EnableConfigurationProperties(某个类.class)表示自动配置属性,而自动配置属性就是它括号里面那个类里面的属性.还有@ConditionalOnWebAppliction()等几个注解是Spring的底层注解,它会根据不同的条件来判断当前配置或类是否生效,它括号里面就是条件.最终要的是它们有一个@ConfigurationProperties()注解,而且括号里的东西一般都是spring.啥啥啥,这就是一个前缀,从配置文件里面获取属性的前缀.
  * @Conditional注解它有很多的扩展,它就是进行条件判断的,条件判断成功后才会生效

* 咱的配置文件能写啥

  * 结合上面的联系,那个@ConfigurationProperties注解,如果它的括号里是spring.http,

    那我们在我们的配置文件里面想要给它属性就这样:

    ```yaml
    spring:
    	http:
    		#一堆属性
    ```

  * 在配置文件里面能配置的东西,都存在一个对应的xxxProperties类,而这个类又是给xxxAutoConfiguration类(就是spring.factories里面那一堆路径对应的类)自动装配属性的类,就是xxxAutoConfiguration类是从xxxProperties类中获取默认值的.而xxxProperties类是跟配置文件中的内容相匹配的,我们在配置文件里面写的东西就是在修改xxxProperties类里面的属性值,进而改变整个配置,达到我们想要的效果.

* 综上,自动装配的原理:

  * SpringBoot启动的时候加载大量的xxxAutoConfiguration类
  * xxxAutoConfiguration类会根据一些条件判断是否要进行自动装配,如果条件满足,就进行装配,不满足就不装配;它就是给容器添加组件的类
  * 如果条件满足.进行自动装配的话,就会到xxxProperties类里面去获取配置的信息,xxxProperties类中的配置信息又是从我们的配置文件里面去拿的.

  * 如果我们想知道那些生效了哪些没生效,就可以在配置文件里面给个debug:true.
  * 如果这些类里面没有我们需要的功能,我们就可以自己写对应的类了.

* SpringBoot到底给我们配置了啥,我们能改么,能改啥,能扩展不?

  * 配置了啥:
    * 即xxxxAutoConfiguration类配置的组件
  * 能改么,改啥,能扩展不:
    * xxxxProperties类包含配置的属性,它从我们的配置文件里拿值,我们改的就是这个
    * 当没有相应的功能时,我们就可以通过编写xxxxAutoConfiguration类与xxxxProperties类来进行扩展

#### SpringBoot Web

咱新建一个SpringBoot项目后,发现没有Web-app,那么我们要咋个写Web项目嘞?

回顾:

SpringBoot的使用步骤:

* 1.创建项目,选择模块
* 2.配置文件编写
* 3.业务代码编写

这个阶段要学啥:

* 导入静态资源
* 启动首页
* jsp,模板引擎Thymeleaf
* 装配扩展SpringMVC
* 增删改查咋做
* 拦截器
* 国际化

##### SpingBootWeb-静态资源导入

要导入静态资源,我们就需要知道我们的静态资源应该放在哪才能让springboot读到,我们打开spring.factories,找到WebMvcAutoConfiguration,进入它的源码,我们会在它下面找到一个addResourceHandlers方法,里面的内容有这些:

```java
public void addResourceHandlers(ResourceHandlerRegistry registry) {
    if (!this.resourceProperties.isAddMappings()) {//如果静态资源已经被自定义了,就直接输出日志
       logger.debug("Default resource handling disabled");
     } else {//不然就添加个webjars啥啥啥的,那这个玩意是啥?看下面
        //如果没有自定义,第一种找静态资源的方式就是去那个webjars下面找,比如导入了JQuery,那我们就只需要在浏览器地址栏输入:
        // webjars/jquery/3.4.1/jquery.js就可以直接访问到这个文件,浏览器就会输出内容
       this.addResourceHandler(registry, "/webjars/**", "classpath:/META-INF/resources/webjars/");
        //第二种找静态资源的方式:getStaticPathPattern获取静态资源的路径,这个getStaticPathPattern它return了一个this.saticPathPattern,这个staticPathPattern="/**",意思就是当前目录下的东西.除了这两种方式,看下面
       this.addResourceHandler(registry, this.mvcProperties.getStaticPathPattern(),
                              (registration) -> {
            registration.addResourceLocations(this.resourceProperties.getStaticLocations());
            if (this.servletContext != null) {
            ServletContextResource resource = new ServletContextResource(this.servletContext, "/");
             registration.addResourceLocations(new Resource[]{resource});
        	}
        });
```

里面那个webjars:这个东西可以去它的官网,里面有maven的路径,只要导入进来就行,它里面就是那些个资源而已,比如JQuery.

我们再往上翻翻我们会发现一个东西:有一个内部类:public static class Resources,它里面有一个属性:

```java
private static final String[] CLASSPATH_RESOURCE_LOCATIONS = new String[]{"classpath:/META-INF/resources/", "classpath:/resources/", "classpath:/static/", "classpath:/public/"};
```

这个属性里面的四个字符串就是支持的静态资源路径,这个classpath就是对应我们项目的resources文件夹.

所以有五个地方可以放静态资源:上面哪些字符串对应的路径,还有classpath路径下都是可以的.webjars基本是不会去用的

我们最常用的就是默认的static文件夹来放静态资源

注意了:最好别在配置文件里面去指定静态资源路径,默认的已经够用了,如果自定义了,默认的这些全部会失效.



##### SpringBootWeb-首页设置

在MebMvcAutoConfiguration.java中,有这么一个方法:

```java
private Resource getIndexHtml(Resource location) {
			try {
				Resource resource = location.createRelative("index.html");
				if (resource.exists() && (resource.getURL() != null)) {
					return resource;
				}
			}
			catch (Exception ex) {
			}
			return null;
		}
```

这个方法就是获取到首页映射的方法,只要我们把index.html首页放到上面提到的那些路径里面,它就能够识别到并且进行映射.首页我们推荐就仍在static里面或者public里面

我们一般是通过一个请求来跳转的,在templates目录下的资源,只能通过controller来跳转,所以我们可以把静态资源仍在这个里面.但是这样要模板引擎:thymeleaf.

我们以前用的模板引擎是jsp,但是jsp已经很老了,SpringBoot推荐我们的是thymeleaf,我们也可以用freemaker.要使用这个东西我们要导入它的jar包,而且是基于它的3.xx版本以上的.

```xml
<dependency>
            <groupId>org.thymeleaf</groupId>
            <artifactId>thymeleaf-spring5</artifactId>
            <version>3.0.12.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.thymeleaf.extras</groupId>
            <artifactId>thymeleaf-extras-java8time</artifactId>
        </dependency>
```

我们导入完后,它还是有一个ThymeleafProperties.java,这里面就实现了对页面的解析.

它里面有两条属性:

```java
public static final String DEFAULT_PREFIX = "classpath:/templates/";

	public static final String DEFAULT_SUFFIX = ".html";
```

这里就是说它会识别templates文件夹下的.html后缀的资源.

完成导入后,我们就可以使用Controller来进行跳转了:

```java
@Controller
public class TestController {

    @RequestMapping("/test")
    public String test(){
        return "test";
    }
}

```

然后我们有一个test.html,给一个请求test,就可以跳转过来了.

##### Thymeleaf模板引擎

这个东西就像jsp一样,jsp是在jsp文件里面直接用<%%>等这样的东西,而Thymeleaf不使用jsp文件了,它可以直接使用html,只需要在html文件的html标签中添加属性约束:xmlns:"http://www.thymeleaf.org"就可以在html中使用Thymeleaf语法,通过这个跟后台交互了.

所有的html标签,都可以被Thymeleaf接管,只需要在标签里面写属性的地方写一个: th:属性名,就可以使用Thymeleaf来进行后台交互了.

##### Thymeleaf语法:

* ${} : Thymeleaf通过该符号获取model里面的变量.

* 指令:Thymeleaf中为了保证前后端的分离,使用了指令,指令就是th:这个东西,一般指令包括了th:和属性名以及=属性值,而且指令是作为html的自定义标签存在的,即使是静态环境下页面也可以直接运行.

* 向下兼容性:html5以下的浏览器可以把指令写成data-th-属性名=属性值

* 对于th:text的注意事项:该属性会对值进行预处理,防止html注入,比如<p>你好</p>将会被格式化输出为$lt;p$gt;你好$lt;/p$lt;在页面显示就是<p>你好</p>,如果想要不进行格式化,就使用th:utext指令吧.

* 自定义变量:当通过对象拿值的时候,可以在父标签上给一个th:object = ${对象名},然后在子标签里面直接用th:text="*{对象的各种属性名}"就可以省去写对象.属性拿值的麻烦了.

* 方法调用:Thymeleaf支持方法调用,${}里面可以直接调用方法.

* Thymeleaf缓存开启与关闭:spring.thymeleaf.cache = false关闭,默认是开启的.

* Thymeleaf内置对象:

  一些环境相关对象:

  * \#ctx                   		:获取Thymeleaf自己的Context对象
  * \#requset                  :如果是web程序，可以获取HttpServletRequest对象
  * \#response               :如果是web程序，可以获取HttpServletReponse对象
  * \#session                  :如果是web程序，可以获取HttpSession对象
  * \#servletContext     :如果是web程序，可以获取HttpServletContext对象

  一些全局对象:

  * \#dates                     :处理java.util.date的工具对象
  * \#calendars             :处理java.util.calendar的工具对象
  * \#numbers              :用来对数字格式化的方法
  * \#strings                  :用来处理字符串的方法
  * \#bools                    :用来判断布尔值的方法
  * \#arrays                  :用来护理数组的方法
  * \#lists                       :用来处理List集合的方法
  * \#sets                       :用来处理set集合的方法
  * \#maps                   :用来处理map集合的方法
  
* 在Controller层中的方法中,可以通过返回ModelAndView对象,把Model的数据给到Thymeleaf引擎,它就会去从模板文件夹中找到对应名称的html页面并把数据转载进去然后返回给前端.

* 除了返回ModelAndView以外,返回String也行,Model数据就需要从参数列表中的Model对象来进行设置.最后返回模板的名称就行.

##### SpringMVC自动配置:

* 自定义视图解析器:只需要实现ViewResolver接口,我们的类就变成了一个视图解析器,在里面就可以进行自定义了.

  ```java
  //打上这个注解让这个类变成配置类
  @Configuration
  public class MyMvcConfig implements WebMvcConfigurer {
      //自动配置MVC
      //实现WebMvcConfigurer接口,以实现自定义配置MVC
      //只需要重写这个接口里面的方法就可以进行各种自定义配置
  
      //实现ViewResolver这个接口的类我们就可以把它看作视图解析器.
      public static class MyViewResolver implements ViewResolver {
  
          @Override
          public View resolveViewName(String s, Locale locale) throws Exception {
              //这个就是一个自定义的视图解析器
              return null;
          }
      }
  
      //自定义的视图解析器需要注册到Bean里面才可以被识别
      @Bean
      public ViewResolver myViewResolver(){
          return new MyViewResolver();
      }
      //这里注册完后,就可以在IOC里面看到这个东西
  }
  ```

* 扩展MVC:

  * 格式化解析器

    我们可以在application.properties里面自定义配置日期格式化:即配置属性:spring.mvc.date-format

  * 在Springboot中,有很多的xxxConfiguration类,会帮助我们进行扩展配置,只要看见它,我们就需要注意,它可能已经更改过了原有的Springboot的东西,我们需要看看里面更新了什么功能.



#### SpringBoot项目流程

进行一个SpringBoot小项目的编写,其流程如下:

* 首先编写dao和pojo,即实体和数据.

  ```java
  //在启动类同级的包下,新建dao包,pojo包,在pojo报下:
  //Department.java
  import lombok.AllArgsConstructor;
  import lombok.Data;
  import lombok.NoArgsConstructor;
  
  @Data
  @AllArgsConstructor
  @NoArgsConstructor
  public class Department {
      //部门表
      private Integer id;
      private String departmentName;
  }
  //Employee.java
  import lombok.AllArgsConstructor;
  import lombok.Data;
  import lombok.NoArgsConstructor;
  
  import java.util.Date;
  
  @Data
  @AllArgsConstructor
  @NoArgsConstructor
  public class Employee {
      private Integer id;
      private String lastName;
      private String email;
      private Integer gender;//0:girl,1:boy
      private Department department;
      private Date birth;
  }
  //在dao包下:
  //DepartmentDao.java
  @Resource
  @Component
  public class DepartmentDao {
      //部门Dao
      //模拟数据库
      private static Map<Integer, Department> department = null;
  
      static {
          department = new HashMap<Integer, Department>();//创建一个部门表
          department.put(101, new Department(101, "A部门"));
          department.put(102, new Department(102, "B部门"));
          department.put(103, new Department(103, "C部门"));
          department.put(104, new Department(104, "D部门"));
          department.put(105, new Department(105, "E部门"));
          department.put(106, new Department(106, "F部门"));
          department.put(107, new Department(107, "G部门"));
      }
  
  
  
      //获取部门信息
      public Collection<Department> getDepartment(){
          return department.values();
      }
  
      //通过id得到部门
      public Department getDepartmentById(Integer id){
          return department.get(id);
      }
  }
  //EmployeeDao.java
  @Resource
  public class EmployeeDao {
      //员工DAO
      private static Map<Integer, Employee> employees = null;
  
      //员工所属部门
      @Autowired
      private DepartmentDao departmentDao;
      static {
          employees = new HashMap<Integer, Employee>();//创建一个部门表
          employees.put(101, new Employee(101, "AA","asdasdad@.com",1,new Department(101,"A部门"),new Date()));
          employees.put(102, new Employee(102,"BB","ASDASDAS@.com",1,new Department(102,"B部门"),new Date()));
          employees.put(103, new Employee(103, "CC","Q23FWQ@.com",1,new Department(103,"C部门"),new Date()));
          employees.put(104, new Employee(104, "DD","ASBEN55@.com",0,new Department(104,"D部门"),new Date()));
          employees.put(105, new Employee(105, "EE","AS654D1A65@.com",0,new Department(105,"E部门"),new Date()));
          employees.put(106, new Employee(106,"FF","A6S43D6A@.com",1,new Department(106,"F部门"),new Date()));
          employees.put(107, new Employee(107, "GG","98746A5S1D9A@.com",0,new Department(107,"G部门"),new Date()));
      }
      //模拟主键自增
      private static Integer initId  = 1006;
      //添加员工
      public void save(Employee employee){
          if(employee.getId()==null){
              employee.setId(initId++);
          }
          employee.setDepartment(departmentDao.getDepartmentById(employee.getDepartment().getId()));
          employees.put(employee.getId(),employee);
      }
  
      //查询全部员工
      public Collection<Employee> getAll(){
          return employees.values();
      }
  
      //通过ID查询员工
      public Employee getEmployeeById(Integer id){
          return employees.get(id);
      }
  
      //删除员工
      public void deleteEmployeeById(Integer id){
          employees.remove(id);
      }
  }
  ```

* 导入静态资源,比如各种html资源,css资源等

  * html页面放在resources文件夹下的templates文件夹下
  * css,js,图片等资源放在resources文件夹下的static文件夹下

* 静态页面我们还访问不了,要有控制器,在启动类同级的包下新建controller包,里面的类都是控制类.

  ```java
  //要实现页面跳转,可以在controller报下写控制类,或者在config包下的自定义mvc配置类中重写方法
  //通过controller实现:
  //IndexController.java:
  @Controller
  public class IndexController {
  
      @RequestMapping("/")
      public String index(){
          return "index";
          //推荐在自定义MVC配置里面进行跳转
      }
  }
  //通过自定义MVC配置实现:
  //MyMvcConfig.java
  @Configuration
  public class MyMvcConfig implements WebMvcConfigurer {
      @Override
      public void addViewControllers(ViewControllerRegistry registry) {
          //这里也可以跳转
          registry.addViewController("/").setViewName("index");
      }
  }
  ```

* 国际化:在resources文件夹下添加一个i18n文件夹,在里面添加login.properties配置文件,和login_zh_CH.properties配置文件,他们会被合并,然后我们可以通过右键那个大的文件add,而且编辑文件的左下方有一个Resource Bundle选项,可以在这里进行可视化配置,只需要在可视化界面里面点+,写上键值以及每个语言对应的值就行了,然后在application.propreties里面进行配置,要用spring.message.basename属性进行配置,它的值就是我们国际化配置文件所在的路径,比如login的话就是:i18n.login.然后需要在前端页面使用Thymeleaf模板引擎的#{}来把那些对应的显示的值括起来.



### 分布式理论

在<分布式系统原理与范型>中有如此定义:分布式系统是若干独立计算机的集合,这些计算机对于用户来说就像单个相关系统.分布式系统是由一组通过网络进行通信,为了完成共同任务而协调工作的计算机节点组成的系统,它的出现是为了用多个廉价的,普通的机器完成单个计算机无法完成的计算,存储任务,目的是利用更多的机器,处理更多的数据.

#### Dubbo

随着网络的发展,网站应用的规模不断扩大,常规的垂直应用框架已经无法应对,分布式服务架构与流动计算架构1势在必行,急需一个治理系统确保架构有条不紊的演进,这也就是Dubbo的由来原因.

Dubbo的一张图:

![Dubbo](C:\Users\qj176\Pictures\Saved Pictures\linux\Dubbo.PNG)

这个图形象演示了一直以来互联网架构的发展,也就是这个流程:

单一架构(ORM)->垂直应用架构(MVC)->分布式服务架构(RPC)->流动计算架构(SOA)

RPC:Remote Procedure Call,远程过程调用,它是相较于Http的了另一种分布式架构之间各种服务的通信方式.远程过程调用是相比于本地过程调用的,本地过程调用就是在本地去调用服务,比如我要启动本机上的某个服务,我就要在本机上操作;而远程过程调用是通过另一台机器来启动本机的服务.它是一种技术思想而不是一种规范.它的核心就是通信和序列化

RPC原理:

![RPC原理](C:\Users\qj176\Pictures\Saved Pictures\linux\RPC原理.PNG)

过程:

![RPC过程](C:\Users\qj176\Pictures\Saved Pictures\linux\RPC过程.PNG)



SOA:面向服务的分布式架构

Dubbo是一款轻量级的,开源的JavaRPC框架,它是Apache的,它提供了三大核心能力:面向接口的远程方法调用,智能容错与负载均衡,服务自动注册和发现.

**Dubbo的原理需要会Netty,计算机网络传输原理.**

Dubbo在13年的时候摸了.直到18年才重启,而这期间,SpringCloud出来了,它就被干掉了.但它仍然是一个专业的RPC框架,比SpringCloud那个强.

Dubbo的执行流程:
![Dubbo执行流程](C:\Users\qj176\Pictures\Saved Pictures\linux\Dubbo执行流程.PNG)



Provider:服务提供者,暴露服务的服务提供方,服务提供者在启动时,向注册中心注册自己提供的服务

Registry:注册中心,注册中心返回服务提供者地址列表给消费者,如果有变更,注册中心将基于长连接推送变更数据给消费者

Consumer:服务消费者,调用远程服务的服务消费方,服务消费者在启动时,向注册中心订阅自己所需的服务,服务消费者从提供者地址列表中,基于软负载均衡算法,选一台提供者进行调用,如果调用失败,就选另一台调用

Monitor:监控中心,服务消费者和提供者在内存中累计调用次数与调用时间,定时发送一次统计数据到监控中心中

Dubbo-Admin:这时一个Dubbo的管理控制台,它是基于SpringBoot的,它现在托管在GITHUB上,我们可以下载上面的项目,然后改好相关配置项,将它打包,运行后就可以进入这个管理控制台了.它可以监控我们部署的所有服务等.



#### Zookeeper

Zookeeper是一个分布式的,开源的分布式的程序协调服务，是 hadoop 项目下的一个子项目。他提供的主要功 能包括：配置管理、名字服务、分布式锁、集群管理。它也就是一个注册中心.

它提供的作用:

* 配置管理
* 名字服务
* 分布式锁
* 集群管理

它也是Hadoop,Hive等大数据框架的注册中心

#### SpringBoot整合Dubbo+Zookeeper(服务注册与发现)

创建两个SpringBoot项目,一个作为服务提供方,一个作为消费方.记得要导入Dubbo和Zookeeper的一些相关依赖.

```xml
<!-- https://mvnrepository.com/artifact/org.apache.dubbo/dubbo-spring-boot-starter -->
<dependency>
    <groupId>org.apache.dubbo</groupId>
    <artifactId>dubbo-spring-boot-starter</artifactId>
    <version>3.0.3</version>
</dependency>
<!-- https://mvnrepository.com/artifact/com.github.sgroschupf/zkclient -->
<dependency>
    <groupId>com.github.sgroschupf</groupId>
    <artifactId>zkclient</artifactId>
    <version>0.1</version>
</dependency>
<!-- https://mvnrepository.com/artifact/org.apache.curator/curator-framework -->
<dependency>
    <groupId>org.apache.curator</groupId>
    <artifactId>curator-framework</artifactId>
    <version>5.2.0</version>
</dependency>
<!-- https://mvnrepository.com/artifact/org.apache.curator/curator-recipes -->
<dependency>
    <groupId>org.apache.curator</groupId>
    <artifactId>curator-recipes</artifactId>
    <version>5.2.0</version>
</dependency>
<!-- https://mvnrepository.com/artifact/org.apache.zookeeper/zookeeper -->
<dependency>
    <groupId>org.apache.zookeeper</groupId>
    <artifactId>zookeeper</artifactId>
    <version>3.7.0</version>
</dependency>
<!-- https://mvnrepository.com/artifact/org.slf4j/slf4j-log4j12 -->
<dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-log4j12</artifactId>
    <version>1.7.32</version>
    <scope>test</scope>
</dependency>

```

```properties
#常用的配置
dubbo.application.name = provider-server  #配置注册服务应用的名字
dubbo.registry.address = zookeeper://127.0.0.1:2181 #配置注册中心的IP与端口
dubbo.annotation.package = 包路径
```

在我们服务接口实现类上添加dubbo包下的@Server注解,就可以在启动应用时自动注册服务到注册中心去.

在消费者的项目下,通过@Reference注解来远程引用服务.并且这里用的是Spring的@Server,引用远程服务的时候,需要在消费者项目下与服务端项目下服务接口存在的包相同位置上去创建一个相同的服务接口,但不用写实现类.

总结:

* 提供者提供服务
  * 导入依赖
  * 配置注册中心的地址,服务发现名,要扫描的包
  * 在需要注册的服务上添加一个dubbo的@Server注解
* 消费者消费服务
  * 导入依赖
  * 配置注册中心的地址,配置自己的服务名
  * 从远程引用服务

## SpringCloud

分布式架构的四个核心问题:

* 很多的服务,那么客户端要怎么访问?
* 很多的服务,服务间要怎么通信?
* 很多的服务,要如果治理?
* 很多的服务,服务挂了怎么办?

SpringCloud就是目前解决以上问题的一站式解决方案.而现在已经有了下一代微服务标准:服务网格(Server Mesh),其中的一个解决方案就是istio,它正在孵化,出来后可能就要成为主流了.

SpringCloud是一个生态,它是很多技术互相连接互相协调的一个解决上面四个问题的解决方案.通常使用的三种解决方案:

* SpringCloud NetFlix : 一站式解决方案,由Google开发.
  * 它解决第一个问题的方案: API网关,zuul组件
  * 对于第二个问题: Feign,这是一个基于HTTP协议的,它是同步阻塞的
  * 对于第三个问题: Eureka实现服务注册与发现
  * 对于第四个问题: Hystrix服务熔断机制
  * 但它2018年后因为某种原因停止更新了.
* Apache Dubbo Zookeeper: 半自动解决方案,需要协同其他的
  * 对于第一个问题: 本身没有解决方案,只能通过第三方组件或者自己写一个组件
  * 对于第二个问题: Dubbo
  * 对于第三个问题: Zookeeper
  * 对于第四个问题: 本身也没有,只能通过第三方,比如去借助Hystrix
* SpringCloud Alibaba : 新的一站式解决方案,由阿里开发,与NetFlix类似,但比NetFlix更加简化                                         

但是这些东西还是万变不离其宗的:

* API网关,服务路由
* HTTP,RPC框架,异步调用
* 服务注册与发现,高可用
* 熔断机制,服务降级

这些问题的根源,就是:网络是不可靠的.

基于这些东西,我们面试就会有这些面试题:

* 什么是微服务
* 微服务之间如何独立通信
* SpringCloud与Dubbo有什么区别
* SpringBoot与SpringCloud,谈谈对于它们的理解
* 什么是服务熔断,什么是服务降级
* 微服务的优缺点,在实际项目开发中遇到的坑
* 微服务技术栈有哪些
* Eureka和Zookeeper都可以提供服务注册与发现功能,它俩有啥区别

### 微服务技术栈

| 微服务技术                             | 已落地技术                                                 |
| -------------------------------------- | ---------------------------------------------------------- |
| 服务开发                               | SpringBoot,SpringMVC,Spring等                              |
| 服务配置与管理                         | Netflix的Aechaius,阿里的Diamond等                          |
| 服务注册与发现                         | Eureka,Consul,Zookeeper等                                  |
| 服务调用                               | Rest,RPC,gRPC                                              |
| 服务熔断器                             | Hystrix,Envoy等                                            |
| 负载均衡                               | Ribbon,Nginx等                                             |
| 服务接口调用(客户端调用服务的简化工具) | Feign等                                                    |
| 消息队列                               | Kafka,RabbitMQ,ActiveMQ等                                  |
| 服务配置中心管理                       | SpringCloud Config,Chef等                                  |
| 服务路由(API网关)                      | Zuul等                                                     |
| 服务监控                               | Zabbix,Nagios,Metrics,Specatator等                         |
| 全链路跟踪                             | Zipkin,Brave,Dapper等                                      |
| 服务部署                               | Docker,Openstack,Kubernetes等                              |
| 数据流操作开发包                       | SpringCloud Stream(封装与Redis,Rabbit,Kafka等发送接收消息) |
| 时间消息总线                           | SpringCloud Bus                                            |

为什么选择SpringCloud作为微服务架构呢?

* 选型依据

  * 整体解决方案与框架成熟度高
  * 社区热度高
  * 可维护性好
  * 学习曲线平滑

* 当前各大IT公司用的微服务架构有那些

  * 阿里: Dubbo + HFS
  * 京东: JSF
  * 新浪: Motan
  * 当当: DubboX
  * ...

* 各自微服务框架对比

  | 功能点/服务框架 | Nefflix/SpringCloud                                          | Motan                                                       | gRPC                      | Thrift   | Dubbo/DubboX                     |
  | --------------- | ------------------------------------------------------------ | ----------------------------------------------------------- | ------------------------- | -------- | -------------------------------- |
  | 功能定位        | 一站式解决方案,完整的微服务框架                              | RPC框架,但整合了ZK或Consul,实现集群环境基本的服务注册与发现 | RPC框架                   | PRC框架  | 服务框架                         |
  | 支持RestFull    | 是,Ribbon支持多种可插拔的序列化选择                          | 否                                                          | 否                        | 否       | 否                               |
  | 支持RPC         | 否                                                           | 是(Hession2)                                                | 是                        | 是       | 是                               |
  | 支持多语言      | 是(Rest形式)                                                 | 否                                                          | 是                        | 是       | 否                               |
  | 负载均衡        | 是(服务端zuul+客户端Ribbon),zuul-服务,动态路由,云端负载均衡,Eureka(针对中间层服务器) | 是(客户端)                                                  | 否                        | 否       | 是(客户端)                       |
  | 配置服务        | Netfix Archaius,SpringCloud Config Server集中配置            | 是(Zookeeper提供)                                           | 否                        | 否       | 否                               |
  | 服务调用链监控  | 是(Zuul),zuul提供边缘服务,API网关                            | 否                                                          | 否                        | 否       | 否                               |
  | 高可用/容错     | 是(服务端Hystrix+客户端Ribbon)                               | 是(客户端)                                                  | 否                        | 否       | 是(客户端)                       |
  | 典型应用案例    | Netflix                                                      | Sina                                                        | Google                    | FaceBook |                                  |
  | 社区活跃度      | 高                                                           | 一般                                                        | 高                        | 一般     | 2017年后才开始维护,之前中断了5年 |
  | 学习难度        | 中                                                           | 低                                                          | 高                        | 高       | 低                               |
  | 文档丰富度      | 高                                                           | 一般                                                        | 一般                      | 一般     | 高                               |
  | 其他            | SpringCloud Bus为我们的应用程序带来了更多管理端点            | 支持降级                                                    | Netflix内部在开发集成gRPC | IDL定义  | 实践的公司较多                   |

### SpringCloud入门

#### SpringCloud是啥

![SpringCloud](C:\Users\qj176\Pictures\Saved Pictures\linux\SpringCloud.PNG)

SpringCloud是基于SpringBoot提供了一套微服务解决方案,包括服务注册与发现,配置中心,全链路监控,服务网关,负载均衡,熔断器等组件,除了基于Netflix的1开源组件做了高度抽象的封装之外,还有一些选型中立的开源组件.

SpringCloud利用SpringBoot的开发便利性,巧妙的简化了分布式系统基础设施的开发,SpringCloud为开发人员提供了快速构建分布式系统的一些工具,**包括配置管理,服务发现,断路器,路由,微代理,事件总线,全局锁,决策竞选,分布式会话等,**它们都可以用SpringCloud的开发分工做到一键启动和部署.

SpringBoot并没有重复造轮子,它是将目前各个企业开发的比较成熟,经得起实际考验的服务框架组合起来,通过SpringBoot风格进行再封装,屏蔽掉了复杂的配置与实现原理,最终给开发者留出了一套简单易懂,容易部署,容易维护的分布式系统开发工具包.SpringCloud是分布式微服务架构下的一站式解决方案,是各个微服务架构落地技术的集合体,也就是微服务全家桶.

#### SpringBoot与SpringCloud的关系

* SpringBoot专注于快速开发单个个体的微服务,也就是一个个jar包
* SpringCloud是关注全局的微服务协调治理框架,它将SpringBoot开发的一个个单体微服务整合并管理起来,为各个微服务之间提供: 配置管理,服务发现,断路器,路由,微代理,事件总线,全局锁,决策竞选,分布式会话等集成服务.
* SpringBoot可以离开SpringCloud单独使用,开发项目.但是SpringCloud是依赖于SpringBoot的,

#### SpringCloud与Dubbo技术选型

##### 分布式+服务治理Dubbo

目前成熟的互联网架构: 应用服务化拆分 + 消息中间件

![当前大型网站后台的架构1](C:\Users\qj176\Pictures\Saved Pictures\linux\当前大型网站后台的架构1.PNG)

##### Dubbo与SpringCloud对比

|              | Dubbo         | SpringCloud                 |
| ------------ | ------------- | --------------------------- |
| 服务注册中心 | Zookeeper     | SpringCloud Netflix Eureka  |
| 服务调用方式 | RPC           | REST API                    |
| 服务监控     | Dubbo-monitor | Spring Boot Admin           |
| 断路器       | 不完善        | SpringCloud Netflix Hystrix |
| 服务网关     | 无            | SpringCloud Netflix Zuul    |
| 分布式配置   | 无            | SpringCloud Config          |
| 服务跟踪     | 无            | SpringCloud Sleuth          |
| 消息总线     | 无            | SpringCloud Bus             |
| 数据流       | 无            | SpringCloud Stream          |
| 批量任务     | 无            | SpringCloud Task            |

**最大区别: SpringCloud抛弃了Dubbo的RPC通信,采用的是基于HTTP的REST方式**

严格来讲,它俩各有优势,虽然从一定程度来说,Cloud牺牲了服务调用的性能,但也避免了上面提到的原生RPC带来的问题,并且REST比RPC更加灵活,服务提供方和调用方的依赖只依靠一纸契约,不存在代码级别的强制依赖,这在强调快速演化的微服务环境下显得更加合适.

**品牌机与组装机的区别**

看上面的表,很明显,SpringCloud比Dubbo更加强大,涵盖面更加广,而且作为Spring的头牌项目,它还可以与SpringFramework,SpringBoot,SpringData,SpringBatch等其他Spring项目无缝融合,这对于微服务而言是至关重要的.使用Dubbo构建的微服务架构就像组装电脑一样,各环节我们的选择自由度很高,但最终结果就是如果内存不足就无法运行,除非你是一个究极高手.而SpringCloud就像知名的品牌机,在SpringSource的整合下,做了大量的兼容性测试,保证了机器的高稳定性,但是如果要在使用非原装组件外的东西,就需要对其架构有足够的了解 

**社区支持与更新力度**

Dubbo之前停止更新了5年,直到17年7月才重启项目,这期间需要开发者自行升级(这期间当当弄出了DubboX),对于很多想要采用微服务架构的中小企业或者组织来说,是不太合适的,中小企业没有这么强大的技术能力去修改Dubbo的源码与周边的一套解决方案.并不是每个公司都有像阿里那样各种各样的大佬与真实的线上生产环境.

**总结:**Dubbo的定位是一款RPC通信框架,而SpringCloud的目标是微服务架构下的一站式解决方案 

我们在企业里面,需要讨论最多的两个问题:

* 如何优化编码,如何从架构上去优化与实现需求与功能.
* 技术选型,如何让现有代码更加容易维护,如何让现有代码变得高可用.

这两个问题的核心,就是**设计模式与微服务拆分**.当我们能够完全掌握着两个,我们就可以在公司里拥有话语权.

对于SpringCloud的版本号:

* SpringCloud是一个由众多独立子项目组成的大型综合项目,每个子项目都有不同的发行节奏,它们都维护着自己的版本号,SpringCloud呢就通过一个资源清单BOM(Bill of Materials)来管理每个版本的子项目清单.为了避免与子项目的发布版本号混淆,所以没用版本号的形式,而是用命名的方式.
* 它的版本命名是以伦敦地铁站的名称来命名的,同时根据字母表顺序对应版本时间顺序.

学习SpringCloud的一些网站:

* [Spring Cloud Dalston 中文文档 参考手册 中文版](https://www.springcloud.cc/spring-cloud-dalston.html)
* [Spring Cloud Netflix 中文文档 参考手册 中文版](https://www.springcloud.cc/spring-cloud-netflix.html)
* [Spring Cloud中文网-官方文档中文版](https://www.springcloud.cc/)
* [Spring Cloud中国社区 · GitHub](https://github.com/SpringCloud)



### SpringCloud案例与学习

#### SpringCloud案例

我们会使用一个Dept部门模块做一个微服务通用案例: Consumer(消费者Client)通过REST调用Provider(提供者Server)提供的服务.

对于SpringCloud的版本说明:

| SpringBoot版本 | SpringCloud版本 | 关系                       |
| -------------- | --------------- | -------------------------- |
| 1.2.x          | Angel           | 兼容SpringBoot1.2.x        |
| 1.3.x          | Brixton         | 兼容SpringBoot1.3.x和1.4.x |
| 1.4.x          | Camden          | 兼容SpringBoot1.4.x与1.5.x |
| 1.5.x          | Dalston         | 兼容1.5.x,不兼容2.0.x      |
| 1.6.x          | Edgware         | 兼容1.5.x,不兼容2.0.x      |
| 2.0.x          | Finchley        | 兼容2.0.x,不兼容1.5.x      |
| 2.1.x          | Greenwich       |                            |

我们已经使用了超过2.2.x版本的SpringBoot,所以只要超过G版本的都可以用.实际开发中,我们一般用2.0.6版本的SpringBoot与Finchley版本的SpringCloud;或者2.1.4版本的SpringBoot与Greenwich版本的SpringCloud.

我们的的项目结构:我们一般会用一个父项目,然后在父项目里创建多个modul,父项目的pom.xml中会去定义打包方式,引入SpringCloud的依赖与SpringBoot依赖.总的这个pom就是我们的所有子项目都会用到的依赖.

```xml
   <!--父项目里的pom.xml-->

	<properties>
        <!--这里统一配版本-->
        <maven.compiler.source>11</maven.compiler.source>
        <maven.compiler.target>11</maven.compiler.target>
    </properties>

    <!--打包方式-->
    <packaging>pom</packaging>


    <dependencyManagement>
        <dependencies>
        <!--SpringCloud的依赖-->
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>Hoxton.SR12</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        <!--SpringBoot的依赖-->
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-dependencies</artifactId>
                <version>2.3.12.RELEASE</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        <!--数据库依赖-->
            <dependency>
                <groupId>com.oracle.ojdbc</groupId>
                <artifactId>orai18n</artifactId>
                <version>21.1.0.0</version>
            </dependency>
            <!-- https://mvnrepository.com/artifact/com.oracle.database.jdbc/ojdbc8 -->
            <dependency>
                <groupId>com.oracle.database.jdbc</groupId>
                <artifactId>ojdbc8</artifactId>
                <version>21.1.0.0</version>
            </dependency>
            <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
            <dependency>
                <groupId>mysql</groupId>
                <artifactId>mysql-connector-java</artifactId>
                <version>8.0.27</version>
            </dependency>
        <!--数据源-->
            <dependency>
                <groupId>com.alibaba</groupId>
                <artifactId>druid</artifactId>
                <version>1.1.10</version>
            </dependency>
        <!--SpringBoot启动器-->
            <dependency>
                <groupId>org.mybatis.spring.boot</groupId>
                <artifactId>mybatis-spring-boot-starter</artifactId>
                <version>2.2.0</version>
            </dependency>

            <dependency>
                <groupId>log4j</groupId>
                <artifactId>log4j</artifactId>
                <version>1.2.17</version>
            </dependency>
            <dependency>
                <groupId>junit</groupId>
                <artifactId>junit</artifactId>
                <version>4.13.1</version>
                <scope>test</scope>
            </dependency>
            <dependency>
                <groupId>org.projectlombok</groupId>
                <artifactId>lombok</artifactId>
                <version>1.18.20</version>
            </dependency>
            <dependency>
                <groupId>ch.qos.logback</groupId>
                <artifactId>logback-core</artifactId>
                <version>1.2.5</version>
            </dependency>
        </dependencies>
    </dependencyManagement>
```

项目结构:

![springcloud项目结构](C:\Users\qj176\Pictures\Saved Pictures\linux\springcloud项目结构.PNG)

spingcloud_api的内容:

![springcloud_api内容](C:\Users\qj176\Pictures\Saved Pictures\linux\springcloud_api内容.PNG)

springcloud_provider_dept_8001的内容:
![springcloud_provider_dept_8001内容](C:\Users\qj176\Pictures\Saved Pictures\linux\springcloud_provider_dept_8001内容.PNG)

DeptController:

![DeptController内容](C:\Users\qj176\Pictures\Saved Pictures\linux\DeptController内容.PNG)

DpetDao:

![DeptDao内容](C:\Users\qj176\Pictures\Saved Pictures\linux\DeptDao内容.PNG)

DeptServerImpl:

![DeptServcerImpl内容](C:\Users\qj176\Pictures\Saved Pictures\linux\DeptServcerImpl内容.PNG)

springcloud_consumer_dept_80的内容:
![springcloud_consumer_dept_80的内容](C:\Users\qj176\Pictures\Saved Pictures\linux\springcloud_consumer_dept_80的内容.PNG)



ConfigBean:

![ConfigBean内容](C:\Users\qj176\Pictures\Saved Pictures\linux\ConfigBean内容.PNG)

DeptConsumerController:

![DeptConsumerController内容](C:\Users\qj176\Pictures\Saved Pictures\linux\DeptConsumerController内容.PNG)



以上就是一个简单的SpringCloud模板,一个服务提供者,一个服务消费者,和一个api

#### Eureka:服务注册中心

##### Eureka入门

Eureka是Netflix的一个子模块,也是一个核心模块之一,它是一个基于REST的服务,用于定位服务,以实现云端中间层服务发现和故障转移,服务注册与发现对于微服务来说是非常重要的,有了服务注册与发现,只需要使用服务的标识符,就可以访问到服务,而无需修改服务调用的配置文件了,它的功能类似于Dubbo的注册中心,比如Zookeeper.它遵循的设计原则是AP()原则



##### Eureka原理

* Eureka的基本架构
  * SpringCloud封装了Netflix公司的Eureka模块来实现服务注册与发现(对比于Zookeeper来讲,EurekaServer是我们自己写的,Zookeeper下载即用)
  * Eureka采用了CS架构来设计,EurekaServer作为服务注册功能的服务器,它就是服务注册中心
  * 系统中其他的微服务,使用Eureka的客户端连接到EurekaServer并维持连接(心跳链接,如果服务提供者或者消费者断开连接超过一定时间就会认为它死了),这样系统的维护者就可以通过EurekaServer来监控系统中各个微服务是否正常运行,SpringCloud的一些其他模块,比如Zuul就可以通过EurekaServer来发现系统中的其他微服务,并执行相关的逻辑
  * 和Dubbo的架构对比:
    * Eureka包含两个组件: EurekaServer与EurekaClient
    * EurekaServer提供服务注册服务,各个节点启动后,会在这里进行服务注册,这样EurekaServer中的服务注册表中将会存储所有可用服务节点的信息,服务节点的信息可以在界面中直观的看到
    * EurekaClient是一个Java客户端,用于简化与EurekaServer的交互,哭护短同时也是一个内置的,使用轮询负载算法的负载均衡器.在应用启动后,将会向EurekaServer发送心跳(默认周期为每30s一次),如果EurekaServer在多个心跳周期内没有接收到某个节点的心跳,EurekaServer将会从服务注册表中把这个服务节点移除掉(默认周期为90s)
    * Eureka的三大角色:
      * EurekaServer : 提供服务注册与发现服务,与Zookeeper一样
      * Service Provider : 服务提供者,将自身服务注册到EurekaServer中,从而是消费者能够找到
      * Service Consumer : 服务消费者,从Eureka中获取注册服务列表,从而找到需要消费的服务 \\

##### Eureka实际使用

在我们上面的三个工程后,再加一个工程:![Eureka工程](C:\Users\qj176\Pictures\Saved Pictures\linux\Eureka工程.PNG)

在这个工程的pom中:

![Eureka依赖](C:\Users\qj176\Pictures\Saved Pictures\linux\Eureka依赖.PNG)

编写Eureka配置文件:

![Eureka配置](C:\Users\qj176\Pictures\Saved Pictures\linux\Eureka配置.PNG)

然后编写主启动类:

![Eureka启动类](C:\Users\qj176\Pictures\Saved Pictures\linux\Eureka启动类.PNG)

这样我们就创建好了一个EurekaServer,运行工程,在浏览器访问http:\\\localhost:7001就可以进入Eureka服务注册中心客户端查看所有注册的服务了.

对于服务提供者:

在它的pom里增加Eureka依赖,然后在配置文件中新增:
![服务提供者Eureka配置](C:\Users\qj176\Pictures\Saved Pictures\linux\服务提供者Eureka配置.PNG)

然后在它的主启动类中添加注解:

![自动注册到Eureka中的注解](C:\Users\qj176\Pictures\Saved Pictures\linux\自动注册到Eureka中的注解.PNG)

这样在该服务启动时就会自动注册到配置中心中.

##### Eureka的自我保护机制

当我们正在连接的服务关掉后,过一会在EurekaServer的浏览器端上会显示一行红字,那就表示它开启了自我保护机制.

某一时刻下某一个在Eureka中注册的服务有问题了,G了,Eureka不会立刻就把它鲨了,它仍然会对该服务的信息进行保存.

* 默认情况下,如果EurekaServer在一定时间内没有收到服务实例的心跳,EurekaServer会注销该实例,但如果是因为网络分区故障,导致服务与Eureka之间无法通信,以上行为可能就是非常危险并且不该发生的,因为这时服务是正常的,这时候不该注销这个服务.Eureka就通过自我保护机制来解决这个问题:当EurekaServer节点在短时间内丢失过多的客户端时(发生网络故障),那么这个节点就会进入自我保护模式,进入该模式后,Eureka就会保护服务注册表中的信息,不会删除服务注册表中的数据(也就是不会注销服务),当网络故障恢复后,这个EurekaServer节点就会自动退出自我保护模式.
* 在自我保护模式中,EurekaServer会保护服务注册表中的信息,但当它收到的心跳数重新恢复到阈值或以上时,这个EurekaServer节点就会退出自我保护模式,所以可以看出,Eureka管理服务的设计理念就是宁可保留错误的服务注册信息,也不会盲目注销任何健康的服务.也就是好死不如赖活
* 自我保护模式是一种应对网络异常的安全保护措施,它的架构哲学是宁可保留所有,也不会盲目注销服务.因为自我保护机制的存在,Eureka集群才更加的健壮和稳定
* 在SpringCloud中,可以使用eureka.server.enable-self-preservation = false来禁用自我保护机制.

##### Eureka服务暴露

对于注册到了Eureka中的服务,可以通过服务发现来获取该服务的信息:

在DeptController.java中加上:

![服务发现](C:\Users\qj176\Pictures\Saved Pictures\linux\服务发现.PNG)

然后在启动类里加上:![开启服务发现](C:\Users\qj176\Pictures\Saved Pictures\linux\开启服务发现.PNG)

就可以看到相关服务的信息了.

##### Eureka集群配置

我们创建多个EurekaServer项目:
![Eureka集群](C:\Users\qj176\Pictures\Saved Pictures\linux\Eureka集群.PNG)

其中7002与7003的内容都和7001一样,都是一个配置文件和一个主启动类,只需要修改它们的配置文件的一点点东西,就可以让它们三个构成集群:

![Eureka集群配置](C:\Users\qj176\Pictures\Saved Pictures\linux\Eureka集群配置.PNG)

其他两个也这样关联起来就行了.而服务的配置文件里也只用修改一点:

![服务注册到集群](C:\Users\qj176\Pictures\Saved Pictures\linux\服务注册到集群.PNG)

Eureka的集群搭建就完成了,十分的简单

##### CAP原则与对比Zookeeper

CAP原则在redis里讲过,C(Consistency)A(Availability)P(Partition tolerance):强一致性,可用性,分区容错性.它是NoSQL与分布式的核心.

CAP理论的核心:

* 一个分布式系统不可能全部满足CAP,智能同时满足其中两个.

Eureka与Zookeeper的区别:

* Zookeeper保证的是CP(一致性与分区容错性)

  当向注册中心查询服务列表时,可以容忍注册中心返回的是一段时间前的注册信息,但不能接受服务直接挂掉不可用.也就是说,服务注册功能对可用性的要求高于一致性,但是Zookeeper会出现这样一种情况:当主节点因为网络故障与其他节点市区联系的时候,剩余节点会进行Leader选举.而这个选举的时间很长,一般是30s-120s,而且选举期间整个Zookeeper集群是不可用的,这会导致在选举期间注册的服务会瘫痪,在云部署的环境下,因为网络问题导致Zookeeper集群失去主节点是较大概率会发生的事件,虽然服务最终能够恢复,但漫长的选举时间导致服务长期不可用是非常严重的问题.

* Eureka保证的是AP(可用性与分区容错性)

  Eureka在设计时优先保证了可用性.Eureka的各个节点是平等的,几个节点挂掉不会影响正常节点的工作,剩余的节点仍然可以提供服务注册与查询服务.而Eureka的客户端在向某个Eureka节点进行注册时,如果发现连接失败,那它就会自动切换到另外的节点,只要有一个Eureka节点还是健康存在的,那就能保持注册服务的可用性,只不过查询的服务信息可能不是最新的.此外,Eureka还有自我保护机制,如果在15分钟内超过85%的节点都没有正常的心跳,那么Eureka就会认为客户端与注册中心出现了网络故障,此时会出现以下几种情况:

  * Eureka不再从注册列表中移除因为长时间没收到心跳而应该过期的服务
  * Eureka仍然可以接受新的服务的注册与查询请求,但不会被同步到其他节点上(保证当前节点可用)
  * 当网络稳定时,当前正常节点的新的注册信息会被同步到其他节点中

因此呢,Eureka可以很好的应对因为网络故障而导致部分节点失去联系的情况,而不会像Zookeeper那样会使得整个服务都瘫痪掉.

#### Ribbon:负载均衡

Ribbon是SpringCloud基于Netflix Ribbon实现的一套基于客户端负载均衡的工具.

Ribbon是Netflix发布的一个开源项目,主要功能是提供客户端的软件负载均衡算法,间Netflix的中间层服务连接在一起.Ribbon的客户端组件提供一系列完整的配置如:连接超时,重试等.也就是在配置文件中列出LoadBalancr(LB,负载均衡)后面所有的机器,Ribbon会自动的帮助我们基于某种规则(如简单轮询,随机连接等)去连接这些机器(服务器),我们也很容易使用Ribbon实现自定义的负载均衡算法.

Ribbon的功能:

* LB,负载均衡,在微服务或分布式集群中常用的一种应用

* 负载均衡就是将用户的请求平摊到多个服务上,从而达到系统的HA(高可用)

* 常见的能够提供负载均衡服务的软件:Nginx,Lvs等

* Dubbo,SpringCloud中均给我们提供了负载均衡,而SpringCloud中的负载均衡算法可以自定义

* 负载均衡的分类:

  * 集中式LB:
    在服务的消费方与提供方之技安使用独立的LB设备,比如Nginx,由该设施负责把请求访问通过某种测量略转发到服务的提供方

  * 进程式LB:

    将LB逻辑集成到消费方,消费方从服务注册中心获知有那些服务可用,然后自己从这些地址中选取一个合适的服务器进行请求

* Ribbon属于进程式LB,它是一个类库,集成于消费方进程,消费方通过它来获取提供方服务的地址

##### 使用Ribbon实现负载均衡

在80的客户端(服务消费者)中加入依赖:

![Ribbon客户端依赖](C:\Users\qj176\Pictures\Saved Pictures\linux\Ribbon客户端依赖.PNG)

然后在主启动类里添加上@EnableEurekaClient注解

然后在配置文件中加上这些:

![Ribbon客户端配置](C:\Users\qj176\Pictures\Saved Pictures\linux\Ribbon客户端配置.PNG)

在配置类里加一个注解:

![Ribbon客户端配置类注解](C:\Users\qj176\Pictures\Saved Pictures\linux\Ribbon客户端配置类注解.PNG)

在Controller里:

![Ribbon客户端controller的url配置](C:\Users\qj176\Pictures\Saved Pictures\linux\Ribbon客户端controller的url配置.PNG)

在Ribbon于Eureka整合之后,客户端可以直接调用服务,可用不用关心IP地址和端口号

现在还只是一个服务,看不出来,现在我们多加几个服务提供方8002与8003.同时也要多整俩数据库.

![三个服务](C:\Users\qj176\Pictures\Saved Pictures\linux\三个服务.PNG)

三份一样的服务,它们的服务名一致.它们使用不同的数据库.

都启动它们后就可以进行客户端访问,进行请求,就可以发现它又是会请求到不同的数据库的结果.这就是它负载均衡的结果.并且我们会看到它是默认是轮询的.



##### 自定义负载均衡算法

负载均衡策略的实现核心是一个接口:IRule.它表示路由.它的实现类就是负载均衡的策略.它自己有这七种:

| 名称                      | 解释                                                         |
| ------------------------- | ------------------------------------------------------------ |
| RoundRobinRule            | 轮询策略                                                     |
| RandomRule                | 随机策略                                                     |
| BestAvailableRule         | 过滤出故障服务器后，选择一个并发量最小的                     |
| WeightedResponseTimeRule  | 针对响应时间加权轮询                                         |
| AvailabilityFilteringRule | 可用过滤策略，先过滤出故障的或并发请求大于阈值的一部分服务实例，然后再以线性轮询的方式从过滤后的实例清单中选出一个; |
| ZoneAvoidanceRule         | 从最佳区域实例集合中选择一个最优性能的服务实例               |
| RetryRule                 | 按轮询选择一个Server，如果失败，重新选择一个Server重试       |

在客户端的配置类里面,加一个Bean:

```Java
@Bean
public IRule myRule(){
    return new RandomRule();
}
```

这样就可以使用随机策略了





我们来康康经典的轮询算法在Ribbon里是怎么实现的:

```Java
package com.netflix.loadbalancer;

import com.netflix.client.config.IClientConfig;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.util.List;
import java.util.concurrent.atomic.AtomicInteger;

/**
 * The most well known and basic load balancing strategy, i.e. Round Robin Rule.
 *
 * @author stonse
 * @author Nikos Michalakis <nikos@netflix.com>
 *
 */
public class RoundRobinRule extends AbstractLoadBalancerRule {

    private AtomicInteger nextServerCyclicCounter;
    private static final boolean AVAILABLE_ONLY_SERVERS = true;
    private static final boolean ALL_SERVERS = false;

    private static Logger log = LoggerFactory.getLogger(RoundRobinRule.class);

    public RoundRobinRule() {
        nextServerCyclicCounter = new AtomicInteger(0);
    }

    public RoundRobinRule(ILoadBalancer lb) {
        this();
        setLoadBalancer(lb);
    }

    //这个就是轮询算法的核心实现
    public Server choose(ILoadBalancer lb, Object key) {//第一个参数是从父类获取的
        if (lb == null) {//如果这个东西是空的
            log.warn("no load balancer");//没有负载均衡
            return null;
        }

        Server server = null;
        int count = 0;//计数
        while (server == null && count++ < 10) {
            List<Server> reachableServers = lb.getReachableServers();//获取可用的服务集合
            List<Server> allServers = lb.getAllServers();//获取所有的服务
            int upCount = reachableServers.size();
            int serverCount = allServers.size();

            if ((upCount == 0) || (serverCount == 0)) {//没有可用服务就返回空
                log.warn("No up servers available from load balancer: " + lb);
                return null;
            }

            int nextServerIndex = incrementAndGetModulo(serverCount);//如果有就获取下一个节点
            server = allServers.get(nextServerIndex);

            if (server == null) {//如果这个是空的那就礼让线程
                /* Transient. */
                Thread.yield();
                continue;
            }

            if (server.isAlive() && (server.isReadyToServe())) {//活着的话就返回当前的
                return (server);
            }

            // Next.
            server = null;
        }

        if (count >= 10) {
            log.warn("No available alive servers after 10 tries from load balancer: "
                    + lb);
        }
        return server;
    }

    /**
     * Inspired by the implementation of {@link AtomicInteger#incrementAndGet()}.
     *
     * @param modulo The modulo to bound the value of the counter.
     * @return The next value.
     */
    private int incrementAndGetModulo(int modulo) {
        for (;;) {
            int current = nextServerCyclicCounter.get();
            int next = (current + 1) % modulo;
            if (nextServerCyclicCounter.compareAndSet(current, next))
                return next;
        }
    }

    @Override
    public Server choose(Object key) {
        return choose(getLoadBalancer(), key);
    }

    @Override
    public void initWithNiwsConfig(IClientConfig clientConfig) {
    }
}

```

我们只要照着它的样子,就可以很容易整出一个自己的负载均衡算法.但是要注意一个点:自己写的配置类最好别放在跟主启动类同级的地方,因为它会覆盖掉所有的Ribbon客户端配置.我们可以起一个跟主启动类所在包同级的包,在里面建负载均衡算法的配置类:

![自定义的Ribbon负载均衡算法配置类](C:\Users\qj176\Pictures\Saved Pictures\linux\自定义的Ribbon负载均衡算法配置类.PNG)

这里return可以return自己的负载均衡算法类.

然后要在主启动类中加一个注解,高速项目Ribbon负载均衡的配置类:

![Ribbon在主启动类中加的注解](C:\Users\qj176\Pictures\Saved Pictures\linux\Ribbon在主启动类中加的注解.PNG)

我们现在可以仿照随机算法:

```Java
public class RandomRule extends AbstractLoadBalancerRule {

    /**
     * Randomly choose from all living servers
     */
    @edu.umd.cs.findbugs.annotations.SuppressWarnings(value = "RCN_REDUNDANT_NULLCHECK_OF_NULL_VALUE")
    public Server choose(ILoadBalancer lb, Object key) {
        if (lb == null) {
            return null;
        }
        Server server = null;

        while (server == null) {
            if (Thread.interrupted()) {
                return null;
            }
            List<Server> upList = lb.getReachableServers();
            List<Server> allList = lb.getAllServers();

            int serverCount = allList.size();
            if (serverCount == 0) {
                /*
                 * No servers. End regardless of pass, because subsequent passes
                 * only get more restrictive.
                 */
                return null;
            }

            int index = chooseRandomInt(serverCount);
            server = upList.get(index);

            if (server == null) {
                /*
                 * The only time this should happen is if the server list were
                 * somehow trimmed. This is a transient condition. Retry after
                 * yielding.
                 */
                Thread.yield();
                continue;
            }

            if (server.isAlive()) {
                return (server);
            }

            // Shouldn't actually happen.. but must be transient or a bug.
            server = null;
            Thread.yield();
        }

        return server;

    }

    protected int chooseRandomInt(int serverCount) {
        return ThreadLocalRandom.current().nextInt(serverCount);
    }

	@Override
	public Server choose(Object key) {
		return choose(getLoadBalancer(), key);
	}

	@Override
	public void initWithNiwsConfig(IClientConfig clientConfig) {
		// TODO Auto-generated method stub
		
	}
}
```

整一个自己的随机算法类:

```Java
package com.yuzu.myRule;

import com.netflix.client.config.IClientConfig;
import com.netflix.loadbalancer.AbstractLoadBalancerRule;
import com.netflix.loadbalancer.ILoadBalancer;
import com.netflix.loadbalancer.Server;

import java.util.List;
import java.util.concurrent.ThreadLocalRandom;

/**
 * 仿照随机算法,写一个有自己需求的负载均衡算法类
 * 这里的需求:
 * 每个服务访问5次,然后就随机换下一个访问.
 * */
public class MyRandomRule extends AbstractLoadBalancerRule {

    /**
     * Randomly choose from all living servers
     */
    //@edu.umd.cs.findbugs.annotations.SuppressWarnings(value = "RCN_REDUNDANT_NULLCHECK_OF_NULL_VALUE").
    /*整几个变量:
    	total = 0;默认0,如果=5,就指向下一个服务节点
    	currentIndex = 0;默认0,如果total=5,就+1,如果=3,就=0;
    */
    private int total = 0;
    private int currentIndex = 0;
    public Server choose(ILoadBalancer lb, Object key) {
        if (lb == null) {
            return null;
        }
        Server server = null;

        while (server == null) {
            if (Thread.interrupted()) {
                return null;
            }
            List<Server> upList = lb.getReachableServers();//获取存活的服务
            List<Server> allList = lb.getAllServers();//获取全部服务

            int serverCount = allList.size();
            if (serverCount == 0) {//如果没有服务就直接返回null
                return null;
            }

//            int index = chooseRandomInt(serverCount);
//            server = upList.get(index);
            //======================MyCode=======================//
            if(total < 5){
                server = upList.get(currentIndex);
                total++;
            }else {
                total = 0;
                currentIndex++;
                if (currentIndex > upList.size()){
                    currentIndex = 0;
                }
                server = upList.get(currentIndex);
            }
            //=======================End=========================//
            if (server == null) {//如果服务是空的,就线程礼让,进行下次判断
                Thread.yield();
                continue;
            }

            if (server.isAlive()) {//服务是存活的,就返回当前服务
                return (server);
            }

            // Shouldn't actually happen.. but must be transient or a bug.
            server = null;
            Thread.yield();
        }

        return server;

    }

    protected int chooseRandomInt(int serverCount) {
        return ThreadLocalRandom.current().nextInt(serverCount);
    }

    @Override
    public Server choose(Object key) {
        return choose(getLoadBalancer(), key);
    }

    @Override
    public void initWithNiwsConfig(IClientConfig clientConfig) {
        // TODO Auto-generated method stub

    }
}

```

#### Feign:负载均衡

Feign是声明式的WebService客户端,它让微服务之间的调用变得更简单了,类似controller去调用server,SpringCloud集成了Ribbon与Eureka,可用使用Feign时提供负载均衡给HTTP客户端.

只需要创建一个接口,加注解就完事了.

我们调用微服务访问的两种方法:
1.通过微服务名(也就是用Ribbon)

2.通过接口和注解(也就是使用Feign)

Feign的功能

* Feign旨在编写Java HTTP客户端更加容易
* 我们在使用Ribbon+RESTTemplate的时候,利用了RestTemplate对HTTP请求的封装处理,新成立一套模板化的调用方法.但是在实际开发的时候,由于对服务依赖的调用可能不止一处,往往一个接口会被多处调用,所以通常都会针对每个微服务自行封装一些客户端依赖服务接口的定义,在Feign的实现下,我们只需要创建一个接口并使用注解的方式来配置它(就类似于以前Dao接口上标注Mapper注解,现在是一个微服务接口上去标注一个Feign注解)就可以完成对服务提供方的接口绑定,简化了使用SpringCloud Ribbon的时候,自动封装服务调用客户端的开发量.

Feign继承了Ribbon,利用Ribbon维护了MicroServiceCloud-Dept的服务列表信息,并且通过轮询实现了客户端的负载均衡,而与Ribbon不同的是,通过Feign只需要定义服务绑定接口且以声明式的方法,优雅而简单的实现了服务调用.

##### Feign的使用

我们在api项目里加一个包:server包,在里面加一个接口,内容如下:

![Feign远程调用服务的接口](C:\Users\qj176\Pictures\Saved Pictures\linux\Feign远程调用服务的接口.PNG)

然后新建一个与80项目一样的项目,它的controller做一点修改:
![Feign远程调用Controller](C:\Users\qj176\Pictures\Saved Pictures\linux\Feign远程调用Controller.PNG)

在这个新的消费者项目里的主启动类里改点注解:

![Feign主类注解配置](C:\Users\qj176\Pictures\Saved Pictures\linux\Feign主类注解配置.PNG)

api和这个新的消费端记得加依赖:

```XML
<dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-feign</artifactId>
            <version>1.4.7.RELEASE</version>
        </dependency>
```

emmm这里有个很大的坑,就算这个@FeignClient这个注解,它的value属性值里面的服务名称,它不支持下划线也就是_,所以我们的服务名最好写成-而不是下划线,就很蛋疼.

#### Hystrix:服务熔断/降级

##### 服务雪崩

多个微服务之间进行调用的时候,比如服务A调用服务B和服务C,服务B和服务C又去调用其他的服务,这就是所谓的**扇出**,如果扇出的链路上某个微服务的调用响应时间过长或者不可用,对微服务A的调用就会占用越来越多的系统资源,进而引起系统崩溃,也就是所谓的**雪崩效应**.

对于高流量的应用来说,单一的后端依赖可能会导致所有服务器上的所有资源在几秒钟内饱和,这些应用程序还可能导致服务之间的延迟增加,备份队列,线程和其他系统资源的紧张,导致整个系统发生更多的级联故障,这些都表示我们需要对故障和延迟进行隔离和管理,以便单个依赖关系的失败不会引起整个应用程序或系统的崩溃.也就是要**弃车保帅**

##### Hystrix是什么

[首页 »Netflix/海斯特里克斯维基 »吉图布 (github.com)](https://github.com/Netflix/Hystrix/wiki)

Hystrix是一个用于处理分布式系统的延迟和容错的开源库,在分布式系统里,许多依赖不可避免的会调用失败,比如调用超时,异常等,Hystrix能够保证在一个依赖出现问题的情况下,不会导致整个服务崩掉,避免级联故障,以提高分布式系统的可用性.

Hystrix是一个断路器,**断路器**是一种开关装置,当某个服务单元发生故障后,通过断路器的故障监控(比如熔断保险丝),像调用方返回一个服务预期的,可处理的备选响应(FallBack),而不是长时间的等待或者抛出调用方法无法处理的异常,这样就可用保证服务调用方的线程不会被长时间不必要的占用,从而避免了故障在分布式系统中的蔓延,以致整个服务崩溃.

正常来讲,一个分布式系统是这样的:

![一个健康的微服务请求过程](C:\Users\qj176\Pictures\Saved Pictures\linux\一个健康的微服务请求过程.PNG)

用户的请求去请求网络上的服务.

然后请求的一个服务因为网络故障或者服务不可用:

![请求的服务出问题](C:\Users\qj176\Pictures\Saved Pictures\linux\请求的服务出问题.PNG)

当一个服务出现问题,它就会阻塞整个用户请求,当流量变大的时候就会这样:

![服务雪崩](C:\Users\qj176\Pictures\Saved Pictures\linux\服务雪崩.PNG)

可能导致服务器资源饱和,引起服务雪崩.也就是系统爆炸.

Hystrix的解决:

![Hystrix解决服务雪崩的方案](C:\Users\qj176\Pictures\Saved Pictures\linux\Hystrix解决服务雪崩的方案.PNG)

使用服务备份.当服务崩了就去掉另一个服务返回错误信息.

Hystrix提供的功能:

* 服务熔断 

  服务熔断机制是对雪崩效应的一种微服务链路保护机制.

  当扇出链路的某个微服务不可用或者响应时间太长的时候,**会进行服务的降级,进而熔断该节点微服务的调用,快速返回错误的响应信息.**当检测到该节点微服务调用响应正常后恢复调用链路.在SpringCloud里熔断机制通过Hystrix实现.Hystrix会监控服务间调用的状况,当失败的调用到一定阈值时,默认是5秒内20次调用失败就会启动熔断机制.熔断机制的注解是@HystrixCommand

* 服务降级

  就是在大流量流入的情况下,系统资源不够了,我们要忍痛把一些服务给关了,等到流量减少了再把那些服务开回来.

* 服务限流

* 几乎是实时的故障监控

##### Hystrix服务熔断的使用

现在让我们的8001服务提供者开启熔断机制:

复制一份8001的服务项目:
![带hystrix的8001服务提供者](C:\Users\qj176\Pictures\Saved Pictures\linux\带hystrix的8001服务提供者.PNG)

内容与8001一致.

现在加入Hystrix依赖:

```xml
<!--添加Hystrix服务熔断机制-->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-hystrix</artifactId>
            <version>1.4.7.RELEASE</version>
        </dependency>
```

对controller里的get方法搞个异常,并写一个方法作为解决方案:

![异常以及Hystrix解决方案](C:\Users\qj176\Pictures\Saved Pictures\linux\异常以及Hystrix解决方案.PNG)

在我们提供get服务这个方法上加上@HystrixCommand注解就可以开启Hystrix熔断机制了,它的fallbackMethod可以指定服务熔断时调用的方法,也就是解决方案.

最后在主启动类里标注上注解,表示开启断路器:![开启断路器注解](C:\Users\qj176\Pictures\Saved Pictures\linux\开启断路器注解.PNG)



##### Hystrix服务降级的使用:

服务降级的本意是舍弃一些客户的连接,直接让它们没法访问那些服务.所以说,服务降级的本质是跟服务提供方没有关系的.它只跟客户端有关系.

我们的api项目里有个service的接口,我们一般对它还有一些实现类,通过它的实现类去实现失败回调,不过没有也行,我们可以整一个类来实现FallBackFactory接口:

![Hystrix服务降级失败回调类](C:\Users\qj176\Pictures\Saved Pictures\linux\Hystrix服务降级失败回调类.PNG)

然后在提供服务的接口上的Feign注解添加属性和值:
![Feign添加属性fallback](C:\Users\qj176\Pictures\Saved Pictures\linux\Feign添加属性fallback.PNG)

然后在fign的客户端上添加配置:

![开启Hystrix服务降级](C:\Users\qj176\Pictures\Saved Pictures\linux\开启Hystrix服务降级.PNG)

这样我们就完成了服务降级的配置,现在如果我们启动8001服务和8002服务,客户端可以正常访问,如果此时关掉8001服务,而客户端此时还是向8001发送了请求也不会出错,而是会输出我们上面写的那个服务降级的信息.也就是在我们写的回调工厂类的那个return new Dept().set...的信息.

##### 服务熔断与服务降级的区别

* 服务熔断是在服务端的,而且问题导致的原因是因为服务有问题,比如超时或者出现异常,就会引起服务熔断
* 服务降级是在客户端的,主要是从整体网站请求负载上来考虑.当某个服务熔断或者关闭之后,服务将不会被调用,此时在客户端可以准备一个失败回调,这时返回一个提示信息,来提示用户服务不可访问,此时整体的服务水平下降了,此时的请求是可用的,比挂掉好.

##### Hystrix的Dashboard流监控

我们新建一个工程:![Hystrix的DeshBoard](C:\Users\qj176\Pictures\Saved Pictures\linux\Hystrix的DeshBoard.PNG)

它跟80一样是客户端的,所以它俩依赖一样,不过这个有自己的依赖,新加上这两项:

```xml
		<dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-hystrix</artifactId>
            <version>1.4.7.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-hystrix-dashboard</artifactId>
            <version>1.4.7.RELEASE</version>
        </dependency>
```

然后写一个配置文件,配个端口9001,然后加一个主启动类,并添加一个开启监控注解:

![DashBoard流监控主启动类](C:\Users\qj176\Pictures\Saved Pictures\linux\DashBoard流监控主启动类.PNG)

要保证服务被监控,那么服务提供者的依赖里就得有这个依赖:

```xml
<!--完善监控信息-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
```

在需要被监控的服务里面也需要hystrix的依赖,然后我们在需要监控的服务提供者里注册一个Bean(可以写在主启动类里面,也可以写其他能被扫描到的地方),比如我们要监控8001这个服务:

![监控8001](C:\Users\qj176\Pictures\Saved Pictures\linux\监控8001.PNG)



注意这个ServletRegisterationBean里要有一个参数: new HystrixMetricsStreamServlet().

如果不写这个参数会导致Tomcat无法启动.

这个Bean一般是固定的,它就是为了配合监控的.

监控页面我们主要看这几个点:

* 7色数字
  * 绿色的表示成功的请求
  * 黄色表示超时请求
  * 红色表示失败请求
  * 亮蓝色表示错误请求
  * 蓝色表示熔断数
  * 紫色的表示线程池拒绝数
  * 灰色的百分比数表示最近10s内的错误占比
* 一个实心圆圈
  * 这个圆圈有两种含义,它通过颜色的变化代表了实例的健康程度,它的健康程度从: 绿色->黄色->橙色->红色递减
  * 除了颜色变化外,它的大小会根据实例的请求流量发生变化,流量越大,这个圆圈就越大,所以通过该实心圆的展示,就可以在大量实例中快速发现故障实例和高压力的实例.

* 一线

  它是记录两分钟内监控流量的曲线

#### Zuul:路由网关

Zuul是SpringCloud提供的一个能够进行路由和过滤的组件.

路由功能负责将对外部请求转发到具体的微服务实例上,是实现外部访问统一入口的基础,而过滤功能是负责对请求的处理过程进行干预,是实现请求校验,服务聚合等功能的基础.Zuul和Eureka进行整合,将Zuul自身注册为Eureka服务中心治理下的应用,同时从Eureka中获取其他微服务的信息,也就是以后的访问微服务都是通过Zuul跳转后获得.

Zuul能够提供的三大功能:

* 代理
* 路由
* 过滤

##### Zuul的使用

我们建立一个工程:![Zuul的工程](C:\Users\qj176\Pictures\Saved Pictures\linux\Zuul的工程.PNG)

它也是一个应用,所以我们要给它写配置:

![Zuul的配置](C:\Users\qj176\Pictures\Saved Pictures\linux\Zuul的配置.PNG)

然后写一个主启动类,还要在主启动类上加一个注解:

![Zuul启动类](C:\Users\qj176\Pictures\Saved Pictures\linux\Zuul启动类.PNG)

现在我们就不仅可以通过服务的地址来访问到服务,还可以通过Zuul的地址来访问到微服务,只需要中间加上微服务的名字,就比如:http://localhost:8001/dept/get/1可以写成http://localhost:9527/8001的服务名/dept/get/1,都可以访问到8001的服务.而正常情况来说,我们不应该暴露微服务的名字.对于这个我们只需要改一下Zuul的配置:

![路由配置](C:\Users\qj176\Pictures\Saved Pictures\linux\路由配置.PNG)

一般ignored-services我们会用通配符 "*"来禁止所有的微服务名访问.此外,我们还可以用zuul.prefix来配置访问时统一的前缀.



#### Config











































## Docker

#### Docker概述

在我们的开发过程中,常常有这样的问题: 我们的项目一旦离开了我们的开发环境,也就是我们的电脑,换一台电脑就G了,这是因为我们项目依赖的环境没有一起跟过去,而环境配置的过程是非常麻烦的,特别在集群环境下,比如Redis集群,ES集群,Hadoop集群的搭建是非常麻烦的,有些环境甚至不能跨平台,这是非常麻烦的一件事.而Docker就是为了解决这个问题的,使用Docker,我们可以开发打包部署一条龙完成,非常的方便.Docker做的事,就是把我们的整个项目,包括所有环境,它可以打包成一个镜像,放在仓库里,只要从仓库里拿取镜像,就可以得到可运行的一个包了.

Docker的思想来源于集装箱的,核心是隔离,也就是打的每个包是独立的,并且能很好的隔离,彼此不会影响彼此,也就是这个机制,它能将服务器利用到极致.

#### Docker的历史

2010年几个老哥在美国创了个公司,交dotCloud,是做pass的云计算服务,跟虚拟机有关的容器技术,他们将自己的容器化技术进行了命名,就叫Docker,它刚出来的时候并没有引起行业的关注,然后他们就把这个东西就开源了.然后Docker就火起来了,它自从2013年开源后,它每个月都会更新一次,以致于现在它是每个开发人员必学的东西.那它为啥这么火嘞?因为它很小,在容器技术出来前,我们使用的虚拟机是非常庞大的.虚拟机是属于虚拟化技术的,而Docker的容器技术也属于虚拟化技术,但是它是软件虚拟化的,体量非常小.

Docker是基于GO语言开发的开源项目.Docker的文档非常详细.关于Docker,还有一个DockerHub网站,它是一个像GitHub的东西,操作也跟GitHub基本一样,我们可以把我们的镜像发布到上面.

#### Docker的作用

对于传统虚拟机技术,首先要模拟内核于核心库,然后引用基于这些来运行.

传统虚拟机技术的缺点:

* 资源占用大
* 冗余资源多
* 启动慢

而容器化技术并不会去模拟一个完整的操作系统,它只会通过隔离机制,在一个个容器里面,有应用需要的核心与应用,各个容器彼此分离.

容器技术与传统虚拟机技术的区别:

* 传统虚拟机是模拟一个完整的计算机,包括硬件软件,然后在操作系统上安装运行软件
* 容器内的应用直接可以运行在主机中,容器是没有自己的内核的,也没有虚拟我们的计算机硬件,非常小.
* 每个容器互相隔离,每个容器内都有一个属于自己的文件系统,互不影响.

Docker带给我们的好处:

* DevOps(开发,运维) : 打包镜像发布测试,一键运行.
* 更便捷的升级和扩缩容 : 简化应用升级与更改,只需要更改镜像,可以不需要管本机环境.扩展服务器耶很容易
* 更简单的系统运维 : 运行环境是高度一致的,杜绝我的电脑能跑,你的电脑跑不了的问题
* 更高效的资源利用 : 一个1核2G的服务器,甚至能跑十几个Tomcat.因为它是内核级别的虚拟化,它可以在一个计算机上运行非常多的容器实例.服务器性能可以被发挥到极致.非常的牛逼.

#### Docker基础

##### Docker的组成

客户端----Docker主机----Docekr仓库

Docker中的一些名词:

* 镜像(image) : 就好比是一个模板,可以通过这个模板来创建容器服务,比如tomcat镜像->run命令->tomcat01容器(提供服务器服务),通过镜像可以创建多个容器(最终服务运行或者项目运行都是在容器中的).
* 容器(container) : 独立运行一个或者一个组的应用,通过镜像来创建.我们可以把它理解为一个微型的Linux系统
* 仓库(repository) : 存放镜像的敌方,分为公有仓库与私有仓库.

##### Docker运行helloword解析

```shell
yuzu@DESKTOP-0BMOP28:~$ docker run hello-world  #执行docker run命令运行hello-world
Unable to find image 'hello-world:latest' locally    #本地找不到镜像:helloworld
latest: Pulling from library/hello-world   #进行远程拉取镜像
2db29710123e: Pull complete  #拉取完成,并输出一些签名等信息
Digest: sha256:393b81f0ea5a98a7335d7ad44be96fe76ca8eb2eaa76950eb8c989ebf2b78ec0
Status: Downloaded newer image for hello-world:latest

Hello from Docker!    #运行起来了,输出Hello form Docker,表示我们安装好了
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

```shell
yuzu@DESKTOP-0BMOP28:~$ docker images  #该命令可以查看我们Docker下的所有镜像的信息
REPOSITORY    TAG       IMAGE ID       CREATED                  SIZE
hello-world   latest    feb5d9fea6a5   Less than a second ago   13.3kB
```

Docker Hello World流程解析:

```shell
#我们使用docker run 镜像 命令来进行运行镜像,这个命令后,Docker会在本机寻找这个镜像,要么找到,要么没找到,如果找到了,就运行这个镜像,如果没有这个镜像,就去DockerHub或者其他云上的DockerHub上下载镜像,如果在DockerHub上找不到的话,就会返回错误,如果找到了就进行镜像的下载,下载到本地后,就可以运行本地上的镜像了.

#那么Docker到底是咋工作的嘞?
#Docker是一个Client-Server结构的系统,Docker是一个守护进程,它运行在主机上,它是通过Sockert从客户端访问主机的,DockerServer接受到DockerClient的指令(我们发的),就会执行这个命令.

#当我们通过命令运行镜像后,镜像会运行处对应的容器实例,每个容器相当于一个小型虚拟机,它也是会占用端口的
```

因为Docker的抽象层比传统虚拟机少,少了一层虚拟的操作系统,所以效率会很高.

Docker还利用的是主机的内核,而传统虚拟机会抽象出操作系统内核.

##### Docker的基本命令

![ACBFA81BB16F7CC8C8A76DAB5AA073AE](D:\QQDownLoad\2905037705\FileRecv\MobileFile\ACBFA81BB16F7CC8C8A76DAB5AA073AE.png)

对于Docker命令,它跟Linux命令很像,可以使用${}进行复数语句拼接,就像SQL语句里面的嵌套SQL语句

* docker version : docker的信息
* docker info : 显示更详细的信息
* docker 命令 --help : 显示当前docker命令的帮助,不写命令的话,就会输出全部的命令
* docker logs [] 容器id : 查看指定容器中的日志信息.之间可以加个-ft --tail 10 表示隔行输出10条日志,也可也直接-f -t显示全部的日志,可以用Ctrl + C退出显示日志
* docker top 容器id : 显示指定运行容器中的进程信息
* docker inspect 容器id : 查看指定容器的详细信息,输出一个JSON对象数组信息,其中包括了这个容器的全部的详细信息.
* docker exec -it 容器id 路径: 进入正在运行中的容器,并以交互模式运行且指定工作目录.一般很多容器我们都是后台跑的,时不时要回来进去改配置啥的,这个命令就非常重要.这个命令是开启一个新的终端,并在新的终端里操作
* docker attach  容器id 路径 : 进入正在运行中的容器,不过会进入当前正在运行的中断,不会启动新的进程
* docker cp 容器id : 容器内路径 目的主机路径 : 拷贝容器内的文件到主机上指定的路径下,不管容器是不是在运行的.拷贝是一个手动过程,后面有个-v数据卷的技术,可以实现容器与外部数据同步.
* docker stats : 查看CPU状态

###### 镜像命令

* docker images : 查看所有本地镜像,还可以输入一些中间命令,可以输出更详细或者过滤指定的镜像
* docker search 镜像名 : 查找仓库里的指定镜像名对应的镜像
* docker pull 镜像名[:tag] : 从仓库拉取指定镜像名对应的镜像到本地,如果不指定tag(版本号),就会默认拉取最新的那个,而且它的pull是分层的,完事之后会输出一个digest签名信息和status后面的真实地址.我们的命令也就等价于那个真实地址.
* docker rmi -f 镜像id/镜像名称 : 删除指定的镜像.

###### 容器命令

我们有了镜像,才可以创建容器,这个容器甚至是可以跑操作系统的.

* docker run 镜像名 : 运行镜像并创建容器

  * docker run --name="容器名" 镜像名 : 创建容器并命名

    * docker run -d 镜像名 : 表示以后台方式运行,通过这个方式的话,用ps命令我们会发现没有正在运行的容器,说明它被停止了.因为后台运行的话,没有前台进程的话就会被认为这是没被启动的,比如nginx这样的没有前台进程的,docker会认为这个容器没有提供服务,就可以杀掉了,所以这个容器会被鲨了.

  * docker run -it 镜像名 [目录(比如/bin/bash)]: 使用交互方式运行,也就是可以进入容器查看内容,指定目录的话就像我们在linux下面那样的进入工作目录.

    ```shell
    yuzu@DESKTOP-0BMOP28:~$ docker run -it centos /bin/bash    #进入容器
    [root@404f64b88eae /]#                                     #进入容器并从指定目录下开始.这里就相当于在跑个centos系统.不过它是个基础版本,很多命令是不完善的
    ```

  * exit : 容器退出,并返回主机

  * 使用按键: Ctrl + R + Q 可以不退出容器,但是会回到主机界面

  * docker run -p/-P  镜像名 : 大P是指定容器端口,小p是随机指定一个端口

    * -P 主机端口:容器端口
    * -P 容器端口
    * 直接写容器端口
    * ip:主机端口:容器端口

  * docker ps : 显示当前正在运行中的容器.还可以带个-a表示历史运行过的容器,带个-n=...可以显示最近创建的容器,可以写个数

* docker rm 容器id : 删除指定容器,但是不能删正在运行的容器,要强制删除就得用下面那条

* docker rm -f ${....} : 可以嵌套一些命令进去,比如写上docker ps -aq 就会删全部的容器

* docker start 容器id : 启动指定容器

* docker restart 容器id : 重启指定容器

* docker stop 容器id : 停止指定容器

* docker kill 容器id : 强制关停容器

#### Docker案例

##### Docker部署Nginx

1.查找nginx : docker search nginx

2.拉取nginx : docker pull nginx

3.运行nginx : docker run -d --name nginx01 -p 3344:80 nginx

这样就可以运行起来一个名为nginx01的nginx容器了,并且让它的端口(在容器中默认也是80)映射到了外部主机的3344端口.这是Docker容器的端口映射机制.

```shell
yuzu@DESKTOP-0BMOP28:~$ docker run -d --name nginx01 -p 3344:80 nginx   #启动nginx容器
1ddbd736c5741b9e9b387b9eb1a553975c85f5bb603c72bda2f449dea3b8e6a5
yuzu@DESKTOP-0BMOP28:~$ curl localhost:3344   #在主机上发起一个请求,请求到本机的3344端口,或者打开浏览器,也可以访问到
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
#接下来就可以进入容器,找到nginx的配置文件,进行配置就可以对它进行配置了,但是这样比较麻烦,那我们可以在外部修改配置文件然后内部同时同步么?答案是可以的,也就是docker的-v数据卷技术.
```

##### Docker部署Tomcat

```shell
#对于Tomcat,我们根据上面的操作,部署tomcat后,会发现,官方的镜像被阉割了,少了很多linux命令,并且webapps目录下是空的,因为默认是最小镜像,会把不需要的东西都扔了.只保存了最小可运行系统.
#它的那些网站文件是在webapp.dist下的,我们可以进入容器,并使用cp -r webapps.dist/* webapps 这样复制过去就可以把所有的文件都复制到webapps下了,再访问我们就可以看到网站了.同样的,我们也可以使用docker的数据卷技术去同步数据
```

##### Docker部署ElasticSearch与Kibanna

```shell
#对于ES来说,它暴露的端口很多,消耗内存也非常的多,并且它的数据是需要放置在安全目录下的,也就是从容器中挂载出来.
#我们启动ES后,我们再用docker stats命令查看CPU的状态,我们会发现就ES一个就占用了1.3G的内存,tomcat才占了200M,可见它是多能吃内存的.所以我们也可以进到它的容器里去改配置.或者在启动的时候就配置:
docker run -d --name ES01 -p 9200:9200 -p 9300:9300 -e "discovery.type=signle-node" -e ES_JAVA_OPTS="Xms64m -Xmx512m" elasticsearch:7.6.23
#给它配置了内存限制
```

而Kibana是要和ES连接的,这里就需要通过网络来连接他俩.因为容器是互相隔离的,也不能通过localhost来访问,但是我们可以通过linxu内网来让他俩连接上.而这个linux内网的连接并不是直接就可以连上的,涉及到一些网络知识.

#### Docker可视化工具

##### Portainer

这是一个Docker图形化界面管理工具,提供一个后台面板供我们操作.

```shell
docker run -d -p 8088:9000 --restart=always -v /var/run/docker.sock:/var/run/docker.sock --privileged=true portainer/portainer
```

然后我们在浏览器打开,登录上去,就可以看见我们当前服务器上Docker的详细信息了.

#### Docker镜像详解

镜像是一种轻量级,可执行的独立软件包,用来打包软件运行环境和基于运行环境开发的软件,它包含运行某个软件所需的所有内容,包括代码,运行时库,环境变量和配置文件.所有的应用,直接打包成docker镜像,就可以在随便一台电脑上跑起来.

得到镜像的方法:

* 从远程仓库下载
* CV战士
* 制作DockerFile,也就是自己做镜像

##### Docker镜像加载原理

* UnionFS(联合文件系统)

  UniosFS是一种分层,轻量级,并且高性能的文件系统,它支持对文件系统的修改作为一次提交来一层层叠加,同时可以将不同目录挂载到同一个虚拟文件系统下,Union文件系统是Docker镜像的基础,镜像可以通过分层来进行继承,基于基础镜像,可以制作各种具体的应用镜像.

  特性: 一次同时加载多个文件系统,但从外面看来只能看到一个文件系统,联合加载会把各层文件系统叠加起来,这样最终的文件系统会包含所有底层的文件和目录

Docker的镜像实际上是由一层一层的文件系统构成,这种层级文件系统就是UnionFS

BootFS(Boot File System)主要包含bootloader和kernel,bootloader主要是引导加载kernel,Linux启动的时候会加载BootFS文件系统,在Docker镜像的最底层也就是这个系统,这一层与经典的Linux/Unix系统是一样的,包含Boot加载器与内核,当Boot加载完成(也就相当于我们主机开机从黑屏到显示操作系统这个过程)后整个内核都在内存中了,此时内存的使用权已经由BootFS转交给内核,此时系统也会卸载BootFS.

RootFS(Root File System)在BootFS之上,包含的就是典型的Linux/Unix系统中的/dev,/proc,/bin,/etc等标准目录和文件,RootFS就是各种不同的操作系统的发行版,比附Ubuntu,CentOS等.

就比如说,一个CentOS我们在虚拟机或者本体计算机上安装时,它是由好几个G这么大的,而在Docker这,为啥就只有200M了呢?这是因为对于一个精简的OS,RootFS可以非常的小,只需要包含最基本的命令,工具和程序库就行了,底层的话可以直接使用主机的Kernel,自己只需要提供RootFS.由此可见,对于不同的Linux发行版来说,BootFS基本都是一样的,RootFS会有一些差别,因此不同的发行版对于BootFS是可以公用的.

Docker也就是运用了这个方法,把BootFS与内核(Kernel)都使用了主机的,本身只启动了RootFS,所以它的执行速度与占用内存非常的高效与小.

##### Docker分层的理解

我们在下载Docker的镜像的时候,发现它是一层一层去下载的.我们可以使用inspect命令去看这个镜像的详细信息,我们会发现输出的JSON字符串里面,有个属性叫RootFS,它里面又有一个属性叫Layers,这个对应的东西就是它需要装的东西,而且每下载一次都会进行一次文件级别的记录.

理解:

Docekr的镜像都是开始于一个基础镜像层的,当我们对它进行修改或者去加新的内容时,就会在当前镜像上创建新的镜像层.比如对于一个Ubuntu创建镜像的话,它首先会有一个基本的镜像:Ubuntu,它就是这个镜像的第一层,如果我们向这个镜像去添加一个Python包,这个Python包就会在第一层镜像的基础上创建第二个镜像层.以此类推.**在添加额外的镜像层的同时,镜像始终保持是当前所有镜像的组合**,这一点很重要.

这有个例子 : 在一层镜像里面有1,2,3这三个文件,然后另一层镜像里有4,5,6这三个文件,我们可以把这两层镜像给打包成一个,它们之间的文件是没有冲突的,那么打包好的镜像就包含了6个文件.如果我们要对这个镜像进行更新,比如加了一层镜像,这个镜像对第二层镜像中的5文件进行了更新,那么这个时候上层镜像层中的文件会去覆盖底层镜像层中的文件,这样就使得问你将的更新版本作为一个新的镜像层去添加到镜像当中.Docker通过存储引擎(新版的Docker使用了快照机制)的方式来实现镜像层的堆栈,并保证多镜像层对外展示为统一的文件系统.

Linux上可用的存储引擎有:AUFS,Overlay2,DeviceMapper,Btrfs以及ZFS,每种存储引擎都基于Linux中对应的文件系统或者块设备技术,且每种存储引擎都有其独有的性能特点.

特点:

* Docker镜像是只读的,容器启动时,一个新的可写层会被加载到镜像的顶部,这个可写层就算我们通常说的容器层,容器之下都叫镜像层.
* 当某些不同应用的一些层是相同的话,就可以进行复用

#### Docker提交自己的镜像

docker commit  -m="提交描述信息" -a="作者" 容器id 目标镜像名:版本号  : 表示提交容器成为一个新的副本.

进行这样的操作后,就会生成一个新的镜像在我们的本地上.后面我们还可以提交给远程仓库供别人下载.

这个提交嘞,就是保存我们当前容器的状态,相当于给它的当前状态拍了个快照并且保存下来,后面要用可以直接从这个点开始去用.

到此为止,我们成功入门了Docker,下面三个:数据卷,DockerFile,网络是Docker的精髓.



#### Docker容器数据卷

很多时候,我们的容器是一删除它里面的东西都会没的,而在大多数情况下,我们是需要将容器内的数据同步到主机上的.也就是需要将容器数据持久化.比如MySQL容器,删容器就像我们删库跑路一样了.所以我们需要一个数据共享与持久化的技术.

卷技术就是可以让容器与主机之间数据共享,也就是目录挂载(将容器内的目录挂载到主机本地的目录上)

实现挂载的方式:

* ```shell
  #使用-v命令
  docker run -it -v 主机目录:容器内目录 镜像名字
  #在inspect命令里面,我们可以找到Mounts属性,里面的Source对应的就是主机目录,Destination就表示容器内目录,正确显示了的话就是挂载成功了
  #挂载成功后,两边目录就同步了,我们在容器内部加个文件,这个文件也会同步到主机上.
  ```

举个例子:

```shell
#在Docker里装mysql
docker run -d -p 3310:3306 -v /home/mysql/conf:/etc/mysql/conf.d -v /home/mysql/conf:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 --name mysql01 mysql
#启动mysql,并指定端口,挂载目录,设置mysql密码,给容器取名
#启动成功后,就可以通过IDEA或者SQLYOG来连接容器里面的数据库了
```

匿名挂载和具名挂载

```shell
#当我们使用-v去写路径的时候,如果只写上容器内的目录,不写主机目录,那么这种方式就是匿名挂载.
docker run -d -p 80:80 --name nginx01 -v /etc/nginx nginx #这样就是匿名挂载.
#当我们使用匿名挂载的方式的话,怎么去看数据卷的情况嘞,可以用下面的命令
docker volume ls
#对于匿名挂载的数据卷信息,它输出的volume name信息是一堆64位的串,匿名卷挂载的因为没名字,所以它就会是由系统随机分配的串
#当我们使用-v写路径的时候,这么写: -v 卷名:容器内路径 这样的,就是具名挂载
docker run -d -p 80:80 --name nginx01 -v juming-nginx:/etc/nginx nginx #具名挂载,这样再去看数据卷信息就可以看见这个卷名了.
#通过docker volume inspect 卷名 这样去查看对应数据卷的详细信息,其中的Mountpoint属性就是对应主机的路径.
#如果我们不指定主机目录,那么容器数据卷都会在/var/lib/docker/volumes/卷名这个目录下.
#推荐使用具名挂载奥
#我们怎么确定是具名挂载还是匿名挂载还是指定路径挂载呢?
#-v 容器内路径 : 这就是匿名挂载
#-v 卷名:容器内路径 : 这就是具名挂载
#-v /主机路径/:/容器内路径 : 这就是指定路径挂载
#有时候我们会见到这样的: docker -run ........ -v juming:/etc/...:ro或者rw 这样的,
#这个ro就是read only表示只读,那么容器就对挂载出来的文件的内容就由限制了,在容器里就不可以操作这个文件了,只能从外部挂载的文件进行操作.rw就是read write,也就是容器可以对挂载出来的文件进行读和写,跟平时一样.
```

数据卷容器

数据卷容器也就是多个容器之间的数据同步,

```shell
#比如我们现在有个镜像:docker,我们通过它启动一个叫docker01的容器,它里面有数据卷volume.
#然后我们再通过docker镜像去创建一个docker02容器,然后通过这样的命令:
docker run -it --name docker02 --volume-from docker01 镜像名 
#就可以让容器docker02与docker01的数据卷同步,并且docker01这个容器就是数据卷容器.
#现在在容器docker02或者docker01的数据卷文件中新建文件等操作,它们之间的数据都会同步
#这个数据卷容器挂载是可以挂载多次的,就像多继承一样.
#也可以让多个容器去挂载上同一个父容器(docker01)的数据卷
#如果把这个父容器删了,那些数据也不会丢失,这就相当与一个数据共享+数据备份呢的机制.它们之间的数据是一个互相拷贝的操作.
```



#### DockerFile

DockerFile是用于构建Docker镜像的构建文件.它就是个全自动命令脚本.

```shell
#我们现在就来写个DockerFile脚本
#通过这个脚本就可以生成镜像,这个脚本就是很多命令.
FROM centos                       #指定根镜像,也就是第一层那个镜像,这里提一下,scratch这个镜像是最基本的镜像.
VOLUME ["volume01","volume02"...] #进行卷挂载,会在容器里面生成相应的挂载目录,并且是匿名挂载方式
CMD echo "-----------"            #让控制台输出------------
CMD /bin/bash                     #进入指定目录
#上面的每个命令,就是镜像的一层
```

写好上面那个文件后,就可以通过docker build 命令来生成镜像

docker build -f dockerfile名(可写全路径) -t 镜像名:版本号 .

##### DockerFile构建过程

注意点:

* 每个指令都必须是大写字母
* 执行顺序从上到下
* #表示注释
* 每个指令都会生成一个镜像层并提交

DockerFile是一个面向开发的文件,我们要发布项目,做镜像的时候就需要编写dockerfile文件.DockerFile现在逐渐成为了企业不同部门之间交付或者交付上线的标准.它定义了镜像的所有信息.负责生成DockerImages.也就是最终交付和发布运行的东西.

##### DockerFile指令

###### 构建命令

* FROM 镜像名 : 指定基础镜像,镜像从这开始构建
* MAINTAINER 作者名 : 指定维护者/作者信息
* COPY : 类似ADD,也就是将文件拷贝到镜像中
* ADD : 需要向容器中添加的内容 
* RUN : 镜像构建的时候需要运行的命令
* ONBUILD : 当构建一个被继承的DockerFile的时候会运行这个命令的指令,也就是一个触发指令
* .dockerignore

###### 连接命令

* WORKDIR 目录 : 指定镜像的工作目录,比如/bin/bash这样的

* USER

###### 运行命令

* CMD : 指定容器启动的时候运行的命令
* ENV : 构建的时候设置环境变量
* EXPOSE : 指定暴露端口,可以省去在启动容器的时候指定容器
* VOLUME : 设置数据卷的挂载目录
* ENTRYPOINT : 跟CMD基本一样,而CMD命令只有最后一个会生效,而且可以被替代,而这个可以追加命令

这有个例子:我们自己构建一个centos:

```shell
#构建一个自己的CentOS
#首先创建一个dockerfile文件,然后开始写:
FROM scratch                                #指定基础镜像
MAINTAINER yuzu<qj17687313829@outlook.com>  #指定作者信息
ENV MYPATH /usr/local 						#配置环境变量
WORKDIR $MYPATH								#配置工作路径
RUN yum -y install vim    					#配置构建镜像时要执行的命令
RUN yum -y install net-tools
EXPOSE 80									#配置暴露的端口
CMD echo "------------"                     #运行镜像产生容器的时候要执行的命令,这里输出-----------,CMD后面跟的可以是一个[],里面可以放很多命令
CMD /bin/bash								#运行容器时进入的路径
#对于上面的命令,如果我们在启动这个镜像的时候这样:
#docker run 我们这个镜像的id -l
#就会报错,因为这个-l不是命令,它把CMD给替换掉了
#我们可以用ENTRYPOINT来代替这个CMD,这样就不会报错了,因为这个指令允许我们追加命令.
```

我们可以通过docker history 镜像名 这个命令可以查看历史修改,看到的就是dockerfile命令.

这还有个例子:构建一个Tomcat镜像

```shell
#准备dockerfile文件
#准备tomcat压缩包和jdk压缩包,因为tomcat是依赖于jdk的
FROM centos
MAINTAINER qj
COPY readme.txt /usr/local/readme.txt
ADD jdk压缩包名 /usr/local/
ADD tomcat压缩包名 /usr/local/
RUN sudo apt install vim
RUN sudo apt insatll net-tools
ENV MYPATH /usr/local
WORKDIR $MYPATH
ENV JAVA_HOME /usr/local/jdk1.8
ENV CLASSPATH $JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
ENV CATALINA_HOME /usr/local/apache-tomcat-9.0.22
ENV CATALINA_BASH /usr/local/apache-tomcat-9.0.22
ENV PATH $JAVA_HOME/bin:$CATALINA_HOME/bin:$CATALINA_HOME/lib
EXPOSE 8080
ENTRYPOINT /usr/local/apache-tomcat-9.0.22/bin/startup.sh && tail -f /usr/local/apache-tomcat-9.0.22/bin/logs/catalina.out
```



#### Docker网络



## Redis

### nosql

nosql是一个非关系型数据库,现在这个时代是一个大数据时代,大数据对于一般的数据库(也就是MySQL啦,Oracle啦)来说是没法处理的,于是就出现了对于大数据进行优化的数据库,比如NoSQL就是其中的一员.

数据库的发展历程:

1.单机MySQL时代 : 也就是Web应用通过一个数据库操作层与数据库进行连接进行增删改查.此时的Web应用是很小的,数据量不大,且用的是静态网页,单机数据库就足以承载了.此时网站的瓶颈就是: 数据量有限(因为访问量很少很少);数据索引问题(对于MySQL来说,如果数据量超过300W条,就该使用索引了,但数据和索引都需要占用空间,单机内存有限,处理器处理速度有限.);访问量承受问题(太多数据访问和读写了,服务器无法处理).这些问题对于各个时代是共通的,遇到了这些问题就说明目前的架构已经不适合我们的Web应用了,必须升级.

2.Memcached(数据缓存)+MySQL+垂直拆分(读写分离) 时代 : 这个时代在第一时代的基础上,数据库数量增多了,并且让一些数据库负责读,一些数据库负责写,但全部的服务器内容同步.此外,因为查询操作的频繁度,还新增了缓存机制,对数据进行缓存,缓存层就放在数据库操作层与数据库之间.缓存的出现并不是一蹴而就的,它经历了这样一个过程:

在第一世代的基础上,人们对数据库进行优化 : 

首先是对数据库的数据结构与索引进行优化,但发现这方面很难继续优化了;

其次就是数据库类型的优化,就使用文件数据库系统来进行优化,但文件系统涉及到了IO操作,当访问量继续增大,IO的瓶颈也出现了,而且它是与硬件相关,也不好优化了;

进而就是高速缓存技术Memcached的出现;

3.分库分表 + 水平拆分(MySQL(数据库)集群) : 由于数据量愈发庞大,都放在单个表的话难以保证效率,于是就对数据库进行分库分表,并将多个数据库按主从关系构建成一个个集群,缓存端就连接各个数据库集群,每个数据库集群放着一部分用户数据,这样就有效分担了数据库的压力.

4.到了最近这段时间(10年到今年),是一个技术爆炸,科技腾飞的时间段,数据库在这段时间也是快速发展.此时数据量极其庞大,并且数据类型繁杂,MySQL,Oracle等关系型数据库处理这些数据就开始力不从心了.这是就出现了一些其他的非关系型数据库.比如一些专门存图片啊,存网站啊,存定位信息啊等等这些东西的数据库,这些东西不存到关系型数据库里面,就可以大大降低关系型数据库的压力.

在数据库的发展历程中,总是为了读和写的各种问题.比如缓存就是为了解决读数据的问题.分库分表和集群用来解决写数据的压力.

NoSQL数据库可以很好的处理关系型数据库处理不了的数据.

NoSQL: Not Only SQL不只是SQL,它泛指非关系型数据库.在Web2.0时代,数据量飞速增加,尤其是超大规模的高并发的社区网站,这时关系型数据库就不是很能处理了.这里我们先明确关系型数据库与非关系型数据库:

* 关系型数据库:用表记录信息,以一行为一条记录,一列数据为一同一数据类型的数据.
* 非关系型数据库:比如redis这样的键值对数据库.

NoSQL数据库的特点:

* 数据之间没有关系,数据横向扩展能力强.
* 存储数据量大,读写性能强(比如Redis,它在一秒内,可以进行8W条数据的读取,11W条数据的写入)
* 缓存粒度细,NoSQL的数据缓存都是一个记录一个缓存.
* 数据类型多样性,可以不需要前期设计数据库.

关系型数据库与非关系型数据库的区别:

* 关系型数据库的组织是结构化的,主观来就是一个表,而非关系型数据库组织结构不一,有键值对存储的,有图存储的,有文档存储的,有列存储的等等
* 关系型数据库使用结构化查询语言,非关系型数据库没有固定的查询语言
* 关系型数据库数据和关系都放在单独的表中,非关系型数据库数据库基本就是可以随便放
* 关系型数据库有严格的一致性,非关系型数据库是最终一致性的,它不需要在操作的过程中时刻保持一致性
* 关系型数据库具有事务操作,非关系型数据库的事务与关系型的事务是不一样的
* 非关系型数据库的CAP定理和BASE概念.非关系型数据库可以保证高性能,高可用性,高扩展性

Redis就是一种NoSQL型的数据库,它是现在发展最快,使用最广泛的一个NoSQL数据库.

大数据时代的3V与3高: 

* 3V (描述问题): Volume海量  Variet多样  Velocity实时
* 3高(对程序的要求): 高性能 高并发 高可扩展

在这个大数据时代,需要非关系型数据库与数据库的结合,才能更好的处理数据

```
对于不同信息,可以放在不同的数据库里
/对于一个电商网站,有很多的商品,商品显示页面有这些东西:商品基本信息,商品描述,图片等
//对于商品基本信息,一般包含名称,价格,商家信息等等,对于这样的信息,就可以存储在关系型数据库中
//对于商品的描述,评论来说,它们是经常变动的,就可以放在文档数据库里面,比如MongoDB
//对于图片信息,就可以放在分布式文件系统里面,防止丢失,分布式文件系统一般有淘宝的TFS,谷歌的GFS,Hadoop的HDFS,阿里云的oss
//对于商品的搜索关键字,我们不可能用SQL去查这些关键字,而是用搜索引擎,常见的搜索引擎有solr,elasticsearch,淘宝的是ISerach
//对于商品的一些热门信息,就可以放在一些内存数据库里面,就比如Redis和Memacache等
//对于商品的交易,需要调用外部接口
```



### 阿里的框架演进

* 1999年,第一代网站架构,PHP网站,这时还用着Oracle数据库

* 2000年,阿里进入Java时代,使用J2EE的Servelt技术

* 2001-2004年,EJB时代

* 2005-2007,EJB重构,引入Spring,iBatis,Webx等

* 2008-2009,数据量起飞,进入分布式时代,使用Memcached集群,MySQL数据切分,分布式存储,Hadoop等

* 2010-2011,引入NoSQL,大数据,做安全与镜像等

* 以上就是前四世代的网站架构.

* 2011年底,阿里提出第五世代网站架构的使命:敏捷,开放,体验

* 对于大型互联网企业的网站,会有这些问题:

  ```Java
  //1.数据类型太多
  //2.数据源繁多,经常需要重构
  //3.数据需要改造,要修改大量数据库接口
  //对于这些问题,阿里的解决方案是:UDSL同一数据服务层(这里插一嘴,微软的dapr也是这样的一个东西)
  ```

  

### nosql数据模型

* 键值对类型
  * Key指向Value的键值对,通常用散列表也就是哈希表来实现
* 列存储类型
  * 以列簇式存储,将同一列数据存放在一起
* 文档类型
  * Key-Value对应的键值对,Value为结构化数据
* 图类型
  * 图结构

### nosql四大分类

* 键值对类型
  * Redis(必会)
  * 经典应用场景
    * 内容缓存
    * 处理大量数据的高访问负载
    * 日志系统
  * 特点
    * 查找速度飞快
    * 缺点是数据无结构化,通常只被当作字符串或者二进制数据
* 文档型(bson格式,其实看起来很像Json)
  * MongoDB(一般也得会)
    * 这个东西是一个基于分布式文件存储的数据库
    * 由C++开发,主要用于处理大量的文档
    * MongoDB是介于关系型数据库与非关系型数据库之间的东东.MongoDB又是非关系型数据库里面最像关系型数据库的,它也是非关系型数据库中功能最丰富的
  * ConthDB
  * 经典应用场景
    * Web应用中,与K-V结构类似,不同的文档型的数据库的Value是结构化的,因此可以了解Value的内容
  * 特点
    * 数据结构要求不严格,表结构可变,不需要像关系型数据库那样要预先定义表结构
    * 缺点就是查询性能不高,而且缺乏同一的查询语法
* 列存储型
  * HBase(大数据必学)
  * 分布式文件系统
  * 经典应用场景
    * 分布式文件系统
  * 特点
    * 查找速度快
    * 可扩展性强,容易进行分布式扩展
    * 缺点就是功能相对局限
* 图关系数据库
  * 这种类型的数据库不是存图的,它存的是互相有关系的东西,就比如人际关系图这样的
  * 产用于存储朋友圈社交网络,广告推荐的东西
  * 常见的就有Neo4j,InfoGrid
  * 经典应用场景
    * 社交网络
    * 推荐系统
    * 专注于构建关系图谱的系统
  * 特点
    * 可利用图结构相关算法,比如最短路径寻址,N度关系查找等
    * 很多时候需要对整个图做计算才能得出需要的信息,而且这种结构不太好做分布式集群方案

### CAP

CAP原则又称CAP定理，指的是在一个[分布式系统](https://baike.baidu.com/item/分布式系统/4905336)中， Consistency（一致性）、 Availability（可用性）、Partition tolerance（分区容错性），三者不可得兼。

一致性（C）：在[分布式系统](https://baike.baidu.com/item/分布式系统/4905336)中的所有数据备份，在同一时刻是否同样的值。（等同于所有节点访问同一份最新的数据副本）

可用性（A）：保证每个请求不管成功或者失败都有响应。

分区容忍性（P）：系统中任意信息的丢失或失败不会影响系统的继续运作

CAP原则的精髓就是要么AP，要么CP，要么AC，但是不存在CAP。如果在某个分布式系统中数据无副本， 那么系统必然满足强一致性条件， 因为只有独一数据，不会出现数据不一致的情况，此时C和P两要素具备，但是如果系统发生了网络分区状况或者宕机，必然导致某些数据不可以访问，此时可用性条件就不能被满足，即在此情况下获得了CP系统，但是CAP不可同时满足 。

因此在进行分布式架构设计时，必须做出取舍。当前一般是通过分布式缓存中各节点的最终一致性来提高系统的性能，通过使用多节点之间的数据异步复制技术来实现集群化的数据一致性。通常使用类似 memcached 之类的 NOSQL 作为实现手段。虽然 memcached 也可以是分布式集群环境的，但是对于一份数据来说，它总是存储在某一台 memcached 服务器上。如果发生网络故障或是服务器死机，则存储在这台服务器上的所有数据都将不可访问。由于数据是存储在内存中的，重启[服务器](https://baike.baidu.com/item/服务器/100571)，将导致数据全部丢失。当然也可以自己实现一套机制，用来在分布式 memcached 之间进行数据的同步和持久化，但是实现难度是非常大的.

### BASE理论

BASE是Basically Available（基本可用）、Soft state（软状态）和Eventually consistent（最终一致性）三个短语的简写。

BASE是对CAP中一致性和可用性权衡的结果，其来源于对大规模互联网系统分布式实践的结论，是基于CAP定理逐步演化而来的，其核心思想是即使无法做到强一致性（Strong consistency），但每个应用都可以根据自身的业务特点，采用适当的方式来使系统达到最终一致性（Eventual consistency）。接下来我们着重对BASE中的三要素进行详细讲解。基本可用：指分布式系统在出现不可预知故障的时候，允许损失部分可用性。

注意，这绝不等价于系统不可用，以下两个就是“基本可用”的典型例子：

响应时间上的损失：正常情况下，一个在线搜索引擎需要0.5秒内返回给用户相应的查询结果，但由于出现异常（比如系统部分机房发生断电或断网故障），查询结果的响应时间增加到了1~2秒。

功能上的损失：正常情况下，在一个电子商务网站上进行购物，消费者几乎能够顺利地完成每一笔订单，但是在一些节日大促购物高峰的时候，由于消费者的购物行为激增，为了保护购物系统的稳定性，部分消费者可能会被引导到一个降级页面。

弱状态：也称为软状态，和硬状态相对，是指允许系统中的数据存在中间状态，并认为该中间状态的存在不会影响系统的整体可用性，即允许系统在不同节点的数据副本之间进行数据同步的过程存在延时。

最终一致性：强调的是系统中所有的数据副本，在经过一段时间的同步后，最终能够达到一个一致的状态。因此，最终一致性的本质是需要系统保证最终数据能够达到一致，而不需要实时保证系统数据的强一致性。

### Redis基础

Redis,全名Remote Dictionary Server,远程字典服务,它是一个纯C编写,支持网络,可基于内存也可持久化的日志型,键值对类型的数据库,它提供了多种语言的调用API,它是免费开源的,是当下最热门的NoSQL技术之一,也被称为结构化数据库.

Redis可以周期性的把更新数据写入磁盘或者把修改操作写入追加的记录文件,并且在此基础上提供了主从同步.它基本支持所有的语言.

Redis能干啥呢?

* 内存存储,进行数据持久化
* 因为它的读写效率非常高,所以可以拿来做缓存
* 发布订阅系统
* 地图信息分析
* 计时器,计数器(比如网站浏览量这样的)
* ....还有很多

Redis特性

* 持久化
* 多样的数据类型
* 支持集群
* 事务
* ....还有很多

Redis有一个工具:redis-benchmark,这是一个官方提供的一个性能测试工具.它的使用是这样的:启动redis并连接后,使用该命令 redis-benchmark -命令.....

常用命令可以查看文档.

它会测试每个命令在完成我们设置的请求数所需要的时间,还有并发客户端数,每次写入的字节数,保持连接数,也就是有多少个服务器.

Redis的基础知识

* Redis默认有16个数据库,在它的配置文件里,有这么一条: database 16,这就是数据库数量的配置.它默认使用第0个数据库,我们可以用select 第n个数据库 命令来进行切换数据库

  ```shell
  127.0.0.1:6379>select 3  #切换数据库
  OK
  127.0.0.1:6379[3]>dbsize  #查看数据库大小
  0
  ```

* 常用的命令

  * keys * :查看当前数据库中所有的key值
  * flushdb :表示清空当前数据库
  * flushall :表示清空全部的数据库

* Redis是单线程的

  * Redis是基于内存操作的,它的性能瓶颈不在于CPU,而是内存与网络带宽,能使用单线程就用单线程了.

* Redis的高性能原因

  * Redis是将所有数据放在内存中的,所以使用单线程去操作就是效率最高的.因为使用多线程,CPU的上下文切换所消耗的时间会更高.对于内存系统来说,多次读写操作都是在一个CPU上的.没有上下文切换效率会更高.

#### Redis的数据类型

Redis的官方介绍: Redis是一个开源的,基于内存的数据结构存储系统.它可以用作数据库,缓存和消息中间件.它支持多种类型的数据结构,如字符串,散列,列表,集合,有序集合与范围查询,地理空间,索引半径查询等.Redis内置了复制,LUA脚本,LRU驱动事件,事务和不同级别的磁盘持久化,并通过Redis哨兵和自动分区提高可用性(支持集群).

* Redis-Key

  Redis命令

  * EXISTS 键名  : 查看指定键名是否存在,如果存在就返回1,不存在就返回0
  * MOVE 键名 数据库 : 移除某个数据库中的指定键名
  * SET 键名 键值 : 设置一个键值对
  * GET 键名 : 通过键名获取键值
  * EXPIRE 键名 数值 : 设置指定键的存活时间,超过设定数值后,该键名对应的值变为nil
  * TTL 键名: 查看某键名的剩余有效时间
  * TYPE 键名 : 查看指定键名是什么类型
  * 更多命令可以看官方文档

* String

  字符串类型,也是一个最常用的类型

  * APPEND 键名 值 : 向指定键名对应的值后追加指定的值,如果键名不存在,就会新建一个

  * STRLEN 键名 : 获取指定键名对应值的长度

  * INCR 键名 : 将指定键名对应的值+1

  * DECR 键名 : 将指定键名对应的值-1

  * INCRBY 键名 自增量 : 将指定键名对应的值+设置的自增量

  * DECRBY 键名 自减量 : 将指定键名对应的值-设置的自减量

  * GETRANGE 键名 开始下标 结束下标 : 获取指定键名对应值的从开始下标到结束下标的子串,包含开始下标与结束下标

  * SETRANGE 键名 偏移量 替换的值 : 将指定键名对应的值从偏移量开始的字符串替换成指定的替换的值

  * SETNX 键名 值 : 如果不存在指定的键名就设置这个键值对,如果存在这个键名,就不能设置.在分布式锁中我们会经常用这个命令   

  * SETEX 键名 过期时间 值: 设置一个键值对,并可以指定过期时间

  * MSET [键名 值, 键名 值 ......] : 同时设置多个键值对

  * MGET [键名 键名 .....] : 同时获取多个键名对应的值

  * MSETNX [键名 值 键名 值 键名 值....] : 同时设置多个键值对,如果不存在的话,不高它是一个原子性的操作,有一个键值对设置失败的话其他都得失败.

    对于SET来说,我们一般想要通过键值对来存对象的话,一般可以这样:

    SET user:1 {name:zhangsan,age:1},也就是键名是用户1,对应的值是一个json字符串,但是我们还可以这样:

    MSET user:1:name zhangsan user:1:age 1,这样弄的话,就相当于user:{id}:{name},这样我们就能更清晰的知道这个对象是啥,并且它的属性是啥.

  * GETSET 键名 值 : 先获取指定键名再去设置键值对,如果不存在值就返回nil,在设置新的值,如果存在了就获取当前值再设置新的值

  * 字符串类型的使用场景

    * 字符串的键值不仅可以是字符串,还可以是数字,如果是数字的话,就可以做计数器了,还可以做统计数
    * 反正这东西能存的东西太多了,用处也大把大把的

* List

  这是个列表类型,在Redis里面,这个东西因为是连着的,它就可以当栈也可以当队列,用处很多.

  * List的命令都用L开头
  * LPUSH 键名 [值...] : 设置一个名为键名的列表,并向他里面加一个值,我们可以多次使用这个命令对一个列表加多个东西.这个L表示从左边开始加值,加多个的话原先的值就会被挤到右边去.
  * RPUSH 键名 [值 ...] : 跟LPUSH差不多,但是是从右边开始加值的,多次使用这个的话,原先的值就会被挤到左边去.
  * LPOP 键名 : 从左边开始一个值
  * RPOP 键名 : 从右边移除一个值
  * LINDEX 键名 下标值 : 从左边算起,获取下标对应的值
  * RINDEX 键名 下标值 : 从右边算起,获取下标对应的值
  * LLEN 键名 : 获取键名对应列表的长度
  * LREM 键值 移除数量 值 : 移除列表中指定移除数量的值
  * LTRIM 键值 开始点 结束点 : 从左边开始,截断列表中包括开始点和结束点的值,也就是列表中只剩下了包括开始点到结束点之间的值.
  * LRANGE 键名 开始点 结束点 : 从名为键名的列表里,拿从开始点与结束点间(包括他俩)的值,跟String类型不同,这里的开始点是从PUSH列表的末尾开始的.
  * RPOPLPUSH 列表名1 列表名2 : 从列表1的右边开始,移除第一个元素到列表2中
  * LSET 键名 下标值 值 : 从左边开始,向指定键名对应的列表中指定的下标添加一个值,但是首先得有这个列表和这个下标.
  * LINSERT 键名 BEFORE/AFTER 值 要插入的值 : 从左边开始,向指定键名对应的列表中指定的值,向它的后/前插入指定的要插入的值
  * List的一些问题
    * List实际上是一个链表,而且还是个双向链表
    * 一个key不存在,就创建新链表
    * key存在,就可以新增结点
    * 如果移除所有的值,链表就为空,也就代表不存在了
    * 在两边插入或修改值的话效率会高,如果是对于中间值的插入和该值的话效率就低点

* Set

  这个就是个不重复的集合类型.Set类型的话它的命令开头都是S开头的

  * SADD 键名 [值...] : 向指定键名代表的SET中存值
  * SMEMBERS 键名 : 显示指定键名代表的SET中的值
  * SISMEMBER 键名 值 : 判断指定的值在指定的键名代表的SET中是否存在
  *  SCARD 键名 : 获取指定的键名代表的SET中值的数量
  * SREM 键名 [值...] : 移除指定键名代表的SET中的指定值
  * SRANDMEMBER 键名 [数量] : 随机获取指定键名代表的SET中指定数量的元素
  * SPOP 键名 : 随机弹出指定键名中的一个元素
  * SMOVE 键名1 键名2 键名1中的成员 : 移动指定键名1对于的SET中指定的成员到键名2对应的SET中
  * SDIFF 键名1 [键名2 键名3.....] : 比较指定键名1对应SET与其他键名对应SET中的差集,即输出其他键名对应SET中不存在键名1对应SET中的值
  * SINTER 键名1 [键名2 键名3.....] : 比较指定键名1对应SET与其他键名对应SET中的并集,即输出其他键名对应SET中与键名1对应SET中的值相同的值
  * SUNION 键名1 [键名2 键名3....] : 输出键名1指定SET与其他键名对应SET间的并集,也就是全部的元素

* Hash

  哈希类型,是一个散列表,它就像一个Map集合,也就是一个键值对,对Hash类型的命令都是以H开头

  * HSET 键名 字段名 [值...] : 设置一个键名对应一个 键值对,字段名就是对应键值对的键名,值就是键名对应的值
  * HGET 键名 [字段名..] : 获取指定键名对应的Hash中字段名所对应的值
  * HGETALL 键名 : 获取指定键名对应Hash中所有的键值对,按键值对显示
  * HDEL 键名 [字段名....] : 删除指定键名对应Hash中指定字段名对应的键值对
  * HLEN 键名 : 获取指定键名对应的Hash的键值对个数
  * HEXISTS 键名 字段名 : 判断指定键名对应Hash中指定字段名的键值对是否存在
  * HEYS 键名 : 获取指定键名对应Hash中所有的键值对的键值
  * HVALS 键名 : 获取指定键名对应Hash中所有的键值对的值
  * HINCRBY 键名 字段名 自增值 : 让指定键名对应Hash中指定字段名对应值+子增值
  * HDECRBY 键名 字段名 自减值 : 让指定键名对应Hash中指定字段名对应值-子增值
  * HSETNX 键名 字段名 值 : 如果指定键名对应的Hash中不存在对应字段名对应的键值对,就新增这个键值对,存在的话就不行.
  * Hash类型常用的地方
    * 存储常变数据,比如用户信息的保存
    * Hash因为存的是键值对,更适合去存对象

* Zset

  这个在SET的基础上,增加了一个值,它是一个可排序的SET.

  * ZADD 键名 [NX/XX] [CH] [INCR] [排序值 值 排序值 值.....] : 创建一个键名对应的ZSET,只写上排序值和值的话,就是向ZSET中放入一个排序值与值,这个排序值是作为排序规则使用的.
  * ZRANGEBYSCORE 键名 最小值 最大值 [withscores]: 在键名对应的ZSET中去根据排序值进行值的排序,[并同时输出排序值],最小值可以写-inf,最大值可以写+inf,表示无限小和无限大.语法只支持升序排序,并且可以用括号来设置开区间
  *  ZREM 键名 [值] : 移除键名指定ZSET中指定的值
  * ZCARD 键名 : 获取键名对应ZSET中的元素个数
  * ZREVRANGE 键名 开始点 结束点 [withscores] : 可以指定开始点和结束点去排序,比如写0 1就是升序,0 -1就是降序
  * ZCOUNT 键名 开始点 结束点 : 获取指定键名对应ZSET开始点到结束点之间的元素(包括他俩)
  * ZSET的引用场景
    * 对于一些需要根据一些东西的权重进行排序的普通数据,比如一天更新一次的排行榜,热搜这样的

* Geospatial

  这个东西是地理空间类型,比如那些城市的距离,打车地图距离,方圆半径内的人数,城市位置这样的,就是由这个类型来存的,它里面就存城市的经度纬度信息等.这个类型是在Redis3.2以上出现的.它的命令是由GEO开头的

  * GEOADD 键名 [经度 纬度 成员 ....] : 向指定键名对应的GEO中放一个成员,以及它的经度纬度.有效经度从-180度到180度,有效纬度从-85.05112878到85.05112878之间.不过这些东西我们不会手动去加,而是用程序去加.
  * GEODIST 键名 成员1 成员2 [单位] : 获取指定键名对应GEO中成员1与成员2之间的绝对距离,可以指定单位,默认是m,单位可以有m,km,mi英里,ft英尺
  * GEOHASH 键名 [成员...] : 返回键名对应GEO中指定成员的经纬度信息转换为一个11位的hash值,如果两个成员之间的这个11位的hash值相似度越高,它们之间的距离就越近
  * GEOPOS 键名 [成员...] : 获取键名对应GEO中指定成员的经纬度
  * GEORADIUS 键名 经度 纬度 半径(要带单位) [withdist] [withcoord] [count 数量]: 以给定经纬度为中心,查找所给半径中的所有元素,[并显示元素到所给经纬度的直线距离],[显示元素经纬度],[显示指定元素的数量]
  * GEORADIUSBYMEMBER 键名 成员 半径(带单位) : 以给定键名对应的GEO的指定成员为中心,查找所给半径中的所有元素,其他跟上面那个命令一样.
  * GEO底层的原理: 其实就是使用ZSET实现的,我们是可以使用ZSET命令来操作GEO的,比如删除,查找全部

* Hyperloglog

  基数统计,基数:一个集合中不重复元素的个数,该数据类型在Redis2.8.9新增的.它是Redis用于做基数统计的数据结构.Hyperloglog类型的命令一般都用PF开头

  * 应用场景
    * 比如统计人数,原先我们可以用SET来做,但是在并发情况下SET可能不准确,而且存的是用户id,消耗的内存比较多,为了计数而去存id是非常浪费的.
    * 使用Hyperloglog的优点
      * 占用内存是固定的,即使是2^64给不同元素的计数,只需要12KB的内存.
      * 存在0.81%的错误率,如果不允许容错的话,就不能使用Hyperloglog类型了
  * PFADD 键名 [值....] : 向名为键名对应的Hyperloglog中加值
  * PFCOUNT 键名 : 获取指定键名对应的Hyperloglog中的数据个数
  * PFMERGE 新键名 [目标键名...] : 将目标键名对应的Hyperloglog取并集并放到新键名对应的Hyperloglog中

* Bitmaps

  位存储,也就是用00000001111这样的方式存储,也就是分状态存储,比如疫情中感染人数的统计,全部人都是0,感染一个就有一个0变成1,还有用户的活跃与非活跃,登录与未登录的这样的,也可以用这种方式.对于Bitmaps,它的命令一般以bit结尾

  * SETBIT 键名 字段名 值 : 为指定键名对应的Bitmaps的指定字段名赋值,字段名也就是位名,值也就是位名对应的值,
  * GETBIT 键名 字段名 : 获取指定键名对应Bitmaps指定字段名对应的值
  * BITCOUNT 键名 [开始字段名 结束字段名] : 统计指定键名对应的Bitmaps中值为1的位个数,可以设置统计的开始位与结束位

#### Redis的配置详解

还记得么,我们启动Redis的命令: redis-server -p redis.conf,这个redis.conf就是redis的配置文件,我们康康它里面有啥.

进入了这个文件,我们会发现有很多注释,它这些注释都是对配置的具体介绍.

首先是对于单位的介绍,可以设置1k,1kb,1m,1mb,1g,1gb这样的大小,并且对大小写不敏感.

然后是可以通过include 配置文件路径来引入其他配置文件

bind ip地址 : 这个表示为Redis绑定的IP地址

protected-mode yes/no : 表示Redis是否处于保护模式

prot 端口号 : 这个表示端口号

daemonize yes/no : Redis是否作为守护进程方式允许,默认是no,我们需要开启为yes,不然的话我们一关掉命令窗口服务就关了

pidfile pid文件路径 : 如果开启了守护线程,就需要指定pid进程文件

loglevel notice/debug/verbose/warning : 日志等级

logfile "文件名" : 日志输出的文件名

databases 数据库数量 : 配置数据库的数量,默认是16

always-show-logo yes/no : 是否经常显示logo(也就是开启服务的时候显示的方块)

持久化相关的

save 时间(秒) key数量 : 表示如果在指定时间内有指定数量的key数量进行了修改操作,那么就会进行持久化,该条配置项可以写多个

stop-writes-on-bgsave-error yes/no : 表示在持久化出错后是否继续进行工作

rdbcompression yes/no : 表示是否压缩rdb文件

rdbchecksum yes/no : 表示是否在保存rdb文件的时候进行错误检查

dir 目录 : 表示rdb文件保存的目录

requirepass 密码 : 为Redis设置密码,设置密码后就需要auth 密码命令来进行验证登录

maxclients 客户端数量 : 设置能连接Redis的最大客户端数量

maxmemory <内存单位> : 设置最大内存容量

maxmemory-policy noevication : 内存达到最大的时候触发的处理策略,一般有六种:

1.volatile-lru:只对设置了过期时间的key进行lru(设置默认值)

2.allkeys-lru:删除lru算法的key

3.volatile-random:随机删除即将过期的key

4.allkeys-random:随机删除

5.volatile-ttl:删除即将过期的

6.noeviction:永不过期,报错

appendonly no/yes : 默认不开启AOF模式,即默认是使用RDB持久化方式,因为大部分情况下,RDB已经够用

appendfilename "文件名" : 持久化的文件名字

appendfsync everysec : 每秒执行一次同步,但可能会丢失某一秒的值,还可以设置成always,就表示每次修改都会进行同步,设置成no就是不执行同步,这时就会让操作系统去同步数据

auto-aof-rewrite-percentage 数量 : 

auto-aof-rewrite-min-size 文件大小 : 如果AOF文件打过设置的文件大小,就会开辟一个子进程,然后将文件进行重写,毕竟AOF就是文件追加的机制

这些配置在实际生产环境中是可能可以进行性能的优化的



#### Redis持久化

Redis是一个内存数据库,如果不将内存中的数据库状态保存到磁盘中,如果机器宕机了,就会导致数据丢失,这是非常致命的,所以Redis提供了持久化操作,Redis能够在指定的时间间隔中及那个内存中的数据库以快照方式写入磁盘,也就是Snapshot快照,它恢复的时候就是将快照文件直接读入内存中.Redis会单独创建一个子进程来进行持久化,它会先将数据写入一个临时文件中,待持久化过程结束,再用这个临时文件替换上次持久化完成的文件.整个过程中,主进程不需要进行任何IO操作,这就提高了性能,如果需要进行大规模的数据恢复,且对于数据的完整性不是非常敏感,那么RDB方式会比AOF方式性能高很多,但它的缺点就是最后一次持久化后的数据可能会丢失.

##### RDB

大部分情况下,Redis使用的是RDB模式进行持久化.默认情况下,Redis默认的rdb文件名叫:dump.rdb,RDB触发机制是由save配置决定的,除此之外,执行flushall或者flushdb都会产生这个rdb文件.

如何恢复rdb文件: 只需要将rdb文件放到redis的启动目录下,Redis在启动的时候会自动扫描目录中的rdb文件,如果有,它就会自动恢复文件,将内容读入内存中.

优点:

* 对于大量数据,它的效率非常高,所以它适合大规模数据恢复
* 对于数据完整性要求不是很高的情况下,就使用rdb机制

缺点

* 需要设置一定的时间间隔才能进行持久化,中途宕机的话,最后一次数据的修改可能就没了
* 由于是开辟子进程进行持久化的,所以需要占用一部分资源

##### AOF

AOF即append only file,它会将我们所有的命令记录下来,当数据恢复的适合,就把这些命令再执行一次.

它的机制是这样的: 以日志形式去记录每个写操作,将Redis执行过的指令记录下来(除了读操作),只许追加文件不可以改写文件,Redis启动的适合会读取这个文件进行数据的重构,也就是Redis启动的适合会根据日志文件的内容将写指令从前到后执行一遍来完成数据的恢复工作.

因为是对数据进行重构,命令级别的处理,所以数据恢复会非常准确,但是因为要执行指令,所以在数据量极大的场合会恢复的很慢.

AOF保存的文件名是appendonly.aof

AOF机制默认是不开启的,我们需要把appendonly 配置为yes,Redis就会启用AOF模式进行持久化.它的很多配置默认就已经够用了,如有特殊情况,再进行具体配置.AOF机制是默认执行一次的.

对于AOF文件,它是可能会产生错误的,比如我们编辑了它,并写入了非法的命令,就会导致文件出错,如果AOF文件有问题,那么我们就无法启动Redis文件,如果是这样的问题,我们就可以通过redis-check-aof 文件名 来进行文件修复.

优点:

* 每秒都会进行一次同步,也可以自己设置,它的文件完整性很高,数据错误率非常小,它只可能会丢失错误指令中的几条数据而已

缺点

* 相对于数据文件来说,它的数据文件比rdb大,而且修复速度也比rdb慢
* 因为AOF是IO操作,所以它的运行效率比较低



#### Redis事务操作

在关系型数据库里面,事务是一组SQL指令的集合,它具有ACID的原则.但是在NoSQL中的事务与关系型数据库的事务是不一样的.虽然Redis的事务也是多个命令的集合.但Redis,它的单条命令是原子性的,但是Redis的事务是不保证原子性的.

Redis的事务是用执行队列来操作的,在食物中的所有命令都会被序列化,在事务执行的过程中,会按照顺序执行,因为是队列.而且Redis的事务是没有隔离的概念.所有的命令在事务中,并没有被直接执行,只有在发起执行命令的时候才会去顺序执行命令.

Redis的事务特点

* 一次性
* 顺序性
* 排他性

Redis的事务阶段

* 开启事务
  * MULTI 
* 命令入队
  * 执行开启事务指令后,之后执行的命令都会入队
* 执行事务
  * EXEC
  * 执行该命令后,入队的命令会顺序执行
* 放弃事务
  * DISCARD 
  * 执行该命令后会放弃已经开启的事务
* 如果事务中命令有问题的话,也就是命令(比如写错字)有错,那么事务中的所有命令都不会被执行.并且错误的命令会报错
* 如果事务中存在运行时错误(比如让字符串+1),在执行命令的时候,其他命令是会执行的,错误命令会报错

Redis有时候有监控这种操作,比如我们可以用它来实现乐观锁.

* 悲观锁 : 认为什么时候都可能会有问题,所以做什么都要上锁
* 乐观锁 : 认为什么时候都不会有问题,所以不会在任何时候都上锁,而是在更新数据的时候判断在此期间是否有人修改过这个数据.在MySQL中我们是用version来做的(获取version,在数据更新是时比较version).而在Redis里,可以用WATCH来进行监控,它就相当于一个乐观锁
  * WATCH [键名] : 设置监视指定的键名
  * 当一个事务执行完成后,监控就会结束.
  * 对于Redis这个WATCH,它会在其他线程修改了它所监控的对象后会通知其他线程这个值被修改了.然后会导致原来的事务执行失败.
  * 但监控失败后,需要用UNWATCH [键名] 把本次监控解除,再重新监控,才可以继续另外的事务.其实的话,EXEC命令会自动解锁.



#### Redis实现订阅发布以及消息队列

比如微信公众号订阅功能,推荐,热搜这种东西是怎么实现的?

Redis的发布订阅(Pub/Sub)是一种消息通信模式,发送者(Pub)发送消息,订阅者(Sub)接收消息.Redis客户端可以订阅任意数量的频道.

Redis的订阅的核心还是基于一个队列实现的.

订阅发布的核心角色 : 消息发布者 频道 消息订阅者.

Redis中关于构建即时通信应用的命令:

1.PSUBSCRIBE [频道....] : 订阅一个或多个给定模式的频道

2.PUBSUB subcommand [argument  [argument [....]]] : 查看订阅与发布系统状态

3.PUBLISH channel message : 将信息发送到指定的频道

4.PUNSUBSCRIBE [pattern [pattern....]] : 退订所有给定模式的频道

5.SUBSCRIBE channel [channel ....] : 订阅给定的一个或多个频道的信息

6.UNSUBSCRIBE [channel...] : 退订给定的频道

Redis消息订阅的实现原理:

Redis的源码中,有一个叫pubsub.c的文件,这个文件就是处理订阅与发布信息机制的.当我们通过SUBSCRIBE命令订阅某个频道后,redis-server里维护了一个字典,字典的键就是一个个的频道,而字典的值则色一个链表,链表中保存了所有订阅这个频道的客户端,SUBSCRIBE命令的关键就是将客户端添加到给定频道的订阅链表中.通过PUBLISH发布订阅消息,redis-server会使用给定的频道作为键,在它维护的频道字典中查找记录了订阅这个频道的所有客户端的链表,遍历这个链表,将消息发送给所有的订阅者.

PUB/SUB机制也就是发布与订阅模式,在Redis中,我们可以设定对某一个键(频道)进行消息的发布与消息的订阅,当一个键值上进行了消息的发布后,所有订阅它的客户端都会接收到信息,这一功能最显著的用法就是即时聊天功能,群聊功能等,复杂的场景的话就需要使用消息中间件,比如MQ,KafKa这些来做了.



#### Redis主从复制

在主机复制中,我们主要就用的就是RDB文件来进行数据备份到从机上.

主从复制,就是将一台Redis服务器的数据,复制到其他Redis服务器上,前者称为主节点(master/leader),后者称为从节点(slave/follower),数据的复制是单向的,只能由主节点到从节点,Master以写为主,Slave以读为主.

默认情况下,每台Redis服务器都是主节点,且每一个主节点可以有多个从节点或者没有从节点,但一个从节点只能有一个主节点,

主从复制的作用包括:

* 数据冗余:主从复制实现了数据的热备份,是持久化之外的一种数据冗余方式.
* 故障恢复:当主机出现问题后时,可以由从节点提供服务,实现快速的故障恢复,这实际上是一种服务的冗余
* 负载均衡:在主从复制的基础上,配合读写分离,可以由主节点提供写服务,由从节点提供读服务.以此分担服务器负载,尤其是在写少读多的情况下,通过多个从节点分担读负载,可以大大提高Redis服务器的并发量.
* 高可用基石:除了上述作用外,主从复制机制也是哨兵和集群得以实施的基础,所以说主从复制还是高可用的基础

在架构中,如果需要配置一个Redis集群,就至少需要一台主机与两台从机.

一般来讲,在实际项目的开发中,只使用一台Redis服务器是万万不能的,原因:

* 从结构上来讲,单个Redis服务器会发生单点故障,并且一台服务器需要处理所有的请求,负载过大.
* 从容量上来讲,单个Redis服务器内存容量有限,即使一台服务器的内存为256G,也不能将所有内存用于Redis存储.而且一般来讲,单台Redis最大使用内存不应该超过20G.因为20G的时候,Redis承受的压力非常大,容易出问题.

##### Redis主从复制配置

通过info replication命令可以查看当前库信息,其中role就是当前服务的角色(主还是从).

因为要启动多个Redis,所以每个Redis对应的配置文件都要配好,如果是在一台机器上模拟集群,就要注意更改:

* 端口
* pid文件名
* rdb/aof文件名
* 日志文件名字

修改完成后就可以启动相应的服务了.

启动服务后,并且连上服务后就可以通过命令: SALVEOF IP地址 端口 就可以指定一个对应的主机.也就是指定主机.自己作为从机.然后查看主机就可以看见从机数量有两台了,并且显示出从机的ip与端口以及状态.注意一个点,就是如果主机是有密码的话,从机的配置文件里需要加上**masterauth 主机密码** 这一项.

在真实的开发环境中,很少用我们这样的命令来配置,这样配置的话下次启动就不是主从的了.开发中一般使用配置文件来配置,这样的话就是永久配置的.

在配置文件里,有一项配置项: **replicaof 主机ip 主机端口** 这一项,我们只要在这里配了,那么一启动就会自动进行主从配置,上面那个密码的也是在这个配置旁边的.

配置完了主从配置,主机中所有的数据改动都会同步到所有的从机上.并且不可以通过从机写入数据.只能同主机写入数据.这时即使主机断开了,从机仍然是从机.不过这时对于数据就不可以写了.而且主机恢复了就可以立即连上.如果是从机宕机了的话,重新连回来的时候如果不是配置文件配置的主从机,那么它就会变成主机.如果是在配置文件配置的话,它连回来后就会立刻同步数据.

我们可以搞一个骚操作,就是一个主机有一个从机,然后这个从机又是另一个从机的主机.这个时候也是可以完成主从复制的.不过这个样子很像一个链表,不过这样跟原来的也是一样的,都是主机死了自己就只能等着,不过我们可以通过命令:**SLAVEOF ON ONE**这个命令让自己变成主机.而且通过这样的话,主机就算活过来了,主机就没用了.而且这样是手动的,效率太低了.

这里有个问题:就是当我们的主机如果断了,那么能不能让一个从机变成主机继续提供写服务呢?
答案是有的,这就是哨兵模式.哨兵就是一个自动选取主机的模式.

##### 主从复制的机制

从机启动成功连接到主机后会发送一个sync同步命令

主机接收到命令后启动后台的存盘进程,同时收集所有接收到的用于修改数据集的命令,在后台执行完毕后,主机将传送整个数据文件到从机上,并完成一次数据完全同步

全量复制:在从机接收到数据文件后,将其存盘并加载到内存中,这个操作一般在从机连上的时候进行.

增量复制:主机继续将新的所有收集到的修改命令以此传给从机,完成同步,这个操作一般在写入数据的时候进行.

但是只要是重新连接主机,一次完全同步(全量复制)将被自动执行



##### Redis哨兵模式

在Redis2.8开始正式加入了Sentinel(哨兵模式),哨兵模式是一个特殊的的模式,能够后台监控主机是否故障,如果故障率就可以根据投票数**自动将从机转换为主机**.

哨兵模式是一个特殊模式,Redis提供了哨兵的命令,哨兵是一个独立进程,作为进程,它会独立允许,其原理是**哨兵通过发送命令,等待Redis服务器响应,从而监控运行的多个Redis实例.**

也就是哨兵可以监控所有的主机与从机.这个监控是通过发命令的给Redis,Redis能够响应来实现的,如果没有收到返回的东西,那就认为这个Redis机器死了,就需要进行配置了.

对于哨兵来说,它也得配置成集群,因为它也是一个进程,如果它死了就不能去监控Redis了.

哨兵的作用:

* 通过发送命令,让Redis服务器返回监控其运行状态,包括主机与从机
* 当哨兵检测到主机宕机,会自动将从机转换为主机,然后通过**发布订阅模式**通知其他的从机,修改配置文件,让它们切换主机到这个新的主机,就算主机回来了,它只能做当前主机的从机了.
* 哨兵也像主从机一样,需要配置多个哨兵形成集群,防止单机模式下哨兵出问题死了后监控失效.

集群哨兵的情况下:

假设主服务器宕机了,哨兵1先检测这个结果,系统并不会马上进行failover过程,仅仅是哨兵1认为主服务器宕机了,这个现象称为**主观下线,**但后面的哨兵也检测到主服务器不可用的时候,并且数量达到一定值时,那么哨兵之间就会进行一次投票,投票的结果由一个哨兵发起,进行failover(故障转移)的操作,切换成功后,就通过订阅发布模式,让各个哨兵把自己监控的从服务器切换主机,这个过程称为**客观下线**.

###### 哨兵的配置

写一个哨兵配置文件,名字就算sentinel.conf,在里面写上:

 SENTINEL monitor 哨兵名 监控主机IP 监控主机端口 主观下线数

这条配置的意思就配置一个哨兵,指定它的名字,监控的服务器IP,监控的服务器端口,有多少个哨兵认为服务器宕机就确定服务器是宕机的,开始选举.

如果要监控的主机有密码的话,要加个配置: sentinel auth-pass 监控对象的密码

这条配置是最核心的配置,对于哨兵来说,它的配置有很多.我们只用最基本的就差不多了.

配置完成后,就可以通过命令: redis-sentinel 配置文件路径 来启动哨兵了.

在哨兵日志里可以看出各种信息,包括监控主机信息,新的主机信息,故障转移信息等.



哨兵模式的有点

* 哨兵集群是基于主从复制的,所有的主从配置的有点它都有
* 主从机可智能切换,故障可以转移,系统可用性高
* 哨兵模式升级了主从模式,从手动到自动.

缺点:

* Redis的集群容量一旦到达上线,在线扩容将是一件及其复杂麻烦的事情.
* 哨兵模式的配置其实非常麻烦,命令繁杂.



#### Redis缓存穿透和解决

Redis缓存的使用极大的提升了应用程序的性能和效率,特别是数据查询方面,但同时也存在一些问题,其中最为致命的问题就是数据的一致性问题,严格来说,数据一致性问题是无解的.如果对数据一致性要求非常高,那么就不能使用缓存.另外的典型问题就是缓存穿透与雪崩问题.

缓存穿透是指,当一个用户想要查一个数据,发现redis里面没有,也就是缓存里面没有,于是就向持久层数据库查询.发现也没有,于是本次查询失败.当用户很多的时候,如果大量的查询在redis缓存里都没有命中,于是都去请求了持久层数据库,这个时候会疯狂的查一个数据,这时持久层数据库的压力会突然变得很大,这就是缓存穿透现象.(比如秒杀场景)

解决方案:

* 布隆过滤器

  布隆过滤器是一种数据结构,对所有可能查询的参数以hash形式存储,在控制层先进行校验,不符合则丢弃,从而避免了对底层存储系统的查询压力.

  直观的说，bloom算法类似一个hash set，用来判断某个元素（key）是否在某个集合中。
  和一般的hash set不同的是，这个算法无需存储key的值，对于每个key，只需要k个比特位，每个存储一个标志，用来判断key是否在集合中。

  算法：

  1. 首先需要k个hash函数，每个函数可以把key散列成为1个整数
  2. 初始化时，需要一个长度为n比特的数组，每个比特位初始化为0
  3. 某个key加入集合时，用k个hash函数计算出k个散列值，并把数组中对应的比特位置为1
  4. 判断某个key是否在集合时，用k个hash函数计算出k个散列值，并查询数组中对应的比特位，如果所有的比特位都是1，认为在集合中。

  优点：不需要存储key，节省空间

  缺点：

  1. 算法判断key在集合中时，有一定的概率key其实不在集合中
  2. 无法删除

  典型的应用场景：
  某些存储系统的设计中，会存在空查询缺陷：当查询一个不存在的key时，需要访问慢设备，导致效率低下。
  比如一个前端页面的缓存系统，可能这样设计：先查询某个页面在本地是否存在，如果存在就直接返回，如果不存在，就从后端获取。但是当频繁从缓存系统查询一个页面时，缓存系统将会频繁请求后端，把压力导入后端。

  这是只要增加一个bloom算法的服务，后端插入一个key时，在这个服务中设置一次
  需要查询后端时，先判断key在后端是否存在，这样就能避免后端的压力。

  在Redis这所有的i请求要经过布隆过滤器.只要请求不符合校验,就丢弃该请求.

* 缓存空对象

  当存储层不命中后,即使返回空对象也将其缓存起来,同时设置过期时间,之后再访问这个数据将会从缓存中获取,保护了后端数据源,但是用这个方式会存在两个问题:

  * 如果空值能够被缓存起来,这就以为着缓存需要更多的空间存储更多的键,因为这当中可能会有很多的空值的键
  * 即使对空值设置了过期时间,还是会存在缓存层和存储层的数据会有一段时间窗口的不一致,这对于需要保持一致性的业务会有影响

#### Redis缓存击穿与解决

缓存击穿是指一个键非常热点,在不停的扛着大并发,大并发集中对这一个点进行访问,当这个键在失效的瞬间,持续的大并发就穿破缓存,直接去请求数据库了,就像在缓存层上击穿了一个洞.当某个键在过期的瞬间,有大量的请求并发访问,这类数据一般是热点数据,由于缓存过期,会同时访问数据库来查询最新数据,并且写回缓存,会导致持久层数据库瞬间压力过大崩溃.

解决方案:

* 设置热点数据永不过期

  从缓存层面来说,没有设置过期时间,所以不会出现热点键值过期后产生的问题,但这样的话就可能造成资源浪费.

* 加互斥锁

  分布式锁:使用分布式锁,保证对于每个键同时只有一个线程去查询后端服务,其他线程没有获得分布式锁的权限,因此只需要等待即可,这种方式将高并发的压力转移到了分布式锁,因此对分布式锁的考验很大.

#### Redis缓存雪崩和解决

缓存雪崩是指,在某一个时间段内,缓存集中过期失效.或者Redis宕机了

产生雪崩的原因之一,比如快到双十二的0点的时候,很快就要进行一波抢购了,这波商品时间比较集中的放到了缓存,加入缓存一个小时,那么到了凌晨一点的时候,这批商品的缓存就都过期了.而对这批商品的访问查询都落到了数据库上,对于数据库而言,就会产生周期性的压力波峰,于是所有请求都会到达存储层,存储层的调用量会暴增,造成存储层也会挂掉的情况.

其实数据集中过期倒不是非常的致命,比较致命的缓存雪崩是由缓存服务器某个节点宕机或者网络断开,因为自然形成的缓存雪崩,一定是在某个时间段集中创建缓存,这个时候,数据库也是可以顶住压力的,无非就是对数据库产生周期性的压力而已,而缓存服务节点的宕机,对数据库服务器造成的压力是不可预知的,很有可能在一瞬间就能把数据库服务器压垮.

解决方案:

* 使用缓存服务器集群,就比如Redis集群.

* 限流.服务降级

  这个解决方案的思想是,在缓存失效后,通过加锁或者队列来控制读数据写缓存的线程数量.比如对某个键只允许一个线程查询数据和写缓存.其他线程等待

* 数据预热

  就是在正式部署前,我先把可能的数据先预先访问一遍,这样部分可能大量访问的数据就会预先加载到缓存中,在即将发生大并发访问前手动触发加载缓存不同的键,设置不同的过期时期,让缓存失效的时间点尽量均匀.

#### Java与Redis(基础API:Jedis使用)

```XML
<!-- https://mvnrepository.com/artifact/redis.clients/jedis -->
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>3.7.0</version>
</dependency>

```

Jedis是Redis官方推荐的一个Java连接工具,它是一个Java操作Redis的中间件,如果要使用Java操作Redis,我们必须对Jedis非常熟悉.

Java操作Redis的操作步骤:

* 导入Redis包

* 连接数据库

  ```Java
  public class Test{
      public static void main(String[] args){
          Jedis jedis = new Jedis("127.0.0.1","6379");//构建一个Jedis对象,也就是连接上Redis数据库.它有很多个构造函数,我们一般也就用这个输入主机号和端口号的来连接.
      }
  }
  ```

  

* 操作数据库

  连接上数据库后,通过jedis对象就可以进行操作数据库了,而Redis命令在jedis这里就是一个个方法,全都是一模一样的.

  Jedis的常用API: 也就是上面的五大基本数据类型与一些其他的数据类型.

  Jedis的事务:

  ```Java
  Transaction multi = jedis.multi();//开启事务
  String c = "c";
  multi.set("a","a");
  multi.set("b","b");
  multi.exec(); //执行事务
  multi.discard();//放弃事务
  jedis.watch(c);//为c设置监控
  ```

  

* 断开数据库

  用jedis.close()方法关闭连接

#### SpringBoot集成Redis

SpringBoot对于数据层的操作,它都集合在spring-data包里面,SpringData是一个与SpringBoot其名的项目.

在SpringData里,有一个SpringData Redis,这个就是用来整合Redis的.我们在查看它的依赖的底层的时候,我们会发现,底层没有Jedis了,而是变成了lettuce了.

也就是spring-boot-starter-data-redis ->spring-data-redis->lettuce

lettuce与jedis的区别

jedis: 底层使用的是直接连接,在并发情况下是不安全的,要避免不安全问题的话,可以使用jedis pool来解决, 但使用池来解决又会有其他问题,比如线程太多怎么办,它属于BIO模式.

lettuce : 底层采用的是netty异步网络请求,它的实例可以在多个线程中进行共享,性能高,并且不存在线程不安全的清空.它属于NIO模式.

在SpringBoot2.0以后,都是lettuce

在SpringBoot中的RedisAutoConfigration中对应的RedisProperties中,我们可以看到外面可以设置的属性.这些东西跟Redis的配置文件相关,后面再看.除此之外,自动配置类还给我们提供了一个模板RedisTemplate,通过它,外面就可以进行对Redis的操作了.我们还会发现有一个StringRedisTemplate,这时因为String类型太常用了,所以弄出来了一个单独的.对于这个RedisTemplate,它甚至没有进行默认配置,只弄了一些最简单的东西;

```Java
public RedisTemplate<Object,Object> redisTemplate(RedisConnectionFactory f) throw unkonwnHostException{
    //传入redis的对象都是需要被序列化的,如果不序列化会导致报错
    //泛型里都是两个Obj,和后面我们需要进行强转,所以我们可以自定义一个RedisTemplate来替换这个默认的.
    //默认的序列化方式是通过JDK序列化的,而我们一般用的是JSON序列化.
    RedisTemplate<Object,Object> template = new RedisTemplate<>();
    template.setConnectionFactory(f);
    return template;
}
```

```Java
//自定义一个RedisTemplate配置类
@Configration
public class RedisConfig{
    @Bean
    public RedisTemplate<String,Object> redisTemplate(RedisConnectionFactory f) throw unkonwnHostException{
    	RedisTemplate<String,Object> template = new RedisTemplate<>();
        //自定义的这个配置主要配的就是我们的序列化方式
        //比如这里用Json序列化
        Jackson2JsonRedisSerializer<Object> jsonSer = new Jackson2JsonRedisSerializer<>();
        template.setKeySerializer(jsonSer);
    	template.setConnectionFactory(f);
    	return template;
    }
}

```

在SpringBoot中操作Redis的步骤:

* 导入依赖

* 配置redis

  在application.properties或者.yaml中用spring.redis开头的配置项进行配置就行了.如果是要配置集群的话,记得用spring.redis.lettuce下的配置项.

* 操作redis

  ```Java
  @Autowired
  private RedisTemplate redis;
  
  @Test
  void contextLoads(){
      //opsForValue是用来操作字符串的,后面跟redis命令对应的方法就完事了
      //同样的,opsForList就是操作列表的,opsForSet就是操作集合的
      //除了这些基本的操作,我们常用的方法可以直接通过redis对象来.方法,比如事务和set,get这些.
      //清空数据库操作(flushdb这样的)要通过连接对象,连接对象要这么拿:RedisConnction rc = redis.getConnectionFactory().getConnection();
      //然后rc.flushdb();
      redis.opsForValue().set("a","a");
  }
  ```

  对于这些操作,我们可以用一个工具类来进行封装,就可以不用写这么一长串了.同时,工具化的思想也非常重要

## ElasticSearch



## RabbitMQ



## Netty

在当下的互联网环境下,分布式系统大行其道,分布式系统的根基就在于网络编程,而Netty是Java领域里网络编程的佼佼者,如果想要开发高性能服务器程序,高性能的客户端程序,就必须学会Netty.

### NIO

Netty的底层实现是基于NIO的,NIO(Non-Blocking IO)非阻塞IO.NIO是JDK1.4中的新特性.它拥有三大组件:

* Channel与Buffer

  Channel类似于Stream,它就算读写数据的双向通道,而流是单向的.完美可以从Channel将数据读入Buffer(缓存),也可以将Buffer中的数据写入Channel,相比于Stream来讲,Channel跟为底层,它的效率也更高.

  常见的Channel:

  * FileChannle
  * DatagramChannel
  * SockertChannel
  * ServerSocketChannel

  常见的Buffer:

  * ByteBuffer(抽象类)
    * MappedByteBuffer
    * DierctByteBuffer
    * HeapByteBuffer
  * ShortBuffer
  * IntBuffer
  * LongBuffer
  * FloatBuffer
  * DoubleBuffer
  * CharBuffer

* Selector

  在NIO出现前,我们可以通过多线程来进行服务器的设计,对于每个用户请求,就把它们做为一个Socket连接,然后开辟一个线程来单独处理,这样的系统缺点很明显:

  * 内存占用高
  * 线程上下文切换时间长,并且吃配置
  * 不适合高并发场景

  还可以使用线程池来进行处理.线程池虽然控制了线程数,但是它的缺点也是很明显的:

  * Socket是工作在阻塞模式下的,一个线程还是只能处理一个Socket连接
  * 只适合短连接,就是干完一个业务马上就断开连接,进而能处理其他的事,早期的Tomcat就是这样的,处理完一个请求就直接断开了,要想继续就得再请求再连,就会很耗时间

  NIO出现后,就可用Selector来进行设计了,Selector的作用是配合一个线程来管理多个Channel,获取到这些Channel上发生的事件,这些Channel工作在非阻塞模式下,不会让线程都只在一个Channel上.模型:

  ![Netty的selector](C:\Users\qj176\Pictures\Saved Pictures\linux\Netty的selector.PNG)

  调用Selector组件的select()会阻塞线程直到Channel发生了读写就绪事件,但发生这些事件的时候,select()就会返回这些事件交给线程来处理.

  使用Selector就可以设计大连接数量,但流量不高的系统.

#### ByteBuffer的使用





























