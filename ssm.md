# 基础框架SSM

Spring Framework系统框架

![](D:\mybatis笔记\images\ssm2.png)

学习路线：

1. 第一部分：核心容器、概念（Ioc/DI）、容器的基本操作
2. 第二部分：整合、整合数据层技术MyBatis
3. 第三部分：AOP、核心概念、AOP基础操作、AOP实用开发
4. 第四部分：事务、事务实用开发
5. 第五部分家族、SpringMVC、SpringBoot、SpringCloud

## 一、第一部分

### 1.核心概念：

- 代码书写现状
  - 耦合度高
- 解决方案
  - 使用对象时，在程序中不要主动使用new产生对象，转换为由外部提供对象
- IoC（Inversion of Control）控制反转
  - 对象的创建控制权由程序转移到外部，这种思想称为控制反转
- Spring技术对IoC进行了实现
  - 提供了一个容器，称为IoC容器，用来充当IoC思想中的”**外部**“
  - IoC容器负责对象的创建、初始化等一系列工作，被创建或被管理的对象在IoC容器中统称为Bean
- DI（Dependency Injection）依赖注入
  - 在容器中建立bean与bean之间的依赖关系的整个过程，称为依赖注入

- 做这些的目标：**充分解耦**
  - 使用IoC容器管理Bean(IoC)
  - 在IoC容器内将有依赖关系的bean进行关系绑定（DI）
- 最终效果
  - 使用对象时不仅可以直接从IoC容器中获取，并且获取到的bean已经绑定了所有的依赖关系

### 2.IoC入门案例

IoC入门案例思路分析

1. 管理什么？（Service和Dao）

2. 如何将被管理的对象告知IoC容器？（配置    创建spring配置文件applicationContext.xml）

   - 首先要在pom.xml总添加spring坐标才能够创建Spring的配置文件

     - ```xml
       <dependency>
           <groupId>org.springframework</groupId>
           <artifactId>spring-context</artifactId>
           <version>5.2.10.RELEASE</version>
       </dependency>
       ```

   - 创建Spring配置文件即applicationContext.xml

     - 配置bean

     - ```xml
       <!--2.配置bean-->
       <!--bean标签表示配置bean
       id属性表示给bean起名字
       class属性表示给bean定义类型-->
       <bean id="bookDao" class="com.yyue.dao.impl.BookDaoImpl"/>
       <bean id="bookService" class="com.yyue.service.impl.BookServiceImpl"/>
       ```

3. 被管理的对象交给IoC容器，如何获取到IoC容器？（接口）

   - ```java
     //获取IoC容器
     ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
     ```

4. IoC容器获得后，如何从容器中获取bean？（接口方法）

   - ```java
     //4.获取bean
     BookDao bookDao =(BookDao) ctx.getBean("bookDao");
     ```

5. 使用Spring导入哪些坐标？（pom.xml）

### 3.DI入门案例

问题：由于类中还存在new对象，还是没有实现解耦合

DI入门案例思路分析

1. 基于IoC管理bean

2. Service中使用new形式创建的Dao对象能否保留？（不能保留）

   - ```java
     //5.删除业务层中使用new的方式创建dao对象
     private BookDao bookDao;
     ```

3. Service中需要的Dao对象如何进入到Service中？（提供方法）

   - ```java
     //6.提供对应的set方法
     public void setBookDao(BookDao bookDao) {
         this.bookDao = bookDao;
     }
     ```

4. Service与Dao之间的关系如何描述？（配置）

   - ```xml
     <!--7.配置service与dao的关系-->
     <!--property标签表示配置当前bean的属性
     name属性表示配置哪一个具体的属性
     ref属性表示参照哪一个bean-->
     <bean id="bookService" class="com.yyue.service.impl.BookServiceImpl">
         <property name="bookDao" ref="bookDao"></property>
     </bean>
     ```

### 4.bean

#### 4.1bean配置

##### 4.1.1bean基础配置

![](D:\mybatis笔记\images\s1.png)

##### 4.1.2bean别名配置

![](D:\mybatis笔记\images\s2.png)

##### 4.1.3bean作用范围配置

![](D:\mybatis笔记\images\s3.png)

bean作用范围说明

- 为什么bean默认为单例？因为非单例，每次创建一个对象就多一个bean，那么会给spring容器造成很大的压力，而且可以只用一个对象来实现所有功能并不需要过多的重复对象
- 适合交给容器进行管理的bean
  - 表现层对象
  - 业务层对象
  - 数据层对象
  - 工具对象
- 不适合交给容器进行管理的bean
  - 封装实体的域对象

#### 4.2bean实例化

学习内容：

- bean究竟是怎么创建出来的

  - bean本质上是对象，创建bean使用构造方法完成

- 实例化bean的三种方式

  - 第一种方式：

    - 提供可访问的构造方法
    - ![](D:\mybatis笔记\images\s4.png)
    - 配置
    - ![](D:\mybatis笔记\images\s5.png)
    - **注:无参构造方法如果不存在，将抛出异常BeanCreationException**

  - 第二种方式

    - 使用静态工厂创建对象

      - 以往方式：用静态工厂创建对象
        - ![有一个静态工厂类来创建对象](D:\mybatis笔记\images\s6.png)
        - ![](D:\mybatis笔记\images\s7.png)
      - 现在方式：
        - 静态工厂初始化bean
        - ![](D:\mybatis笔记\images\s8.png)
        - 配置
        - ![](D:\mybatis笔记\images\s9.png)

    - 第三种方式：实例工厂初始化bean

      - 以往方式

        - 实例工厂

        - ```java
          public class UserDaoFactory {
              public UserDao getUserDao(){
                  System.out.println("factory setup....");
                  return new UserDaoImpl();
              }
          }
          ```

        - ```java
          public static void main(String[] args) {
              //创建实例工厂对象
              UserDaoFactory userDaoFactory = new UserDaoFactory();
              //通过实例工厂对象创建对象
              UserDao userDao = userDaoFactory.getUserDao();
              userDao.save();
          }
          ```

      - 现在方式：

        - 配置

        - ```java
          <!--方式三：使用实例工厂实例化bean-->
          <bean id="userFactory" class="com.yyue.factory.UserDaoFactory"/>
          <bean id="userDao" factory-method="getUserDao" factory-bean="userFactory" />
          ```

        - 使用

        - ```java
          ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
          UserDao userDao = (UserDao)ctx.getBean("userDao");
          userDao.save();
          ```

        - ![](D:\mybatis笔记\images\s10.png)

    - 第四种方式：第三种方式的变种：为了解决上面问题

      - 新建一个UserDaoFactoryBean实现FactoryBean接口

      - ```java
        public class UserDaoFactoryBean implements FactoryBean<UserDao> {
            @Override
            public UserDao getObject() throws Exception {
                return new UserDaoImpl();
            }
        
            @Override
            public Class<?> getObjectType() {
                return UserDao.class;
            }
        }
        ```

      - 配置文件

      - ```java
        <!--方式四：使用FactoryBean的实例化bean-->
        <bean id="userDao" class="com.yyue.factory.UserDaoFactoryBean"></bean>
        ```

      - 此处创建的对象也是单例对象，若是想要变成非单例对象，则可以在UserDaoFactory种重写单例方法。

      - ```java
        @Override
        public boolean isSingleton() {
            return false;
        }
        ```

    - ![](D:\mybatis笔记\images\s11.png)

总结：实例化bean的三种方式

- 构造方法（常用）
- 静态工厂（了解）
- 实例工厂（了解）
  - FactoryBean（实用）

#### 5.bean生命周期

- 生命周期：从创建到消亡的完整过程
- bean生命周期：bean从创建到销毁的整体过程
- bean生命周期控制：在bean创建后到销毁前做一些事情

**测试生命周期1：**

- 首先在方法中添加创建和销毁两个方法

- ```java
   //初始化方法
      public void init(){
          System.out.println("init.....");
      }
    
      //销毁方法
      public void destroy(){
          System.out.println("destroy....");
      }
  ```

- 在配置文件中配置创建和销毁方法

- ```xml
  <bean id="bookDao" class="com.yyue.dao.impl.BookDaoImpl" init-method="init" destroy-method="destroy"/>
  ```

- **关闭容器方法1**（由于本身的接口不存在close方法，所以换了类）

- ```java
  ConfigurableApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
  BookDao bookDao = (BookDao) ctx.getBean("bookDao");
  bookDao.save();
  ctx.close();//比较暴力的关闭了容器
  ```

- **关闭容器方法2**

- ```java
  ctx.registerShutdownHook();//关闭注册钩子
  ```

- 关闭容器两种方法的区别

- close如果写在上面的话，会在程序未执行完之前就关闭容器，那样则会报错，

- 而registerShutdownHook可以写在任意位置，在程序执行完成后执行

**测试生命周期2**

- 让其实现创建和销毁接口
- ![](D:\mybatis笔记\images\s13.png)

bean生命周期（初始化都经历了哪些阶段）

- 初始化容器
  1. 创建对象（内存分配）
  2. 执行构造方法
  3. 执行属性注入（set操作）
  4. 执行bean初始化方法
- 使用bean
  1. 执行业务操作
- 关闭/销毁容器
  1. 执行bean销毁方法

![](D:\mybatis笔记\images\s14.png)

总结：

1. bean生命周期控制
   - 配置
     - init-method
     - destroy-method
   - 接口（了解）
     - InitializingBean
     - DisposableBean
2. 关闭容器
   - ConfigurableApplicationContext
     - close()
     - registerShutdownHook()

### 5.依赖注入方式

思考：向一个类中**传递数据**的方式有几种？

- 普通方法（set方法）
- 构造方法

思考：依赖注入描述了在容器中建立bean与bean之间依赖关系的过程，如果bean运行需要的是数字或字符串呢？

- 引用类型
- 简单类型（基本数据类型与String）

依赖注入方式

#### 5.1setter注入

- 简单类型

  - ```java
    private int dataSourceNum;
    private String dataSourceName;
    public void setDataSourceNum(int dataSourceNum) {
            this.dataSourceNum = dataSourceNum;
        }
    public void setDataSourceName(String dataSourceName) {
            this.dataSourceName = dataSourceName;
        }
    ```

  - 配置文件

  - ```xml
    <bean id="bookDao" class="com.yyue.dao.impl.BookDaoImpl">
        <property name="dataSourceName" value="yyue"></property>
        <property name="dataSourceNum" value="100"></property>
    </bean>
    ```

  - ![](D:\mybatis笔记\images\s16.png)

- 引用类型

  - ![](D:\mybatis笔记\images\s15.png)

#### 5.2构造器注入

- 引用类型
  - 标准书写
  - ![](D:\mybatis笔记\images\s17.png)
  - ![](D:\mybatis笔记\images\s18.png)
- 简单类型
  - ![](D:\mybatis笔记\images\s19.png)
  - ![](D:\mybatis笔记\images\s20.png)
- 上述程序的耦合性太高，若是参数名变了，还需再修改配置文件中的name
- 所以为了解耦合提出了下面一种方式，利用数据类型匹配
  - ![](D:\mybatis笔记\images\s21.png)
- 但是现在又出现了另外一个问题，若是两个参数类型是一样的该怎么办
  - ![](D:\mybatis笔记\images\s22.png)

**依赖注入方式选择**

1. 强制依赖使用构造器进行，使用setter注入有概率不进行注入导致null对象出现
2. 可选依赖使用setter注入进行，灵活性强
3. Spring框架倡导使用构造器，第三方框架内部大多数采用构造器注入的形式进行数据初始化，相对严谨
4. 如果有必要可以两者同时使用，使用构造器注入完成强制依赖的注入，使用setter完成可选依赖的注入
5. 实际开发过程中还要根据实际情况分析，如果受控对象没有提供setter方法就必须使用构造器注入
6. 自己开发的模块推荐使用setter注入

#### 5.3依赖自动装配

- IoC容器根据bean所依赖的资源在容器中自动查找并注入到bean中的过程称为自动装配

- 自动装配方式

  - 按类型(常用)

    - ![](D:\mybatis笔记\images\j14.png)

    - ```xml
      <bean id="bookDao" class="com.yyue.dao.impl.BookDaoImpl"></bean>
      <bean id="bookService" class="com.yyue.service.impl.BookServiceImpl" autowire="byType">
      ```

    - 若是有两个bean的类型都是所需要的BookDao，那么如果按类型装配，应该装配哪一个呐，此时就会出现**错误**

  - 按名称

    - ```xml
      <bean id="bookDao" class="com.yyue.dao.impl.BookDaoImpl"></bean>
      <bean id="bookService" class="com.yyue.service.impl.BookServiceImpl" autowire="byName">
      </bean>
      ```

  - 按构造方法

  - 不启用自动装配

依赖自动装配特征

- 自动装配用于引用类型依赖注入，不能对简单类型进行操作
- 使用按类型装配时(byType)必须保障容器中相同类型的bean唯一，推荐使用
- 使用按名称装配时(byName)必须保障容器中具有指定名称的bean，因变量名与配置耦合，不推荐使用
- 自动装配优先级低于setter注入与构造器注入，同时出现时自动装配配置失效

#### 5.4集合注入

##### 数组

- ```java
  private List<String> list;
  public void setArray(int[] array) {
          this.array = array;
      }
  ```

- ```xml
  <property name="array">
      <array>
          <value>1</value>
          <value>2</value>
          <value>3</value>
      </array>
  </property>
  ```

##### List

- ```java
  private List<String> list;
  public void setList(List<String> list) {
          this.list = list;
      }
  ```

- ```xml
  <property name="list">
      <list>
          <value>itcast</value>
          <value>yyue</value>
          <value>com</value>
          <value>itcast</value>
      </list>
  </property>
  ```

##### Set

- ```java
  private Set<String> set;
  public void setSet(Set<String> set) {
          this.set = set;
      }
  ```

- ```xml
  <property name="set">
      <set>
          <value>itcast</value>
          <value>yyue</value>
          <value>com</value>
          <value>itcast</value>
      </set>
  </property>
  ```

##### Map

- ```java
  private Map<String,String> map;
  public void setMap(Map<String, String> map) {
          this.map = map;
      }
  ```

- ```xml
  <property name="map">
      <map>
          <entry key="country" value="中国"></entry>
          <entry key="province" value="江苏"></entry>
          <entry key="city" value="南京"></entry>
      </map>
  </property>
  ```

##### Properties

- ```java
  private Properties properties;
  public void setProperties(Properties properties) {
          this.properties = properties;
      }
  ```

- ```xml
  <property name="properties">
      <props>
          <prop key="country">中国</prop>
          <prop key="province">江苏</prop>
          <prop key="city">南京</prop>
      </props>
  </property>
  ```

#### 5.5案例:数据源对象管理

**第三方资源配置管理**

1. druid数据源

   - 导入druid坐标

   - ```xml
     <dependency>
         <groupId>com.alibaba</groupId>
         <artifactId>druid</artifactId>
         <version>1.2.15</version>
     </dependency>
     ```

   - 配置数据源对象作为spring管理的bean

   - ```xml
     <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
         <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
         <property name="url" value="jdbc:mysql://localhost:3306/spring_db"/>
         <property name="username" value="root"/>
         <property name="password" value="root"/>
     </bean>
     ```

2. c3p0数据源

   - 导入c3p0坐标

   - ```xml
     <dependency>
         <groupId>c3p0</groupId>
         <artifactId>c3p0</artifactId>
         <version>0.9.1.2</version>
     </dependency>
     ```

   - 配置数据源对象作为spring管理的bean

   - ```xml
     <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
         <property name="driverClass" value="com.mysql.jdbc.Driver"/>
         <property name="jdbcUrl" value="jdbc:mysql://localhost:3306/spring_db"/>
         <property name="user" value="root"/>
         <property name="password" value="root"/>
     </bean>
     ```

   - 此时会提示没有mysql驱动的错误，将mysql坐标导入即可

   - ```xml
     <dependency>
         <groupId>mysql</groupId>
         <artifactId>mysql-connector-java</artifactId>
         <version>5.1.16</version>
     </dependency>
     ```

小结：

Spring管理第三方资源

- DruidDataSource
- ComboPooledDataSource

### 6.加载properties文件

步骤：

1. 开启context命名空间
   - ![](D:\mybatis笔记\images\j18.png)
2. 使用context命名空间，加载指定properties文件
   - ![](D:\mybatis笔记\images\j16.png)
3. 使用${}读取加载的属性值
   - ![](D:\mybatis笔记\images\j17.png)

![](D:\mybatis笔记\images\j19.png)

### 7.容器

#### 7.1创建容器

两种方式

![](D:\mybatis笔记\images\j20.png)

#### 7.2获取bean

三种方式

![](D:\mybatis笔记\images\j21.png)

**注：按类型查找，容器中只能有该种类型的一个bean，多个则不可以**

#### 7.3容器类层次结构

![](D:\mybatis笔记\images\j22.png)

#### 7.4BeanFactory

![](D:\mybatis笔记\images\j23.png)

小结：

1. 创建容器（两种）
   - ClassPathXmlApplicationContext
   - FileSystemXmlApplicationContext
2. 获取bean（3种）
3. 容器类层次结构
4. BeanFactory

### 8.核心容器总结

1. 容器相关
   - BeanFactory是IoC容器的顶层接口，初始化BeanFactory对象时，加载的bean延迟加载
   - ApplicationContext接口是Spring容器的核心接口，初始化时bean立即加载
   - ApplicationContext接口提供基础的bean操作相关方法，通过其他接口扩展其功能
   - ApplicationContext接口常用初始化类
     - ClassPathXmlApplicationContext
     - FileSystemApplicationContext
2. bean相关
   - ![](D:\mybatis笔记\images\j24.png)
3. 依赖注入相关
   - ![](D:\mybatis笔记\images\j25.png)

## 二、第二部分：注解开发

### 1.注解开发

#### 1.1注解开发定义bean

- 使用@Component定义bean

  - ![](D:\mybatis笔记\images\j26.png)

- 核心配置文件种通过组件扫描加载bean

  - ```xml
    <context:component-scan base-package="com.yyue"/>
    ```

- Spring提供@Component注解的三个衍生注解

  - @Controller：用于表现层bean定义
  - @Service：用于业务层bean定义
  - @Repository：用于数据层bean定义
  - ![](D:\mybatis笔记\images\j27.png)

#### 1.2纯注解开发

- Spring3.0升级了纯注解开发模式，使用Java类替代配置文件，开启了Spring快速开发赛道
  - ![](D:\mybatis笔记\images\j28.png)
- 读取Spring核心配置文件初始化容器对象切换为读取Java配置类初始化容器对象
  - ![](D:\mybatis笔记\images\j29.png)

总结：

1. 定义bean
   - @Component
     - @Controller
     - @Service
     - @Repository
   - <context:component-scan/>
2. 纯注解开发
   - @Configuration
   - @ComponentScan
   - AnnotationConfigApplicationContext

### 2.bean管理

#### 2.1bean作用范围

- 使用@Scope定义bean范围   singleton表示单例，prototype表示非单例
  - ![](D:\mybatis笔记\images\j30.png)

#### 2.2bean生命周期

- 使用@PostConstruct、@PreDestroy定义bean生命周期
- ![](D:\mybatis笔记\images\j31.png)

### 3.依赖注入

- 使用**@Autowired**注解开启自动装配模式(按类型)
- ![](D:\mybatis笔记\images\springboot28.png)
- 使用**@Qualifier**注解开启指定名称装配bean
- ![](D:\mybatis笔记\images\ssm3.png)
- 注意：@Qualifier注解无法单独使用，必须配合@Autowired注解使用
- 使用**@Value**实现简单类型注入
- ![](D:\mybatis笔记\images\ssm4.png)

加载properties文件

- 使用@PropertySource注解加载properties文件

- ![](D:\mybatis笔记\images\ssm5.png)

- ```java
  @Configuration
  @ComponentScan("com.yyue")
  @PropertySource("jdbc.properties")  //不支持使用通配符
  public class SpringConfig {
  }
  ```

- **注意：**路径仅支持单一文件配置，多文件请使用数组格式配置，不允许使用通配符* 

小结：

1. 自动装配
   - @Autowired
   - @Qualifier
   - @Value
2. 读取properties文件
   - @PropertySource

### 4.第三方bean管理

#### 1.第三方bean管理

- 使用@Bean配置第三方bean
- ![](D:\mybatis笔记\images\ssm6.png)

但是不建议使用上述做法，建议使用下面两种方式

1. 方式一：导入式
   - 使用独立的配置类管理第三方bean
   - ![](D:\mybatis笔记\images\ssm7.png)
   - ![](D:\mybatis笔记\images\ssm8.png)
2. 方式二： 扫描式
   - ![](D:\mybatis笔记\images\ssm9.png)

#### 2.第三方bean依赖注入

- 简单类型注入

- ![](D:\mybatis笔记\images\ssm10.png)
- 引用类型依赖注入
- ![](D:\mybatis笔记\images\ssm11.png)

小结：

1. 第三方bean管理
   - @Bean
2. 第三方bean依赖注入
   - 引用类型：方法形参
   - 简单类型：成员变量

### 5.总结

**XML配置比对注解配置**

![](D:\mybatis笔记\images\ssm12.png)

##   三、第三部分：整合

### 1.Spring整合MyBatis

- 一个简单的Mybatis程序

- Account实体类

  - ```java
    package com.yyue.domain;
    
    public class Account {
        private Integer id;
        private String name;
        private double money;
    
        public Account() {
        }
    
        public Integer getId() {
            return id;
        }
    
        public void setId(Integer id) {
            this.id = id;
        }
    
        public String getName() {
            return name;
        }
    
        public void setName(String name) {
            this.name = name;
        }
    
        public double getMoney() {
            return money;
        }
    
        public void setMoney(double money) {
            this.money = money;
        }
    
        @Override
        public String toString() {
            return "Account{" +
                    "id=" + id +
                    ", name='" + name + '\'' +
                    ", money=" + money +
                    '}';
        }
    }
    
    ```

- 数据层AccountDao

  - ```java
    package com.yyue.dao;
    
    import com.yyue.domain.Account;
    import org.apache.ibatis.annotations.Delete;
    import org.apache.ibatis.annotations.Insert;
    import org.apache.ibatis.annotations.Select;
    import org.apache.ibatis.annotations.Update;
    
    import java.util.List;
    
    public interface AccountDao {
        //保存
        @Insert("insert into account(name,money) values(#{name},#{money})")
        void save(Account account);
        //按id删除
        @Delete("delete from account where id = #{id}")
        void delete(Integer id);
        //修改
        @Update("update account set name = #{name} ,money = #{money} where id = #{id}")
        void update(Account account);
        //查询全部
        @Select("select * from account")
        List<Account> findAll();
        //按id查询
        @Select("select * from account where id = #{id}")
        Account findById(Integer id);
    }
    ```

- 业务层接口AccountService.interface

  - ```java
    package com.yyue.service;
    import com.yyue.domain.Account;
    import java.util.List;
    public interface AccountService {
        void save(Account account);
        void delete(Integer id);
        void update(Account account);
        List<Account> findAll();
        Account findById(Integer id);
    }
    ```

- 业务层实现类AccountServiceImpl.java

  - ```java
    package com.yyue.service.impl;
    import com.yyue.dao.AccountDao;
    import com.yyue.domain.Account;
    import com.yyue.service.AccountService;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.stereotype.Service;
    
    import java.util.List;
    
    @Service
    public class AccountServiceImpl implements AccountService {
        @Autowired
        private AccountDao accountDao;
        @Override
        public void save(Account account) {
            accountDao.save(account);
        }
        @Override
        public void delete(Integer id) {
            accountDao.delete(id);
        }
        @Override
        public void update(Account account) {
            accountDao.update(account);
        }
        @Override
        public List<Account> findAll() {
            return accountDao.findAll();
        }
        @Override
        public Account findById(Integer id) {
            return accountDao.findById(id);
        }
    }
    ```

- SqlMapConfig.xml配置文件

- ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <!DOCTYPE configuration
          PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
          "http://mybatis.org/dtd/mybatis-3-config.dtd">
  <configuration>
      <properties resource="jdbc.properties"></properties>
      <typeAliases>
          <package name="com.yyue.domain"/>
      </typeAliases>
      <environments default="mysql">
          <environment id="mysql">
              <transactionManager type="JDBC"></transactionManager>
              <dataSource type="POOLED">
                  <property name="driver" value="${jdbc.driver}"/>
                  <property name="url" value="${jdbc.url}"/>
                  <property name="username" value="${jdbc.username}"/>
                  <property name="password" value="${jdbc.password}"/>
              </dataSource>
          </environment>
      </environments>
      <mappers>
          <package name="com.yyue.dao"/>
      </mappers>
  </configuration>
  ```

- jdbc.properties配置文件

  - ```properties
    jdbc.driver=com.mysql.jdbc.Driver
    jdbc.url=jdbc:mysql://localhost:3306/spring_db?useSSL=false
    jdbc.username=root
    jdbc.password=root
    ```

- 运行程序

  - ```java
    package com.yyue;
    import com.yyue.dao.AccountDao;
    import com.yyue.domain.Account;
    import org.apache.ibatis.io.Resources;
    import org.apache.ibatis.session.SqlSession;
    import org.apache.ibatis.session.SqlSessionFactory;
    import org.apache.ibatis.session.SqlSessionFactoryBuilder;
    import java.io.IOException;
    import java.io.InputStream;
    import java.util.List;
    public class App {
        public static void main(String[] args) throws IOException {
            //1.创建SqlSessionFactoryBuilder对象
            SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new SqlSessionFactoryBuilder();
            //2.加载SqlMapConfig.xml
            InputStream inputStream = Resources.getResourceAsStream("SqlMapConfig.xml");
            //3.创建SqlSessionFactory对象
            SqlSessionFactory sqlSessionFactory = sqlSessionFactoryBuilder.build(inputStream);
            //4.获取SqlSession
            SqlSession sqlSession = sqlSessionFactory.openSession();
            //5.执行SqlSession对象执行查询，获取结果Account
            AccountDao accountDao = sqlSession.getMapper(AccountDao.class);
            Account account = accountDao.findById(1);
            System.out.println(account);
            //6.释放资源
            sqlSession.close();
        }
    }
    ```

提出问题：Spring是用来管理bean的，那么mybatis中哪些bean是值得让Spring来管理的

![](D:\mybatis笔记\images\ssm13.png)

![](D:\mybatis笔记\images\ssm14.png)

**开始整合MyBatis**

1. 导入相关jar坐标

   - ```xml
     Spring操作数据库的jar包-->
             <dependency>
                 <groupId>org.springframework</groupId>
                 <artifactId>spring-jdbc</artifactId>
                 <version>5.2.10.RELEASE</version>
             </dependency>
             <!--Spring整合mybatis要导入的jar包-->
             <dependency>
                 <groupId>org.mybatis</groupId>
                 <artifactId>mybatis-spring</artifactId>
                 <version>1.3.0</version>
             </dependency>
         </dependencies>
     ```

2. 将原来的配置文件改写成配置类MybatisConfig.class

   - ![](D:\mybatis笔记\images\ssm16.png)

   - ![](D:\mybatis笔记\images\ssm17.png)

   - JdbcConfig.class

     - ```java
       package com.yyue.config;
       
       import com.alibaba.druid.pool.DruidDataSource;
       import org.springframework.beans.factory.annotation.Value;
       import org.springframework.context.annotation.Bean;
       
       import javax.sql.DataSource;
       
       public class JdbcConfig {
           @Value("${jdbc.driver}")
           private String driver;
           @Value("${jdbc.url}")
           private String url;
           @Value("${jdbc.username}")
           private String username;
           @Value("${jdbc.password}")
           private String password;
       
           @Bean
           public DataSource dataSource(){
               DruidDataSource druidDataSource = new DruidDataSource();
               druidDataSource.setDriverClassName(driver);
               druidDataSource.setUrl(url);
               druidDataSource.setUsername(username);
               druidDataSource.setPassword(password);
               return druidDataSource;
           }
       }
       ```

### 2.Spring整合junit

开始整合junit

1. 使用Spring整合Junit专用的类加载器
   - ![](D:\mybatis笔记\images\ssm18.png)

小结：

1. 整合JUnit
   - @Runwith(SpringJUnit4ClassRunner.class)
   - @ContextConfiguration

## 四、第四部分

### 1.AOP简介

- AOP面向切面编程，一种编程范式，指导开发者如何组织程序结构
  - OOP面向对象编程
- 作用：在不惊动原始设计的基础上为其进行功能增强
- Spring理念：无入侵式/无侵入式

AOP核心概念

![](D:\mybatis笔记\images\ssm.png)

- 连接点(JoinPoint):程序执行过程中的任意位置，粒度为执行方法、抛出异常、设置变量等
  - 在SpringAOP中，理解为方法的执行
- 切入点(PointCut)：匹配连接点的式子
  - 在SpringAOP中，一个切入点可以只描述一个具体方法，也可以匹配多个方法
    - 一个具体方法：com.yyue.dao包下的BookDao接口中的无形参无返回值的save方法
    - 匹配多个方法：所有的save方法，所有的get开头的方法，所有以Dao结尾的接口中的任意方法，所有带有一个参数的方法
- 通知(Advice)：在切入点处执行的操作，也就是共性功能
  - 在SpringAOP中，功能最终以方法的形式呈现
- 通知类：定义通知的类
- 切面（Aspect）：描述通知与切入点的对应关系

总结：AOP核心概念

- 连接点(JoinPoint)
- 切入点(Pointcut)
- 通知(Advice)
- 通知类
- 切面(Aspect)

### 2.AOP入门案例

案例设定：测定接口执行效率

简化设定：在接口执行前给出当前系统时间

开发模式：XML or 注解

思路分析：

1. 导入坐标(pom.xml)
   - ![](D:\mybatis笔记\images\ssm19.png)
2. 制作连接点方法(原始操作，Dao接口与实现类)
   - ![](D:\mybatis笔记\images\ssm20.png)
3. 制作共性功能(通知类与通知)
   - ![](D:\mybatis笔记\images\ssm21.png)
4. 定义切入点
   - ![](D:\mybatis笔记\images\ssm22.png)
5. 绑定切入点与通知关系(切面)
   - ![](D:\mybatis笔记\images\ssm23.png)
   - ![](D:\mybatis笔记\images\ssm24.png)
   - ![](D:\mybatis笔记\images\ssm25.png)

### 3.AOP工作流程

#### 1.工作流程

1. Spring容器启动
2. 读取所有切面配置中的切入点
3. 初始化bean，判断bean对应的类中的方法是否匹配到任意切入点
   - 匹配失败，创建对象
   - 匹配成功，创建原始对象(目标对象)的代理对象
4. 获取bean执行方法
   - 获取bean，调用方法并执行，完成操作（失败 ）
   - 获取的bean是代理对象时，根据代理对象的运行模式运行原始方法与增强的内容，完成操作

#### 2.AOP核心概念

- 目标对象（Target）：原始功能去掉共性功能对应的类产生的对象，这种对象是无法直接完成最终工作的
- 代理（Proxy）：目标对象无法直接完成工作，需要对其进行功能回填，通过原始对象的代理对象实现

总结：

1. AOP工作流程
2. AOP核心概念
   - 目标对象
   - 代理
3. SpringAOP本质：代理模式

### 4.AOP切入点表达式

- 切入点：要进行增强的方法
- 切入点表达式：要进行增强的方法的描述方式

描述方式一：执行com.yyue.dao包下的BookDao接口中的无参数update方法

```
execution(void com.yyue.dao.BookDao.update())
```

描述方式二：执行com.yyue.dao.impl包下的BookDaoImpl类中的无参数update方法

```
execution(void com.yyue.dao.impl.BookDaoImpl.update())
```

#### 1.**语法格式**

- 切入点表达式标准格式：动作关键字(访问修饰符	返回值	包名.类/接口名.方法名(参数)	异常名)

- ```java
  execution(public User com.yyue.service.UserService.findById(int))
  ```

  - 动作关键字：描述切入点的行为动作，例如execution表示执行到指定切入点
  - 访问修饰符：public ，private等，可以省略
  - 返回值
  - 包名
  - 类/接口名
  - 方法名
  - 参数
  - 异常名：方法定义中抛出指定异常，可以省略

#### **2.通配符**

由于上述的描述方式要写很多内容，所以提出下面的描述方式

- 可以使用通配符描述切入点，快速描述

  - ​    *：单个独立的任意符号，可以独立出现，也可以作为前缀或者后缀的匹配符出现

    - ```
      execution(public * com.yyue.*.UserService.find*(*))
      //匹配com.yyue包下的任意包中的UserService类或接口中所有find开头的带有一个参数的方法
      ```

  -   ..    ：多个连续的任意符号，可以独立出现，常用于简化包名与参数的书写

    - ```
      execution(public User com..UserService.findById(..))
      //匹配com包下的任意包中的UserService类或接口中所有名称为findById的方法
      ```

  - +：专用于匹配子类类型

    - ```java
      execution(* *..*Service+*(..))
      ```

#### 3.书写技巧

- ![](D:\mybatis笔记\images\ssm27.png)

### 5.AOP通知类型

- AOP通知描述了抽取的共性功能，根据共性功能抽取的位置不同，最终运行代码时要将其加入到合理的位置
- AOP通知共分为五种类型
  - 前置通知
  
    - ```java
      @Pointcut("execution(void com.yyue.dao.BookDao.update())")
      private void pt(){}
      //前置通知
      @Before("pt()")
      public void before(){
      	System.out.println("before advice ...")
      }
      ```
  
  - 后置通知
  
    - ```java
      @Pointcut("execution(void com.yyue.dao.BookDao.update())")
      private void pt(){}
      //后置通知
      @After("pt()")
      public void after(){
          System.out.println("after advice ...");
      }
      ```
  
  - 环绕通知（重点）
  
    - ```java
      @Pointcut("execution(void com.yyue.dao.BookDao.update())")
      private void pt(){}
      //环绕通知
      @Around("pt()")
      public void around(ProceedingJoinPoint pjp) throws Throwable {
          System.out.println("around before advice ...");
          //表示对原始操作的调用
          pjp.proceed();
          System.out.println("around after advice ...");
      }
      ```
  
    - 对于有返回值的操作，在方法增强结束后要将返回值返回。否则会出现错误Null return value from advice does not match primitive return type for: public abstract int com.yyue.dao.BookDao.select()
  
    - ```java
      @Pointcut("execution(int com.yyue.dao.BookDao.select())")
      private void pt2(){}
      @Around("pt2()")
      public Object around2(ProceedingJoinPoint pjp) throws Throwable {
          System.out.println("around before advice ...");
          //表示对原始操作的调用
          Object res = pjp.proceed();
          System.out.println("around after advice ...");
          return res;
       }
      ```
  
  - 返回后通知（了解），只有正常结束才会执行
  
    - ```java
      @AfterReturning("pt()")
          public void afterReturning(){
              System.out.println("afterReturning advice ...");
          }
      ```
  
  - 抛出异常通知（了解），只有抛异常才会执行
  
    - ```java
      @AfterThrowing("pt()")
          public void afterThrowing(){
              System.out.println("afterThrowing advice ...");
          }
      ```

### 6.案例：测量业务接口万次执行效率

```java
@Configuration
@Aspect
public class ProjectAdvice {
    //匹配业务层所有方法
    @Pointcut("execution(* com.yyue.service.*Service.*(..))")
    private void servicePt(){}

    @Around("servicePt()")
    public void runSpeed(ProceedingJoinPoint  pjp) throws Throwable {
        Signature signature = pjp.getSignature();
        String className = signature.getDeclaringTypeName(); //类名
        String methodName = signature.getName(); //方法名
        long start = System.currentTimeMillis();
        for (int i = 0; i < 10000; i++) {
            pjp.proceed();
        }
        long end = System.currentTimeMillis();
        System.out.println("万次执行"+className+"."+methodName+"----->" + (end-start) + "毫秒");
    }
```

### 7.AOP通知获取数据

获取参数、返回值、异常

- 获取切入点方法的参数

  - JoinPoint：适用于前置、后置、返回后、抛出异常后通知

    - ```java
      @Before("pt()")
          public void before(JoinPoint jp){
              Object[] args = jp.getArgs();
              System.out.println(Arrays.toString(args));
              System.out.println("before advice ...");
          }
      ```

    - ```java
      @After("pt()")
      public void after(JoinPoint jp){
          Object[] args = jp.getArgs();
          System.out.println(Arrays.toString(args));
          System.out.println("after advice ...");
      }
      ```

  - ProceedJointPoint：适用于环绕通知

    - ```java
      @Around("pt()")
      public Object around(ProceedingJoinPoint pjp) throws Throwable {
          Object[] args = pjp.getArgs();
          System.out.println(Arrays.toString(args));
          args[0] = 777;
          Object ret = pjp.proceed(args);
          return ret;
      }
      ```

- 获取切入点方法返回值

  - 返回后通知

    - ```java
      @AfterReturning(value = "pt()", returning = "ret")·
      public void afterReturning(Object ret){ //用ret接收返回值   若是有JoinPoint参数，则必须放在前面 
          System.out.println("afterReturning advice..."+ret);
      }
      ```

  - 环绕通知

- 获取切入点方法运行异常信息

  - 抛出异常后通知

    - ```java
      @AfterThrowing(value = "pt()", throwing = "throwable")
      public void afterThrowing(Throwable throwable){
          System.out.println("afterThrowing advice..."+throwable);
      }
      ```

  - 环绕通知

### 8.百度网盘密码数据兼容处理

需求：对百度网盘分享链接输入密码时尾部多输入的空格做兼容处理

分析：

1. 在业务方法执行之前对所有的输入参数进行格式处理----trim()
2. 使用处理后的参数调用原始方法---环绕通知中存在对原始方法的调用

```java
@Configuration
@Aspect
public class MyAdvice {
    //切面
    @Pointcut("execution(boolean com.yyue.service.ResourcesService.openURL(*,*))")
    private void pt(){}

    @Around("pt()")
    public Object check(ProceedingJoinPoint pj) throws Throwable {
        Object[] args = pj.getArgs();
        System.out.println(Arrays.toString(args));
        for (int i = 0; i < args.length; i++) {
            //判断参数是否为字符串
            if (args[i].getClass().equals(String.class)){
                args[i] =args[i].toString().trim();
            }
        }
        Object ret = pj.proceed(args);
        return ret;
    }
}
```

## 五、Spring事务

### 1.简介

![](D:\mybatis笔记\images\ssm30.png)

结果：

- 程序正常执行时，没问题
- 程序出现异常后，转账失败，但异常之前操作成功，异常之后操作失败，整体业务失败

①：在业务层接口上添加Spring事务管理

```java
//开事务
    @Transactional
    void transfer(String out, String in, Double money);
```

**注：Spring注解式事务通常添加在业务层接口中而不会添加到业务层实现类，降低耦合。注解式事务可以添加到业务方法上表示当前方法开启事务，也可以添加到接口上表示当前接口所有方法开启事务**

②：设置事务管理器

```java
//配置事务管理器
    @Bean
    public PlatformTransactionManager transactionManager(DataSource dataSource){
        //jdbc事务管理器
        DataSourceTransactionManager dataSourceTransactionManager = new DataSourceTransactionManager();
        dataSourceTransactionManager.setDataSource(dataSource);
        return dataSourceTransactionManager;
    }
```

**注：事务管理器要根据实现技术进行选择，Mybatis框架使用的是JDBC事务**

③：开启注解式事务驱动

```java
//spring配置类
@EnableTransactionManagement
```

### 2.Spring事务角色

![](D:\mybatis笔记\images\ssm31.png)

事务角色：

- 事务管理员：发起事务方，在Spring中通常指代业务层开启事务的方法
- 事务协调员：加入事务方，在Spring中通常指代数据层方法，也可以是业务层方法

### 3.事务相关配置

![]()![ssm32](D:\mybatis笔记\images\ssm32.png)

有些异常默认不参加回滚，例如IOException不参加回滚，可以通过设置事务回滚异常，将其加入回滚。

```java
@Transactional(rollbackFor = {IOException.class})
```

![](D:\mybatis笔记\images\ssm33.png)

```java
//所有的事务都被加入到事务T中，进行一起成功一起失败
//但是要实现的是，无论转账操作是否成功，均进行转账操作的日志留痕
public void transfer(String out, String in, Double money) throws IOException {
    try{
        accountDao.outMoney(out, money);
        int a = 1/0;
        accountDao.inMoney(in, money);
    }finally {
        logService.log(out,in,money);
    }
}
```

#### 事务传播行为

- 事务协调员对事务管理员所携带事务的处理态度（加入或者不加入）

- ```java
  //在不需要加入事务管理员的事务上添加属性，创建新的事务
  @Transactional(propagation = Propagation.REQUIRES_NEW)
      void log(String out, String in, Double money);
  ```

  ![](D:\mybatis笔记\images\ssm34.png)

## 六、SpringMVC

Springmvc是一种基于Java实现MVC模型的轻量级Web框架

### 1.入门案例

1. 导入springmvc相关依赖

   - ```java
     <dependencies>
             <dependency>
                 <groupId>javax.servlet</groupId>
                 <artifactId>javax.servlet-api</artifactId>
                 <version>3.1.0</version>
             </dependency>
             <dependency>
                 <groupId>org.springframework</groupId>
                 <artifactId>spring-webmvc</artifactId>
                 <version>5.2.10.RELEASE</version>
             </dependency>
         </dependencies>
     ```

2. 创建SpringMVC控制器

   - ```java
     //2.定义controller
     //2.1使用@Controller定义bean
     @Controller
     public class UserController {
         //2.2设置当前操作的访问路径
         @RequestMapping("/save")
         //2.3设置当前操作的返回值类型
         @ResponseBody
         public String save(){
             System.out.println("user save...");
             return "{'module'}:{'springmvc'}";
         }
     }
     ```

3. 初始化SpringMvc环境，设定SpringMVC加载对应的bean

   - ```java
     //3。创建springmvc的配置文件，加载controller对应的bean
     @Configuration
     @ComponentScan("com.yyue.controller")
     public class SpringConfig {
     }
     ```

4. 初始化servlet容器，加载springmvc环境，并设置springmvc技术处理的请求

   - ```java
     //4.定义一个servlet容器启动的配置类，在里面加载spring的配置
     public class ServletContainersInitConfig extends AbstractDispatcherServletInitializer {
         //加载springmvc容器配置
         @Override
         protected WebApplicationContext createServletApplicationContext() {
             AnnotationConfigWebApplicationContext ctx = new AnnotationConfigWebApplicationContext();
             ctx.register(SpringConfig.class);
             return ctx;
         }
     
         //设置哪些请求归属springmvc处理
         @Override
         protected String[] getServletMappings() {
             return new String[]{"/"};
         }
     
         //加载spring容器配置
         @Override
         protected WebApplicationContext createRootApplicationContext() {
             return null;
         }
     }
     ```

总结：

![](D:\mybatis笔记\images\ssm35.png)

![](D:\mybatis笔记\images\ssm36.png)

![](D:\mybatis笔记\images\ssm37.png)

### 2.入门案例工作流程

- 启动服务器初始化过程
  - ![](D:\mybatis笔记\images\ssm388.png)
- 单次请求过程
  - ![](D:\mybatis笔记\images\ssm38.png)

### 3.Springmvc-bean加载控制

![](D:\mybatis笔记\images\ssm39.png)

```java
@Configuration
//扫描bean，排除controller
@ComponentScan(value = "com.yyue",
        excludeFilters = @ComponentScan.Filter(
                type = FilterType.ANNOTATION,
                classes = Controller.class
        ))
```

Controller加载控制与业务bean加载控制

![](D:\mybatis笔记\images\ssm40.png)

![](D:\mybatis笔记\images\ssm41.png)

简化开发，将上面的继承类换成一个已经封装好这些方法的类

![](D:\mybatis笔记\images\ssm42.png)

### 4.设置请求映射路径

![](D:\mybatis笔记\images\ssm43.png)

### 5.请求与响应

请求方式

- Get请求

  - ![](D:\mybatis笔记\images\ssm44.png)

- Post请求

  - ![](D:\mybatis笔记\images\ssm45.png)

  - 处理post请求中乱码问题

  - ```java
    package com.yyue.config;
    import org.springframework.web.filter.CharacterEncodingFilter;
    import org.springframework.web.servlet.support.AbstractAnnotationConfigDispatcherServletInitializer;
    import javax.servlet.Filter;
    import java.io.File;
    public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {
        @Override
        protected Class<?>[] getRootConfigClasses() {
            return new Class[0];
        }
        @Override
        protected Class<?>[] getServletConfigClasses() {
            return new Class[]{SpringMvcConfig.class};
        }
        @Override
        protected String[] getServletMappings() {
            return new String[]{"/"};
        }
        //乱码处理
        @Override
        protected Filter[] getServletFilters() {
            CharacterEncodingFilter filter = new CharacterEncodingFilter();
            filter.setEncoding("UTF-8");
            return new Filter[]{filter};
        }
    }
    ```

  - ![](D:\mybatis笔记\images\ssm46.png)

### 6.请求与响应

请求参数

- 参数种类

  - 普通参数

    - 解决传的参数与需要映射的参数名不一样的问题，通过@RequestParam("")进行绑定

  - POJO类型参数 

    - ```java
      //POJO参数
      @RequestMapping("/pojoParam")
      @ResponseBody
      public String pojoParam(User user){
          System.out.println("pojo参数传递 user ==>"+user);
          return "{'module':'pojo param'}";
      }
      ```

    - ![](D:\mybatis笔记\images\ssm47.png)

  - 嵌套POJO类型参数（一个实体类中含有另外一个实体类）

    - ```java
      //嵌套POJO参数
      @RequestMapping("/pojoContainPojoParam")
      @ResponseBody
      public String pojoContainPojoParam(User user){
          System.out.println("pojo嵌套pojo参数传递 user ==>"+user);
          return "{'module':'pojo contain param'}";
      }
      ```

    - ![](D:\mybatis笔记\images\ssm49.png)

  - 数组类型参数

    - ```java
      //数组参数
      @RequestMapping("/arrayParam")
      @ResponseBody
      public String arrayParam(String[] likes){
          System.out.println("数组参数传递 likes ==> "+ Arrays.toString(likes));
          return "{'module':'array param'}";
      }
      ```

    - ![](D:\mybatis笔记\images\ssm50.png)

  - 集合类型参数

    - ```java
      //集合参数
      @RequestMapping("/listParam")
      @ResponseBody
      public String listParam(@RequestParam List<String> list){
          System.out.println("集合参数传递 list ==> "+list);
          return "{module：list param}";
      }
      ```

    - ![](D:\mybatis笔记\images\ssm51.png)

### 7.请求与响应

请求参数（传递json数据）

```xml
<!--导入json坐标处理jar包-->
<dependency>
  <groupId>com.fasterxml.jackson.core</groupId>
  <artifactId>jackson-databind</artifactId>
  <version>2.9.0</version>
</dependency>
```

- json数组

  - ```java
    @Configuration
    @ComponentScan("com.yyue.controller")
    //开启由json数据转换成对象的数据
    @EnableWebMvc
    public class SpringMvcConfig {
    }
    ```

  - ```java
    //集合参数：json格式
    @RequestMapping("/listParamForJson")
    @ResponseBody
    public  String listParamForJson(@RequestBody List<String> likes){
        System.out.println("list comman(json) 参数传递 list==> "+ likes);
        return "{module:list common for json param}";
    }
    ```

  - ![](D:\mybatis笔记\images\ssm52.png)

- json对象(POJO)

  - ```java
    //POJO参数：json格式
    @RequestMapping("/pojoParamForJson")
    @ResponseBody
    public String pojoParamForJson(@RequestBody User user){
        System.out.println("ojo(json)参数传递 user==> "+user);
        return "{module:pojo for json param}";
    }
    ```

  - ![](D:\mybatis笔记\images\ssm53.png)

- json数组(POJO)

  - ```java
    //POJO参数：json格式
    @RequestMapping("/listPojoParamForJson")
    @ResponseBody
    public String listPojoParamForJson(@RequestBody List<User> list){
        System.out.println("ojo(json)参数传递 user==> "+list);
        return "{module:pojo for json param}";
    }
    ```

  - ![](D:\mybatis笔记\images\ssm54.png)

总结

![](D:\mybatis笔记\images\ssm55.png)

### 8.请求与响应

**日期类型参数传递**

```java
//日期参数
@RequestMapping("/dataParam")
@ResponseBody
public String dataParam(Date date,
                        @DateTimeFormat(pattern = "yyyy-MM-dd") Date date1,
                        @DateTimeFormat(pattern = "yyyy-MM-dd HH:mm:ss") Date date2){
    System.out.println("参数传递 date==>" +date);
    System.out.println("参数传递 date==>" +date1);
    System.out.println("参数传递 date==>" +date2);
    return "{module:date param}";
}
```

![](D:\mybatis笔记\images\ssm56.png)

![](D:\mybatis笔记\images\ssm57.png)

### 9.请求与响应

响应

- 响应页面

  - ```java
    //响应页面
    @RequestMapping("/toJumpPage")
    public String toJumpPage(){
        System.out.println("跳转页面");
        return "page.jsp";
    }
    ```

- 响应数据

  - 文本数据

    - ```java
      //响应文本数据
      @RequestMapping("/toText")
      @ResponseBody
      public String toText(){
          System.out.println("返回纯文本数据");
          return "response.txt";
      }
      ```

  - json数据

    - ```java
      //响应POJO对象
      @RequestMapping("/toJsonPOJO")
      @ResponseBody
      public User toJsonPOJO(){
          System.out.println("返回json对象数据");
          User user = new User();
          user.setName("yyue");
          user.setAge(18);
          return user;
      }
      ```

![](D:\mybatis笔记\images\ssm58.png)

## 7.rest风格

#### 2.2REST风格入门案例

原始写法

```java
package com.yyue.controller;

import com.yyue.domain.User;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class UserController {
    @RequestMapping("/save")
    @ResponseBody
    public String save(@RequestBody User user){
        System.out.println("user save..."+user);
        return "{'module:user save}";
    }
    @RequestMapping("/delete")
    @ResponseBody
    public String delete(Integer id){
        System.out.println("user delete"+id);
        return "{'module:user delete}";
    }
    @RequestMapping("/update")
    @ResponseBody
    public String update(@RequestBody User user){
        System.out.println("user update"+user);
        return "{'module:user update}";
    }

    @RequestMapping("/getById")
    @ResponseBody
    public String getById(Integer id){
        System.out.println("user getById"+id);
        return "{'module:user getById}";
    }

    @RequestMapping("/getAll")
    @ResponseBody
    public String getAll(){
        System.out.println("user getAll");
        return "{'module:user getAll}";
    }
}
```

修改后

```java
package com.yyue.controller;

import com.yyue.domain.User;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.*;

@Controller
public class UserController {
    @RequestMapping(value = "/users",method = RequestMethod.POST)
    @ResponseBody
    public String save(){
        System.out.println("user save...");
        return "{'module:user save}";
    }
    @RequestMapping(value = "/users/{id}",method = RequestMethod.DELETE)
    @ResponseBody
    public String delete(@PathVariable Integer id){
        System.out.println("user delete"+id);
        return "{'module:user delete}";
    }
    @RequestMapping(value = "/users",method = RequestMethod.PUT)
    @ResponseBody
    public String update(){
        System.out.println("user update");
        return "{'module:user update}";
    }

    @RequestMapping(value = "/users/{id}",method = RequestMethod.GET)
    @ResponseBody
    public String getById(@PathVariable Integer id){
        System.out.println("user getById"+id);
        return "{'module:user getById}";
    }

    @RequestMapping(value = "/users",method = RequestMethod.GET)
    @ResponseBody
    public String getAll(){
        System.out.println("user getAll");
        return "{'module:user getAll}";
    }
}
```

![](D:\mybatis笔记\images\springboot8.png)

![](D:\mybatis笔记\images\springboot9.png)

![](D:\mybatis笔记\images\springboot10.png)

 ![](D:\mybatis笔记\images\springboot11.png)

![](D:\mybatis笔记\images\springboot12.png)

#### 2.3RESTful快速开发 

![](D:\mybatis笔记\images\springboot13.png)

能否简化呢？

```java
package com.yyue.controller;

import com.yyue.domain.User;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.*;

//@Controller
//@ResponseBody
@RestController  // 包含上面两个内容
@RequestMapping("/users")
public class UserController {
//    @RequestMapping(method = RequestMethod.POST)
    @PostMapping
    public String save(){
        System.out.println("user save...");
        return "{'module:user save}";
    }
//    @RequestMapping(value = "/{id}",method = RequestMethod.DELETE)
    @DeleteMapping("/{id}")
    public String delete(@PathVariable Integer id){
        System.out.println("user delete"+id);
        return "{'module:user delete}";
    }
//    @RequestMapping(method = RequestMethod.PUT)
    @PutMapping
    public String update(){
        System.out.println("user update");
        return "{'module:user update}";
    }

//    @RequestMapping(value = "/{id}",method = RequestMethod.GET)
    @GetMapping("/{id}")
    public String getById(@PathVariable Integer id){
        System.out.println("user getById"+id);
        return "{'module:user getById}";
    }

//    @RequestMapping(method = RequestMethod.GET)
    @GetMapping
    public String getAll(){
        System.out.println("user getAll");
        return "{'module:user getAll}";
    }
}
```

![](D:\mybatis笔记\images\springboot14.png)

![](D:\mybatis笔记\images\springboot15.png)

##  8.SSM整合

### 8.1SSM整合

整合流程

1. 创建工程

2. SSM整合

   - Spring

     - SpringConfig
     - ![](D:\mybatis笔记\images\ssm59.png)

   - Mybatis

     - MybatisConfig
     - ![](D:\mybatis笔记\images\ssm62.png)
     - JdbcConfig
     - ![](D:\mybatis笔记\images\ssm60.png)
     - jdbc.properties
     - ![](D:\mybatis笔记\images\ssm61.png)

   - SpringMVC

     - ServletConfig

     - ![](D:\mybatis笔记\images\ssm69.png)

     - SpringMvcConfig

     - ```java
       @Configuration
       @ComponentScan("com.yyue.controller")
       //开启json数据转换成对象数据
       @EnableWebMvc
       public class SpringMvcConfig {
       }
       ```

3. 功能模块

   - 表与实体类
   - dao(接口+自动代理)
   - service（接口+实现类）
     - 业务层接口测试（整合JUnit）
   - controller
     - 表现层接口测试（PostMan）

### 8.2表现层数据封装

- 设置统一数据返回结果类

  - ```java
    public class Result{
    	private Object data;
    	private Integer code;
    	private String msg;
    }
    ```

    ```java
    public class Result {
        //数据
        private Object data;
        //状态码
        private Integer code;
        //消息
        private String message;
    
        public Result(Integer code, Object data, String message) {
            this.data = data;
            this.code = code;
            this.message = message;
        }
    
        public Result() {
        }
    
        public Result(Integer code, Object data) {
            this.data = data;
            this.code = code;
        }
    
        public Object getData() {
            return data;
        }
    
        public void setData(Object data) {
            this.data = data;
        }
    
        public Integer getCode() {
            return code;
        }
    
        public void setCode(Integer code) {
            this.code = code;
        }
    
        public String getMessage() {
            return message;
        }
    
        public void setMessage(String message) {
            this.message = message;
        }
    }
    ```

    ```java
    public class Code {
        public static final Integer SAVE_OK = 20011;
        public static final Integer DELETE_OK = 20021;
        public static final Integer UPDATE_OK = 20031;
        public static final Integer GET_OK = 20041;
    
        public static final Integer SAVE_ERR = 20010;
        public static final Integer DELETE_ERR = 20020;
        public static final Integer UPDATE_ERR = 20030;
        public static final Integer GET_ERR = 20040;
    }
    ```

  - ```java
    //返回统一数据类型
    @RestController
    @RequestMapping("/books")
    public class BookController {
    
        @Autowired
        private BookService bookService;
    
        /**
         * 新增book
         * @param book
         */
        @PostMapping
        public Result save(@RequestBody Book book){
            boolean flag = bookService.save(book);
            return new Result(flag ? Code.SAVE_OK : Code.SAVE_ERR, flag);
        }
    
        @DeleteMapping("/{id}")
        public Result deleteById(@PathVariable Integer id){
            boolean flag = bookService.deleteById(id);
            return new Result(flag ? Code.DELETE_OK : Code.DELETE_ERR, flag);
        }
    
        @PutMapping
        public Result updateById(@RequestBody Book book){
            boolean flag = bookService.updateById(book);
            return new Result(flag ? Code.UPDATE_OK : Code.UPDATE_ERR, flag);
        }
        @GetMapping("/{id}")
        public Result findById(@PathVariable Integer id){
            Book book = bookService.findById(id);
            Integer code = book != null ? Code.GET_OK : Code.GET_ERR;
            String msg = book != null ? "" : "数据查询失败，请重试";
            return new Result(code,book,msg);
        }
        @GetMapping
        public Result findAll(){
            List<Book> books = bookService.findAll();
            Integer code = books != null ? Code.GET_OK : Code.GET_ERR;
            String msg = books != null ? "" : "数据查询失败，请重试";
            return new Result(code,books,msg);
        }
    }
    ```

  - ![](D:\mybatis笔记\images\ssm73.png)

### 8.3异常处理器

1. 出现异常的常见位置与常见诱因
   - 框架内部抛出的异常：因使用不合规导致
   - 数据层抛出的异常：因外部服务器故障导致（如：服务器访问超时）
   - 业务层抛出的异常：因业务逻辑书写错误导致（如：遍历业务书写操作，导致索引异常）
   - 表现层抛出异常：因数据收集、校验等规则导致（不匹配数据类型间导致异常）
   - 工具类抛出的异常：因工具类书写不严谨不够健壮导致（必要释放的连接长期未释放等）

1.各个层级均出现异常，异常处理代码书写在哪一层？

- 所有的异常均抛出到表现层进行处理

2.表现层处理异常，每个方法中单独书写，代码书写量巨大且意义不强，如何解决---------AOP思想

**SpringMVC为我们提供了异常处理器**

**异常处理器**：集中的、统一的处理项目中出现的异常

![](D:\mybatis笔记\images\ssm74.png)

![](D:\mybatis笔记\images\ssm75.png)

![](D:\mybatis笔记\images\ssm76.png)

### 8.4项目异常处理方案

项目异常分类

- 业务异常(BusinessException)
  - 规范的用户行为产生的异常
  - 不规范的用户行为产生的异常
- 系统异常(SystemException)
  - 项目运行过程中可预计且无法避免的异常
- 其他异常(Exception)
  - 编程人员未预期到的异常

处理方案

- 业务异常(BusinessException)
  - 发送对应消息传递给用户，提醒规范操作
- 系统异常(SystemException)
  - 发送固定消息传递给用户，安抚
  - 发送特定消息给运维人员，提醒维护
  - 记录日志
- 其他异常(Exception)
  - 发送固定消息传递给用户，安抚
  - 发送特定消息给运维人员，提醒维护
  - 记录日志

![](D:\mybatis笔记\images\ssm77.png)

![](D:\mybatis笔记\images\ssm78.png)

![](D:\mybatis笔记\images\ssm79.png)

![](D:\mybatis笔记\images\ssm80.png)

![](D:\mybatis笔记\images\ssm81.png)

### 8.5案例：SSM整合标准开发

![](D:\mybatis笔记\images\ssm82.png)

## 9.拦截器

### 9.1拦截器概念

- 拦截器是一种动态拦截方法调用的机制
- 作用
  - 在指定的方法调用前后执行预先设定好的代码
  - 阻止原始方法的执行

拦截器与过滤器区别

- 归属不同：filter是关于天涯servlet技术，Interceptor术语SpringMvc技术
- 拦截内容不同：Filter对所有访问进行增强，Interceptor仅针对Springmvc的访问进行增强

### 9.2入门案例

1.制作拦截器功能类

![](D:\mybatis笔记\images\ssm83.png)

2.配置拦截器要执行的位置

![](D:\mybatis笔记\images\ssm84.png)

![](D:\mybatis笔记\images\ssm85.png)

![](D:\mybatis笔记\images\ssm86.png)

![](D:\mybatis笔记\images\ssm87.png)

### 9.3拦截器参数

![](D:\mybatis笔记\images\ssm88.png)

![](D:\mybatis笔记\images\ssm89.png)

![](D:\mybatis笔记\images\ssm90.png)

### 9.4拦截器工作流程分析

![](D:\mybatis笔记\images\ssm91.png)

## 10.maven进阶

### 1.分模块开发与设计

- 将原始模块按功能拆分成若干子模块，方便模块间的相互调用，接口共享

![](D:\mybatis笔记\images\ssm92.png)

![](D:\mybatis笔记\images\ssm93.png)

![](D:\mybatis笔记\images\ssm94.png)

### 2.依赖管理

- 依赖传递
- 可选依赖
  - ![](D:\mybatis笔记\images\ssm96.png)
- 排除依赖
  - ![](D:\mybatis笔记\images\ssm97.png)

![](D:\mybatis笔记\images\ssm95.png)

### 3.聚合与继承

- 聚合：将多个模块组织成一个整体，同时进行项目构建的过程称为聚合
- 聚合工程：通常是一个不具有业务功能的“空”工程（有且仅有一个pom文件）
- 作用：使用聚合工程可以将多个工程编组，通过对聚合工程进行构建，实现对所包含的模块进行同步构建
  - 当工程中某个模块发生更新时，必须保障工程中与已更新模块关联的模块同步更新，此时可以使用聚合工程来解决批量模块同步构建的问题

![](D:\mybatis笔记\images\ssm98.png)

![](D:\mybatis笔记\images\ssm99.png)

- 继承：描述两个工程间的关系，与java中的继承相似，子工程可以继承父工程中的配置信息，常见于依赖关系的继承
- 作用：简化配置，减少版本冲突
  - ![](D:\mybatis笔记\images\ssm100.png)
  - ![](D:\mybatis笔记\images\ssm101.png)
  - ![](D:\mybatis笔记\images\ssm102.png)
  - ![](D:\mybatis笔记\images\ssm103.png)
  - ![](D:\mybatis笔记\images\ssm104.png)

### 4.属性管理

![](D:\mybatis笔记\images\ssm105.png)

![](D:\mybatis笔记\images\ssm106.png)

![](D:\mybatis笔记\images\ssm107.png)

![](D:\mybatis笔记\images\ssm108.png)

![](D:\mybatis笔记\images\ssm109.png)

![](D:\mybatis笔记\images\ssm110.png)

其他属性

- 属性列表
  - 自定义属性
  - 内置属性
  - Setting属性
  - Java系统属性
  - 环境变量属性

版本管理

- 工程版本
  - SNAPSHOT（快照版本）
    - 项目开发过程中临时输出的版本，称为快照版本
    - 快照版本会随着开发的进展不断更新
  - RELEASE（发布版本）
    - 项目开发到进入阶段里程碑后，向团队外部发布较为稳定的版本，这种版本所对应的构建文件是稳定的，即便进行功能的后续开发，也不会改变当前发布版本内容，这种版本称为发布版本
  - 发布版本
    - alpha版
    - beta版
    - 纯数字版

### 5.多环境配置与应用

多环境开发

- maven提供配置多种环境的设定，帮助开发者使用过程中快速切换环境
- ![](D:\mybatis笔记\images\ssm111.png)
- ![](D:\mybatis笔记\images\ssm112.png)

打包的时候跳过测试

![](D:\mybatis笔记\images\ssm113.png)

![](D:\mybatis笔记\images\ssm114.png)

### 6.私服

1. 私服简介
   - 独立的服务器，用于解决团队内部的资源共享与资源同步问题
   - Nexus安装与启动
     - 启动服务器（命令行运行）
     - nexus.exe /run nexus
     - 访问服务器（默认端口：8080）
     - http://localhost:8080

1. 私服仓库分类
2. 资源上传与下载
   - ![](D:\mybatis笔记\images\ssm115.png)
   - ![](D:\mybatis笔记\images\ssm116.png)
   - ![](D:\mybatis笔记\images\ssm117.png)













