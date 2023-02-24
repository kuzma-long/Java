# Spring

## 什么是 spring 装配？

> 百度

当 bean 在 Spring 容器中组合在一起时，它被称为装配或 bean 装配。 Spring 容器需要知道需要什么 bean 以及容器应该如何使用依赖注入来将 bean 绑定在一起，同时装配 bean。

Spring 容器能够自动装配 bean。也就是说，可以通过检查 BeanFactory 的内容让 Spring 自动解析 bean 的协作者。

自动装配的不同模式：

- **no** - 这是默认设置，表示没有自动装配。应使用显式 bean 引用进行装配。
- **byName** - 它根据 bean 的名称注入对象依赖项。它匹配并装配其属性与 XML 文件中由相同名称定义的 bean。
- **byType** - 它根据类型注入对象依赖项。如果属性的类型与 XML 文件中的一个 bean 名称匹配，则匹配并装配属性。
- **构造函数** - 它通过调用类的构造函数来注入依赖项。它有大量的参数。
- **autodetect** - 首先容器尝试通过构造函数使用 autowire 装配，如果不能，则尝试通过 byType 自动装配。

## Spring 框架中用到了哪些设计模式？

> 比亚迪，zoom

- **工厂设计模式** : Spring 使用工厂模式通过 `BeanFactory`、`ApplicationContext` 创建 bean 对象。
- **代理设计模式** : Spring AOP 功能的实现。
- **单例设计模式** : Spring 中的 Bean 默认都是单例的。
- **模板方法模式** : Spring 中 `jdbcTemplate`、`hibernateTemplate` 等以 Template 结尾的对数据库操作的类，它们就使用到了模板模式。
- **包装器设计模式** : 我们的项目需要连接多个数据库，而且不同的客户在每次访问中根据需要会去访问不同的数据库。这种模式让我们可以根据客户的需求能够动态切换不同的数据源。
- **观察者模式:** Spring 事件驱动模型就是观察者模式很经典的一个应用。
- **适配器模式** :Spring AOP 的增强或通知(Advice)使用到了适配器模式、spring MVC 中也是用到了适配器模式适配`Controller`。

------

## Spring常见注解？

> zoom

![Spring常用注解](https://cdn.tobebetterjavaer.com/tobebetterjavaer/images/sidebar/sanfene/spring-8d0a1518-a425-4887-9735-45321095d927.png)

**Web**:

- @Controller：组合注解（组合了@Component 注解），应用在 MVC 层（控制层）。
- @RestController：该注解为一个组合注解，相当于@Controller 和@ResponseBody 的组合，注解在类上，意味着，该 Controller 的所有方法都默认加上了@ResponseBody。
- @RequestMapping：用于映射 Web 请求，包括访问路径和参数。如果是 Restful 风格接口，还可以根据请求类型使用不同的注解：
  - @GetMapping
  - @PostMapping
  - @PutMapping
  - @DeleteMapping
- @ResponseBody：支持将返回值放在 response 内，而不是一个页面，通常用户返回 json 数据。
- @RequestBody：允许 request 的参数在 request 体中，而不是在直接连接在地址后面。
- @PathVariable：用于接收路径参数，比如 `@RequestMapping(“/hello/{name}”)`申明的路径，将注解放在参数中前，即可获取该值，通常作为 Restful 的接口实现方法。

**容器**:

- @Component：表示一个带注释的类是一个“组件”，成为 Spring 管理的 Bean。当使用基于注解的配置和类路径扫描时，这些类被视为自动检测的候选对象。同时@Component 还是一个元注解。
- @Service：组合注解（组合了@Component 注解），应用在 service 层（业务逻辑层）。
- @Repository：组合注解（组合了@Component 注解），应用在 dao 层（数据访问层）。
- @Autowired：Spring 提供的工具（由 Spring 的依赖注入工具（BeanPostProcessor、BeanFactoryPostProcessor）自动注入）。
- @Qualifier：该注解通常跟 @Autowired 一起使用，当想对注入的过程做更多的控制，@Qualifier 可帮助配置，比如两个以上相同类型的 Bean 时 Spring 无法抉择，用到此注解
- @Configuration：声明当前类是一个配置类（相当于一个 Spring 配置的 xml 文件）
- @Value：可用在字段，构造器参数跟方法参数，指定一个默认值，支持 `#{} 跟 \${}` 两个方式。一般将 SpringbBoot 中的 application.properties 配置的属性值赋值给变量。
- @Bean：注解在方法上，声明当前方法的返回值为一个 Bean。返回的 Bean 对应的类中可以定义 init()方法和 destroy()方法，然后在`@Bean(initMethod=”init”,destroyMethod=”destroy”)`定义，在构造之后执行 init，在销毁之前执行 destroy。
- @Scope:定义我们采用什么模式去创建 Bean（方法上，得有@Bean） 其设置类型包括：Singleton 、Prototype、Request 、 Session、GlobalSession。

**AOP**:

- @Aspect:声明一个切面（类上） 使用@After、@Before、@Around 定义建言（advice），可直接将拦截规则（切点）作为参数。
  - `@After` ：在方法执行之后执行（方法上）。
  - `@Before`： 在方法执行之前执行（方法上）。
  - `@Around`： 在方法执行之前与之后执行（方法上）。
  - `@PointCut`： 声明切点 在 java 配置类中使用@EnableAspectJAutoProxy 注解开启 Spring 对 AspectJ 代理的支持（类上）。

**事务：**

- @Transactional：在要开启事务的方法上使用@Transactional 注解，即可声明式开启事务。

## Spring 事务

> 百度，华讯网络

https://javaguide.cn/system-design/framework/spring/spring-transaction.html

## Spring 事务的注解不生效，是什么原因

> 百度，华讯网络

**原因一：**是否是数据库引擎设置不对造成的。比如我们最常用的mysql，引擎MyISAM，是不支持事务操作的。需要改成InnoDB才能支持

**原因二：**入口的方法必须是public，否则事务不起作用（这一点由Spring的AOP特性决定的，理论上而言，不public也能切入，但spring可能是觉得private自己用的方法，应该自己控制，不应该用事务切进去吧）。另外private 方法, final 方法 和 static 方法不能添加事务，加了也不生效

**原因三**：Spring的事务管理默认只对出现运行期异常(java.lang.RuntimeException及其子类)进行回滚（至于为什么spring要这么设计：因为spring认为Checked的异常属于业务的，coder需要给出解决方案而不应该直接扔该框架）

**原因四**：@EnableTransactionManagement // 启注解事务管理，等同于xml配置方式的 <tx:annotation-driven />
备注：本系列所有博文的讨论都针对于springboot而不再对spring做说明。
@EnableTransactionManagement 在springboot1.4以后可以不写。框架在初始化的时候已经默认给我们注入了两个事务管理器的Bean（JDBC的DataSourceTransactionManager和JPA的JpaTransactionManager ），其实这就包含了我们最常用的Mybatis和Hibeanate了。当然如果不是AutoConfig的而是自己自定义的，请使用该注解开启事务

**原因五：**请确认你的类是否被代理了（因为spring的事务实现原理为AOP，只有通过代理对象调用方法才能被拦截，事务才能生效）

**原因六：**请确保你的业务和事务入口在同一个线程里，否则事务也是不生效的。

**原因七：**也是我最想要去讲的一个原因：service方法中调用本类中的另一个方法，事务没有生效。

## Spring是如何解决的循环依赖？

> 德胧集团，百度，字节

我们都知道，单例 Bean 初始化完成，要经历三步：

![Bean初始化步骤](https://cdn.tobebetterjavaer.com/tobebetterjavaer/images/sidebar/sanfene/spring-867066f1-49d1-4e57-94f9-4c66a3a8797e.png)

注入就发生在第二步，**属性赋值**，结合这个过程，Spring 通过**三级缓存**解决了循环依赖：

1. 一级缓存 : `Map<String,Object>` **singletonObjects**，单例池，用于保存实例化、属性赋值（注入）、初始化完成的 bean 实例
2. 二级缓存 : `Map<String,Object>` **earlySingletonObjects**，早期曝光对象，用于保存实例化完成的 bean 实例
3. 三级缓存 : `Map<String,ObjectFactory<?>>` **singletonFactories**，早期曝光对象工厂，用于保存 bean 创建工厂，以便于后面扩展有机会创建代理对象。

![三级缓存](https://cdn.tobebetterjavaer.com/tobebetterjavaer/images/sidebar/sanfene/spring-01d92863-a2cb-4f61-8d8d-30ecf0279b28.png)

我们来看一下三级缓存解决循环依赖的过程：

当 A、B 两个类发生循环依赖时： ![循环依赖](https://cdn.tobebetterjavaer.com/tobebetterjavaer/images/sidebar/sanfene/spring-cfc09f84-f8e1-4702-80b6-d115843e81fe.png)

A 实例的初始化过程：

1. 创建 A 实例，实例化的时候把 A 对象⼯⼚放⼊三级缓存，表示 A 开始实例化了，虽然我这个对象还不完整，但是先曝光出来让大家知道

![1](https://cdn.tobebetterjavaer.com/tobebetterjavaer/images/sidebar/sanfene/spring-1a8bdc29-ff43-4ff4-9b61-3eedd9da59b3.png)

1. A 注⼊属性时，发现依赖 B，此时 B 还没有被创建出来，所以去实例化 B
2. 同样，B 注⼊属性时发现依赖 A，它就会从缓存里找 A 对象。依次从⼀级到三级缓存查询 A，从三级缓存通过对象⼯⼚拿到 A，发现 A 虽然不太完善，但是存在，把 A 放⼊⼆级缓存，同时删除三级缓存中的 A，此时，B 已经实例化并且初始化完成，把 B 放入⼀级缓存。

![2](https://cdn.tobebetterjavaer.com/tobebetterjavaer/images/sidebar/sanfene/spring-bf2507bf-96aa-4b88-a58b-7ec41d11bc70.png)

1. 接着 A 继续属性赋值，顺利从⼀级缓存拿到实例化且初始化完成的 B 对象，A 对象创建也完成，删除⼆级缓存中的 A，同时把 A 放⼊⼀级缓存
2. 最后，⼀级缓存中保存着实例化、初始化都完成的 A、B 对象

![5](https://cdn.tobebetterjavaer.com/tobebetterjavaer/images/sidebar/sanfene/spring-022f7cb9-2c83-4fe9-b252-b02bd0fb2435.png)

所以，我们就知道为什么 Spring 能解决 setter 注入的循环依赖了，因为实例化和属性赋值是分开的，所以里面有操作的空间。如果都是构造器注入的化，那么都得在实例化这一步完成注入，所以自然是无法支持了。

# Spring IoC

## IoC 是什么？

> 宁波银行总行、比亚迪，英雄游戏，百度，字节，度小满

**IoC（Inversion of Control:控制反转）** 是一种设计思想，而不是一个具体的技术实现。IoC 的思想就是将原本在程序中手动创建对象的控制权，交由 Spring 框架来管理。不过， IoC 并非 Spring 特有，在其他语言中也有应用。

将对象之间的相互依赖关系交给 IoC 容器来管理，并由 IoC 容器完成对象的注入。这样可以很大程度上简化应用的开发，把应用从复杂的依赖关系中解放出来。 IoC 容器就像是一个工厂一样，当我们需要创建一个对象的时候，只需要配置好配置文件/注解即可，完全不用考虑对象是如何被创建出来的。

IoC 的实现方式有依赖注入。依赖注入指对象被动地接受依赖类而不用自己主动去找，对象不是从容器中查找它依赖的类，而是在容器实例化对象时主动将它依赖的类注入给它。

------

## IoC 容器初始化过程？

**基于 XML 的容器初始化**

当创建一个 ClassPathXmlApplicationContext 时，构造方法做了两件事：① 调用父容器的构造方法为容器设置好 Bean 资源加载器。② 调用父类的 `setConfigLocations` 方法设置 Bean 配置信息的定位路径。

ClassPathXmlApplicationContext 通过调用父类 AbstractApplicationContext 的 `refresh` 方法启动整个 IoC 容器对 Bean 定义的载入过程，`refresh` 是一个模板方法，规定了 IoC 容器的启动流程。在创建 IoC 容器前如果已有容器存在，需要把已有的容器销毁，保证在 `refresh` 方法后使用的是新创建的 IoC 容器。

容器创建后通过 `loadBeanDefinitions` 方法加载 Bean 配置资源，该方法做两件事：① 调用资源加载器的方法获取要加载的资源。② 真正执行加载功能，由子类 XmlBeanDefinitionReader 实现。加载资源时首先解析配置文件路径，读取配置文件的内容，然后通过 XML 解析器将 Bean 配置信息转换成文档对象，之后按照 Spring Bean 的定义规则对文档对象进行解析。

Spring IoC 容器中注册解析的 Bean 信息存放在一个 HashMap 集合中，key 是字符串，值是 BeanDefinition，注册过程中需要使用 synchronized 保证线程安全。当配置信息中配置的 Bean 被解析且被注册到 IoC 容器中后，初始化就算真正完成了，Bean 定义信息已经可以使用且可被检索。Spring IoC 容器的作用就是对这些注册的 Bean 定义信息进行处理和维护，注册的 Bean 定义信息是控制反转和依赖注入的基础。

**基于注解的容器初始化**

分为两种：① 直接将注解 Bean 注册到容器中，可以在初始化容器时注册，也可以在容器创建之后手动注册，然后刷新容器使其对注册的注解 Bean 进行处理。② 通过扫描指定的包及其子包的所有类处理，在初始化注解容器时指定要自动扫描的路径。

------

## 依赖注入的实现方法有哪些？

> 字节

Spring 支持**构造方法注入**、**属性注入**、**工厂方法注入**,其中工厂方法注入，又可以分为**静态工厂方法注入**和**非静态工厂方法注入**。

![Spring依赖注入方法](https://cdn.tobebetterjavaer.com/tobebetterjavaer/images/sidebar/sanfene/spring-491f8444-54ba-4628-b8eb-8418a2197096.png)

- **构造方法注入**

  通过调用类的构造方法，将接口实现类通过构造方法变量传入

  ```java
   public CatDaoImpl(String message){
     this. message = message;
   }
  ```

  ```java
  <bean id="CatDaoImpl" class="com.CatDaoImpl">
    <constructor-arg value=" message "></constructor-arg>
  </bean>
  ```

- **属性注入**

  通过 Setter 方法完成调用类所需依赖的注入

  ```java
   public class Id {
      private int id;
  
      public int getId() { return id; }
  
      public void setId(int id) { this.id = id; }
  }
  ```

  ```java
  <bean id="id" class="com.id ">
    <property name="id" value="123"></property>
  </bean>
  ```

- **工厂方法注入**

  - **静态工厂注入**

    静态工厂顾名思义，就是通过调用静态工厂的方法来获取自己需要的对象，为了让 Spring 管理所有对象，我们不能直接通过"工程类.静态方法()"来获取对象，而是依然通过 Spring 注入的形式获取：

    ```java
    public class DaoFactory { //静态工厂
    
       public static final FactoryDao getStaticFactoryDaoImpl(){
          return new StaticFacotryDaoImpl();
       }
    }
    
    public class SpringAction {
    
     //注入对象
     private FactoryDao staticFactoryDao;
    
     //注入对象的 set 方法
     public void setStaticFactoryDao(FactoryDao staticFactoryDao) {
         this.staticFactoryDao = staticFactoryDao;
     }
    
    }
    ```

    ```java
    //factory-method="getStaticFactoryDaoImpl"指定调用哪个工厂方法
     <bean name="springAction" class=" SpringAction" >
       <!--使用静态工厂的方法注入对象,对应下面的配置文件-->
       <property name="staticFactoryDao" ref="staticFactoryDao"></property>
     </bean>
    
     <!--此处获取对象的方式是从工厂类中获取静态方法-->
    <bean name="staticFactoryDao" class="DaoFactory"
      factory-method="getStaticFactoryDaoImpl"></bean>
    ```

  - **非静态工厂注入**

    非静态工厂，也叫实例工厂，意思是工厂方法不是静态的，所以我们需要首先 new 一个工厂实例，再调用普通的实例方法。

    ```java
    //非静态工厂
    public class DaoFactory {
       public FactoryDao getFactoryDaoImpl(){
         return new FactoryDaoImpl();
       }
     }
    
    public class SpringAction {
      //注入对象
      private FactoryDao factoryDao;
    
      public void setFactoryDao(FactoryDao factoryDao) {
        this.factoryDao = factoryDao;
      }
    }
    ```

    ```java
     <bean name="springAction" class="SpringAction">
       <!--使用非静态工厂的方法注入对象,对应下面的配置文件-->
       <property name="factoryDao" ref="factoryDao"></property>
     </bean>
    
     <!--此处获取对象的方式是从工厂类中获取实例方法-->
     <bean name="daoFactory" class="com.DaoFactory"></bean>
    
    <bean name="factoryDao" factory-bean="daoFactory" factory-method="getFactoryDaoImpl"></bean>
    ```

------

## 依赖注入的相关注解？

`@Autowired`：自动按类型注入，如果有多个匹配则按照指定 Bean 的 id 查找，查找不到会报错。

`@Qualifier`：在自动按照类型注入的基础上再按照 Bean 的 id 注入，给变量注入时必须搭配 `@Autowired`，给方法注入时可单独使用。

`@Resource` ：直接按照 Bean 的 id 注入，只能注入 Bean 类型。

`@Value` ：用于注入基本数据类型和 String 类型。

------

## 依赖注入的过程？

`getBean` 方法获取 Bean 实例，该方***调用 `doGetBean` ，`doGetBean` 真正实现从 IoC 容器获取 Bean 的功能，也是触发依赖注入的地方。

具体创建 Bean 对象的过程由 ObjectFactory 的 `createBean` 完成，该方法主要通过 `createBeanInstance` 方法生成 Bean 包含的 Java 对象实例和 `populateBean` 方法对 Bean 属性的依赖注入进行处理。

在 `populateBean`方法中，注入过程主要分为两种情况：① 属性值类型不需要强制转换时，不需要解析属性值，直接进行依赖注入。② 属性值类型需要强制转换时，首先解析属性值，然后对解析后的属性值进行依赖注入。依赖注入的过程就是将 Bean 对象实例设置到它所依赖的 Bean 对象属性上，真正的依赖注入是通过 `setPropertyValues` 方法实现的，该方法使用了委派模式。

BeanWrapperImpl 类负责对完成初始化的 Bean 对象进行依赖注入，对于非集合类型属性，使用 JDK 反射，通过属性的 setter 方法为属性设置注入后的值。对于集合类型的属性，将属性值解析为目标类型的集合后直接赋值给属性。

当容器对 Bean 的定位、载入、解析和依赖注入全部完成后就不再需要手动创建对象，IoC 容器会自动为我们创建对象并且注入依赖。

------

## Bean 的生命周期？

> 比亚迪，小米，美团

![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2020/2/15/1704860a4de235aa~tplv-t2oaga2asx-zoom-in-crop-mark:4536:0:0:0.awebp)

------

## Bean 的作用范围？

通过 scope 属性指定 bean 的作用范围，包括：

① singleton：单例模式，是默认作用域，不管收到多少 Bean 请求每个容器中只有一个唯一的 Bean 实例。

② prototype：原型模式，和 singleton 相反，每次 Bean 请求都会创建一个新的实例。

③ request：每次 HTTP 请求都会创建一个新的 Bean 并把它放到 request 域中，在请求完成后 Bean 会失效并被垃圾收集器回收。

④ session：和 request 类似，确保每个 session 中有一个 Bean 实例，session 过期后 bean 会随之失效。

⑤ global session：当应用部署在 Portlet 容器时，如果想让所有 Portlet 共用全局存储变量，那么该变量需要存储在 global session 中。

------

## 如何通过 XML 方式创建 Bean？

默认无参构造方法，只需要指明 bean 标签中的 id 和 class 属性，如果没有无参构造方***报错。

静态工厂方法，通过 bean 标签中的 class 属性指明静态工厂，factory-method 属性指明静态工厂方法。

实例工厂方法，通过 bean 标签中的 factory-bean 属性指明实例工厂，factory-method 属性指明实例工厂方法。

------

## 如何通过注解创建 Bean？

`@Component` 把当前类对象存入 Spring 容器中，相当于在 xml 中配置一个 bean 标签。value 属性指定 bean 的 id，默认使用当前类的首字母小写的类名。

`@Controller`，`@Service`，`@Repository` 三个注解都是 `@Component` 的衍生注解，作用及属性都是一模一样的。只是提供了更加明确语义，`@Controller` 用于表现层，`@Service`用于业务层，`@Repository`用于持久层。如果注解中有且只有一个 value 属性要赋值时可以省略 value。

如果想将第三方的类变成组件又没有源代码，也就没办法使用 `@Component` 进行自动配置，这种时候就要使用 `@Bean` 注解。被 `@Bean` 注解的方法返回值是一个对象，将会实例化，配置和初始化一个新对象并返回，这个对象由 Spring 的 IoC 容器管理。name 属性用于给当前 `@Bean` 注解方法创建的对象指定一个名称，即 bean 的 id。当使用注解配置方法时，如果方法有参数，Spring 会去容器查找是否有可用 bean对象，查找方式和 `@Autowired` 一样。

------

## 如何通过注解配置文件？

`@Configuration` 用于指定当前类是一个 spring 配置类，当创建容器时会从该类上加载注解，value 属性用于指定配置类的字节码。

`@ComponentScan` 用于指定 Spring 在初始化容器时要扫描的包。basePackages 属性用于指定要扫描的包。

`@PropertySource` 用于加载 `.properties` 文件中的配置。value 属性用于指定文件位置，如果是在类路径下需要加上 classpath。

`@Import` 用于导入其他配置类，在引入其他配置类时可以不用再写 `@Configuration` 注解。有 `@Import` 的是父配置类，引入的是子配置类。value 属性用于指定其他配置类的字节码。

------

## BeanFactory和FactoryBean的区别？

> zoom

BeanFactory 是一个 Bean 工厂，使用简单工厂模式，是 Spring IoC 容器顶级接口，可以理解为含有 Bean 集合的工厂类，作用是管理 Bean，包括实例化、定位、配置对象及建立这些对象间的依赖。BeanFactory 实例化后并不会自动实例化 Bean，只有当 Bean 被使用时才实例化与装配依赖关系，属于延迟加载，适合多例模式。

FactoryBean 是一个工厂 Bean，使用了工厂方法模式，作用是生产其他 Bean 实例，可以通过实现该接口，提供一个工厂方法来自定义实例化 Bean 的逻辑。FactoryBean 接口由 BeanFactory 中配置的对象实现，这些对象本身就是用于创建对象的工厂，如果一个 Bean 实现了这个接口，那么它就是创建对象的工厂 Bean，而不是 Bean 实例本身。

## @Autowired 和 @Resource 的区别是什么？

> zoom

- `@Autowired` 是 Spring 提供的注解，`@Resource` 是 JDK 提供的注解。
- `Autowired` 默认的注入方式为`byType`（根据类型进行匹配），`@Resource`默认注入方式为 `byName`（根据名称进行匹配）。
- 当一个接口存在多个实现类的情况下，`@Autowired` 和`@Resource`都需要通过名称才能正确匹配到对应的 Bean。`Autowired` 可以通过 `@Qualifier` 注解来显式指定名称，`@Resource`可以通过 `name` 属性来显式指定名称。

------

## Autowired 实现原理

> 百度

# Spring AOP

## AOP 是什么？

> 比亚迪，英雄游戏，百度，字节，度小满

AOP(Aspect-Oriented Programming:⾯向切⾯编程)能够将那些与业务⽆关，却为业务模块所共同调用的逻辑或责任（例如事务处理、⽇志管理、权限控制等）封装起来，便于减少系统的重复代码，降低模块间的耦合度，并有利于未来的可拓展性和可维护性。

 Spring AOP是基于动态代理的，如果要代理的对象，实现了某个接口，那么Spring AOP会使⽤JDK Proxy，去创建代理对象，⽽对于没有实现接口的对象，就⽆法使⽤ JDK Proxy 去进行代理了，这时候Spring AOP会使⽤ Cglib ⽣成⼀个被代理对象的⼦类来作为代理。

------

## AOP 的相关注解有哪些？

`@Aspect`：声明被注解的类是一个切面 Bean。

`@Before`：前置通知，指在某个连接点之前执行的通知。

`@After`：后置通知，指某个连接点退出时执行的通知（不论正常返回还是异常退出）。

`@AfterReturning`：返回后通知，指某连接点正常完成之后执行的通知，返回值使用returning属性接收。

`@AfterThrowing`：异常通知，指方法抛出异常导致退出时执行的通知，和`@AfterReturning`只会有一个执行，异常使用throwing属性接收。

------

## AOP 的相关术语有什么？

`Aspect`：切面，一个关注点的模块化，这个关注点可能会横切多个对象。

`Joinpoint`：连接点，程序执行过程中的某一行为，即业务层中的所有方法。。

`Advice`：通知，指切面对于某个连接点所产生的动作，包括前置通知、后置通知、返回后通知、异常通知和环绕通知。

`Pointcut`：切入点，指被拦截的连接点，切入点一定是连接点，但连接点不一定是切入点。

`Proxy`：代理，Spring AOP 中有 JDK 动态代理和 CGLib 代理，目标对象实现了接口时采用 JDK 动态代理，反之采用 CGLib 代理。

`Target`：代理的目标对象，指一个或多个切面所通知的对象。

`Weaving` ：织入，指把增强应用到目标对象来创建代理对象的过程。

------

## AOP 的过程？

> 百度

Spring AOP 由 BeanPostProcessor 后置处理器开始，这个后置处理器是一个***，可以监听容器触发的 Bean 生命周期事件，向容器注册后置处理器以后，容器中管理的 Bean 就具备了接收 IoC 容器回调事件的能力。BeanPostProcessor 的调用发生在 Spring IoC 容器完成 Bean 实例对象的创建和属性的依赖注入后，为 Bean 对象添加后置处理器的入口是 `initializeBean` 方法。

Spring 中 JDK 动态代理通过 JdkDynamicAopProxy 调用 Proxy 的 `newInstance` 方法来生成代理类，JdkDynamicAopProxy 也实现了 InvocationHandler 接口，`invoke` 方法的具体逻辑是先获取应用到此方法上的拦截器链，如果有拦截器则创建 MethodInvocation 并调用其 `proceed` 方法，否则直接反射调用目标方法。因此 Spring AOP 对目标对象的增强是通过拦截器实现的。

------

## Spring AOP的实现方式

> 百度，字节

**（一）静态代理**

就是在代码里面创建一个代理类，实现目标类的接口，目标对象是代理类的成员变量，外界需要执行方法时，调用代理类的方法，代理类的方法内部先执行额外的操作，日志记录等，然后再调用目标类的方法。

```java
public interface IUserDao {
    void save();
}
public class UserDao implements IUserDao {
    public void save() {
        System.out.println("已经保存数据...");
    }
}
//代理类
public class UserDaoProxy implements IUserDao {
    private IUserDao target;
    public UserDaoProxy(IUserDao iuserDao) {
        this.target = iuserDao;
    } 
    public void save() {
        System.out.println("开启事务...");
        target.save();
        System.out.println("关闭事务...");
    }
}
```

**（二）JDK动态代理**

  **Spring默认使用JDK的动态代理实现AOP，类如果实现了接口，Spring就会使用这种方式实现动态代理**。熟悉`Java`语言的应该会对`JDK`动态代理有所了解。`JDK`实现动态代理需要两个组件，首先第一个就是`InvocationHandler`接口。我们在使用`JDK`的动态代理时，需要编写一个类，去实现这个接口，然后重写`invoke`方法，这个方法其实就是我们提供的代理方法。然后`JDK`动态代理需要使用的第二个组件就是`Proxy`这个类，我们可以通过这个类的`newProxyInstance`方法，返回一个代理对象。生成的代理类实现了原来那个类的所有接口，并对接口的方法进行了代理，我们通过代理对象调用这些方法时，底层将通过反射，调用我们实现的`invoke`方法。

**（三）cglib动态代理**

  `JDK`的动态代理存在限制，那就是被代理的类必须是一个实现了接口的类，代理类需要实现相同的接口，代理接口中声明的方法。若需要代理的类没有实现接口，此时`JDK`的动态代理将没有办法使用，于是`Spring`会使用`CGLib`的动态代理来生成代理对象。`CGLib`直接操作字节码，生成类的子类，重写类的方法完成代理。

CGLIB主要是通过创建一个代理类，继承原来的类，并且重写父类的方法，然后将代理类实例返回，后续调用代理类的方法时，先执行一些额外的AOP相关的记录操作，然后再去执行父类的方法。（由于在Java中子类只能继承父类的非private的属性和方法，所以**由CGLIB创建的代理类，不会包含父类中的final或者private修饰的方法，**aop也无法捕获private相关的方法）

创建一个类，继承MethodInterceptor类，重写intercept方法，接受方法调用。创建一个Enhancer实例，设置代理类的父类为目标类，设置回调。

```java
public static void main(final String[] args) {
    System.setProperty(DebuggingClassWriter.DEBUG_LOCATION_PROPERTY, "/Users/ruiwendaier/Downloads/testaop");
    Enhancer enhancer = new Enhancer();
    enhancer.setSuperclass(Test.class);
    enhancer.setCallback(new MyMethodInterceptor());
    Test test1 = (Test)enhancer.create();
    test1.test();

}
public static class MyMethodInterceptor implements MethodInterceptor {
    @Override
    public Object intercept(Object o, Method method, Object[] objects, MethodProxy methodProxy) throws Throwable {
        System.out.println("Before: "  + method.getName());
        Object object = methodProxy.invokeSuper(o, objects);
        System.out.println("After: " + method.getName());
        return object;
    }
}
public static class Test implements TestInterface {
    public void test() {
        System.out.printf("111111");
    }
}
```

生成的代理类中，对于父类中每一个能够继承重写的方法，动态代理类都会生成两个相应的方法。一个是方法内是直接调用父类(也就是目标类的方法)，一个是生成的对应的动态代理的方法，里面会先调用代理类设置的intercept回调方法，然后再调用父类的方法。在调用时，会直接先调用重写的方法。

## AOP在什么时候会失效

> 百度

# Spring MVC

## SpringMVC 工作原理了解吗?

> zoom

**Spring MVC 原理如下图所示：**

> SpringMVC 工作原理的图解我没有自己画，直接图省事在网上找了一个非常清晰直观的，原出处不明。

![img](https://img-blog.csdnimg.cn/img_convert/de6d2b213f112297298f3e223bf08f28.png)

**流程说明（重要）：**

1. 客户端（浏览器）发送请求， `DispatcherServlet`拦截请求。
2. `DispatcherServlet` 根据请求信息调用 `HandlerMapping` 。`HandlerMapping` 根据 uri 去匹配查找能处理的 `Handler`（也就是我们平常说的 `Controller` 控制器） ，并会将请求涉及到的拦截器和 `Handler` 一起封装。
3. `DispatcherServlet` 调用 `HandlerAdapter`适配执行 `Handler` 。
4. `Handler` 完成对用户请求的处理后，会返回一个 `ModelAndView` 对象给`DispatcherServlet`，`ModelAndView` 顾名思义，包含了数据模型以及相应的视图的信息。`Model` 是返回的数据对象，`View` 是个逻辑上的 `View`。
5. `ViewResolver` 会根据逻辑 `View` 查找实际的 `View`。
6. `DispaterServlet` 把返回的 `Model` 传给 `View`（视图渲染）。
7. 把 `View` 返回给请求者（浏览器）

------

## Spring MVC 有哪些组件？

`DispatcherServlet`：SpringMVC 中的前端控制器，是整个流程控制的核心，负责接收请求并转发给对应的处理组件。

`Handler`：处理器，完成具体业务逻辑，相当于 Servlet 或 Action。

`HandlerMapping`：完成 URL 到 Controller 映射，DispatcherServlet 通过 HandlerMapping 将不同请求映射到不同 Handler。

`HandlerInterceptor`：处理器拦截器，是一个接口，如果需要完成一些拦截处理，可以实现该接口。

`HandlerExecutionChain`：处理器执行链，包括两部分内容：Handler 和 HandlerInterceptor。

`HandlerAdapter`：处理器适配器，Handler执行业务方法前需要进行一系列操作，包括表单数据验证、数据类型转换、将表单数据封装到JavaBean等，这些操作都由 HandlerAdapter 完成。DispatcherServlet 通过 HandlerAdapter 来执行不同的 Handler。

`ModelAndView`：装载模型数据和视图信息，作为 Handler 处理结果返回给 DispatcherServlet。

`ViewResolver`：视图解析器，DispatcherServlet 通过它将逻辑视图解析为物理视图，最终将渲染的结果响应给客户端。

------

## Spring MVC 的相关注解？

`@Controller`：在类定义处添加，将类交给IoC容器管理。

`@RequtestMapping`：将URL请求和业务方法映射起来，在类和方法定义上都可以添加该注解。`value` 属性指定URL请求的实际地址，是默认值。`method` 属性限制请求的方法类型，包括GET、POST、PUT、DELETE等。如果没有使用指定的请求方法请求URL，会报405 Method Not Allowed 错误。`params` 属性限制必须提供的参数，如果没有会报错。

`@RequestParam`：如果 Controller 方法的形参和 URL 参数名一致可以不添加注解，如果不一致可以使用该注解绑定。`value` 属性表示HTTP请求中的参数名。`required` 属性设置参数是否必要，默认false。`defaultValue` 属性指定没有给参数赋值时的默认值。

`@PathVariable`：Spring MVC 支持 RESTful 风格 URL，通过 `@PathVariable` 完成请求参数与形参的绑定。

------

## Spring MVC拦截器

Spring MVC拦截器包含三个方法：preHandle()、postHandle()、afterCompletion()。

preHandle方法在Controller之前执行，若返回false，则终止执行后续的请求。

postHandle方法在Controller之后、模板之前执行。

afterCompletion方法在模板之后执行。

------

# Mybatis

## Mybatis 的优缺点？

**优点**

相比 JDBC 减少了大量代码量，减少冗余代码。

使用灵活，SQL 语句写在 XML 里，从程序代码中彻底分离，降低了耦合度，便于管理。

提供 XML 标签，支持编写动态 SQL 语句。

提供映射标签，支持对象与数据库的 ORM 字段映射关系。

**缺点**

SQL 语句编写工作量较大，尤其是字段和关联表多时。

SQL 语句依赖于数据库，导致数据库移植性差，不能随意更换数据库。

------

## Mybatis 的 XML 文件有哪些标签属性？

`select`、`insert`、`update`、`delete` 标签分别对应查询、添加、更新、删除操作。

`parameterType` 属性表示参数的数据类型，包括基本数据类型和对应的包装类型、String 和 Java Bean 类型，当有多个参数时可以使用 `#{argn}` 的形式表示第 n 个参数。除了基本数据类型都要以全限定类名的形式指定参数类型。

`resultType` 表示返回的结果类型，包括基本数据类型和对应的包装类型、String 和 Java Bean 类型。还可以使用把返回结果封装为复杂类型的 `resultMap` 。

------

## Mybatis 的一级缓存是什么？

一级缓存是 SqlSession 级别，默认开启且不能关闭。

操作数据库时需要创建 SqlSession 对象，对象中有一个 HashMap 存储缓存数据，不同 SqlSession 之间缓存数据区域互不影响。

一级缓存的作用域是 SqlSession 范围的，在同一个 SqlSession 中执行两次相同的 SQL 语句时，第一次执行完毕会将结果保存在缓存中，第二次查询直接从缓存中获取。

如果 SqlSession 执行了 DML 操作（insert、update、delete），Mybatis 必须将缓存清空保证数据有效性。

------

## Mybatis 的二级缓存是什么？

二级缓存是Mapper 级别，默认关闭。

使用二级缓存时多个 SqlSession 使用同一个 Mapper 的 SQL 语句操作数据库，得到的数据会存在二级缓存区，同样使用 HashMap 进行数据存储，相比于一级缓存，二级缓存范围更大，多个 SqlSession 可以共用二级缓存，作用域是 Mapper 的同一个 namespace，不同 SqlSession 两次执行相同的 namespace 下的 SQL 语句，参数也相等，则第一次执行成功后会将数据保存在二级缓存中，第二次可直接从二级缓存中取出数据。

要使用二级缓存，需要在全局配置文件中配置 `<setting name="cacheEnabled" value="true"/>` ，再在对应的映射文件中配置一个 `<cache/>` 标签。

------

## Mybatis `#{}` 和 `${}` 的区别？

> 华为

- `#{}`是占位符，预编译处理；`${}`是拼接符，字符串替换，没有预编译处理。
- MyBatis 会将 sql 中的`#{}`替换为 ? 号，在 sql 执行前会使用 PreparedStatement 的参数设置方法，按序给 sql 的 ? 号占位符设置参数值
- `#{}` 可以有效的防止SQL注入，提高系统安全性；`${}` 不能防止SQL 注入
- `#{}` 的变量替换是在DBMS 中；`${}` 的变量替换是在 DBMS 外

## ORM

> 腾讯IEG

ORM(Object-relational mapping)，中文翻译为对象关系映射，是一种为了解决面向对象与关系数据库存在的互不匹配的现象的技术。简单的说，ORM是通过使用描述对象和数据库之间映射的元数据，将程序中的对象自动持久化到关系数据库中。

与传统的数据库访问技术相比，ORM有以下优点：

- 开发效率更高
- 数据访问更抽象、轻便
- 支持面向对象封装

# SpringBoot

## 说说你对Spring Boot的理解

> 字节

从本质上来说，Spring Boot就是Spring，它做了那些没有它你自己也会去做的Spring Bean配置。Spring Boot使用“习惯优于配置”的理念让你的项目快速地运行起来，使用Spring Boot很容易创建一个 能独立运行、准生产级别、基于Spring框架的项目，使用Spring Boot你可以不用或者只需要很少的 Spring配置。简而言之，Spring Boot本身并不提供Spring的核心功能，而是作为Spring的脚手架框架，以达到快速构建项目、预置三方配置、开箱即用的目的。Spring Boot有如下的优点： 

- 可以快速构建项目； 
- 可以对主流开发框架的无配置集成； 
- 项目可独立运行，无需外部依赖Servlet容器； 
- 提供运行时的应用监控； 
- 可以极大地提高开发、部署效率； 
- 可以与云计算天然集成。

## Springboot底层原理

> 交通银行合肥研发

## Springboot常用注解

> 交通银行合肥研发，华讯网络

## SpringBoot的优点

> 英雄游戏

1、内置服务器

内置服务器：正如我们所知，spring boot提供了一个内置的构建服务器。这些被称为spring boot中的嵌入式服务器；这有助于我们快速进行本地开发，因为我们不需要从外部添加服务器并进行必要的配置；我们可以从头开始创建应用程序，并将主类作为spring boot应用程序运行，它将自动选择服务器并启动应用程序。

2、支持java和groovy

Spring boot同时支持Java和Groovy。这意味着我们可以根据需求在spring boot中开发基于java或groovy的应用程序，而不需要像spring这样进行繁重的配置。

3、无版本

在spring boot中，我们知道我们不需要提及应用程序的版本。如果我们想添加任何新的依赖项，它将在内部为我们管理，然后我们可以直接添加它而不需要版本。因此，与spring框架一样，管理所有依赖项的版本非常困难，因为每次应用程序失败时，版本中都存在不匹配。我们可以将依赖项更改为pom。xml或.gradle文件，无版本或不关心版本。spring boot将为我们提供此功能。

4、注释少

在spring boot应用程序中，我们需要更少的注释来配置spring应用程序；在主spring boot类中，我们只使用了一个注释，它告诉编译器它是一个spring boot应用程序，并包含更多的注释，这些注释在内部起作用，正如我们在spring framework中看到的那样，我们必须添加这么多注释才能运行应用程序。在spring boot中情况并非如此。该注释包含所有@Configuration、@EnableAutoConfiguration和@ComponentScan，优化了配置，使代码更清晰易懂，如果我们遗漏了一些东西，也不必担心。

5、提高效率

spring boot删除了必要的代码，为我们提供了内置服务器，使开发顺利；无需在构建文件中提及版本，所有这些都有助于开发人员和团队快速开发应用程序，因此提高了生产效率，因为我们在spring framework中看到，运行应用程序和测试我们所做的更改需要做很多工作，因此也节省了开发人员的时间。

6、创建程序简单

我们有一个spring初始化器，可以帮助我们非常轻松地创建spring boot应用程序；我们只需要通过点击checkcob并提及项目名称来提供必要的配置。最后，我们可以根据需要将所需的依赖项添加到我们的项目中，只需在搜索框中键入依赖项的名称。

7、缓存机制

spring boot为缓存机制提供了良好的支持，配置非常简单。我们只需要使用依赖项，然后就可以在应用程序中使用它了。

8、管理配置文件

我们也可以在spring boot应用程序中轻松管理配置文件，我们可以为每个环境设置配置文件并创建应用程序文件，而不需要做很多事情。

9、为插件提供良好支持

spring boot为许多插件提供了良好的支持，这些插件可以在spring boot应用程序中使用，并在Gradle、maven等工具中进行测试。

10、实现微服务框架

通过使用spring boot框架，我们可以在应用程序中轻松实现微服务架构；它为此提供了良好的支持。此外，我们在线上有很多文档，如果我们遇到困难，可以找到很多解决方法。

## springboot的依赖注入是什么

> 小米

## springboot中的自动装配是怎么实现的（原理）

> 小米，zoom

SpringBoot 开启自动配置的注解是`@EnableAutoConfiguration` ，启动类上的注解`@SpringBootApplication`是一个复合注解，包含了@EnableAutoConfiguration：

![SpringBoot自动配置原理](https://cdn.tobebetterjavaer.com/tobebetterjavaer/images/sidebar/sanfene/spring-df77ee15-2ff0-4ec7-8e65-e4ebb8ba88f1.png)

- `EnableAutoConfiguration` 只是一个简单的注解，自动装配核心功能的实现实际是通过 `AutoConfigurationImportSelector`类
- `AutoConfigurationImportSelector` 类实现了 `ImportSelector`接口，也就实现了这个接口中的 `selectImports`方法，该方法主要用于**获取所有符合条件的类的全限定类名，这些类需要被加载到 IoC 容器中**。
- 获取注入类的方法是 selectImports()，它实际调用的是`getAutoConfigurationEntry`，这个方法是获取自动装配类的关键，主要流程可以分为这么几步：
  1. 判断自动装配开关是否打开。默认`spring.boot.enableautoconfiguration=true`，可在 `application.properties` 或 `application.yml` 中设置
  2. 获取`EnableAutoConfiguration`注解中的 `exclude` 和 `excludeName`，用于后面的排除
  3. **获取所有需要自动装配的配置类的路径**：这一步是最关键的，从 META-INF/spring.factories 获取自动配置类的路径
  4. 去掉重复的配置类和需要排除的重复类，把需要自动加载的配置类的路径存储起来

## SpringBoot启动流程

> 阿里云，浪潮

1. 从`spring.factories`配置文件中**加载`EventPublishingRunListener`对象**，该对象拥有`SimpleApplicationEventMulticaster`属性，即在SpringBoot启动过程的不同阶段用来发射内置的生命周期事件;
2. **准备环境变量**，包括系统变量，环境变量，命令行参数，默认变量，`servlet`相关配置变量，随机值以及配置文件（比如`application.properties`）等;
3. 控制台**打印SpringBoot的`bannner`标志**；
4. **根据不同类型环境创建不同类型的`applicationcontext`容器**，因为这里是`servlet`环境，所以创建的是`AnnotationConfigServletWebServerApplicationContext`容器对象；
5. 从`spring.factories`配置文件中**加载`FailureAnalyzers`对象**,用来报告SpringBoot启动过程中的异常；
6. **为刚创建的容器对象做一些初始化工作**，准备一些容器属性值等，对`ApplicationContext`应用一些相关的后置处理和调用各个`ApplicationContextInitializer`的初始化方法来执行一些初始化逻辑等；
7. **刷新容器**，这一步至关重要。比如调用`bean factory`的后置处理器，注册`BeanPostProcessor`后置处理器，初始化事件广播器且广播事件，初始化剩下的单例`bean`和SpringBoot创建内嵌的`Tomcat`服务器等等重要且复杂的逻辑都在这里实现，主要步骤可见代码的注释，关于这里的逻辑会在以后的spring源码分析专题详细分析；
8. **执行刷新容器后的后置处理逻辑**，注意这里为空方法；
9. **调用`ApplicationRunner`和`CommandLineRunner`的run方法**，我们实现这两个接口可以在spring容器启动后需要的一些东西比如加载一些业务数据等;
10. **报告启动异常**，即若启动过程中抛出异常，此时用`FailureAnalyzers`来报告异常;
11. 最终**返回容器对象**，这里调用方法没有声明对象来接收。
