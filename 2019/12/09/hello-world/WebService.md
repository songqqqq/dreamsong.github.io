### 1. Webservice介绍

#### 概述

​	WebService是一种跨编程语言和跨操作系统平台的远程调用技术。所谓跨编程语言和跨操作平台，就是说服务端程序采用java编写，客户端程序则可以采用其他编程语言编写，反之亦然！跨操作系统平台则是指服务端程序和客户端程序可以在不同的操作系统上运行。 http协议

![1562471828501](E:/新建文件夹/就业班/12.saax-export_day12/assets/1562471828501.png)

#### 应用场景(异构系统  两家公司的系统)

比如： 气象局监测天气变化，做成一个功能提供给外界访问（网址），谁要用这个功能直接调用就可以了。

![1557417300783](E:/新建文件夹/就业班/12.saax-export_day12/assets/1557417300783-1572356695793.png)

#### webservice的三个规范

JAVA 中共有三种WebService 规范，分别是<font color=red>JAX-WS、JAX-RS</font>、JAXM&SAAJ(废弃)。

##### JAX-WS规范

​	JAX-WS 的全称为Java API for XML-Based Webservices ，早期的基于SOAP 的JAVA 的Web 服务规范JAX-RPC(Java API For XML-Remote Procedure Call)目前已经被JAX-WS 规范取代。从java5开始支持JAX-WS2.0版本，Jdk1.6.0_13以后的版本支持2.1版本，jdk1.7支持2.2版本。
​	采用标准SOAP(Simple Object Access Protocol) 协议传输，soap属于w3c标准。Soap协议是基于http的应用层协议，soap协议传输是xml数据。
​	采用wsdl作为描述语言即webservice使用说明书，wsdl属w3c标准。xml是webservice的跨平台的基础，XML主要的优点在于它既与平台无关，又与厂商无关。
​	XSD，W3C为webservice制定了一套传输数据类型，使用xml进行描述，即XSD(XML Schema Datatypes)，任何编程语言写的webservice接口在发送数据时都要转换成webservice标准的XSD发送。

<soap>

<id>1</id>

</soap>

​	<font color=red><b>客户端与服务端通讯： soap协议 = http+ xml</b></font>

#####  JAX-RS规范

​	JAX-RS 是JAVA 针对REST(Representation State Transfer)风格制定的一套Web 服务规范，由于推出的较晚，该规范（JSR 311，目前JAX-RS 的版本为1.0）并未随JDK1.6 一起发行。
支持JAX-RS服务规范的框架有：
​	CXF——XFire和Celtix的合并（一个由IONA赞助的开源ESB，最初寄存在ObjectWeb上）。
​	Jersey——Sun公司的JAX-RS参考实现。
​	RESTEasy——JBoss的JAX-RS项目。
​	Restlet——也许是最早的REST框架了，它JAX-RS之前就有了。
​	注：REST 是一种软件架构模式，只是一种风格，rest服务采用HTTP 做传输协议。



​	<font color=red><b>客户端与服务端通讯： http协议 </b></font>+ XML/JSON

##### JAXM&SAAJ规范

​	JAXM（JAVAAPI For XML Message）主要定义了包含了发送和接收消息所需的API，相当于Web 服务的服务器端，其API 位于javax.messaging.*包，它是JAVA EE 的可选包，因此你需要单独下载。SAAJ（SOAP WithAttachment API For Java，JSR67）是与JAXM 搭配使用的API，为构建SOAP 包和解析SOAP 包提供了重要的支持，支持附件传输，它在服务器端、客户端都需要使用。这里还要提到的是SAAJ 规范，其API 位于javax.xml.soap包。

#### 小结&补充

> webservice 也叫作web服务。是java1.5以后推出的 。跨平台跨语言的远程调用技术。

> webservice技术，客户端与服务端进行通讯使用的协议是soap协议。如果是基于restful风格的webservice，使用http协议。

> 其他远程调用的解决方案：（补充了解）

<font color=green>第一：使用Socket远程通信</font>

![image](E:/新建文件夹/就业班/12.saax-export_day12/assets/clip_image002-1572356695793.png)

<font color=green>第二：HttpClient</font>

​	HttpClient是Apache Jakarta Common下的子项目，用来提供高效的、最新的、功能丰富的支持HTTP协议的客户端编程工具包，并且它支持HTTP协议最新的版本和建议。HttpClient已经应用在很多的项目中，比如Apache Jakarta上很著名的另外两个开源项目Cactus和HTMLUnit都使用了HttpClient。

​	下载地址: <http://hc.apache.org/downloads.cgi>

​	官网：http://hc.apache.org/httpclient-3.x

<font color=green>第三：RMI(Remote Method Invoke)</font>

​	RMI（即Remote Method Invoke 远程方法调用）。在Java中，只要一个类extends了java.rmi.Remote接口，即可成为存在于服务器端的远程对象，供客户端访问并提供一定的服务。JavaDoc描述：Remote 接口用于标识其方法可以从非本地虚拟机上调用的接口。任何远程对象都必须直接或间接实现此接口。只有在“远程接口”（扩展 java.rmi.Remote 的接口）中指定的这些方法才可远程使用。 
​	注意：extends了Remote接口的类或者其他接口中的方法若是声明抛出了RemoteException异常，则表明该方法可被客户端远程访问调用。 
​	同时，远程对象必须实现java.rmi.server.UniCastRemoteObject类，这样才能保证客户端访问获得远程对象时，该远程对象将会把自身的一个拷贝以Socket的形式传输给客户端，此时客户端所获得的这个拷贝称为“存根”，而服务器端本身已存在的远程对象则称之为“骨架”。其实此时的存根是客户端的一个代理，用于与服务器端的通信，而骨架也可认为是服务器端的一个代理，用于接收客户端的请求之后调用远程方法来响应客户端的请求。



### 2. Apache的CXF框架

#### 什么是CXF?

​	Apache CXF = Celtix + Xfire，开始叫 Apache CeltiXfire，后来更名为 Apache CXF 了，以下简称为 CXF。Apache CXF 是一个开源的 web Services 框架，CXF 帮助您构建和开发 web Services ，它支持多种协议，比如：SOAP1.1,1,2 XML/HTTP、RESTful 或者CORBA。
​	RESTful: 一种风格而不是一个协议。它理念是网络上的所有事物都被抽象为资源，每个资源对应一个唯一的资源标识符。
​	Cxf是基于SOA总线结构，依靠spring完成模块的集成，实现SOA方式。灵活的部署: 可以运行在Tomcat,Jboss,Jetty(内置),weblogic上面。

#### 官方网址

http://cxf.apache.org

![1557418085347](E:/新建文件夹/就业班/12.saax-export_day12/assets/1557418085347-1572356695794.png)

#### 小结

简单来说，webservice是一套规范，在jdk1.5以后提供规范支持。ApacheCXF是这套规范的实现，可以简化开发。



### 3. JAX-RS 进行webservice开发（一）概述

#### 概述

> jax-rs规范，就是基于restful风格的webservice开发支持。全程：Java API for XML-Based Rest

> JAX-RS是一个Java编程语言接口，被设计用来简化使用REST架构的应用程序的开发。  

>  JAX-RS API使用Java编程语言的注解来简化RESTful web service的开发。

​	开发人员使用JAX-RS的注解修饰Java编程语言的类文件来定义资源和能够应用在资源上的行为。JAX-RS的注解是运行时的注解，因此运行时的映射会为资源生成辅助类和其他的辅助文件。包含JAX-RS资源类的Java EE应用程序中资源是被配置好的，辅助类和辅助文件是生成的，资源通过被发布到JavaEE服务器上来公开给客户端。


> 下表列出了JAX-RS定义的一些Java注解以及怎样使用它们的简要的描述。

| **注解**    | **描述**                                                     |
| ----------- | ------------------------------------------------------------ |
| @Path       | @Path注解的值是一个相对的URI路径，这个路径指定了该Java类的位置，例如/helloworld。在这个URI中可以包含变量，例如可以获取用户的姓名然后作为参数传入URI中：/helloworld/{username}。 |
| @GET        | @GET注解是请求方法指示符，这个指示符注解的Java方法会处理HTTPGET请求。资源的行为由资源回应的HTTP方法决定。 |
| @POST       | @POST注解是请求方法指示符，这个指示符注解的Java方法会处理HTTPPOST请求。资源的行为由资源回应的HTTP方法决定。 |
| @PUT        | @PUT注解是请求方法指示符，这个指示符注解的Java方法会处理HTTPPUT请求。资源的行为由资源回应的HTTP方法决定。 |
| @DELETE     | @DELETE注解是请求方法指示符，这个指示符注解的Java方法会处理HTTPDELETE请求。资源的行为由资源回应的HTTP方法决定。 |
| @HEAD       | @HEAD注解是请求方法指示符，这个指示符注解的Java方法会处理HTTPHEAD请求。资源的行为由资源回应的HTTP方法决定。 |
| @PathParam  | @PathParam注解是可以抽取并用在资源类中的一类参数。URIpath参数是从请求的URI中抽取的，而且参数的名称和@Path注解中定义的变量名对应。 |
| @QueryParam | @QueryParam注解是可以抽取并在资源类中使用的一类参数。Query参数是从请求URI的查询参数中抽取的。 |
| @Consumes   | @Consumes注解是用来指定资源能够接受的客户发送的MIME媒体类型。 |
| @Produces   | @Produces注解用来指定资源能够生成并发送给客户端的MIME媒体类型，例如“text/plain”. |
| @Provider   | @Provider注解用在任何对JAX-RS运行时（如MessageBodyReader和MessageBodyWriter）有意义的事物上。对HTTP请求，MessageBodyReader用来将HTTP请求实体段映射为方法参数。在响应的时候，返回的值使用MessageBodyWriter来映射成HTTP响应实体段。如果应用程序需要提供其他的元数据，如HTTP头或不同的状态代码，方法可以返回一个打包了实体的Response，该Response可以使用Response.ResponseBuilder创建。 |

#### 小结

什么是jax-rs规范？



### 4. JAX-RS 进行webservice开发（二）创建服务端项目

#### 目标

创建服务端项目，发布服务

#### 步骤

1. 创建项目：jaxrs_server
2. 添加依赖
3. 引入实体类
4. 引入service接口、实现
5. 启动服务

#### 实现

1. 创建项目：jaxrs_server

   &nbsp;![1557422396101](E:/新建文件夹/就业班/12.saax-export_day12/assets/1557422396101-1572356695794.png)

2. 添加依赖

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <project xmlns="http://maven.apache.org/POM/4.0.0"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
       <modelVersion>4.0.0</modelVersion>
   
       <groupId>cn.itcast</groupId>
       <artifactId>jaxrs_server</artifactId>
       <version>1.0-SNAPSHOT</version>
   
       <dependencies>
           <dependency>
               <groupId>org.apache.cxf</groupId>
               <artifactId>cxf-rt-frontend-jaxrs</artifactId>
               <version>3.0.1</version>
           </dependency>
   
           <dependency>
               <groupId>org.apache.cxf</groupId>
               <artifactId>cxf-rt-transports-http-jetty</artifactId>
               <version>3.0.1</version>
           </dependency>
   
           <dependency>
               <groupId>org.slf4j</groupId>
               <artifactId>slf4j-log4j12</artifactId>
               <version>1.7.12</version>
           </dependency>
   
           <dependency>
               <groupId>org.apache.cxf</groupId>
               <artifactId>cxf-rt-rs-client</artifactId>
               <version>3.0.1</version>
           </dependency>
   
           <dependency>
               <groupId>org.apache.cxf</groupId>
               <artifactId>cxf-rt-rs-extension-providers</artifactId>
               <version>3.0.1</version>
           </dependency>
           <dependency>
               <groupId>org.codehaus.jettison</groupId>
               <artifactId>jettison</artifactId>
               <version>1.3.7</version>
           </dependency>
           <dependency>
               <groupId>junit</groupId>
               <artifactId>junit</artifactId>
               <version>4.12</version>
               <scope>test</scope>
           </dependency>
       </dependencies>
   </project>
   ```

3. 引入实体类

   &nbsp;![1557422423479](E:/新建文件夹/就业班/12.saax-export_day12/assets/1557422423479-1572356695794.png)

在实体上必须加上注解

![1568954729104](E:/新建文件夹/就业班/12.saax-export_day12/assets/1568954729104.png)



4. 引入service接口、实现

   ![1557422619314](E:/新建文件夹/就业班/12.saax-export_day12/assets/1557422619314-1572356695794.png)

```java
package cn.itcast.service;

import java.util.List;

import cn.itcast.domain.User;

import javax.ws.rs.*;

@Path("/userService") // 定义访问路径
public interface IUserService {

	@POST  // 代表该方法只能接受Post请求
	@Consumes({"application/xml","application/json"})  // 定义服务端接收客户端的数据格式: xml/json
	public void saveUser(User user);

	@PUT
	@Consumes({"application/xml","application/json"})
	public void updateUser(User user);

	//客户端：/userService
	@GET
	@Produces("application/xml")   // 定义服务器把对象转换为什么数据格式
	public List<User> findAllUsers();

	//客户端： /userService/10
	@GET
	@Path("/{id}") // 定义路径的参数
	@Produces("application/xml")
	public User finUserById( @PathParam("id") Integer id);  // @PathParam("id"):接收路径传递的参数

	@DELETE
	@Path("/{id}")
	public void deleteUser(@PathParam("id") Integer id);
}


```



5. 启动服务

   ![1557422641157](E:/新建文件夹/就业班/12.saax-export_day12/assets/1557422641157-1572356695794.png)

   ```java
   package cn.itcast.server;
   
   import cn.itcast.service.IUserService;
   import cn.itcast.service.UserServiceImpl;
   import org.apache.cxf.interceptor.LoggingInInterceptor;
   import org.apache.cxf.interceptor.LoggingOutInterceptor;
   import org.apache.cxf.jaxrs.JAXRSServerFactoryBean;
   
   /**
    * 启动WebService的服务端
    */
   public class ServerDemo {
   
       public static void main(String[] args) {
           //1.创建工厂
           JAXRSServerFactoryBean factory = new JAXRSServerFactoryBean();
   
           //2.设置访问路径
           factory.setAddress("http://localhost:8888");
   
           //3.设置服务实现
           //factory.setServiceClass(IUserService.class); 通常省略的
           factory.setServiceBean(new UserServiceImpl());
   
           //4.加入log4j日志查看拦截器，方便查看日志
           factory.getInInterceptors().add(new LoggingInInterceptor()); // LoggingInInterceptor: 查看进入服务端的请求日志
           factory.getOutInterceptors().add(new LoggingOutInterceptor());//LoggingOutInterceptor: 查看服务端的响应的日志
           
           //5.启动
           factory.create();
   
           System.out.println("服务端已经启动成功...");
       }
   
   }
   
   
   ```

#### 测试

现在只做简单的访问测试，后面写完客户端再做最终测试：

![1557425353018](E:/新建文件夹/就业班/12.saax-export_day12/assets/1557425353018-1572356695794.png)



### 5. JAX-RS 进行webservice开发（三）创建客户端项目

#### 目标

创建客户端项目，调用服务端发布的服务。

#### 步骤

1. 创建项目: jaxrs_client
2. 添加依赖（同服务端项目）
3. 编写实体类（同服务端项目）
4. 编写测试类

#### 实现

1. 创建项目: jaxrs_client

2. 添加依赖（同服务端项目）

3. 编写实体类（同服务端项目）

   &nbsp;![1557426179679](E:/新建文件夹/就业班/12.saax-export_day12/assets/1557426179679-1572356695794.png)

4. 编写测试类

   &nbsp;![1557426098323](E:/新建文件夹/就业班/12.saax-export_day12/assets/1557426098323-1572356695794.png)

   ```java
   package cn.itcast.client;
   
   import cn.itcast.domain.User;
   import org.apache.cxf.jaxrs.client.WebClient;
   import org.junit.Test;
   
   import java.util.List;
   
   /**
    * 演示WebService的客户端请求
    */
   public class ClientDemo {
   
       //测试查询所有用户
       @Test
       public void testFindAllUser(){
           /**
            * create: 传入需要请求的地址
            * accept: 客户端接收服务端的数据格式
            * getCollection(User.class):  发出get请求，把请求返回的数据转换为User对象（支持n个）
            */
           List<User> list = (List<User>)WebClient.create("http://localhost:8888/userService")
                     .accept("application/json")
                     .getCollection(User.class);
   
           for(User u:list){
               System.out.println(u);
           }
       }
   
       //测试查询一个用户
       @Test
       public void testFindById(){
           /**
            * create: 传入需要请求的地址
            * accept: 客户端接收服务端的数据格式
            * get(User.class):  发出get请求，把请求返回的数据转换为User对象（支持1个）
            */
          User user = WebClient.create("http://localhost:8888/userService/1")
                   .accept("application/xml")
                   .get(User.class);
   
          System.out.println(user);
   
       }
   
       //测试增加一个用户
       @Test
       public void testSaveUser(){
           /**
            * create: 传入需要请求的地址
            * type: 客户端传递什么数据格式到服务端
            * get(User.class):  发出get请求，把请求返回的数据转换为User对象（支持1个）
            */
           User user = new User();
           user.setId(100);
           user.setUsername("小苍");
           user.setCity("广州吉山9巷");
   
          WebClient.create("http://localhost:8888/userService")
                   .type("application/json")
                   .post(user);
   
   
       }
   
       //测试更新一个用户
       @Test
       public void testUpdateUser(){
           /**
            * create: 传入需要请求的地址
            * type: 客户端传递什么数据格式到服务端
            * put(User.class):  发出put请求，把参数转换为json格式
            */
           User user = new User();
           user.setId(101);
           user.setUsername("小苍");
           user.setCity("广州吉山9巷");
   
           WebClient.create("http://localhost:8888/userService")
                   .type("application/json")
                   .put(user);
   
   
       }
   
       //测试删除一个用户
       @Test
       public void testDeleteUser(){
           /**
            * create: 传入需要请求的地址
            * type: 客户端传递什么数据格式到服务端
            * delete():  发出put请求，把参数转换为json格式
            */
           WebClient.create("http://localhost:8888/userService/1")
                   .delete();
   
   
       }
   }
   
   
   ```



### 6. Spring整合CXF发布服务

#### 目标

实现Spring整合CXF发布服务。

#### 步骤

1. 创建web项目：springcxf_server
2. 添加依赖
3. 引入实体类
4. 引入服务接口、实现
5. 配置web.xml
6. 配置applicationContext-cxf.xml
7. 启动项目，发布服务

#### 实现

1. 创建web项目：springcxf_server

   &nbsp;![1557426357349](E:/新建文件夹/就业班/12.saax-export_day12/assets/1557426357349-1569027821724.png)

2. 添加依赖

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   
   <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">  
     <modelVersion>4.0.0</modelVersion>  
     <groupId>cn.itcast</groupId>  
     <artifactId>springcxf_server</artifactId>  
     <version>1.0-SNAPSHOT</version>
     <packaging>war</packaging>
     <dependencies>
       <!-- cxf 进行rs开发 必须导入  -->
       <dependency>
         <groupId>org.apache.cxf</groupId>
         <artifactId>cxf-rt-frontend-jaxrs</artifactId>
         <version>3.0.1</version>
       </dependency>
       <!-- 日志引入  -->
       <dependency>
         <groupId>org.slf4j</groupId>
         <artifactId>slf4j-log4j12</artifactId>
         <version>1.7.12</version>
       </dependency>
   
       <!-- 客户端 -->
       <dependency>
         <groupId>org.apache.cxf</groupId>
         <artifactId>cxf-rt-rs-client</artifactId>
         <version>3.0.1</version>
       </dependency>
   
       <!-- 扩展json提供者 -->
       <dependency>
         <groupId>org.apache.cxf</groupId>
         <artifactId>cxf-rt-rs-extension-providers</artifactId>
         <version>3.0.1</version>
       </dependency>
   
       <!-- 转换json工具包，被extension providers 依赖 -->
       <dependency>
         <groupId>org.codehaus.jettison</groupId>
         <artifactId>jettison</artifactId>
         <version>1.3.7</version>
       </dependency>
   
       <!-- spring 核心 -->
       <dependency>
         <groupId>org.springframework</groupId>
         <artifactId>spring-context</artifactId>
         <version>4.2.4.RELEASE</version>
       </dependency>
       <!-- spring web集成 -->
       <dependency>
         <groupId>org.springframework</groupId>
         <artifactId>spring-web</artifactId>
         <version>4.2.4.RELEASE</version>
       </dependency>
       <!-- spring 整合junit  -->
       <dependency>
         <groupId>org.springframework</groupId>
         <artifactId>spring-test</artifactId>
         <version>4.2.4.RELEASE</version>
       </dependency>
       <!-- junit 开发包 -->
       <dependency>
         <groupId>junit</groupId>
         <artifactId>junit</artifactId>
         <version>4.12</version>
       </dependency>
     </dependencies>
   </project>
   ```

3. 引入实体类

   &nbsp;![1557426491678](E:/新建文件夹/就业班/12.saax-export_day12/assets/1557426491678-1569027821725.png)

4. 引入服务接口、实现

   ![1557426537795](E:/新建文件夹/就业班/12.saax-export_day12/assets/1557426537795-1569027821725.png)

5. 配置web.xml

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   	xmlns="http://java.sun.com/xml/ns/javaee"
   	xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"
   	version="2.5">
   
   	<!--读取cxf的配置-->
   	<context-param>
   		<param-name>contextConfigLocation</param-name>
   		<param-value>classpath:applicationContext-cxf.xml</param-value>
   	</context-param>
   	<listener>
   		<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
   	</listener>
   
   	<!--***CXF的启动配置***-->
   	<servlet>
   		<servlet-name>cxfServlet</servlet-name>
   		<servlet-class>org.apache.cxf.transport.servlet.CXFServlet</servlet-class>
   		<load-on-startup>1</load-on-startup>
   	</servlet>
   	<servlet-mapping>
   		<servlet-name>cxfServlet</servlet-name>
   		<!--/ws/* : 这里使用ws前缀访问，避免和springmvc获取项目的其他框架的路径冲突-->
   		<url-pattern>/ws/*</url-pattern>
   	</servlet-mapping>
   
   </web-app>
   ```

6. 配置applicationContext-cxf.xml

   ![1557426824323](E:/新建文件夹/就业班/12.saax-export_day12/assets/1557426824323-1569027821725.png)

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:jaxrs="http://cxf.apache.org/jaxrs"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
   
          http://cxf.apache.org/jaxrs http://cxf.apache.org/schemas/jaxrs.xsd">
          <!--http://cxf.apache.org/jaxrs http://cxf.apache.org/schemas/jaxrs-common.xsd">-->
          <!--注意：默认工具生成的是jaxrs-common.xsd，改为jaxrs.xsd-->
   
   
       <!--使用配置方式发布服务-->
       <jaxrs:server address="/userService" serviceClass="cn.itcast.service.UserServiceImpl">
           <!--加入日志-->
           <jaxrs:inInterceptors>
               <bean class="org.apache.cxf.interceptor.LoggingInInterceptor"/>
           </jaxrs:inInterceptors>
           <jaxrs:outInterceptors>
               <bean class="org.apache.cxf.interceptor.LoggingOutInterceptor"/>
           </jaxrs:outInterceptors>
       </jaxrs:server>
   
   </beans>
   ```

7. 启动项目，发布服务

   ![1557428147887](E:/新建文件夹/就业班/12.saax-export_day12/assets/1557428147887-1569027821725.png)



#### 测试

   还是使用之前的jaxrs_client项目，进行测试：

   图1：

   ![1557428171822](E:/新建文件夹/就业班/12.saax-export_day12/assets/1557428171822-1569027821725.png)

   图2：

```java
 package cn.itcast.service;

import cn.itcast.domain.User;
import org.apache.cxf.jaxrs.client.WebClient;
import org.junit.Test;

import javax.ws.rs.core.MediaType;
import java.util.List;

/**
 * 演示WebService客户端编写
 */
public class WebServiceClient {


    /**
     * 发布查询所有数据的请求
     */
    @Test
    public void testFindAllUsers(){
        List<User> userList = (List<User>)WebClient
                .create("http://127.0.0.1:8082/ws/userService/user")
                .accept(MediaType.APPLICATION_JSON)  //接收服务端返回XML格式
                .getCollection(User.class); // getCollection发布get请求，返回List集合

        System.out.println(userList);


    }

    /**
     * 发布查询一个数据的请求
     */
    @Test
    public void testFindById(){
       User user = WebClient
                .create("http://127.0.0.1:8082/ws/userService/user/1")
                .accept(MediaType.APPLICATION_XML)  //接收服务端返回XML格式
                .get(User.class); // getCollection发布get请求，返回List集合

        System.out.println(user);


    }

    /**
     * 发布添加数据的请求
     */
    @Test
    public void testSaveUser(){
        User user = new User();
        user.setId(666);
        user.setUsername("小苍");

       WebClient
                .create("http://127.0.0.1:8082/ws/userService/user")
                .type(MediaType.APPLICATION_XML)  //发送的数据类型为XML
                .post(user); // getCollection发布get请求，返回List集合



    }
}

```

