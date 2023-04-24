# Spring

## spring启动流程

> 美团

1.加载配置文件，解析配置文件，并创建IoC容器；

2.注册BeanDefinition，将BeanDefinition注册到IoC容器中；

3.实例化Bean，根据BeanDefinition实例化Bean；

4.注入属性，将Bean的属性注入到Bean中；

5.初始化Bean，调用Bean的初始化方法；

6.完成初始化，完成Spring的启动流程。

## Spring 用到了哪些设计模式？

> 比亚迪，zoom，百度

- **工厂模式** : Spring 使用工厂模式通过 `BeanFactory`、`ApplicationContext` 创建 bean 对象。
- **代理模式** : Spring AOP 功能的实现。
- **单例模式** : Spring 中的 Bean 默认都是单例的。
- **模板方法模式** : Spring 中 `jdbcTemplate`、`hibernateTemplate` 等以 Template 结尾的对数据库操作的类，它们就使用到了模板模式。
- **包装器模式** : 我们的项目需要连接多个数据库，而且不同的客户在每次访问中根据需要会去访问不同的数据库。这种模式让我们可以根据客户的需求能够动态切换不同的数据源。
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

## @Controller和@RestController注解的区别

> 邮储

@Controller和@RestController是Spring框架中常用的两个注解，用于标注控制器类。它们的主要区别在于返回结果的类型和用途：

1. 返回结果类型：@Controller通常用于返回视图，而@RestController通常用于返回数据。
2. 用途：@Controller是传统的Spring MVC控制器，用于处理HTTP请求并返回一个视图，通常配合模板引擎如Thymeleaf或JSP使用。而@RestController则是用于创建RESTful风格的API，通常以JSON格式返回数据。

举个例子，如果我们要编写一个返回Hello World字符串的API，使用@Controller和@RestController的代码如下所示：

```java
// 使用@Controller实现API
@Controller
public class HelloWorldController {
    @RequestMapping("/hello")
    public String hello() {
        return "Hello World";
    }
}

// 使用@RestController实现API
@RestController
public class HelloWorldRestController {
    @RequestMapping("/hello")
    public String hello() {
        return "Hello World";
    }
}
```

可以看到，使用@Controller时，返回值为字符串"Hello World"，并且需要通过视图解析器将其渲染成HTML格式返回给客户端。而使用@RestController时，返回值也是字符串"Hello World"，但是直接以JSON格式返回给客户端。

## Spring中完成数据库事务可以有哪些方式？

> 百度，华讯网络

1. 声明式事务管理：通过在配置文件中配置事务切面和切入点，使得Spring自动对匹配的方法进行事务管理。在Spring中，使用@Transactional注解或XML配置来定义事务管理器。
2. 编程式事务管理：通过手动编写代码来实现事务管理。Spring提供了TransactionTemplate、PlatformTransactionManager等接口和类，用于编程式管理事务。
3. 注解式事务管理：通过在方法上添加@Transactional注解来实现事务管理。这种方式可以使代码更加简洁，但是需要在配置文件中配置注解扫描器。
4. 使用Spring Boot自动配置：在Spring Boot中，可以通过简单的配置和依赖管理，实现自动化的事务管理。Spring Boot提供了自动配置的数据源和事务管理器，只需要在项目中添加相应的依赖和注解，就可以轻松完成事务管理。

## spring事务传播机制

> 蚂蚁

Spring事务传播机制指的是在多个事务嵌套执行时，如何将事务的处理结果传递给上层调用的方法。

在Spring中，事务传播机制包括以下几种：

1. REQUIRED：如果当前存在事务，则加入该事务；否则新建一个事务。这是默认的传播行为。
2. SUPPORTS：如果当前存在事务，则加入该事务；否则以非事务的方式继续执行。
3. MANDATORY：如果当前存在事务，则加入该事务；否则抛出异常。
4. REQUIRES_NEW：每次都新建一个事务，并且暂停当前事务（如果存在）。
5. NOT_SUPPORTED：以非事务方式执行操作，如果当前存在事务，则挂起该事务。
6. NEVER：以非事务方式执行操作，如果当前存在事务，则抛出异常。
7. NESTED：如果当前存在事务，则在嵌套事务中执行；否则新建一个事务。如果外层事务提交，则内层事务也会被提交；如果外层事务回滚，则内层事务也会被回滚，但是内层事务回滚并不会影响外层事务。

不同的事务传播机制适用于不同的业务场景，选择合适的事务传播机制可以确保数据的一致性和完整性。

## Spring事务有什么注意事项

> 阿里

当谈到Spring事务时，有一些需要注意的事项，包括本地事务和远程事务。

1. 本地事务注意事项

- 事务传播机制：Spring事务管理器提供了多种事务传播机制，需要根据业务需求来选择适当的事务传播机制，以确保事务的一致性和完整性。
- 事务隔离级别：Spring事务管理器支持多种事务隔离级别，需要根据业务需求来选择适当的事务隔离级别，以确保事务的正确性和性能。
- 事务超时时间：Spring事务管理器支持设置事务超时时间，需要根据业务需求来设置适当的事务超时时间，以避免长时间的事务阻塞数据库连接。
- 异常处理：需要在事务方法中正确处理异常，以确保事务的回滚和异常信息的正确传递。

2. 远程事务注意事项

- 分布式事务管理：在分布式系统中，不同的节点可能会涉及到多个数据源，需要使用分布式事务管理来确保事务的一致性和完整性。
- CAP理论：在分布式系统中，CAP理论指出，在网络分区情况下，一致性、可用性和分区容忍度只能同时满足其中两个，需要根据业务需求来选择适当的策略。
- XA事务：在分布式系统中，XA事务是实现分布式事务的一种标准方式，需要在不同的节点上实现XA协议来确保事务的一致性。
- 性能问题：在分布式系统中，由于网络延迟等原因，事务的性能可能会受到影响，需要使用合适的技术手段来提高性能。

需要注意的是，在选择事务管理机制时，需要根据业务需求来进行权衡，以选择最合适的方案。同时，需要对事务管理的机制和实现细节有深入的了解，以确保事务的正确性和性能。

## @Transactional具体实现原理？

> 阿里

@Transactional注解是Spring框架提供的一种声明式事务管理方式，它的具体实现原理涉及到Spring的AOP和事务管理两个方面。

1. AOP：Spring通过AOP拦截@Transactional注解修饰的方法，将方法中的业务逻辑和事务管理分离开来，使得业务逻辑方法可以专注于业务逻辑，而不需要关注事务管理。
2. 事务管理：在AOP拦截@Transactional注解修饰的方法之后，Spring会根据事务传播行为和隔离级别等配置，创建一个TransactionManager对象，用于管理事务的提交、回滚、挂起等操作。在方法执行过程中，如果出现异常或者执行成功，TransactionManager会根据事务配置自动提交或回滚事务。

具体来说，@Transactional注解的实现原理可以分为以下几个步骤：

1. Spring会将@Transactional注解解析为Advice，通过AOP拦截到目标方法中。
2. 在目标方法开始执行前，Spring会创建TransactionStatus对象，用于保存当前事务的状态。
3. 如果当前没有事务存在，则根据@Transactional注解中的配置创建一个新的事务，如果已经存在事务，则根据事务传播行为进行处理。
4. 目标方法执行过程中，如果出现异常，则根据事务的回滚策略进行事务的回滚操作，否则事务会被提交。
5. 目标方法执行完毕后，Spring会根据事务传播行为和隔离级别等配置，将事务状态进行合并或者挂起。

总之，@Transactional注解的实现原理主要基于Spring框架的AOP和事务管理机制，通过将业务逻辑和事务管理分离开来，实现了简单易用、高效可靠的事务管理功能。

## Spring 事务的注解不生效，是什么原因

> 百度，华讯网络

- **@Transactional 应用在非 public 修饰的方法上**
- **@Transactional 注解属性 propagation 设置错误**
- **@Transactional 注解属性 rollbackFor 设置错误**：rollbackFor 可以指定能够触发事务回滚的异常类型。Spring 默认抛出了未检查 unchecked 异常（继承自 RuntimeException 的异常）或者 Error 才回滚事务，其他异常不会触发回滚事务。若在目标方法中抛出的异常是 rollbackFor 指定的异常的子类，事务同样会回滚。
- 在方法中捕获的异常没有抛出去
- 没有使用代理对象调用

## Spring如何解决循环依赖？

> 德胧集团，百度，字节，阿里云

我们都知道，单例 Bean 初始化完成，要经历三步：

![Bean初始化步骤](https://cdn.tobebetterjavaer.com/tobebetterjavaer/images/sidebar/sanfene/spring-867066f1-49d1-4e57-94f9-4c66a3a8797e.png)Bean初始化步骤

注入就发生在第二步，**属性赋值**，结合这个过程，Spring 通过**三级缓存**解决了循环依赖：

1. 一级缓存 : `Map<String,Object>` **singletonObjects**，单例池，用于保存实例化、属性赋值（注入）、初始化完成的 bean 实例
2. 二级缓存 : `Map<String,Object>` **earlySingletonObjects**，早期曝光对象，用于保存实例化完成的 bean 实例
3. 三级缓存 : `Map<String,ObjectFactory<?>>` **singletonFactories**，早期曝光对象工厂，用于保存 bean 创建工厂，以便于后面扩展有机会创建代理对象。

![三级缓存](https://cdn.tobebetterjavaer.com/tobebetterjavaer/images/sidebar/sanfene/spring-01d92863-a2cb-4f61-8d8d-30ecf0279b28.png)三级缓存

我们来看一下三级缓存解决循环依赖的过程：

当 A、B 两个类发生循环依赖时： ![循环依赖](https://cdn.tobebetterjavaer.com/tobebetterjavaer/images/sidebar/sanfene/spring-cfc09f84-f8e1-4702-80b6-d115843e81fe.png)

A 实例的初始化过程：

1. 创建 A 实例，实例化的时候把 A 对象⼯⼚放⼊三级缓存，表示 A 开始实例化了，虽然我这个对象还不完整，但是先曝光出来让大家知道

![1](https://cdn.tobebetterjavaer.com/tobebetterjavaer/images/sidebar/sanfene/spring-1a8bdc29-ff43-4ff4-9b61-3eedd9da59b3.png)1

2. A 注⼊属性时，发现依赖 B，此时 B 还没有被创建出来，所以去实例化 B

3. 同样，B 注⼊属性时发现依赖 A，它就会从缓存里找 A 对象。依次从⼀级到三级缓存查询 A，从三级缓存通过对象⼯⼚拿到 A，发现 A 虽然不太完善，但是存在，把 A 放⼊⼆级缓存，同时删除三级缓存中的 A，此时，B 已经实例化并且初始化完成，把 B 放入⼀级缓存。

![2](https://cdn.tobebetterjavaer.com/tobebetterjavaer/images/sidebar/sanfene/spring-bf2507bf-96aa-4b88-a58b-7ec41d11bc70.png)2

4. 接着 A 继续属性赋值，顺利从⼀级缓存拿到实例化且初始化完成的 B 对象，A 对象创建也完成，删除⼆级缓存中的 A，同时把 A 放⼊⼀级缓存

5. 最后，⼀级缓存中保存着实例化、初始化都完成的 A、B 对象

![5](https://cdn.tobebetterjavaer.com/tobebetterjavaer/images/sidebar/sanfene/spring-022f7cb9-2c83-4fe9-b252-b02bd0fb2435.png)5

所以，我们就知道为什么 Spring 能解决 setter 注入的循环依赖了，因为实例化和属性赋值是分开的，所以里面有操作的空间。如果都是构造器注入的化，那么都得在实例化这一步完成注入，所以自然是无法支持了。

# Spring IoC

## 说说你对 Spring 控制反转的理解

> 宁波银行总行、比亚迪，英雄游戏，百度，字节，度小满，阿里，美团，万得，蚂蚁

Spring IoC**（Inversion of Control:控制反转）**是一种设计模式，其核心思想是将对象的创建和依赖关系的管理从应用代码中分离出来，交给容器来完成。这样可以将组件之间的依赖关系解耦，提高组件的可维护性和可扩展性。

控制反转的实现方式有两种：依赖注入（DI）和依赖查找（DL）。依赖注入是指容器在创建对象时，自动将对象所依赖的其他对象注入到该对象中，而不是由对象自己去查找和创建它所依赖的对象。依赖查找是指容器在创建对象时，由对象自己去查找和创建它所依赖的对象。

Spring 控制反转的核心是 Spring 容器，它是一个负责创建和管理对象的容器。当需要使用一个对象时，可以通过 Spring 容器来获取该对象，而不是直接在应用代码中创建该对象。Spring 容器可以通过 XML 文件、注解或者 Java 配置来定义和配置对象及其依赖关系。

------

## IOC怎么实现的

> 阿里

IOC（Inversion of Control）是一种设计模式，它将对象的创建、依赖注入等操作交由容器来管理，而不是由程序员手动进行操作。在Java中，IOC通常通过依赖注入（DI）来实现。

在Spring框架中，IOC通过以下方式实现：

1. 定义Bean：在Spring配置文件或者使用注解的方式下，定义需要管理的Bean对象。
2. Bean的实例化：Spring容器在启动时读取配置文件或者扫描注解，并根据配置信息创建Bean的实例。在创建Bean实例时，Spring采用了工厂模式，即使用BeanFactory或ApplicationContext等工厂类来管理Bean实例。
3. Bean的装配：通过DI方式，将Bean实例之间的依赖关系交由Spring容器管理。Spring容器在创建Bean实例时，会自动注入其所依赖的其他Bean实例。
4. 容器管理：Spring容器负责管理所有Bean实例的生命周期，包括实例化、销毁等操作。在Bean实例不再被使用时，Spring容器会自动销毁它们，释放占用的资源。

总的来说，Spring框架中的IOC是通过BeanFactory和ApplicationContext等容器实现的，容器负责管理Bean实例的创建、装配和生命周期等操作，程序员只需要定义好Bean对象和它们之间的依赖关系，就可以让容器来完成其余的工作。这样可以将程序员从繁琐的对象创建和依赖注入中解放出来，提高了代码的可维护性和可扩展性。

------

## 依赖注入的实现方法有哪些？

> 字节

依赖注入（Dependency Injection，DI）是Spring框架的核心功能之一，它允许我们将应用程序中的依赖关系从类内部移到类外部进行管理，使得应用程序更加灵活和可维护。下面是一些常见的依赖注入方式：

1. 构造函数注入：通过构造函数参数的方式将依赖项注入到类中。
2. Setter方法注入：通过Setter方法将依赖项注入到类中。
3. 接口注入：通过实现依赖注入接口来定义注入方法，该方法将依赖项注入到类中。
4. 字段注入：通过类的字段属性来注入依赖项，通常使用@Autowired注解。
5. 注解驱动注入：通过注解来自动装配依赖项，例如@Component、@Service、@Autowired等注解。
6. Java配置注入：使用Java类来配置依赖项，通常使用@Configuration和@Bean注解。

以上几种方式都可以用来实现依赖注入，每一种方式都有各自的优缺点，开发人员可以根据实际情况选择最合适的方式。

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

> 比亚迪，小米，美团，华为，携程，美团，阿里，蚂蚁

![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2020/2/15/1704860a4de235aa~tplv-t2oaga2asx-zoom-in-crop-mark:4536:0:0:0.awebp)

------

## Bean什么时候销毁

> 阿里

在Spring中，Bean的销毁时机分为两种情况：

1. 容器关闭时销毁：当Spring容器关闭时，容器会调用所有单例Bean的销毁方法。
2. 手动销毁：对于非单例Bean，如果需要在容器关闭之前进行销毁操作，可以通过在Bean实现`DisposableBean`接口或者定义自定义销毁方法并在Bean定义中指定销毁方法名来实现。

## bean是单例还是多例，是线程安全的吗

> 阿里

在Spring框架中，默认情况下，Bean是单例的。也就是说，Spring容器在启动时会为每一个Bean创建一个实例，并在整个应用程序中共享这个实例。

但是，如果需要创建多例的Bean，可以通过在Bean定义中添加scope属性，并设置为"prototype"，来实现每次请求Bean时都创建一个新的实例。例如：

```xml
<bean id="userService" class="com.example.UserService" scope="prototype"/>
```

在多线程环境下，如果Bean是单例的，那么它就是线程不安全的。因为多个线程可能会同时访问同一个实例，如果这个实例没有经过特殊处理，那么就会出现线程安全问题。为了解决这个问题，可以在Bean的定义中添加"scope"属性，并设置为"singleton"，这样可以保证每个线程都使用独立的实例。

另外，如果Bean包含了共享的状态，那么它也可能是线程不安全的。在这种情况下，需要考虑如何保证Bean的线程安全性，可以使用同步机制、线程局部变量或者避免在Bean中保存共享状态等方式来实现。

------

## BeanFactory和ApplicationContext区别是什么？使用场景？

> 阿里

BeanFactory和ApplicationContext都是Spring容器的两个核心接口，它们的区别和使用场景如下：

1. BeanFactory是Spring框架最基础的接口，定义了最简单的容器的功能，主要负责对象的创建、管理、依赖注入和生命周期管理等。在Spring容器启动时，BeanFactory并不会对所有的bean进行实例化，而是在第一次使用bean时才进行实例化，这样可以节省系统资源。使用场景：适用于对Spring容器轻量级的使用场景，需要手动配置和初始化BeanFactory对象。
2. ApplicationContext是BeanFactory的一个子接口，扩展了BeanFactory的功能，是Spring框架中最常用的接口之一。ApplicationContext会在Spring容器启动时，将所有的bean进行实例化，并且提供了更多的特性，如国际化、AOP、事件机制等。同时，ApplicationContext还支持各种资源加载方式，如ClassPathXmlApplicationContext、FileSystemXmlApplicationContext、AnnotationConfigApplicationContext等。使用场景：适用于大型的企业级应用，需要更丰富的功能，如国际化、AOP等，同时需要快速启动Spring容器。

综上所述，BeanFactory和ApplicationContext的主要区别在于功能和资源的加载方式，BeanFactory是最基础的Spring容器，支持手动配置和初始化，对系统资源的消耗较少，适用于轻量级的应用；而ApplicationContext扩展了BeanFactory的功能，提供了更多的特性，对系统资源的消耗较大，适用于大型的企业级应用。

## BeanFactory和FactoryBean的区别？

> zoom

BeanFactory 是一个 Bean 工厂，使用简单工厂模式，是 Spring IoC 容器顶级接口，可以理解为含有 Bean 集合的工厂类，作用是管理 Bean，包括实例化、定位、配置对象及建立这些对象间的依赖。BeanFactory 实例化后并不会自动实例化 Bean，只有当 Bean 被使用时才实例化与装配依赖关系，属于延迟加载，适合多例模式。

FactoryBean 是一个工厂 Bean，使用了工厂方法模式，作用是生产其他 Bean 实例，可以通过实现该接口，提供一个工厂方法来自定义实例化 Bean 的逻辑。FactoryBean 接口由 BeanFactory 中配置的对象实现，这些对象本身就是用于创建对象的工厂，如果一个 Bean 实现了这个接口，那么它就是创建对象的工厂 Bean，而不是 Bean 实例本身。

## @Autowired 和 @Resource 的区别是什么？

> zoom，美团

- `@Autowired` 是 Spring 提供的注解，`@Resource` 是 JDK 提供的注解。
- `Autowired` 默认的注入方式为`byType`（根据类型进行匹配），`@Resource`默认注入方式为 `byName`（根据名称进行匹配）。
- 当一个接口存在多个实现类的情况下，`@Autowired` 和`@Resource`都需要通过名称才能正确匹配到对应的 Bean。`Autowired` 可以通过 `@Qualifier` 注解来显式指定名称，`@Resource`可以通过 `name` 属性来显式指定名称。

# Spring AOP

## 什么是AOP

> 比亚迪，英雄游戏，百度，字节，度小满，华为，阿里，美团，万得，蚂蚁

AOP(Aspect-Oriented Programming:面向切面编程)是一种编程范式，它将应用程序的业务逻辑（核心关注点）与其它系统级服务（横切关注点）分离。AOP采用一种称为“切面”的技术来达到这个目的。切面是一个横跨多个对象的代码片段，它与业务逻辑不相关，但却能影响到业务逻辑的行为。AOP技术通过动态代理的方式，在不修改原有代码的情况下，将切面织入到业务逻辑中。

## Spring AOP实现方式

> 阿里，蚂蚁

1. 基于JDK动态代理：使用JDK提供的动态代理技术，在运行时动态创建代理对象，拦截被代理对象的方法，并在方法执行前后进行切面逻辑的处理。这种方式只能对实现了接口的类进行代理，也就是基于接口的代理。
2. 基于CGLIB动态代理：对于没有实现接口的类，Spring可以使用CGLIB提供的动态代理技术，在运行时动态创建子类，并重写被代理对象的方法，从而实现切面逻辑的处理。这种方式可以代理任意的类，不需要实现接口。
3. 基于AspectJ的编译时织入和运行时织入：AspectJ是一个独立的AOP框架，它提供了一套完整的AOP解决方案，包括编译器、类加载器、字节码增强器等。Spring可以集成AspectJ框架，实现AOP的编译时织入和运行时织入。编译时织入需要在编译阶段增强目标类的字节码，而运行时织入则是在运行时通过代理方式实现切面逻辑的处理。

## AOP的应用场景

> 阿里钉钉，蚂蚁

1. 日志记录：在系统中记录操作日志，例如用户的登录、操作行为等。
2. 安全性控制：对系统的访问权限进行控制，例如验证用户的身份、访问限制等。
3. 事务管理：在数据操作中，保证一组相关的操作要么全部成功，要么全部回滚。
4. 性能监控：监控系统运行的性能，例如耗时、并发数、内存使用等。
5. 缓存处理：在系统中使用缓存技术，例如将查询结果缓存在缓存中，减少数据库的访问次数。
6. 异常处理：在系统中处理异常情况，例如捕获异常、记录异常信息等。

# Spring MVC

## SpringMVC 工作原理了解吗?

> zoom，蚂蚁

1. 客户端（浏览器）发送请求， `DispatcherServlet`拦截请求。
2. `DispatcherServlet` 根据请求信息调用 `HandlerMapping` 。`HandlerMapping` 根据请求 url 去查找对应的 `Handler`。
4. `Handler` 完成对用户请求的处理后，会返回一个 `ModelAndView` 对象，其中包含响应视图和模型数据。
5. `ModelAndView` 传递给 `ViewResolver`，它根据视图名称查找对应的视图。
6. `ViewResolver` 找到视图后，将 `ModelAndView` 中的模型数据传递给视图进行渲染。
7. 视图渲染完成后，将渲染结果作为响应返回给客户端。

------

## Spring MVC 中常用的HTTP注解？

> 阿里钉钉

1. @RequestMapping：用于将请求映射到控制器的处理方法上，可以指定请求的URL、请求方法（GET、POST等）、请求参数、请求头等信息。
2. @RequestParam：用于将请求参数绑定到控制器的处理方法的参数上，可以指定参数名、是否必需、默认值等信息。
3. @PathVariable：用于将请求URL中的占位符参数（例如：/user/{id}）绑定到控制器的处理方法的参数上。
4. @RequestBody：用于将请求体中的JSON、XML等格式的数据绑定到控制器的处理方法的参数上。
5. @ResponseBody：用于将控制器的处理结果（例如：JSON、XML等格式的数据）直接返回给客户端。
6. @RequestHeader：用于将请求头中的信息（例如：User-Agent、Accept-Language等）绑定到控制器的处理方法的参数上。
7. @CookieValue：用于将Cookie中的信息绑定到控制器的处理方法的参数上。
8. @SessionAttribute：用于将Session中的信息绑定到控制器的处理方法的参数上。

------

## Spring MVC拦截器

> 唯品会

Spring MVC的拦截器（Interceptor）是一种常用的拦截器机制，它可以在请求进入Controller处理之前或之后，对请求进行拦截和处理。拦截器可以用于进行登录认证、权限验证、日志记录、统计等操作。

Spring MVC的拦截器是基于Java的AOP（Aspect-Oriented Programming，面向切面编程）实现的，拦截器接口定义了beforeCompletion()、postHandle()、preHandle()等方法，可以在请求进入Controller处理之前、Controller处理之后和视图渲染之前进行处理。在拦截器中，可以获取请求信息、响应信息、Session信息等，同时也可以进行异常处理等操作。

在Spring MVC中，可以通过实现HandlerInterceptor接口来创建拦截器。Spring MVC支持多个拦截器，可以通过配置来指定拦截器的执行顺序。在拦截器中，可以对请求进行判断、重定向、修改参数等操作。

下面是一个简单的拦截器实现示例：

```Java
public class MyInterceptor implements HandlerInterceptor {

    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        // 在请求处理之前进行拦截操作，可以进行登录认证、权限验证等操作
        return true; // 如果返回false，则表示请求被拦截，不再继续处理
    }

    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        // 在Controller处理之后，视图渲染之前进行拦截操作，可以进行数据统计、日志记录等操作
    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        // 在请求处理完成后进行拦截操作，可以进行异常处理等操作
    }
}
```

然后，在Spring MVC配置文件中进行拦截器的配置：

```xml
<mvc:interceptors>
    <mvc:interceptor>
        <mvc:mapping path="/**" />
        <bean class="com.example.MyInterceptor" />
    </mvc:interceptor>
</mvc:interceptors>
```

上述配置表示对所有的请求进行拦截，使用MyInterceptor拦截器进行处理。可以配置多个拦截器，并指定它们的执行顺序。

------

# Mybatis

## Mybatis `#{}` 和 `${}` 的区别？

> 华为，美团

- `#{}`是占位符，预编译处理；`${}`是拼接符，字符串替换，没有预编译处理。
- MyBatis 会将 sql 中的`#{}`替换为 ? 号，在 sql 执行前会使用 PreparedStatement 的参数设置方法，按序给 sql 的 ? 号占位符设置参数值
- `#{}` 可以有效的防止SQL注入，提高系统安全性；`${}` 不能防止SQL 注入

## sql预编译是怎么做的？如果没有mybatis，那么怎么来做到sql预编译？

> 美团

SQL预编译（Prepared Statement）是一种将SQL语句和参数分开处理的技术，应用程序先将SQL语句发送给数据库，数据库对SQL语句进行编译，并将编译结果缓存起来，以便后续的执行。这样做的好处是可以避免SQL注入攻击，提高执行效率，减少数据库服务器的压力。

如果没有MyBatis，我们可以使用JDBC中的PreparedStatement来实现SQL预编译。具体的步骤如下：

1. 创建PreparedStatement对象：在创建PreparedStatement对象时，需要传入带有占位符的SQL语句，例如：

```java
String sql = "SELECT * FROM users WHERE id = ?";
PreparedStatement stmt = conn.prepareStatement(sql);
```

2. 设置参数值：使用setXXX方法设置SQL语句中占位符的参数值，例如：

```java
stmt.setInt(1, 1001);
```

3. 执行SQL语句：使用executeQuery或executeUpdate方法执行SQL语句，例如：

```java
ResultSet rs = stmt.executeQuery();
```

PreparedStatement对象会将SQL语句和参数一起发送给数据库服务器，数据库服务器会对SQL语句进行编译，并将编译结果缓存起来。如果应用程序再次执行相同的SQL语句，只需要重新设置参数值并执行即可，不需要重新编译SQL语句，从而提高了执行效率。

需要注意的是，在使用PreparedStatement时，必须将用户输入的数据作为参数传入，而不能将其直接拼接到SQL语句中，否则可能会导致SQL注入攻击。

## ORM

> 腾讯IEG

ORM(Object-relational mapping)，中文翻译为对象关系映射，是一种为了解决面向对象与关系数据库存在的互不匹配的现象的技术。简单的说，ORM是通过使用描述对象和数据库之间映射的元数据，将程序中的对象自动持久化到关系数据库中。

与传统的数据库访问技术相比，ORM有以下优点：

- 开发效率更高
- 数据访问更抽象、轻便
- 支持面向对象封装

# SpringBoot

## 介绍一下 SpringBoot，有哪些优点？

> 字节，德胧，英雄游戏

Spring Boot 是一个开源的 Java Web 框架，它可以帮助开发者快速构建可独立运行的、生产级别的 Spring 应用程序。相比传统的 Spring 框架，Spring Boot 提供了很多自动配置的功能，从而减少了项目配置的工作量，开发者可以更加专注于业务逻辑的开发。

Spring Boot 以`约定大于配置`核心思想开展工作，相比 Spring 具有如下优势：

1. Spring Boot 可以快速创建独立的 Spring 应用程序。
2. Spring Boot 内嵌了如 Tomcat，Jetty 和 Undertow 这样的容器，也就是说可以直接跑起来，用不着再做部署工作了。
3. Spring Boot 无需再像 Spring 一样使用一堆繁琐的 xml 文件配置。
4. Spring Boot 可以自动配置(核心)Spring。SpringBoot 将原有的 XML 配置改为 Java 配置，将 bean 注入改为使用注解注入的方式(@Autowire)，并将多个 xml、properties 配置浓缩在一个 appliaction.yml 配置文件中。
5. Spring Boot 提供了一些现有的功能，如量度工具，表单数据验证以及一些外部配置这样的一些第三方功能。
6. Spring Boot 可以快速整合常用依赖（开发库，例如 spring-webmvc、jackson-json、validation-api 和 tomcat 等），提供的 POM 可以简化 Maven 的配置。当我们引入核心依赖时，SpringBoot 会自引入其他依赖。

## springboot的事务注解

> 普元

Spring Boot是一种基于Spring Framework的快速开发框架，提供了一系列便利的功能来简化应用程序的开发。其中一个非常重要的功能就是事务管理，通过使用事务注解，可以实现对Spring Boot应用中的数据库操作进行事务控制。

以下是Spring Boot中常用的事务注解：

1. @Transactional: 该注解可以被用于类或方法上，表示该类或方法需要进行事务管理。如果被注解的方法在执行过程中发生异常，则事务将回滚。如果没有发生异常，则事务将提交。
2. @Transactional(propagation = Propagation.REQUIRED): 指定事务的传播属性为REQUIRED。这意味着如果当前没有事务，就创建一个新事务；如果已经存在一个事务，就加入该事务，成为它的一部分。
3. @Transactional(propagation = Propagation.REQUIRES_NEW): 指定事务的传播属性为REQUIRES_NEW。这意味着如果当前已经有一个事务在执行，那么该事务将被挂起，新的事务将被启动并执行；如果没有事务在执行，则直接启动一个新的事务。
4. @Transactional(propagation = Propagation.NOT_SUPPORTED): 指定事务的传播属性为NOT_SUPPORTED。这意味着该方法不应该在事务环境中执行，即使当前存在一个事务，也应该暂停它。
5. @Transactional(readOnly = true): 指定事务的只读属性为true。这意味着该事务只能读取数据，不能进行修改。这可以提高应用程序的性能。
6. @Transactional(timeout = 10): 指定事务的超时时间为10秒。如果事务在10秒内没有完成，将会被回滚。

以上是Spring Boot中常用的事务注解，开发者可以根据实际需求来选择合适的注解来进行事务管理。

## Springboot常用注解

> 交通银行合肥研发，华讯网络，普元

Spring Boot是一个基于Spring Framework的快速开发框架，提供了一系列便利的注解来简化应用程序的开发。以下是Spring Boot中常用的注解：

1. @RestController：标注一个类为RESTful风格的控制器，返回的数据是直接放在HTTP响应体中，一般用于提供API服务。
2. @RequestMapping：用于映射HTTP请求的方法或类级别的注解。可以用于处理不同的HTTP请求方法（GET、POST、PUT、DELETE等）。
3. @GetMapping、@PostMapping、@PutMapping、@DeleteMapping：分别用于处理HTTP GET、POST、PUT、DELETE请求的注解。
4. @PathVariable：用于将URL中的模板变量映射到方法的参数中。
5. @RequestParam：用于获取HTTP请求中的参数值。
6. @RequestBody：用于将HTTP请求中的JSON格式的数据转换为对象。
7. @ResponseBody：用于将方法返回的对象转换为JSON格式的数据，并将其放入HTTP响应体中。
8. @Autowired：自动装配Bean。
9. @Component：用于标注一个类为Spring Bean。
10. @Service：用于标注一个类为服务层的Bean。
11. @Repository：用于标注一个类为数据访问层的Bean。
12. @Configuration：用于标注一个类为配置类，相当于Spring配置文件中的<bean>标签。
13. @Value：用于注入配置文件中的属性值。
14. @Transactional：用于实现事务控制。

以上是Spring Boot中常用的注解，它们都具有非常重要的作用，可以帮助开发者快速开发出高质量的应用程序。

## springboot中的自动装配是怎么实现的（原理）

> 小米，zoom，德胧

SpringBoot 开启自动配置的注解是`@EnableAutoConfiguration` 

![SpringBoot自动配置原理](https://cdn.tobebetterjavaer.com/tobebetterjavaer/images/sidebar/sanfene/spring-df77ee15-2ff0-4ec7-8e65-e4ebb8ba88f1.png)

- `EnableAutoConfiguration` 只是一个简单的注解，自动装配核心功能的实现实际是通过 `AutoConfigurationImportSelector`类。
- `AutoConfigurationImportSelector` 类实现了 `ImportSelector`接口，也就实现了这个接口中的 `selectImports`方法，该方法主要用于**获取所有符合条件的类的全限定类名，这些类需要被加载到 IoC 容器中**。
- 获取注入类的方法是 selectImports()，它实际调用的是`getAutoConfigurationEntry`，这个方法是获取自动装配类的关键，主要流程可以分为这么几步：
  1. 判断自动装配开关是否打开。默认`spring.boot.enableautoconfiguration=true`，可在 `application.properties` 或 `application.yml` 中设置
  2. 获取`EnableAutoConfiguration`注解中的 `exclude` 和 `excludeName`，用于后面的排除
  3. **获取所有需要自动装配的配置类的路径**：这一步是最关键的，从 META-INF/spring.factories 获取自动配置类的路径
  4. 去掉重复的配置类和需要排除的重复类，把需要自动加载的配置类的路径存储起来

## SpringBoot启动流程

> 阿里，浪潮

Spring Boot 启动过程主要包括以下几个阶段：

1. 加载配置文件和自动配置：Spring Boot 在启动时会读取 classpath 下的 application.properties 或 application.yml 配置文件，并将配置信息加载到 Spring 环境中。同时，Spring Boot 还会根据类路径下的 META-INF/spring.factories 文件中配置的自动配置类，自动配置 Spring 应用程序。
2. 启动 Spring 应用上下文：Spring Boot 通过 SpringApplication 类来启动应用程序上下文。在启动过程中，Spring Boot 会根据配置文件中的配置信息创建对应的 Spring Bean，并将它们添加到应用程序上下文中。同时，Spring Boot 还会扫描应用程序的类路径，寻找与 Spring 相关的注解，并将这些注解转换为 Spring Bean。
3. 执行 CommandLineRunner 和 ApplicationRunner：Spring Boot 在启动后会依次执行实现了 CommandLineRunner 或 ApplicationRunner 接口的 Bean 的 run 方法，从而完成一些额外的初始化工作。
4. 启动 Servlet 容器：Spring Boot 会启动嵌入式 Servlet 容器（如 Tomcat、Jetty 等），并将应用程序部署到容器中，使得应用程序可以接收请求并处理响应。

总的来说，Spring Boot 启动过程是一个比较复杂的流程，它涉及到了很多模块和组件，需要对 Spring Boot 的各个组成部分有深入的了解才能更好地理解和应用。
