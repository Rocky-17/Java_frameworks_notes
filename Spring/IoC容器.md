# IoC容器  

[toc]

## IoC容器以及Beans  

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

## 容器  
