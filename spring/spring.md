#### Why Spring?
1. Very popular framework for building Java application
2. Initially was a simpler and lightweight alternative to J2EE
3. Provides a large number of helper classes ... makes things easier

### Goals of Spring
1. Lightweight development with Java POJOs
2. Dependency injection to promote loose coupling
3. Declarative programming with AOP
4. Minimize boilerplate Java code

### Brief about J2EE
Client Side Presentation(HTML, JQuery) -> Server Side Presentation(JSP) --> Server Side Business Logic(Java, EJB, Web Services, JAX-RS) -> Database
1. Early versions of EJB were extremely complex
2. Poor performance of Entity Beans

### Founder of Spring > Rod Johnson
Started off 2004 - Spring 1.0
EJB issues were fixed in EJB 3.1 somewhere around 2006-2009, however by this time Spring was already popular.

### What's in Spring 5 ?
1. Minimum requirement for Java 8 or higher
2. Upgraded Spring MVC to use new version of Servlet API 4.0
3. Added new reactive programming framework: Spring WebFlux

### Spring Core framework
* Beans, Core, SpEL, Context
* JDBC, ORM, Transactions, OXM and JMS
* Servlet, WebSocket, Web and Portlet
* Spring Cloud, Spring Data
* Spring Batch, Spring Security

### Inversion of Control
The approach of outsourcing the construction and management of objects.
i.e. initializing the instance and managing its life-cycle

### Configuring Spring Container
* XML Configuration (legacy)
* Java Annotations  + XML(modern)
* Java Source Code (no XML - modern)

In Spring World, Spring Container is called as ```ApplicationContext```


### Why do we specify the Coach interface in getBean() ?
```Coach coach = context.getBean("myCoach", Coach.class);```
When we pass the interface to the method, behind the scenes Spring will cast the object for you.

__From the Spring docs:__
>Behaves the same as getBean(String), but provides a measure of type safety by throwing a ```BeanNotOfRequiredTypeException``` if the bean is not of the required type. This means that ClassCastException can't be thrown on casting the result correctly, as can happen with getBean(String).

### What is Dependency injection ?
The client delegates the responsibility of providing its dependencies to another object. In this case the ```ApplicationContext```

### Types of Dependency Injections in Spring?
1. Constructor Injection
2. Setter Injection
3. Field Injection [__Supported with Autowiring only__]
4. Method Injection [__Supported with Autowiring only__]
   - Use any method with ```@Autowired``` to inject dependencies. Similar to Setter Injection.

### Bean Scopes - Lifecycle of the Bean
Default scope of a bean in Spring is Singleton i.e. only one instance of the bean will be created by Spring and everyone will share it.

| Scope          | Description |
|----------------|-------------------------------------------|
| singleton      | Create a single shared instance of the bean. __Default__ scope.|
| prototype      | Create a new bean instance for each container request. |
| request        | Scope to an HTTP web request. Only used for web apps. |
| session        | Scoped to an HTTP web session. Only used for web apps. |
| global-session | Scoped to a global HTTP web session. Only used for web apps. |

### Bean Lifecycle
![spring-bean-Lifecycle](/spring-bean-lifecycle.png)

When using XML configuration, I want to provide additional details regarding the method signatures of the ```init-method```  and ```destroy-method``` .

__Access modifier__
The method can have any access modifier (public, protected, private)

__Return type__
The method can have any return type. However, "void' is most commonly used. If you give a return type just note that you will not be able to capture the return value. As a result, "void" is commonly used.

__Method name__
The method can have any method name.

__Arguments__
The method can not accept any arguments. The method should be no-arg.

### Special Note about Destrop Lifecycle and Prototype Scope
There is a subtle point you need to be aware of with "prototype" scoped beans.

>For "prototype" scoped beans, Spring does not call the destroy method. Gasp!

__In contrast to the other scopes, Spring does not manage the complete lifecycle of a prototype bean__: the container instantiates, configures, and otherwise assembles a prototype object, and hands it to the client, with no further record of that prototype instance.

Thus, although initialization lifecycle callback methods are called on all objects regardless of scope, __in the case of prototypes, configured destruction lifecycle callbacks are not called__. The client code must clean up prototype-scoped objects and release expensive resources that the prototype bean(s) are holding.

### Annotations
| Annotation  | Description |
| ----------- |-------------|
|@Component   | Declares a class as Spring Bean. __Default Bean ID__ is the class name in _camelCase_ |
|@Autowired   | Injects dependencies automatically  |
|@Value   | Injects literal values to component fields  |
|@Scope   | Defines scope of a component  |
|@PostContruct   | Defines method that executes after bean has been initialized   |
|@PreDestroy   | Defines method that executes before bean is destroyed  |


* __ClassPathBeanDefinitionScanner__: Does the component scanning by default. Supports ```@Component```, ```@Repository```, ```@Service```, ```@Controller``` and also Java CDI annotations - javax.annotation.ManagedBean and javax.inject.Named

* __@Autowired__: _As of Spring Framework 4.3, an ```@Autowired``` annotation on a constructor is no longer necessary if the target bean only defines one constructor to begin with. However, if several constructor are available, at least one must be annotated to teach the container which one to use._
However, as a best practice its good to keep it as it makes the code more readable.
 - Order of Autowiring: ___Constructor > Any Method > Setter > Post Construct___
 - Autowiring first happens by type and then by qualifier hint


### Some Interview Questions
1. Whats Singleton ? How to implement Singleton? How does that related to Spring? What is the default bean scope in Spring? What is prototype scope? How is lifecycle management of prototype bean different than singleton bean?

2. What is the order of autowiring ? lets suppose I have @Autowired on constructor, setter, anyother method and a post construct

3. Using @Value ? is the value available in constructor. Whats the best place to access this value at the earliest.
