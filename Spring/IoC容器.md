# 1. IoC容器  

1.1 [IoC容器以及Beans](https://github.com/Rocky-17/Java_frameworks_notes/blob/master/Spring/IoC%E5%AE%B9%E5%99%A8.md#ioc%E5%AE%B9%E5%99%A8%E4%BB%A5%E5%8F%8Abeans)  
1.2 [容器](https://github.com/Rocky-17/Java_frameworks_notes/blob/master/Spring/IoC%E5%AE%B9%E5%99%A8.md#%E5%AE%B9%E5%99%A8)  
&emsp;1.2.1 [配置元数据](https://github.com/Rocky-17/Java_frameworks_notes/blob/master/Spring/IoC%E5%AE%B9%E5%99%A8.md#121-%E9%85%8D%E7%BD%AE%E5%85%83%E6%95%B0%E6%8D%AE)  
&emsp;1.2.2 [实例化一个容器](https://github.com/Rocky-17/Java_frameworks_notes/blob/master/Spring/IoC%E5%AE%B9%E5%99%A8.md#122-%E5%AE%9E%E4%BE%8B%E5%8C%96%E4%B8%80%E4%B8%AA%E5%AE%B9%E5%99%A8)  
&emsp;&emsp;1.2.2.1. [构建基于XML的配置元数据](https://github.com/Rocky-17/Java_frameworks_notes/blob/master/Spring/IoC%E5%AE%B9%E5%99%A8.md#1221-%E6%9E%84%E5%BB%BA%E5%9F%BA%E4%BA%8Exml%E7%9A%84%E9%85%8D%E7%BD%AE%E5%85%83%E6%95%B0%E6%8D%AE)


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
![The Spring IoC container](https://docs.spring.io/spring/docs/current/spring-framework-reference/images/container-magic.png)  

### 1.2.1. 配置元数据  

&emsp;&emsp;通过配置元数据来告诉容器需要实例化、配置和组装哪些对象。由于XML的元数据不是配置元数据的唯一允许形式，因此Spring IoC容器与实际写入配置元数据的格式无关。现在许多开发人员为他们的Spring应用程序选择基于Java的配置。  

&emsp;&emsp;以下示例展示一个基于XML的配置元数据的基本结构：  
```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="..." class="...">  
        <!-- collaborators and configuration for this bean go here -->
    </bean>

    <bean id="..." class="...">
        <!-- collaborators and configuration for this bean go here -->
    </bean>

    <!-- more bean definitions go here -->

</beans>
```

### 1.2.2. 实例化一个容器  

&emsp;&emsp;提供给`ApplicationContext`构造函数的位置路径是资源字符串，这些资源字符串使容器可以从各种外部资源（例如本地文件系统，Java CLASSPATH等）加载配置元数据。  
```
ApplicationContext context = new ClassPathXmlApplicationContext("services.xml", "daos.xml");
```  
&emsp;&emsp;以下示例展示一个服务层对象（services.xml）配置文件：  
```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- services -->

    <bean id="petStore" class="org.springframework.samples.jpetstore.services.PetStoreServiceImpl">
        <property name="accountDao" ref="accountDao"/>
        <property name="itemDao" ref="itemDao"/>
        <!-- additional collaborators and configuration for this bean go here -->
    </bean>

    <!-- more bean definitions for services go here -->

</beans>
```  
&emsp;&emsp;以下示例展示一个数据访问对象daos.xml文件：  
```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="accountDao"
        class="org.springframework.samples.jpetstore.dao.jpa.JpaAccountDao">
        <!-- additional collaborators and configuration for this bean go here -->
    </bean>

    <bean id="itemDao" class="org.springframework.samples.jpetstore.dao.jpa.JpaItemDao">
        <!-- additional collaborators and configuration for this bean go here -->
    </bean>

    <!-- more bean definitions for data access objects go here -->

</beans>
```
&emsp;&emsp;在前面的示例中，服务层由`PetStoreServiceImpl`类和两个类型为`JpaAccountDao`和`JpaItemDao`的数据访问对象组成（基于JPA对象关系映射标准）。属性名称元素引用JavaBean属性的名称，而ref元素引用另一个bean定义的名称。`id`和`ref`元素之间的这种联系表达了协作对象之间的依赖性。  


#### 1.2.2.1. 构建基于XML的配置元数据  
&emsp;&emsp;通常，每个单独的XML配置文件都代表体系结构中的一个逻辑层或模块。让bean定义能够跨越多个XML配置文件会很有用。

&emsp;&emsp;你可以使用application context构造函数从所有这些XML片段中加载bean定义。如上一节中所示，此构造函数具有多个Resource位置。或者，使用`<import />`元素从其他文件中加载bean定义。以下示例显示了如何执行此操作：  
```
<beans>
    <import resource="services.xml"/>
    <import resource="resources/messageSource.xml"/>
    <import resource="/resources/themeSource.xml"/>

    <bean id="bean1" class="..."/>
    <bean id="bean2" class="..."/>
</beans>
```
&emsp;&emsp;*在前面的示例中，外部 bean定义是从三个文件加载的：services.xml，messageSource.xml和 themeSource.xml。所有位置路径都相对于进行导入的XML文件，因此，services.xml必须与进行导入的文件位于同一目录或类路径位置，而 messageSource.xml和 themeSource.xml必须位于该位置下方的资源位置。如您所见，在导入文件时斜杠被忽略。但是，鉴于这些路径是相对的，所以最好不要使用任何斜线。根据 Spring Schema，导入的文件的内容（包括最高层级的`<beans />`元素）必须是有效的 XML bean定义。*  
>&emsp;&emsp;可以但不建议使用相对的“ ../”路径引用父目录中的文件。这样做会造成对当前应用程序外部文件的依赖。特别是不建议对classpath：URL（例如：classpath：../ services.xml），在URL中使用此引用，运行时解析过程会选择最近的classpath根目录，然后查看其父目录。类路径配置的更改可能导致选择其他错误的目录。  
&emsp;&emsp;你始终可以使用绝对路径来代替相对路径：例如：`file:C:/config/services.xml`以及`classpath:/config/services.xml`。 但是请注意，你正将应用程序的配置耦合到一个绝对路径。通常，最好为这样的绝对路径保留一个间接寻址，例如通过在运行时针对JVM系统属性解析的“ $ {…}”占位符。  

### 1.2.3. 使用这个容器  
&emsp;&emsp;`ApplicationContext`是高级工厂的接口，该工厂能够维护不同bean及其依赖关系的注册表。通过使用方法`T getBean(String name，Class <T> requiredType)`，可以检索bean的实例。  

&emsp;&emsp;使用ApplicationContext可以读取bean定义并访问它们，如以下示例所示：
```
// create and configure beans
ApplicationContext context = new ClassPathXmlApplicationContext("services.xml", "daos.xml");

// retrieve configured instance
PetStoreService service = context.getBean("petStore", PetStoreService.class);

// use configured instance
List<String> userList = service.getUsernameList();
```