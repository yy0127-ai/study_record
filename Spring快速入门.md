# Spring快速入门

### 一、Spring开发步骤

#### 1.导入Spring依赖（导入坐标）

```xml
<dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>5.0.7.RELEASE</version>
</dependency>
```

#### 2.创建Bean(创建UserDao和实现类UserDaoImpl)

```java
public interface UserDao {
    public void save();
}
```

```java
public class UserDaoImpl implements UserDao {
    public void save() {
      System.out.println("save running");
    }
}
```

#### 3.创建applicationContext.xml

```xml
<bean id="userDao" class="com.yyue.impl.UserDaoImpl"></bean>
```

#### 4.在配置文件中进行配置

#### 5.创建ApplicationContext对象getBean

客户端代码

```java
public static void main(String[] args) {
    ApplicationContext app = new ClassPathXmlApplicationContext("applicationContext.xml");
    UserDao userDao = (UserDao) app.getBean("userDao");
    userDao.save();
}
```

### 二、Spring配置文件

#### 1.Bean标签范围配置

scope:指对象的作用范围

##### 1.1测试scope="singleton"

```xml
<bean id="userDao" class="com.yyue.impl.UserDaoImpl" scope="singleton"></bean>
```

测试代码

```java
public void test1(){
    ApplicationContext app = new ClassPathXmlApplicationContext("applicationContext.xml");
    UserDao userDao = (UserDao) app.getBean("userDao");
    UserDao userDao1 = (UserDao) app.getBean("userDao");
    System.out.println(userDao);
    System.out.println(userDao1);
}
```

结果

```
com.yyue.impl.UserDaoImpl@1d8d30f7
com.yyue.impl.UserDaoImpl@1d8d30f7
```

##### 1.2测试scope="prototype"

```xml
<bean id="userDao" class="com.yyue.impl.UserDaoImpl" scope="prototype"></bean>
```

测试结果

```
com.yyue.impl.UserDaoImpl@c46bcd4
com.yyue.impl.UserDaoImpl@3234e239
```

#### 2.Bean标签范围配置

##### 2.1.1当scope的取值为singleton时

Bean的实例化个数：1个

Bean的实例化时机：当Spring核心文件被加载时，实例化配置Bean实例

Bean的生命周期：

- 对象创建：当应用加载，创建容器时，对象就被创建了
- 对象运行：只要容器在，对象一直活着
- 对象销毁：当应用卸载，销毁容器时，对象就被销毁了。

##### 2.1.2当scope的取值为prototype时

Bean的实例化个数：多个

Bean的实例化时机：当调用getBean()方法时实例化Bean

- 对象创建：当使用对象时，创建新的对象实例
- 对象运行：只要对象在使用中，就一直活着
- 对象销毁：当对象长时间不用时，被java的垃圾回收器回收

#### 3.Bean生命周期配置

init-method：指定类中的初始化方法名称

destroy-method：指定类中销毁方法名称

#### 4.Bean实例化三种方式

- 无参构造方法实例化

  配置文件（找UserDaoImpl的无参构造）

  ```xml
  <bean id="userDao" class="com.yyue.impl.UserDaoImpl"></bean>
  ```

- 工厂静态方法实例化

  测试静态方法

  创建一个工厂类

  ```java
  public class staticFactory {
  public static UserDao getUserDao(){
      return new UserDaoImpl();
  }
  }
  ```

  编写配置文件(找staticFactory的无参构造，但是后面指定了找getUserDao这个方法)

  ```xml
  <bean id="userDao" class="com.yyue.factory.staticFactory" factory-method="getUserDao"></bean>
  ```

- 工厂实例方法实例化

  ```xml
  <bean id="factory" class="com.yyue.factory.DynamicFactory"></bean>
  <bean id="userDao" factory-bean="factory" factory-method="getUserDao"></bean>
  ```

  

#### 5.Bean的依赖注入方式

怎么将UserDao注入到UserService内部

##### 5.1构造方法

在UserService中添加构造方法将UserDao传入

```java
public UserServiceImpl(UserDao userDao){//构造函数
    this.userDao=userDao;
}
public UserServiceImpl() {
}
```

配置文件中配置(此name是service构造函数的参数名)

```xml
<bean id="userService" class="com.yyue.impl.UserServiceImpl">
        <constructor-arg name="userDao" ref="userDao"></constructor-arg>
    </bean>
```

如下图所示

![image-20201122211512131](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20201122211512131.png)

##### 5.2set方法

- 在UserServiceImpl中添加一个set方法将UserDao注入

```java
public class UserServiceImpl implements UserService {
    private UserDao userDao;
    public void setUserDao(UserDao userDao){
        this.userDao = userDao;
    }
    public void save() {
        userDao.save();
    }
}
```

在配置文件中配置（此name是对应service的属性名    ref是引用容器中bean的id名）

```xml
<bean id="userDao" class="com.yyue.impl.UserDaoImpl"></bean>
<bean id="userService" class="com.yyue.impl.UserServiceImpl">
    <property name="userDao" ref="userDao"></property>
</bean>
```

![image-20201122203845768](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20201122203845768.png)

- p命名空间注入本质也是set方法注入，但比起上述的set方法注入更加方便，主要体现在配置文件中，如下：

首先引入p命名空间

```xml
 xmlns:p="http://www.springframework.org/schema/p"
```

其次修改注入方式

```xml
<bean id="userService" class="com.yyue.impl.UserServiceImpl" p:userDao-ref="userDao"></bean>
```

如下图所示

![image-20201122205849193](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20201122205849193.png)

#### 6.Bean依赖注入的数据类型

**三类数据量类型：**普通数据类型、引用数据类型、集合数据类型

##### **6.1普通数据类型的注入：**

利用set方法：（编写普通数据类型，给每个数据加上set方法）

```java
public class UserDaoImpl implements UserDao {
    private String name;
    private int age;

    public void setName(String name) {
        this.name = name;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

编写配置文件（由于我们在dao下创建的数据类型，所以给dao增添属性）

```xml
<bean id="userDao" class="com.yyue.impl.UserDaoImpl">
        <property name="name" value="zhangsan"></property>
        <property name="age" value="18"></property>
</bean>
```

##### 6.2引用数据类型(如上一节所说)

##### 6.3集合数据类型（三类集合：List集合、Map集合、Properties集合）

利用set方法注入

1.为集合创建set方法

```java
private List<String> strlist;
    private Map<String, User> userMap;
    private Properties properties;
    public void setStrlist(List<String> strlist) {
        this.strlist = strlist;
    }

    public void setUserMap(Map<String, User> userMap) {
        this.userMap = userMap;
    }

    public void setProperties(Properties properties) {
        this.properties = properties;
    }
```

2.编写配置文件

```xml
<bean id="userDao" class="com.yyue.impl.UserDaoImpl">
        <property name="strlist" ><!--List集合-->
            <list>
                <value>aaa</value>
                <value>bbb</value>
                <value>ccc</value>
            </list>
        </property>
        <property name="userMap"><!--Map集合，key代表键value-ref引入值的路径-->
            <map>
                <entry key="u1" value-ref="user1"></entry>
                <entry key="u2" value-ref="user2"></entry>
            </map>
        </property>
        <property name="properties"><!--properties集合-->
            <props>
                <prop key="p1">ppp1</prop>
                <prop key="p2">ppp2</prop>
                <prop key="p3">ppp3</prop>
            </props>
        </property>
    </bean>

    <bean id="user1" class="com.yyue.domain.User">
        <property name="name" value="zhangsan"></property>
        <property name="add" value="beijing"></property>
    </bean>
    <bean id="user2" class="com.yyue.domain.User">
        <property name="name" value="lisi"></property>
        <property name="add" value="天津"></property>
    </bean>
```

#### 7.引入其他配置文件(分模块开发)

实际开发中，Spring的配置内容非常多，就导致Spring配置很繁杂且体积很大，所以，可以将部分配置拆解到其他配置文件中，而在Spring主配置文件中通过import标签进行加载

<import resource="applicationContext-xxx.xml"/>

#### 8.知识要点总结

<bean>标签

​        id属性：在容器中Bean实例的唯一标识，不允许重复

​        class属性：要实例化的Bean的全限定名

​        scope属性：Bean的作用范围，常用是singleton（默认）和prototype

​		<property>标签：属性注入

 				name属性：属性名称

​				 value属性：注入的普通属性的值

​				 ref属性：注入的对象引用值

​				 <list>标签、<map>标签、<properties>标签

​         <constructor-arg>标签：利用构造函数时使用的标签

<import>标签：导入其他的Spring的分文件

### 三、Spring相关API

3.1ApplicationContext的实现类

- ClassPathXmlApplicationContext：它是从类的根路径下加载配置文件（推荐使用）
- FileSystemXmlApplicationContext：它是从磁盘路径上加载配置文件，配置文件可以在磁盘的任意位置
- AnnotationConfigApplicationContext：当使用注解配置容器对象时，需要使用此类来创建Spring容器，它用来读取注解

**Spring的重点API**

app.getBean("id");

app.getBean(Class);    如app.getBean(UserService.class);

### 四、Spring配置数据源

#### 4.1数据源(连接池)的作用

- 数据源（连接池）是提高程序性能而出现的
- 事先实例化数据源，初始化部分连接资源
- 使用连接资源时从数据源中获取
- 使用完毕后将连接资源还给数据源

常见的数据源（连接池）：BDCP、C3P0、BoneCP、Druid等

**首先导入依赖**

```xml
<dependencies>
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.41</version>
    </dependency>
    <dependency>
        <groupId>com.mchange</groupId>
        <artifactId>c3p0</artifactId>
        <version>0.9.5.2</version>
    </dependency>
    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>druid</artifactId>
        <version>1.1.10</version>
    </dependency>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.13</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.12</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

**1.测试c3p0**

```java
@Test
    //测试手动创建c3p0数据源
    public void test1() throws Exception{
        ComboPooledDataSource dataSource = new ComboPooledDataSource();
        dataSource.setDriverClass("com.mysql.jdbc.Driver");
        dataSource.setJdbcUrl("jdbc:mysql://localhost:3306/test");
        dataSource.setUser("root");
        dataSource.setPassword("root");
        Connection connection = dataSource.getConnection();
        System.out.println(connection);
        connection.close();
    }
```

**2.测试druid数据源**

```java
@Test
    //测试手动创建druid数据源
    public void test2() throws Exception{
        DruidDataSource dataSource = new DruidDataSource();
        dataSource.setDriverClassName("com.mysql.jdbc.Driver");
        dataSource.setUrl("jdbc:mysql://localhost:3306/sys");
        dataSource.setUsername("root");
        dataSource.setPassword("root");
        DruidPooledConnection connection = dataSource.getConnection();
        System.out.println(connection);
        connection.close();
    }
```

**3.由于当前的库以及性质耦合死了，所以抽取到配置文件**

在resources下创建一个文件，可以为jdbc.properties

jdbc.properties

```
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/sys
jdbc.username=root
jdbc.password=root
```

测试手动创建c3p0数据源（使用properties配置文件的方式）

```java
@Test
    //测试手动创建c3p0数据源（使用加载properties配置文件的方法）
    public void test3() throws Exception{
        ResourceBundle resourceBundle = ResourceBundle.getBundle("jdbc");//加载配置文件
        //获取键值对
        String driver = resourceBundle.getString("jdbc.driver");
        String url = resourceBundle.getString("jdbc.url");
        String usename = resourceBundle.getString("jdbc.username");
        String password = resourceBundle.getString("jdbc.password");
        ComboPooledDataSource dataSource = new ComboPooledDataSource();
        dataSource.setDriverClass(driver);
        dataSource.setJdbcUrl(url);
        dataSource.setUser(usename);
        dataSource.setPassword(password);
        Connection connection = dataSource.getConnection();
        System.out.println(connection);
        connection.close();
    }
```

#### 4.2Spring配置数据源

可以将DataSource的创建权交由Spring容器去完成

首先导坐标

```xml
<dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.2.6.RELEASE</version>
        </dependency>
```

创建配置文件（在resources下面创建一个配置文件可以为applicationContext.xml）

##### 4.2.1测试用Spring容器产生c3p0数据源对象

```xml
<bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
    <property name="driverClass" value="com.mysql.jdbc.Driver"></property>
    <property name="jdbcUrl" value="jdbc:mysql://localhost:3306/sys"></property>
    <property name="user" value="root"></property>
    <property name="password" value="root"></property>
</bean>
```

```java
@Test
    //测试Spring容器产生数据源对象
    public void test4() throws Exception{
        ApplicationContext app = new ClassPathXmlApplicationContext("applicationContext.xml");
        DataSource dataSource = (DataSource) app.getBean("dataSource");
        Connection connection = dataSource.getConnection();
        System.out.println(connection);
        connection.close();
    }
```

##### 4.2.1利用Spring容器产生druid数据源对象

配置文件的编写

```xml
 <bean id="dataSource2" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="com.mysql.jdbc.Driver">
        </property>
        <property name="url" value="jdbc:mysql://localhost:3306/sys"></property>
        <property name="username" value="root"></property>
        <property name="password" value="root"></property>
    </bean>
```

测试文件的编写

```java
@Test
    //测试Spring容器产生druid数据源对象
    public void test5() throws Exception{
        ApplicationContext app = new ClassPathXmlApplicationContext("applicationContext.xml");
        DataSource dataSource = (DataSource) app.getBean("dataSource2");
        Connection connection = dataSource.getConnection();
        System.out.println(connection);
        connection.close();
    }
```

#### 4.3抽取jdbc配置文件

applicationContext.xml加载jdbc.properties配置文件获得连接信息

首先，需要引入Context命名空间和约束路径

- 命名空间：xmlns:context="http://www.springframework.org/schema/context"
- 约束路径：http://www.springframework.org/schema/context  http://www.springframework.org/schema/context/spring-context.xsd

代码如下配置加载文件

```xml
<context:property-placeholder location="classpath:jdbc.properties"></context:property-placeholder>
    <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
    <property name="driverClass" value="${jdbc.driver}"></property>
    <property name="jdbcUrl" value="${jdbc.url}"></property>
    <property name="user" value="${jdbc.username}"></property>
    <property name="password" value="${jdbc.password}"></property>
</bean>
```

#### 4.4知识要点

**Spring容器加载properties文件**

<context:property-placeholder location="classpath:xx.properties"/>

<property name="" value="${key}"/>

### 五、Spring注解开发

#### 5.1Spring原始注解

Spring是轻代码而重配置的框架，配置比较繁重，影响开发效率，所以注解开发是一种趋势，注解代替xml配置文件可以简化配置，提高开发效率

![image-20201126102419150](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20201126102419150.png)

注意：使用注解进行开发时，需要在applicationContext.xml中配置组件扫描，作用是指定哪个包及其子包的Bean需要进行扫描以便识别注解配置的类、字段和方法。

```xml
<context:component-scan base-package="com.yyue"></context:component-scan>
```

#### 5.2Spring新注解

使用上面的注解还不能全部替代xml配置文件，还需要使用注解替代的配置如下：

- 非自定义的Bean的配置：<bean>
- 加载properties文件的配置：<context:property-placeholder>
- 组件扫描的配置：<<context:component-scan>>
- 引入其他文件：<import>

![image-20201126201009529](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20201126201009529.png)

注解用例：

UserServiceImpl.class

```java
            //<bean id="userService" class="com.yyue.Impl.UserServiceImpl">
            @Service("userService")
            @Scope("prototype")
            public class UserServiceImpl implements UserService {
                @Value("${jdbc.driver}")
                private String name;
             	//<property name="userDao" ref="userDao"/>
            	//@Autowired//按照数据类型从Spring容器中进行匹配
            	//@Qualifier("userDao")//按照id值从容器中进行匹配的，但是此处@Qualifier要与@Autowired一起用
            	@Resource(name = "userDao")//@Resource相当于@Autowired+@Qualifier
            	private UserDao userDao;
            public void save() {
                System.out.println(name);
                userDao.save();
            }
            @PostConstruct
            public void init(){
                System.out.println("userService创建初始化方法");
            }

            @PreDestroy
            public void destroy(){
                System.out.println("userService销毁方法");
            }
            }
```

DataSourceConfiguration.class

```java
//<context:property-placeholder location="classpath:jdbc.properties"></context:property-placeholder>
@PropertySource("classpath:jdbc.properties")
public class DataSourceConfiguration {
    @Value("${jdbc.driver}")
    private String driver;
    @Value("jdbc.url")
    private String url;
    @Value("jdbc.username")
    private String name;
    @Value("jdbc.password")
    private String password;
    
    @Bean("dataSource")//注入
    public DataSource getdataSource() throws Exception {
        ComboPooledDataSource dataSource = new ComboPooledDataSource();
        dataSource.setDriverClass(driver);
        dataSource.setJdbcUrl(url);
        dataSource.setUser(name);
        dataSource.setPassword(password);
        Connection connection = dataSource.getConnection();
        System.out.println(connection);
        connection.close();
        return dataSource;
    }
```

UserDaoImpl.class

```java
//<bean id="userDao" class="com.yyue.Impl.UserDaoImpl"></bean>
    //@Component("userDao")
    @Repository("userDao")
public class UserDaoImpl implements UserDao {
    public void save() {
        System.out.println("===========");
    }
```

SpringConfiguration.class

```java
@Configuration//标志该类是Spring核心配置类
//<context:component-scan base-package="com.yyue"></context:component-scan>
@ComponentScan("com.yyue")//扫描
//<import resource="" />
@Import(DataSourceConfiguration.class)
public class SpringConfiguration {
}

```

测试类的编写：

```java
ApplicationContext app = new AnnotationConfigApplicationContext(SpringConfiguration.class);
        UserService userService = (UserService) app.getBean("userService");
        userService.save();
```

### 六、Spring整合Junit

#### 6.1原始Junit测试Spring的问题

在测试类中，每个测试方法都有以下两行代码：

```
ClassPathXmlApplicationContext app = new ClassPathXmlApplicationContext("bean.xml");
IAccountService as = app.getBean("userService");
```

这两行代码的作用是获取容器，如果不写的话，直接会提示空指针异常。所以又不能轻易删掉.

#### 6.2上述问题解决思路

让SpringJunit负责创建Spring容器，但是需要将配置文件中名称告诉他

将需要进行测试Bean直接在测试类中进行注入。

#### 6.3Spring集成Junit步骤

- 导入spring集成Junit的坐标
- 使用@Runwith注解替换原来的运行期
- 使用@ContextConfiguration指定配置文件或配置类
- 使用@Autowired注入需要测试的对象
- 创建测试方法进行测试

```java
@RunWith(SpringJUnit4ClassRunner.class)
//@ContextConfiguration("classpath:applicationContext.xml")
@ContextConfiguration(classes = {SpringConfiguration.class})
public class SpringJunitTest {
    @Autowired
    private UserService userService;
    @Autowired
    private DataSource dataSource;
    @Test
    public void test1() throws Exception{
        userService.save();
        System.out.println(dataSource.getConnection());
    }
}
```

## Spring的AOP

### 一、

#### 1、Spring的AOP简介

**面向切面编程**

##### 1.2AOP的作用及其优势

- 作用：在程序运行期间，在不修改源码的情况下对方法进行功能增强
- 优势：减少重复代码，提高开发效率，并且便于维护

##### 1.4AOP的动态代理技术

常见的动态代理技术

- JDK代理：基于接口的动态代理技术

- cglib代理：基于父类的动态代理技术

  ![image-20201128181450771](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\image-20201128181450771.png)

#### 2、基于XML的AOP开发

#### 3、基于注解的AOP开发