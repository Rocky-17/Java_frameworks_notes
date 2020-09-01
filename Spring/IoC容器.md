# 1. IoC容器  

1.1[IoC容器以及Beans](https://github.com/Rocky-17/Java_frameworks_notes/blob/master/Spring/IoC%E5%AE%B9%E5%99%A8.md#ioc%E5%AE%B9%E5%99%A8%E4%BB%A5%E5%8F%8Abeans)  
1.2[容器](https://github.com/Rocky-17/Java_frameworks_notes/blob/master/Spring/IoC%E5%AE%B9%E5%99%A8.md#%E5%AE%B9%E5%99%A8)


## 1.1. IoC容器以及Beans  

&emsp;&emsp;IoC也称依赖注入(DI)，是面向对象中的一种编程原则，用来减少代码间的耦合度。在此过程中，对象仅通过构造函数参数，工厂方法的参数或在从工厂方法返回后在对象实例上设置的属性来定义其依赖项（即与它们一起使用的其他对象）。容器在创建bean时注入那些依赖项，此过程是通过使用类的直接构造或诸如服务定位器模式之类的机制来控制其依赖项的实例化的过程。从根本上讲，此过程是控制实例化的bean本身的逆过程（因此称为Inversion of Control,IoC）。  

&emsp;&emsp;`org.springframework.beans`与`org.springframework.context`包是Spring框架的IoC容器的基础。  
&emsp;&emsp;[BeanFactory](https://docs.spring.io/spring-framework/docs/5.2.8.RELEASE/javadoc-api/org/springframework/beans/factory/BeanFactory.html)接口提供了一种高级配置机制，能够管理任何类型的对象。  
&emsp;&emsp;[ApplicationContext](https://docs.spring.io/spring-framework/docs/5.2.8.RELEASE/javadoc-api/org/springframework/context/ApplicationContext.html)是BeanFactory的子接口，它提供了诸如：  
&emsp;&emsp;1.更容易与Spring的AOP特性集成  
&emsp;&emsp;2.国际化消息资源处理  
&emsp;&emsp;3.事件发布  
&emsp;&emsp;4.应用层特定的上下文，例如Web应用程序中使用的`WebApplicationContext`。  
  
&emsp;&emsp;简而言之，BeanFactory提供了配置框架和基本功能，而ApplicationContext添加了更多企业特定的功能。  

&emsp;&emsp;在Spring中，构成应用程序主干并由Spring IoC容器管理的对象称为Bean。Bean是由Spring IoC容器实例化，组装和以其他方式管理的对象。  

## 1.2. 容器  
&emsp;&emsp;`org.springframework.context.ApplicationContext`接口代表Spring IoC容器，它负责实例化、配置和组装Beans。容器通过读取配置元数据来获取有关要实例化、配置和组装哪些对象的指令。配置元数据可以是XML文件、Java注解或Java代码。它能够展示应用程序由哪些对象组成以及这些对象之间丰富的相互依赖关系。  

&emsp;&emsp;Spring提供了`ApplicationContext`接口的几种实现。 在独立应用程序中，通常创建`ClassPathXmlApplicationContext`或`FileSystemXmlApplicationContext`的实例。尽管XML是传统的定义配置元数据的方法，但是你可以通过配置少量XML来声明性地启用对其他元数据格式的支持，从而指示容器将Java注解或代码用作元数据。  

&emsp;&emsp;下图展示了Spring的工作原理：你的应用程序类与配置元数据结合在一起，在创建和初始化`ApplicationContext`之后，你会得到一个配置好的、可执行的系统或应用程序。  
![](https://docs.spring.io/spring/docs/current/spring-framework-reference/images/container-magic.png)