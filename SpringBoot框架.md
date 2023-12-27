# SpringBoot框架

1.SpringBoot入门程序开发

SpringBoot设计的目的是用来简化Spring应用的初始搭建以及开发过程

**创建springBoot工程的四种方式：**

1. 基于Idea创建SpringBoot工程
2. 基于官网创建SpringBoot工程
3. 基于阿里云创建SpringBoot工程
4. 手工创建Maven工程修改成SpringBoot工程

创建springBoot项目（联网创建版）

![](D:\mybatis笔记\images\springboot2.png)

编写BookController

```java
package com.yyue.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

//Rest模式
@RestController
@RequestMapping("/books")
public class BookController {

    @GetMapping
    public String getById(){
        System.out.println("springboot is running >>>>>>>");
        return "springboot is running >>>>>>";
    }

}
```

入门案例：

最简SpringBoot程序所包含的基础文件

- pom.xml文件
- Application类

第二种方法：（网页版）从官网配置完毕下载导入模块。

第三种方法：阿里云

![](D:\mybatis笔记\images\springboot3.png)

第四种方法：纯手工做法

![](D:\mybatis笔记\images\springboot4.png)

![](D:\mybatis笔记\images\springboot5.png)

隐藏指定文件/文件夹

![](D:\mybatis笔记\images\springboot.png)

### 1.SpringBoot简介

SpringBoot设计的目的是用来简化Spring应用的初始搭建以及开发过程

**Spring程序缺点**

- 依赖设置繁琐
- 配置繁琐

**SpringBoot程序优点**

- 起步依赖（简化依赖配置）
- 自动配置（简化常用工程相关配置）
- 辅助功能（内置服务器）

**入门案例解析：**

- parent

1. 开发SpringBoot程序要继承spring-boot-starter-parent
2. spring-boot-starter-parent中定义了若干个依赖管理
3. 继承parent模块可以避免多个依赖使用相同技术时出现依赖版本冲突
4. 继承parent的形式也可以采用引入依赖的形式实现效果

![](D:\mybatis笔记\images\springboot6.png)

- **starter**

SpringBoot中常见项目名称，定义了当前项目使用的所有依赖坐标，以达到减少依赖配置的目的。

实际开发：

- 使用任意坐标时，仅书写GAV中的G和A，V由SpringBoot提供，除非它未提供对于版本V
- 如发生坐标错误，再指定Version

小结：

1. 开发SpringBoot程序需要导入坐标时通常导入对应的starter
2. 每个不同的starter根据功能不同，通常包含多个依赖坐标
3. 使用starter可以实现快速配置的效果，达到简化配置的目的

- **引导类**

```java
@SpringBootApplication
public class Springboot0101QuickstartApplication {

   public static void main(String[] args) {
      SpringApplication.run(Springboot0101QuickstartApplication.class, args);
      
   }
}
```

- SpringBoot的引导类是Boot工程的执行入口，运行main方法就可以启动项目
- SpringBoot工程运行后初始化Spring容器，扫描引导类所在包加载bean

- **内嵌tomcat**

```java
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

内嵌

```java
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-tomcat</artifactId>
  <version>2.7.6</version>
  <scope>compile</scope>
</dependency>
```

```java
<dependency>
  <groupId>org.apache.tomcat.embed</groupId>
  <artifactId>tomcat-embed-core</artifactId>
  <version>9.0.69</version>
  <scope>compile</scope>
</dependency>
```

不要的可以换

![](D:\mybatis笔记\images\springboot7.png)

内置服务器包括：tomcat(默认)、jetty、undertow

小结：

- 内嵌Tomcat服务器是SpringBoot辅助功能之一
- 内嵌Tomcat工作原理是将Tomcat服务器作为对象运行，并将对象交给Spring容器管理
- 变更内嵌服务器思想是去除现有服务器，添加全新的服务器

### 2.REST开发（补充知识，隶属于SpringMVC）

#### 2.1REST简介

REST（Representational State Transfer），表现形式状态转换，（访问网络资源的格式）

传统风格资源描述形式

- http://localhost/user/getById?id=1
- http://localhost/user/saveUser

REST风格描述形式

- http://localhost/user/1
- http://localhost/user

优点：

- 隐藏资源的访问行为，无法通过地址得知对资源是何种操作
- 书写简化

按照REST风格访问资源时使用行为动作区分对资源进行了何种操作

- http://localhost/users   查询全部用户信息 GET（查询）
- http://localhost/users/1    查询指定用户信息 GET  （查询）
- http://localhost/users    添加用户信息 POST  （新增/保存）
- http://localhost/users    修改用户信息 PUT  (修改/更新)
- http://localhost/users/1   删除用户信息  DELETE  (删除)

**根据REST风格对资源进行访问称为RESTful**

注：

- 上述行为是约定方式，约定不是规范，是可以打破的，所以称REST风格，而不是REST规范
- 描述模块的名称通常使用负数，也就是加s的格式描述，表示此类资源，而非单个资源，例如users、books、accounts

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

### 3.基础配置

做一个纯净的模板

1. 在工作空间中复制对应工程，并修改工程名称
2. 删除与idea相关配置文件，仅保留src目录与pom.xml文件
3. 修改pom.xml文件中的artifactId与新工程/模板名相同
4. 删除name标签(可选)
5. 保留备份工程供后期使用

#### 3.1属性配置

maven项目，配置文件都是放在resources目录下，resources/application.properties

通过键值对配置对应属性，如server.port =80

```properties
# 服务器端口设置
server.port=80
# 修改banner 关闭运行日志图标
spring.main.banner-mode=off
# 设置日志相关  默认info
logging.level.root = info
```

可以通过这个网址https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#application-properties.core.logging.level

官方文档中参考文档第一项：Application properties

![](D:\mybatis笔记\images\springboot16.png)

简化上述

#### 3.2配置文件分类

SpringBoot提供了多种属性配置方式

![](D:\mybatis笔记\images\sprintboot17.png)

SpringBoot提供了3种配置文件的格式

- properties(传统格式/默认格式)
- yml(主流格式)
- yaml

- SpringBoot配置文件加载顺序

  application.properties > application.yml  >  application.yaml

- 常用配置文件种类

  application.yml

不同配置文件中相同配置按照加载优先级相互覆盖，不同配置文件中不同配置全部保留

**自动提示功能消失解决方案**

![](D:\mybatis笔记\images\springboot18.png)

指定SpringBoot配置文件

- setting->Project Structure  -> Facets
- 选中对应项目/工程
- Customize Spring Boot
- 选择配置文件

#### 3.3yaml文件

yaml是一种数据序列化格式

优点：

- 容易阅读
- 容易与脚本语言交互
- 以数据为核心，重数据轻格式

yaml文件扩展名

- .yml(主流)
- .yaml

yaml语法规则

- 大小写敏感
- 属性层级关系使用多行描述，每行结尾使用冒号结束
- 使用缩进表示层级关系，同层级左侧对齐，只允许使用空格（不允许使用Tab键）
- 属性值前面添加空格（属性名与属性值之间使用冒号+空格作为分隔）
- #表示注释

```yml
enterprise:
 name: itcast
 age: 16
 tel: 4006184000
```

核心规则：数据前面要加空格与冒号隔开

![](D:\mybatis笔记\images\springboot19.png)

![](D:\mybatis笔记\images\springboot21.png)

#### 3.4yaml数据读取

![](D:\mybatis笔记\images\springboot22.png)

小结：使用@Value配合SpEL读取单个数据，如果数据存在多层级，依次书写层级名称即可。

![](D:\mybatis笔记\images\springboot23.png)

如何解决上述问题？

![](D:\mybatis笔记\images\springboot24.png)

小结：

1. 在配置文件中可以使用${属性名}方式引用属性值
2. 如果属性中出现特殊字符，可以使用双引号包裹起来作为字符解析

**封装全部数据到Environment对象中 **利用getProperty获取属性

![](D:\mybatis笔记\images\springboot25.png)

小结“

1. 使用Environment对象封装全部配置信息
2. 使用@Autowired自动装配数据到Environment对象中

出现问题：封装到Environment中会一次读完所有属性，但是并不想一次读完这么多属性

解决：读取一部分，把它变成需要的对象

在yml文件中存在这样一组数据

```yml
datasource:
  driver: com.mysql.jdbc.Driver
  url: jdbc:mysql://localhost/springboot_db
  username: root
  password: root
```

1.创建一个对象来封装模型yaml文件对应的数据（MyDataSource.class）

```java
package com.yyue;

import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.stereotype.Component;

//1.定义数据封装模型yaml文件对应的数据
//2.定义为spring管控的bean 
@Component
//3.指定加载的数据  通过这个注解将yaml文件中的数据与整个类中的成员变量相关联
@ConfigurationProperties(prefix = "datasource")
public class MyDataSource {
    //名称要与yaml文件中数据的名称对应
    private String driver;
    private String url;
    private String username;
    private String password;

    public String getDriver() {
        return driver;
    }

    public void setDriver(String driver) {
        this.driver = driver;
    }

    public String getUrl() {
        return url;
    }

    public void setUrl(String url) {
        this.url = url;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    @Override
    public String toString() {
        return "MyDataSource{" +
                "driver='" + driver + '\'' +
                ", url='" + url + '\'' +
                ", username='" + username + '\'' +
                ", password='" + password + '\'' +
                '}';
    }
}
```

2.在controller类中使用

```java
@Autowired
private MyDataSource myDataSource;   //将其注入

//一次调用即可
System.out.println(myDataSource.getDriver());
System.out.println(myDataSource.getUrl());
System.out.println(myDataSource.getUsername());
System.out.println(myDataSource.getPassword());
    
```

![](D:\mybatis笔记\images\springboot26.png)

![](D:\mybatis笔记\images\springboot27.png)

小结：

1. 使用@ConfigurationProperties注解绑定配置信息到封装类中
2. 封装类需要定义为Spring管理的bean，否则无法进行属性注入

### 4.整合第三方技术

#### 4.1整合JUnit

![](D:\mybatis笔记\images\springboot29.png)

1. 导入测试对应的starter（创建工程就有，除非手动创建要自己加入）
2. 测试类使用@SpringBootTest修饰
3. 使用自动装配的形式添加要测试的对象

![](D:\mybatis笔记\images\springboot30.png)

#### 4.2整合MyBatis

1. 勾选Mybatis技术，也就是导入Mybatis对应的starter
2. 数据库连接相关信息转换成配置
3. 数据库SQL映射需要添加@Mapper被容器识别到

![](D:\mybatis笔记\images\springboot31.png)

![](D:\mybatis笔记\images\springboot32.png)

![](D:\mybatis笔记\images\springboot33.png)

**Mysql8.X驱动强制要求设置时区**

- 修改url，添加serverTimezone设定
- 修改Mysql数据库配置

**驱动类过时：提醒更换为com.mysql.cj.jdbc.Driver**

#### 4.3整合MyBatis-Plus

1. 导入新的模块，由于spring框架中没有mybatis-plus的坐标

2. 手工导入mybatis-plus坐标，去maven依赖中查询，导入

   - ```xml
     <dependency>
         <groupId>com.baomidou</groupId>
         <artifactId>mybatis-plus-boot-starter</artifactId>
         <version>3.4.3</version>
     </dependency>
     ```

3. 编写配置环境，连接数据库

   - ```yml
     spring:
       datasource:
         driver-class-name: com.mysql.cj.jdbc.Driver
         url: jdbc:mysql://localhost:3306/ssm_db?serverTimezone=UTC
         username: root
         password: root
     ```

4. 编写实体类，以及dao层

5. dao层直接继承BaseMapper<>,提供了很多方法

   - ```java
     @Mapper
     public interface BookDao extends BaseMapper<Book> {
     }
     ```

6. 测试类中进行测试

#### 4.4整合Druid

导入druid坐标

```xml
<!-- https://mvnrepository.com/artifact/com.alibaba/druid-spring-boot-starter -->
<dependency>
   <groupId>com.alibaba</groupId>
   <artifactId>druid-spring-boot-starter</artifactId>
   <version>1.2.6</version>
</dependency>
```

指定数据源类型

```yml
#配置druid数据源
spring:
  datasource:
    druid:
      driver-class-name: com.mysql.cj.jdbc.Driver
      url: jdbc:mysql://localhost:3306/ssm_db?serverTimezone=UTC
      username: root
      password: root
```

步骤：

1. 整合Druid需要导入Druid对应的starter
2. 根据Druid提供的配置方式进行配置
3. 整合第三方技术通用方式：
   1. 导入对应的starter
   2. 根据提供的配置格式，配置非默认值对应的配置项

### 5.基于SpringBoot的SSMP整合案例

SSMP整合案例

前提：

1. 修改SpringMVC与Mysql坐标
2. 修改配置文件为yml格式
3. 设置端口为80

后：

1. 实体类开发-使用Lombok快速制作实体类

   - ```xml
     <!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
     <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
     </dependency>
     ```

   - ```java
     //使用lombok提供的注解@Data即可省略getter、setter、toString等方法
     @Data
     public class Book {
         private Integer id;
         private String type;
         private String name;
         private String description;
     }
     ```

2. Dao开发-整合MybatisPlus，制作数据层测试类

   - ```xml
     <dependency>
        <groupId>com.baomidou</groupId>
        <artifactId>mybatis-plus-boot-starter</artifactId>
        <version>3.4.3</version>
     </dependency>
     
     <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>druid-spring-boot-starter</artifactId>
        <version>1.2.6</version>
     </dependency>
     ```

   - ```yml
     #给每个表增加前缀
     mybatis-plus:
       global-config:
         db-config:
     #      table-prefix: tbl_
           #自增策略
           id-type: auto
     ```

   - 数据层继承BaseMapper接口，提供许多增删改查方法

   - 测试数据层接口

   **为了方便调试：可以开启MyBatisPlus日志**

   - ```yml
     #给每个表增加前缀
     mybatis-plus:
       configuration:
         log-impl: org.apache.ibatis.logging.stdout.StdOutImpl
     ```

   **分页查询**

   - 1.使用IPage封装分页数据

   - ![](D:\mybatis笔记\images\springboot34.png)
   - 2.分页操作依赖MYbatisPlus分页拦截器实现
   - ![](D:\mybatis笔记\images\springboot35.png)

   **按条件查询**（两种方式）

   1. 使用QueryWrapper对象封装查询条件
   2. 推荐使用LambdaQueryWrapper对象
   3. 所有查询操作封装成方法调用
   4. 查询条件支持动态条件拼装

   - ```java
     //按条件查询
     @Test
     public void getBy(){
        QueryWrapper<Book> qw = new QueryWrapper<>();
        qw.like("name","1");
        System.out.println(bookDao.selectList(qw));
     }
     
     //另外一种lambda表达式类型的按条件查询
     @Test
     public void getBy2(){
        String name = "1";
        //效果一样，只是为了防止字段名写错
        LambdaQueryWrapper<Book> lqw = new LambdaQueryWrapper<>();
        lqw.like(name != null,Book::getName,name);
        bookDao.selectList(lqw);
     }
     ```

   - ![](D:\mybatis笔记\images\springboot36.png)

   - ![](D:\mybatis笔记\images\springboot37.png)

3. Service开发-基于MybatisPlus进行增量开发，制作业务层测试类

   1. Service接口名称定义成业务名称，并与Dao接口名称进行区分
   2. 制作测试类测试Service功能是否有效

   - ```java
     public interface BookService {
         boolean save(Book book);
         boolean update(Book book);
         boolean delete(Integer id);
         Book getById(Integer id);
         List<Book> getAll();
         IPage<Book> getPage(int currentPage, int pageSize);
     }
     ```

   - ```java
     @Service
     public class BookServiceImpl implements BookService {
         @Autowired
         private BookDao bookDao;
         @Override
         public boolean save(Book book) {
             return bookDao.insert(book) > 0;
         }
     
         @Override
         public boolean update(Book book) {
             return bookDao.updateById(book) > 0;
         }
     
         @Override
         public boolean delete(Integer id) {
             return bookDao.deleteById(id) > 0;
         }
     
         @Override
         public Book getById(Integer id) {
             return bookDao.selectById(id);
         }
     
         @Override
         public List<Book> getAll() {
             return bookDao.selectList(null);
         }
          @Override
         public IPage<Book> getPage(int currentPage, int pageSize) {
             IPage<Book> page = new Page<>();
             page.setCurrent(currentPage);
             page.setSize(pageSize);
             bookDao.selectPage(page,null);
             return page;
         }
     }
     ```

   - 由于后期每个模块重复代码过多，所以MyBatisPlus提供了业务层接口

   - **业务层开发——快速开发**

   - 步骤

     1. 使用通用接口(IService<T>)快速开发Service
     2. 使用通用实现类（ServiceImpl<M,T>）快速开发ServiceImpl
     3. 可以在通用接口基础上做功能重载或功能追加
     4. 注意重载时不要覆盖原始操作，避免原始提供的功能丢失

   - 使用MyBatisPlus提供有业务层通用接口（IService<T>）与业务层通用实现类（ServiceImpl<M,T>）

     - ```java
       public interface IBookService extends IService<Book> {
       }
       ```

     - ```java
       @Service
       public class BookServiceImpl extends ServiceImpl<BookDao, Book> implements IBookService {
       }
       ```

   - 在通用类基础上做功能重载或功能追加

   - 注意重载时不要覆盖原始操作，避免原始提供的功能丢失

   - ![](D:\mybatis笔记\images\springboot38.png)

   - ![](D:\mybatis笔记\images\springboot39.png)

4. Controller开发-基于Restful开发，使用postman接口测试功能

   - ```java
     @RestController
     @RequestMapping("/books")
     public class BookController {
         @Autowired
         private IBookService iBookService;
         @PostMapping
         public Boolean save(@RequestBody Book book){
             return iBookService.save(book);
         }
         @DeleteMapping("/{id}")
         public Boolean delete(@PathVariable Integer id){
             return iBookService.removeById(id);
         }
         @PutMapping
         public Boolean update(@RequestBody Book book){
             return iBookService.updateById(book);
         }
         @GetMapping("/{id}")
         public Book getById(@PathVariable Integer id){
             return iBookService.getById(id);
         }
         @GetMapping
         public List<Book> getAll(){
             return iBookService.list();
         }
         @GetMapping("/{currentPage}/{pageSize}")
         public List<Book> getPage(@PathVariable Integer currentPage, @PathVariable Integer pageSize){
             return iBookService.getPage(currentPage,pageSize).getRecords();
         }
     }
     ```

   - ```java
     @Override
     public IPage<Book> getPage(Integer currentPage, Integer pageSize) {
         IPage<Book> page =  new Page<>(currentPage,pageSize);
         return bookDao.selectPage(page,null);
     }
     ```

5. Controller开发-前后端开发协议制作

   - 设计表现层返回结果的模型类，用于后端与前端进行数据格式统一，也成为前后端数据协议

     - 1.设计统一的返回值结果类型便于前端开发读取数据

     - 2.返回值结果类型可以根据需求自行设定，没有固定格式

     - 3.返回值结果模型类用于后端与前端进行数据格式统一，也称为前后端数据协议

     - ```java
       @Data
       public class R {
           private boolean flag;
           private Object data;
       
           public R() {
           }
       
           public R(boolean flag) {
               this.flag = flag;
           }
       
           public R(boolean flag, Object data) {
               this.flag = flag;
               this.data = data;
           }
       }
       ```

     - ```java
       @RestController
       @RequestMapping("/books")
       public class BookController {
           @Autowired
           private IBookService iBookService;
           @PostMapping
           public R save(@RequestBody Book book){
               return new R(iBookService.save(book));
           }
           @DeleteMapping("/{id}")
           public R delete(@PathVariable Integer id){
               return new R(iBookService.removeById(id));
           }
           @PutMapping
           public R update(@RequestBody Book book){
               return new R(iBookService.updateById(book));
           }
           @GetMapping("/{id}")
           public R getById(@PathVariable Integer id){
               return new R(true,iBookService.getById(id));
           }
           @GetMapping
           public R getAll(){
               return new R(true,iBookService.list());
           }
           @GetMapping("/{currentPage}/{pageSize}")
           public R getPage(@PathVariable Integer currentPage, @PathVariable Integer pageSize){
               return new R(true,iBookService.getPage(currentPage,pageSize).getRecords());
           }
       }
       ```

6. 页面开发-基于VUE+ElementUI制作，前后端联调，页面数据处理，页面消息处理

   - 列表、新增、修改、删除、分页、查询
   - 异常处理
   - 按条件查询-页面功能调整、Controller修正功能、Service修正功能

   1.前后端协议联调

   - 前后端分离结构设计中页面归属前端服务器

   - 单体工程中页面放置在resources目录下的static目录中（建议执行clean）

   - 前端发送异步请求，调用后端接口

   - ```html
     getAll() {
         //发送异步请求
         axios.get("/books").then((res) => {
             console.log(res.data);
         });
     },
     ```

   - ```vue
     //弹出添加窗口
     handleCreate() {
         this.dialogFormVisible = true;
         this.resetForm();
     },
     //重置表单
     resetForm() {
         this.formData = {};
     },
     //添加
     handleAdd () {
         axios.post("/books", this.formData).then((res) => {
         if (res.data.flag){
            this.dialogFormVisible = false;//关闭弹层
            this.$message.success("添加成功");
         }else {
            this.$message.error("添加失败");
         }
         }).finally(()=>{
              this.getAll();
      });},
     //取消
     cancel(){
       //关闭弹层
       this.dialogFormVisible = false;
       this.dialogFormVisible4Edit = false;
       this.$message.info("当前操作取消！");
     },
     ```

   - 删除：请求方式使用Delete调用后台对应操作

   - 删除操作需要传递当前行数据对应的id值到后台

   - 删除操作结束后动态刷新页面加载数据

   - 根据操作结果不同，显示对应的提示信息

   - 删除操作前弹出提示框避免误操作

   - ```html
     // 删除
     handleDelete(row) {
         // console.log(row);
         this.$confirm("删除的数据将不可恢复，是否继续？", "提示", {type: "info"}).then(() => {
             axios.delete("/books/" + row.id).then(res => {
                 if (res.data.flag) {
                     this.$message.success("删除成功");
                 } else {
                     this.$message.error("删除失败");
                 }
             }).finally(() => {
                 this.getAll();
             });
         }).catch(() => {
             this.$message.info("取消操作");
         });
     },
     ```

   - 修改：请求方式使用put调用后台对应操作

   - 修改操作结束后动态刷新页面加载数据

   - 根据操作结果不同，显示对应的提示信息

   - ```html
     //弹出编辑窗口
     handleUpdate(row) {
         // 发送异步请求
         axios.get("/books/" + row.id).then(res => {
             // console.log(res.data);
             if (res.data.flag && res.data.data != null) {
                 this.dialogFormVisible4Edit = true;
                 this.formData = res.data.data;
             } else {
                 this.$message.error("数据同步失败，自动刷新");
             }
         }).finally(() => {
             this.getAll();
         });
     },
     ```

   - ```
     //修改
     handleEdit() {
         axios.put("/books", this.formData).then(res => {
             // 判断当前操作是否成功
             if(res.data.flag) {
                 // 1.关闭弹层
                 this.dialogFormVisible4Edit = false;
                 this.$message.success("修改成功");
             } else {
                 this.$message.error("修改失败");
             }
         }).finally(() => {
             // 2.重新加载数据
             this.getAll();
         });
     },
     ```

   - 异常处理

   - ```java
     @RestControllerAdvice
     public class ProjectExceptionAdvice {
         //拦截所有的异常信息
         @ExceptionHandler
         public R doException(Exception e){
             e.printStackTrace();
             return new R("发生异常！！！！");
         }
     }
     ```

   - 分页查询

   - ```html
     getAll() {
         //发送异步请求
         axios.get("/books/"+this.pagination.currentPage+"/"+this.pagination.pageSize).then((res) => {
             // console.log(res.data);
             this.pagination.currentPage = res.data.data.current;
             this.pagination.pageSize = res.data.data.size;
             this.pagination.total = res.data.data.total;
             this.dataList = res.data.data.records;
         });
     },
     //切换页码
      handleCurrentChange(currentPage) {
          // 修改页码值为当前选中的页码值
          this.pagination.currentPage = currentPage;
          // 执行查询
          this.getAll();
      },
     ```

   - 删除功能维护

   - 对查询结果进行校验，如果当前页码值大于最大页码值，使用最大页码值作为当前页码值重新查询

   - ```html
     @GetMapping("/{currentPage}/{pageSize}")
     public R getPage(@PathVariable Integer currentPage, @PathVariable Integer pageSize){
         IPage<Book> page = iBookService.getPage(currentPage,pageSize);
         //如果当前页码值大于总页码值，则重新执行查询操作,使用最大页码值作为当前页码值
         if (currentPage > page.getPages()){
             page = iBookService.getPage((int)page.getPages(), pageSize);
         }
         return new R(true,page);
     }
     ```

   - 按条件查询

   - ```html
     // //分页查询
     getAll() {
         //组织参数，拼到url
         // console.log(this.pagination.type);
         param = "?type="+this.pagination.type;
         param += "&name="+this.pagination.name;
         param += "&description="+this.pagination.description;
         console.log(param);
         //发送异步请求
         axios.get("/books/"+this.pagination.currentPage+"/"+this.pagination.pageSize+param).then((res) => {
             // console.log(res.data);
             this.pagination.currentPage = res.data.data.current;
             this.pagination.pageSize = res.data.data.size;
             this.pagination.total = res.data.data.total;
             this.dataList = res.data.data.records;
         });
     },
     ```

     ```java
     @Override
     public IPage<Book> getPage(Integer currentPage, Integer pageSize, Book book) {
         LambdaQueryWrapper<Book> lq = new LambdaQueryWrapper<Book>();
         lq.like(Strings.isNotEmpty(book.getType()),Book::getType,book.getType());
         lq.like(Strings.isNotEmpty(book.getName()),Book::getName,book.getName());
         lq.like(Strings.isNotEmpty(book.getDescription()),Book::getDescription,book.getDescription());
         IPage<Book> page = new Page<>(currentPage, pageSize);
         bookDao.selectPage(page,lq);
         return page;
     }
     ```


## 二、Springboot运维实用篇

1.springboot项目快速启动

- 对springboot项目打包(执行Maven构建指令package)
  - mvn package
- 运行项目
  - java -jar springboot.jar
- 可能会出现的端口占用错误
- ![](D:\mybatis笔记\images\springboot40.png)

linux系统上启动项目

- 上传文件到linux系统

- 运行

  - ```
    java -jar jar包名称
    ```

- 后台运行

  - ```
    nohup java -jar springboot_08_ssmp-0.0.1-SNAPSHOT.jar > server.log 2>&1 &
    ```

- 查询端口

  - ```
    ps -ef | grep "java -jar"
    ```

- 临时属性设置

- 带属性数启动SpringBoot

  - ```
    java -jar springboot_08_ssmp-0.0.1-SNAPSHOT.jar --server.port=8081
    ```

- 携带多个属性启动SpringBoot，属性间使用空格分隔

![](D:\mybatis笔记\images\springboot41.png)

![](D:\mybatis笔记\images\springboot42.png)

配置文件分类

- 配置文件可以改名称，通过启动参数设定
- 配置文件可以修改路径，通过启动参数设定
- 微服务开发中配置文件通过配置中心进行设置

- ![](D:\mybatis笔记\images\springboot43.png)
- ![](D:\mybatis笔记\images\springboot44.png)
- ![](D:\mybatis笔记\images\springboot45.png)

总结：

1. springboot在开发和运行环境均支持使用临时参数修改工程配置
2. springboot支持4级配置文件，应用于开发与线上环境进行配置的灵活设置
3. springboot支持使用自定义配置文件的形式修改配置文件存储位置
4. 基于微服务开发时，配置文件将使用配置中心进行管理

### 3.多环境开发

#### 1.yaml版

1. 一个文件中

- ![](D:\mybatis笔记\images\springboot47.png)

1. 多个文件
   - ![](D:\mybatis笔记\images\springboot48.png)

总结：

1. 可以使用独立配置文件定义环境属性
2. 独立配置文件便于线上系统维护更新并保障系统安全性

#### 2.properties版

![](D:\mybatis笔记\images\springboot49.png)

#### 3.多环境开发独立配置文件2

![](D:\mybatis笔记\images\springboot50.png)

![](D:\mybatis笔记\images\springboot51.png)

总结：多环境开发使用group属性设置配置文件分组，便于线上维护管理

#### 4.maven与springboot多环境兼容

![](D:\mybatis笔记\images\springboot52.png)

![](D:\mybatis笔记\images\springboot53.png)

总结：

1. 当maven与springboot同时多环境进行控制时，以maven为主，springboot使用@..@占位符读取maven对应的配置属性值
2. 基于springboot读取maven配置属性的前提下，如果在idea下测试工程时pom.xml每次更新需要手动compile方可生效

### 4.日志

![](D:\mybatis笔记\images\springboot54.png)

日志级别：

- ![](D:\mybatis笔记\images\springboot55.png)

![](D:\mybatis笔记\images\springboot56.png)

![](D:\mybatis笔记\images\springboot57.png)

![](D:\mybatis笔记\images\springboot58.png)

![](D:\mybatis笔记\images\springboot59.png)

![](D:\mybatis笔记\images\springboot60.png)

## 三、实用开发篇

### 1.启动热部署

步骤：

1. 开启开发者工具

   1. ```xml
      <dependency>
         <groupId>org.springframework.boot</groupId>
         <artifactId>spring-boot-devtools</artifactId>
      </dependency>
      ```

2. 激活热部署：ctrl + F9

**注：热部署仅仅加载当前开发者自定义开发的资源，不加载jar资源**

但是上述后续步骤还是麻烦，所以利用下述方法

- 在settings->build->compiler->build project automatically勾选，
- ctrl+alt+shift+/  打开register，勾选compiler.automake.allow.when.app.running
- 之后，idea失去焦点5秒后，就会自动热部署

但并不是所有的文件都需要参与热部署，可以通过在配置文件中设置不参与热部署的文件

- 自定义不参与重启排除项

  - ```yml
    devtools:
    	restart:
    		exclude: public/**,static/**
    ```

### 2.第三方bean属性绑定

#### 2.1@ConfigurationProperties

- 使用@ConfigurationProperties给封装的对象进行属性注入

- ```java
  @Component
  @ConfigurationProperties(prefix = "servers")
  @Data
  public class ServerConfig {
      private int port;
      private String ipAddress;
      private long timeout;
  }
  ```

- ```
  servers:
    port: 8080
    ipAddress: 192.168.88.128
    timeout: -1
  ```



- 使用@ConfigurationProperties为第三方bean绑定属性

- ```java
  @Bean
  @ConfigurationProperties(prefix = "datasource")
  public DruidDataSource druidDataSource(){
     DruidDataSource druidDataSource = new DruidDataSource();
     return druidDataSource;
  }
  ```

- ```yml
  datasource:
    DriverClassName: com.mysql.cj.jdbc.Driver
    Url: jdbc:mysql://localhost:3306/ssm_db
    Username: root
    Password: root
  ```

![](D:\mybatis笔记\images\springboot61.png)

![](D:\mybatis笔记\images\springboot62.png)

#### 2.2宽松绑定/松散绑定

上述出现一个问题，将配置文件中的datasource改编成dataSource绑定就会出现错误

宽松绑定：

- ![](D:\mybatis笔记\images\springboot63.png)
- 但是@Value不支持宽松绑定

解决上述问题：绑定前缀命名规则：仅能使用纯小写字母、数字、下划线作为合法的字符

- ![](D:\mybatis笔记\images\springboot64.png)

#### 2.3常用计量单位绑定

springboot支持JDK8提供的时间与空间计量单位

- Duration类型，利用注解可以设置该类型数据的单位

![](D:\mybatis笔记\images\springboot65.png)

#### 2.4数据校验

1.添加JSR303规范坐标与Hibernate校验框架对应坐标

```xml
<!-- https://mvnrepository.com/artifact/javax.validation/validation-api -->
<dependency>
   <groupId>javax.validation</groupId>
   <artifactId>validation-api</artifactId>
</dependency>

<!-- https://mvnrepository.com/artifact/org.hibernate.validator/hibernate-validator -->
<dependency>
   <groupId>org.hibernate.validator</groupId>
   <artifactId>hibernate-validator</artifactId>
</dependency>
```

```yml
servers:
  port: 8080
```

```java
@Validated //开启校验
public class ServerConfig {
    @Max(value = 9000, message = "port最大不能超过9000")
    private int port;
```

### 3.测试

#### 3.1加载测试专用属性

- 启动测试环境时可以通过properties参数设置测试环境专用的属性

```java
//properties属性可以为当前测试用例添加临时的属性配置
@SpringBootTest(properties = {"test.prop = testValue1"}) //添加临时属性
public class PropertiesAndArgsTest {
    @Value("${test.prop}")
    private String msg;

    @Test
    public void testProperties(){
        System.out.println(msg);
    }
}
```

- 可以通过args参数设置测试环境专用的传入参数

```java
//args可以为当前测试用例添加临时的命令参数
@SpringBootTest(args = {"--test.prop=testValue2"})
public class PropertiesAndArgsTest {
    @Value("${test.prop}")
    private String msg;

    @Test
    public void testProperties(){
        System.out.println(msg);
    }
}
```

#### 3.2加载测试专用配置

在本次测试中加入一个外部的bean辅助测试

- 使用@Import注解加载当前测试类专用的配置

- ```java
  
  @Configuration
  public class MsgConfig {
      @Bean
      public String msg(){
          return "msg is running...";
      }
  }
  ```

- ```java
  @Import(MsgConfig.class)
  public class ConfigurationTest {
      @Autowired
      private String msg;
  
      @Test
      public void testConfiguration(){
          System.out.println(msg);
      }
  }
  ```

#### 3.3web层测试回滚

web环境模拟测试

- 模拟端口

  - ```java
    @SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.DEFINED_PORT) //定义的端口
    //可选值MOCK、DEFINED_PORT、RANDOM_PORT、NONE
    public class WebTest {
        @Test
        public void testWeb(){
        }
    }
    ```

- web环境测试

  - ```java
    @SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT) //随机端口
    @AutoConfigureMockMvc //开启虚拟MVC调用
    public class WebTest {
        @Test
        // 注入虚拟MVC调用对象
        public void testWeb(@Autowired MockMvc mockMvc) throws Exception {
            //创建虚拟请求，当前访问/books
            MockHttpServletRequestBuilder builder = MockMvcRequestBuilders.get("/books");
            // 执行请求
            mockMvc.perform(builder);
        }
    }
    ```

  - 虚拟请求状态匹配

  - ```java
    @Test
    // 注入虚拟MVC调用对象
    public void testStatus(@Autowired MockMvc mockMvc) throws Exception {
        //创建虚拟请求，当前访问/books
        MockHttpServletRequestBuilder builder = MockMvcRequestBuilders.get("/books");
        // 执行请求
        ResultActions actions = mockMvc.perform(builder);
    
        //设定预期值与真实值进行比较，成功测试则通过，失败测试失败
        //定义本次调用的预期值
        StatusResultMatchers statusResultMatchers = MockMvcResultMatchers.status();
        //预计本次调用时成功的：状态200
        ResultMatcher ok = statusResultMatchers.isOk();
        //添加预计值到本次调用过程中进行对比
        actions.andExpect(ok);
    }
    ```

  - 虚拟机请求体匹配

  - ```java
    @Test
    // 注入虚拟MVC调用对象
    public void testStatus(@Autowired MockMvc mockMvc) throws Exception {
        //创建虚拟请求，当前访问/books
        MockHttpServletRequestBuilder builder = MockMvcRequestBuilders.get("/books");
        // 执行请求
        ResultActions actions = mockMvc.perform(builder);
    
        //设定预期值与真实值进行比较，成功测试则通过，失败测试失败
        //定义本次调用的预期值
        ContentResultMatchers content = MockMvcResultMatchers.content();
        //定义预期执行结果
        ResultMatcher result = content.string("springboot ...");
        //添加预计值到本次调用过程中进行对比
        actions.andExpect(result);
    }
    ```

  - 虚拟请求体（json）匹配

  - ```java
    @Test
    // 注入虚拟MVC调用对象
    public void testDomain(@Autowired MockMvc mockMvc) throws Exception {
        //创建虚拟请求，当前访问/books
        MockHttpServletRequestBuilder builder = MockMvcRequestBuilders.get("/books");
        // 执行请求
        ResultActions actions = mockMvc.perform(builder);
    
        //设定预期值与真实值进行比较，成功测试则通过，失败测试失败
        //定义本次调用的预期值
        ContentResultMatchers content = MockMvcResultMatchers.content();
        ResultMatcher result = content.json("{\"id\":1,\"type\":\"计算机视觉1\",\"name\":\"深度学习算法\",\"description\":\"cnn、rnn等....\"}");
        //添加预计值到本次调用过程中进行对比
        actions.andExpect(result);
    }
    ```

  - 虚拟请求体(Content-Type)匹配

  - ```java
    @Test
    // 注入虚拟MVC调用对象
    public void testContentType(@Autowired MockMvc mockMvc) throws Exception {
        //创建虚拟请求，当前访问/books
        MockHttpServletRequestBuilder builder = MockMvcRequestBuilders.get("/books");
        // 执行请求
        ResultActions actions = mockMvc.perform(builder);
    
        //设定预期值与真实值进行比较，成功测试则通过，失败测试失败
        //定义本次调用的预期值
        HeaderResultMatchers header = MockMvcResultMatchers.header();
        ResultMatcher resultHeader = header.string("Content-Type", "application/json");
        //添加预计值到本次调用过程中进行对比
        actions.andExpect(resultHeader);
    }
    ```

  - 实际上虚拟请求的使用：任何一个错误都通过不了

  - ```java
    @Test
    public void testGetById(@Autowired MockMvc mockMvc) throws Exception {
        //创建虚拟请求，当前访问/books
        MockHttpServletRequestBuilder builder = MockMvcRequestBuilders.get("/books");
        // 执行请求
        ResultActions actions = mockMvc.perform(builder);
    
        ContentResultMatchers content = MockMvcResultMatchers.content();
        ResultMatcher result = content.string("springboot1 ...");
        actions.andExpect(result);
    
        HeaderResultMatchers header = MockMvcResultMatchers.header();
        ResultMatcher resultHeader = header.string("Content-Type", "application/json");
        actions.andExpect(resultHeader);
        
        ContentResultMatchers content1 = MockMvcResultMatchers.content();
        ResultMatcher result1 = content1.json("{\"id\":1,\"type\":\"计算机视觉1\",\"name\":\"深度学习算法\",\"description\":\"cnn、rnn等....\"}");
        actions.andExpect(result1);
    }
    ```

#### 3.4测试层测试回滚

添加事务注解

![](D:\mybatis笔记\images\springboot67.png)

#### 3.5测试用例数据设定

![](D:\mybatis笔记\images\springboot66.png)

### 4.数据层解决方案

#### 4.1SQL

现有数据层解决方案技术选型

- Druid+ Mybatis-Plus +Mysql
- 数据源：Druid
- 持久化技术：Mybatis-plus
- 数据库：Mysql

1.数据源配置：

- springboot提供3种内嵌的数据源对象供开发者原则
  - HikariCP：默认内置数据源对象
  - Tomcat提供DataSource：HikariCP不可用的情况下，且在web环境中，将使用tomcat服务器配置的数据源对象
  - Commons DBCP：上面不可用时，使用

2.内置持久化解决方案--jdbcTemplate

![](D:\mybatis笔记\images\springboot68.png)

![](D:\mybatis笔记\images\springboot69.png)

3.内嵌数据库

springboot提供三种内嵌数据库供开发者选择，提高开发测试效率

- H2
  - ![](D:\mybatis笔记\images\springboot70.png)
  - ![](D:\mybatis笔记\images\springboot71.png)
  - ![](D:\mybatis笔记\images\springboot72.png)
  - ![](D:\mybatis笔记\images\springboot73.png)
- HSQL
- Derby

#### 4.2NOSQL

NOSQL解决方案

- 市面上常见的
  - Redis
    - Redis是一款key-value存储结构的内存级NoSQL数据库
    - 支持多种数据存储格式
    - 支持持久化
    - 支持集群
  
  - 对于springboot整合redis步骤
  
    - 导入springboot整合Redis坐标
  
    - ```xml
      <dependency>
         <groupId>org.springframework.boot</groupId>
         <artifactId>spring-boot-starter-data-redis</artifactId>
      </dependency>
      ```
  
    - 配置Redis
  
    - ```yml
      spring:
        redis:
          port: 6379
          host: localhost
      ```
  
    - RedisTemplate提供操作各种存储类型的接口API
  
    - ```java
      @Autowired
      private RedisTemplate redisTemplate;
      @Test
      	void set() {
      		ValueOperations ops = redisTemplate.opsForValue();
      		ops.set("name","yyue");
      	}
      	@Test
      	void get() {
      		ValueOperations ops = redisTemplate.opsForValue();
      		Object name = ops.get("name");
      		System.out.println(name);
      	}
          @Test
          void hset() {
              HashOperations hops = redisTemplate.opsForHash();
              hops.put("info","a","aa");
          }
          @Test
          void hget() {
              HashOperations hops = redisTemplate.opsForHash();
              Object name = hops.get("info","a");
              System.out.println(name);
          }
      ```
  
    - 利用RedisTemplate出现控制台与idea不统一的问题
  
    - 原因：RedisTemplate获取类型为object泛型，而StringRedisTemplate获取类型为字符串类型，控制台操作的类型为string类型，所以可以使用StringRedisTemplate，则可以同步。
  
    - springboot整合redis客户端选择
  
      - 默认：lettcue
      - jedis
  
    - 上述Redis默认使用lettuce技术
  
    - 可以通过client-type： jedis属性修改成jedis
  
    - 关于lettcus与jedis区别
  
      - jedis连接Redis服务器是直连模式，当多线程模式下使用jedis会存在线程安全问题，解决方案可以通过配置连接池使每个连接专用，这样整体性能就大受影响
      - lettcus基于Netty框架进行与redis服务器连接，底层设计中采用StatefulRedisConnection。StatefulRedisConnection自身是线程安全的，可以保障并发访问安全问题，所以一个连接可以被多线程复用，当然lettcus也支持多连接实例一起工作。
  
  - Mongodb
  
    - 提出问题：想操作结构化数据（MySQL可以实现，但是响应速度慢），但是又想要很高的响应速度（redis可以实现，但是不能操作结构化数据）
    - 是一个开源、高性能、无模式的文档型数据库。（是最像关系型数据库的非关系型数据库）
  
  Mongodb应用场景
  
  - ![](D:\mybatis笔记\images\springboot74.png)
  
  - ES
  
  #### 4.3
  
  缓存
  
  - 缓存是一种介于数据永久存储介质与数据应用之间的数据临时存储介质
  - 使用缓存可以有效的减少低速数据读取过程的次数（例如磁盘IO），提高系统性能。
  
  缓存使用：
  
  1. 导入缓存技术对应的starter
  
     - ```xml
       <dependency>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter-cache</artifactId>
       </dependency>
       ```
  
  2. 启用缓存
  
     - ```java
       @SpringBootApplication
       @EnableCaching
       public class Springboot16CacheApplication {
          public static void main(String[] args) {
             SpringApplication.run(Springboot16CacheApplication.class, args);
          }
       }
       ```
  
  3. 设置当前操作的结果数据进入缓存
  
     - ```java
       @Override
       @Cacheable(value = "cacheSpace", key = "#id")
       public Book getById(Integer id) {
           return bookDao.selectById(id);
       }
       ```

缓存使用案例——手机验证码

需求：

- 输入手机号获取验证码，组织文档以短信形式发送给用户（页面模拟）
- 输入手机号和验证码验证结果

需求分析：

- 提供controller，传入手机号，业务层通过手机号计算出独有的6位验证码数据，存入缓存后返回此数据

- 提供controller，传入手机号与验证码，业务层通过手机号从缓存中读取验证码进行比对，返回比对结果

- ```java
  @RestController
  @RequestMapping("/sms")
  public class SMSCodeController {
  
      @Autowired
      private SMCCodeService smcCodeService;
      @GetMapping
      public String getCode(String tele){
          String code = smcCodeService.sendMsgToSMS(tele);
          return code;
      }
      @PostMapping
      public boolean checkCode(SMSCode smsCode){
          return smcCodeService.checkCode(smsCode);
      }
  }
  ```

- ```java
  public interface SMCCodeService {
      String sendMsgToSMS(String tele);
      boolean checkCode(SMSCode smsCode);
  }
  ```

- ```java
  @Service
  public class SMCCodeServiceImpl implements SMCCodeService {
      @Autowired
      private CodeUtils codeUtils;
      @Override
  //    @Cacheable(value = "smsCode", key = "#tele")
      @CachePut(value = "smsCode", key = "#tele")
      public String sendMsgToSMS(String tele) {
          String code = codeUtils.generator(tele);
          return code;
      }
      @Override
      public boolean checkCode(SMSCode smsCode) {
          // 取出内存中的验证码与传递过来的验证码比对，如果相同，返回true
          String checkCode = codeUtils.checkCode(smsCode.getTele());
          return smsCode.getCode().equals(checkCode);
      }
  }
  ```

- ```java
  @Component
  public class CodeUtils {
      private String[] patch = {"00000","0000","000","00","0",""};
      public String generator(String tele){
          int hash = tele.hashCode();
          int encryption = 20206666;
          long result = hash ^ encryption;
          long nowTime = System.currentTimeMillis();
          result = result ^ nowTime;
          long code = result % 1000000;
          code = code < 0 ? -code : code;
          String codeStr = code + "";
          int len = codeStr.length();
          return patch[len-1] + codeStr;
      }
      //需要将其放入工具类，加载bean容器该注解才能被读到，若是放在service层相当于方法之间的调用，不会走注解
      @Cacheable(value = "smsCode", key = "#tele")
      public String checkCode(String tele){
          return null;
      }
  }
  ```

  