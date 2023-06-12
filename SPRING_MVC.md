# SPRING MVC

## 1. Explain architecture of Spring MVC Framework

<img src="https://docs.spring.io/spring-framework/docs/4.3.x/spring-framework-reference/html/images/spring-overview.png" width=60%>

- There are around 20 modules in Spring Architecture.

- These modules are grouped into

    1. Core Container
    2. Data Access-Integration
    3. Aspect Oriented Programming(AOP)
    4. Instrumentation
    5. Test

1. Core Container

    1. Core Module
        - This is fundamental part of spring framework.
        - This module consists of IoC and Dependency Injection features.
    2. Bean Module
        - This module provides BeanFactory class.
        - Which is a sophisticated implementation of the factory pattern.
    3. Context Module
        - This module is based on Core and Bean modules.
        - it is a medium to access any objects defined and configured.
        - The ApplicationContext interface is an important point in this module.
    4. Expression Language Module
        - The SpEL module provides a powerful expression language for querying and manipulating an object graph at
        runtime.

2. Data Access/integration

    1. JDBC
        - When we use core JDBC programming then we have to write lot of code.
        - The JDBC module of Spring framework removes this complexity by providing JDBC abstraction layer.
    2. ORM
        - This module provides integration layers for popular object-relational mapping APIs, including JPA, JDO,
        Hibernate, and iBatis.
        - It provides code without worrying about catching exceptions specific to each persistence technology.
    3. OXM
        - It is used to converts object into XML format and vice versa.
        - Provide uniform API to access any of the OXM frameworks such as Castor, XMLBeans, etc.
    4. JMS
        - The Java Messaging Service JMS module contains features for producing and consuming messages.
    5. Transaction
        - This module supports programmatic and declarative transaction management for classes that implement
    special interfaces and for all your POJOs.

3. Web
    1. Web
        - This module provides basic web-oriented integration features such as multipart file-upload functionality.
        - Also provide initialization of the IoC container using servlet listeners and a web-oriented application context.
    2. Web-Servlet
        - This module contains the model view container based implementation for web application.
    3. Web-Struts
        - This module provides the support for the integration of classic struts web tire within the spring application.
    4. Web-Portlet
        - The Web-Portlet module provides the MVC implementation to be used in a portlet environment and mirrors the functionality of Web-Servlet module.

4. AOP

    - This module provides an aspect-oriented programming implementation.
    - It’s allowing you to define method-interceptors and pointcuts to cleanly decouple code that
    implements functionality that should be separated.
    - So you can introduce new functionalities into existing code without modifying it.

5. Aspects

    - This module provides integration with AspectJ.
    - Which is again a powerful and mature AOP framework.

6. Instrumentation

    - This module provides class instrumentation support and class loader implementations to be used in certain application servers.

7. Messaging
    - This module provides support for STOMP(Simple\Streaming Text Oriented Message Protocol) as
    the WebSocket sub-protocol to use in applications.
    - It also supports an annotation programming model for routing and processing STOMP messages from WebSocket clients.

8. Test
    - The Test module supports the testing of Spring components with JUnit or TestNG frameworks.

## 2. Explain the features of Spring web MVC

Spring Web MVC is a powerful framework for building web applications in Java. It follows the Model-View-Controller (MVC) architectural pattern, which separates the application logic into three components: the model, the view, and the controller. Here are the key features of Spring Web MVC:

1. DispatcherServlet: At the heart of Spring Web MVC is the DispatcherServlet, which acts as the front controller. It receives all incoming requests and delegates them to the appropriate controller based on the URL mappings defined in the configuration.

2. HandlerMapping: HandlerMapping is responsible for mapping incoming requests to specific controller methods. Spring provides various implementations of HandlerMapping, including the most commonly used RequestMappingHandlerMapping, which uses annotations to map requests to methods.

3. Controllers: Controllers in Spring Web MVC are responsible for processing requests and generating responses. They are typically implemented as POJOs (Plain Old Java Objects) and are annotated with @Controller. Controllers handle the business logic, interact with the model layer, and decide which view should be rendered.

4. RequestMapping: Spring Web MVC provides the @RequestMapping annotation to map requests to specific controller methods. It supports various request mapping options, such as mapping based on URL patterns, HTTP methods, request parameters, headers, and more.

5. Model: The model represents the data that is passed between the controller and the view. In Spring Web MVC, the model is usually a Map or a Java object that gets populated with data in the controller and is made available to the view for rendering.

6. ViewResolver: ViewResolver is responsible for resolving the logical view names returned by the controller to the actual view templates. Spring Web MVC supports various view technologies, such as JSP, Thymeleaf, Freemarker, and more. You can configure multiple ViewResolvers to handle different types of views.

7. View: The view is responsible for rendering the response that will be sent back to the client. It is typically an HTML template or a template engine that generates dynamic content based on the data provided by the model.

8. Data Binding and Validation: Spring Web MVC provides powerful data binding capabilities, allowing you to bind request parameters or form data directly to Java objects. It also supports validation through annotations or custom validators, helping to ensure the integrity of the data received from the client.

9. Interceptors: Interceptors allow you to intercept requests and responses before and after they reach the controller. They can be used for tasks such as logging, authentication, authorization, and modifying the request or response.

10. Exception Handling: Spring Web MVC provides robust support for handling exceptions that occur during request processing. You can define global exception handlers or handle specific exceptions in individual controllers, allowing for centralized error handling and consistent error responses.

These are some of the key features of Spring Web MVC that make it a popular choice for building web applications in Java. It provides a flexible and highly configurable framework that promotes clean code organization and separation of concerns, making it easier to develop and maintain web applications.

## 3. What is dependency injection? Explain in detail

Dependency Injection (DI) is a design pattern and a fundamental concept in software development that focuses on decoupling the dependencies between components. It allows objects to be created and configured externally, and their dependencies to be injected into them rather than having the objects themselves responsible for creating and managing their dependencies.

In traditional programming, objects often create and manage their dependencies directly, resulting in tight coupling and making it difficult to change or test those objects in isolation. Dependency Injection addresses this issue by inverting the control of object creation and allowing dependencies to be provided from external sources.

Let's delve into the details of Dependency Injection:

1. Dependencies: A dependency is an object or service that another object relies on to perform its functionality. For example, in a web application, a service class may depend on a data access object (DAO) to interact with the database. Dependencies can be other objects, services, configurations, or even primitive types.

2. Injection Types:

   a. Constructor Injection: Dependencies are injected through the constructor of a class. This ensures that all necessary dependencies are provided at the time of object creation, promoting immutability and making the class easier to test.

   b. Setter Injection: Dependencies are injected through setter methods of a class. Setter methods allow dependencies to be set or changed after object creation. This approach is more flexible but can lead to objects being in an incomplete or inconsistent state if not properly managed.

   c. Interface Injection: Dependencies are injected through an interface that the class implements. This approach is less common and often requires more complex infrastructure or frameworks to support.

3. Dependency Injection Container/Injector: A Dependency Injection container or injector is responsible for managing the creation and injection of dependencies. It is usually configured through annotations, XML files, or Java-based configuration, and it resolves dependencies at runtime. Popular DI containers in the Java ecosystem include Spring Framework's ApplicationContext and Google Guice.

4. Benefits of Dependency Injection:

   a. Loose coupling: DI helps to reduce the coupling between components, as dependencies are provided externally. Components can be easily replaced or extended without affecting the existing codebase.

   b. Testability: With DI, dependencies can be easily mocked or replaced during unit testing. By injecting mock objects or test doubles, you can isolate the behavior of a specific class and write focused and reliable tests.

   c. Reusability: DI promotes the reuse of components since they can be decoupled from their dependencies. A component can be used in different contexts or configurations by simply injecting different dependencies.

   d. Configurability: By externalizing dependencies, DI allows for easier configuration and management of components. Dependencies can be wired and configured at runtime, facilitating flexibility and modularity.

5. Inversion of Control (IoC): Dependency Injection is often associated with the broader concept of Inversion of Control. In traditional programming, objects control the creation and management of their dependencies. In contrast, with DI, control is inverted, and the responsibility for creating and managing dependencies is shifted to an external entity (the DI container or injector).

To summarize, Dependency Injection is a design pattern that promotes loose coupling, testability, reusability, and configurability by inverting the control of object creation and allowing dependencies to be injected from external sources. It improves the modularity and maintainability of software systems and is widely used in modern frameworks and applications.

## 4. What is Spring AOP? What are Join points and Point cuts?

Spring AOP (Aspect-Oriented Programming) is a powerful feature of the Spring Framework that provides an additional way to modularize and manage cross-cutting concerns in your application. A cross-cutting concern is a functionality or feature that cuts across multiple modules or components, such as logging, security, transaction management, and caching. AOP allows you to encapsulate these concerns into reusable modules called aspects and apply them to multiple points in the application's codebase.

Key concepts in Spring AOP are join points and pointcuts:

1. Join Points: Join points are specific points in the execution of a program where an aspect can be applied. In Spring AOP, join points can include method invocations, method executions, exception handling, field access, and more. A join point represents a specific moment in the flow of the program's execution, and aspects can be woven in at these join points to perform additional actions or modifications.

2. Pointcuts: A pointcut is a predicate or expression that defines which join points in the application's codebase should be intercepted and associated with an aspect. It allows you to specify the criteria for selecting the join points. Pointcuts are defined using a combination of expressions, annotations, and other matching rules. They define the "where" in the codebase where aspects should be applied.

3. Aspect: An aspect is a modular unit of cross-cutting functionality encapsulated within a class. It defines what actions should be taken or modifications should be made at specific join points. Aspects are typically implemented as classes annotated with the @Aspect annotation in Spring. Within an aspect, you can define advice and pointcuts.

4. Advice: Advice is the action or behavior that is applied at a particular join point. It represents the code that executes before, after, or around the join point. In Spring AOP, different types of advice are supported:
   a. Before advice: Executed before a join point. It can modify the arguments of the method, perform additional checks, or initiate some action.
   b. After returning advice: Executed after a join point successfully completes its execution and returns a result.
   c. After throwing advice: Executed when a join point throws an exception.
   d. After (finally) advice: Executed regardless of whether a join point completes successfully or throws an exception.
   e. Around advice: The most powerful type of advice that surrounds a join point and has full control over its execution. It can choose to proceed with the join point, skip it, modify the arguments or result, or even throw an exception.

5. Weaving: Weaving is the process of linking aspects to the target objects or classes to create the final woven application. It can be performed at compile time, load time, or runtime. Spring AOP supports runtime weaving, which means that aspects are applied to the target objects or classes dynamically during the application's execution.

Spring AOP integrates seamlessly with the Spring Framework, allowing you to apply aspects to Spring-managed beans. It provides a powerful mechanism to separate cross-cutting concerns from the core business logic, resulting in cleaner and more maintainable code.

Note: Spring AOP provides a limited subset of AOP capabilities compared to full-fledged AOP frameworks like AspectJ. If you require more advanced AOP features, you can integrate Spring AOP with AspectJ or use AspectJ directly.

## 5. What are the different bean scopes in spring?

In Spring Framework, bean scope refers to the lifecycle and visibility of a bean instance within the application context. The Spring container can manage beans with different scopes, allowing you to control how and when instances of beans are created and made available. Here are the different bean scopes in Spring:

1. Singleton: This is the default scope in Spring. With singleton scope, the Spring container creates a single instance of the bean for the entire application context. The same instance is returned whenever the bean is requested. Singleton beans are shared across multiple components, and any modifications to the bean's state are visible to all components that use it.

2. Prototype: In contrast to singleton scope, prototype scope creates a new instance of the bean every time it is requested from the container. Each component that requires the bean gets its own instance. Prototype beans are not shared, and any modifications to the state of a prototype bean are isolated to the component using it. It's important to note that Spring does not manage the lifecycle of prototype beans. You are responsible for managing their destruction.

3. Request: The request scope is specific to web applications. With request scope, a new instance of the bean is created for each HTTP request made to the application. The bean instance is bound to the lifecycle of the HTTP request, and different requests will have their own instances of the bean. This scope is useful when you want to have request-specific data or state stored in a bean.

4. Session: The session scope is also specific to web applications. It creates a separate instance of the bean for each user session. The bean instance is bound to the lifecycle of the HTTP session. Each user session will have its own instance of the bean, and the state of the bean is maintained throughout the session. This scope is useful when you need to store user-specific data or state.

5. Application: The application scope creates a single instance of the bean per ServletContext in a web application. The bean instance is shared across the entire application and is accessible to all components within the ServletContext. It is similar to the singleton scope, but limited to a specific web application.

6. WebSocket: The WebSocket scope is also specific to web applications and is available starting from Spring Framework 5.2. It creates a separate instance of the bean for each WebSocket connection. Each WebSocket connection will have its own instance of the bean. This scope is useful when you want to maintain WebSocket-specific data or state.

7. Custom Scopes: Spring also allows you to define custom scopes to meet specific requirements. You can implement your own Scope interface and register it with the Spring container. Custom scopes enable you to define specialized scopes that are tailored to your application's needs.

By selecting an appropriate bean scope, you can control the behavior and lifecycle of your beans in Spring applications, ensuring the correct sharing and management of bean instances based on the specific requirements of your application.

## 6. What is dependency Injection? What is the role IoC container in Spring?

Dependency Injection (DI) is a design pattern and a fundamental concept in software development that focuses on decoupling the dependencies between components. It allows objects to be created and configured externally, and their dependencies to be injected into them rather than having the objects themselves responsible for creating and managing their dependencies.

In the context of Spring, Dependency Injection refers to the process of providing the dependencies of a class from an external source, typically managed by an Inversion of Control (IoC) container. The IoC container takes responsibility for creating and managing objects (beans) and wiring their dependencies.

The key concepts related to Dependency Injection and the role of the IoC container in Spring are as follows:

1. Dependency: A dependency is an object or service that another object relies on to perform its functionality. For example, a service class may depend on a data access object (DAO) to interact with the database. Dependencies can be other objects, services, configurations, or even primitive types.

2. Inversion of Control (IoC): IoC is a broader concept that underlies Dependency Injection. In traditional programming, objects control the creation and management of their dependencies. In contrast, with IoC, control is inverted, and the responsibility for creating and managing dependencies is shifted to an external entity (the IoC container).

3. IoC Container: In the Spring framework, the IoC container is responsible for managing the lifecycle of objects (beans) and their dependencies. It creates, configures, and assembles objects based on the configuration provided, typically in XML files, Java annotations, or Java-based configuration. The IoC container is often referred to as the ApplicationContext or BeanFactory in Spring.

4. Bean: In the context of Spring, a bean is an object that is managed by the IoC container. It is created, configured, and assembled by the container based on the provided configuration. Beans represent components of an application, such as service classes, data access objects, or controllers.

5. Configuration: Spring allows you to define bean configurations that specify how the beans should be created, configured, and wired together. The configuration can be done using XML files, Java annotations, or Java-based configuration classes. The configuration typically includes defining the beans, specifying their dependencies, and configuring any necessary properties.

6. Dependency Injection: Spring's IoC container performs dependency injection by analyzing the configuration and wiring the dependencies between beans. The dependencies can be injected using constructor injection, setter injection, or field injection. The container resolves the dependencies and ensures that the necessary dependencies are available when creating and initializing the beans.

7. Benefits of IoC and Dependency Injection: The use of an IoC container and Dependency Injection brings several benefits to the application development process, including:
   - Loose coupling between components, as dependencies are managed externally.
   - Improved modularity and maintainability, as components are decoupled from their dependencies.
   - Easier unit testing, as dependencies can be easily mocked or replaced.
   - Reusability of components, as they can be easily wired and configured in different contexts.
   - Configurability, as dependencies can be easily changed or updated without modifying the code.

In summary, Dependency Injection is a design pattern that promotes loose coupling and modularity by externalizing the management of dependencies. The IoC container in Spring takes responsibility for creating and managing objects and wiring their dependencies based on the provided configuration. This approach simplifies the development process, improves maintainability, and enhances the flexibility and testability of applications.

## 7. What is Spring Bean? How can you create bean in Spring boot?

In Spring, a bean is an object that is managed by the Spring IoC container. It represents a component of your application and is created, configured, and assembled by the container based on the provided configuration. Beans can be Java objects, instances of classes, or even resources such as database connections or JMS queues.

To create a bean in Spring Boot, you can follow these steps:

1. Annotate the Bean Class: In your Java class, annotate it with the appropriate annotation to indicate that it should be managed as a Spring bean. The most commonly used annotations are:
   - `@Component`: A generic stereotype annotation that indicates a class as a Spring-managed bean.
   - `@Service`: Indicates a service class.
   - `@Repository`: Indicates a data access object (DAO) class.
   - `@Controller`: Indicates a controller class.

2. Define Bean Dependencies: Declare any dependencies that the bean requires. You can use constructor injection, setter methods, or field injection to define the dependencies. The Spring IoC container will resolve and inject these dependencies when creating the bean.

3. Enable Component Scanning: By default, Spring Boot enables component scanning, which means it automatically scans your application's package and its sub-packages for classes annotated with the mentioned stereotype annotations. If your bean class is located in one of these packages, Spring Boot will automatically detect and create the bean.

4. Custom Bean Configuration (Optional): If you want more control over the bean creation and configuration process, you can define a custom bean configuration class. This can be done by creating a separate class annotated with `@Configuration` and defining methods annotated with `@Bean`. These methods return instances of the beans you want to create, and you can provide custom configuration logic within them.

Here's an example of creating a bean in Spring Boot using the `@Component` annotation:

```java
import org.springframework.stereotype.Component;

@Component
public class MyBean {
    // Bean implementation and dependencies
}
```

By annotating the class with `@Component`, Spring Boot will automatically detect and create an instance of `MyBean` as a managed bean.

Alternatively, if you want to define a custom bean configuration, you can create a configuration class:

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class MyBeanConfig {
    
    @Bean
    public MyBean myBean() {
        return new MyBean();
    }
}
```

In this example, the `@Configuration` annotation marks the class as a configuration class, and the `@Bean` annotation indicates that the method `myBean()` will create and provide an instance of `MyBean`. The method can contain custom configuration logic if needed.

Spring Boot will automatically detect the `MyBeanConfig` class and create the bean based on the provided configuration.

These are the basic steps to create a bean in Spring Boot. The Spring IoC container takes care of managing the lifecycle, dependencies, and configurations of the beans, allowing you to focus on the business logic of your application.

## 8. What are the advantages of Spring MVC? Explain the flow of Spring Web MVC

Spring MVC (Model-View-Controller) is a framework within the Spring ecosystem that provides a structured approach to developing web applications. It offers several advantages:

1. Separation of Concerns: Spring MVC follows the MVC architectural pattern, which promotes a clear separation of concerns between the Model (data and business logic), View (presentation layer), and Controller (handles user interactions and coordinates the flow). This separation enhances maintainability, reusability, and testability of the code.

2. Flexible Request Handling: Spring MVC provides a flexible mechanism for handling requests and mapping them to appropriate controllers. It supports multiple ways to define request mappings, including annotations, XML configuration, and default conventions. This allows developers to easily define the routing and handle different types of requests (GET, POST, PUT, DELETE) efficiently.

3. Robust Validation Support: Spring MVC offers built-in support for validation through the integration with the Java Bean Validation API (JSR 303). It provides a rich set of validation annotations that can be used to validate user input, request parameters, and form data. The validation framework helps in ensuring data integrity and provides customizable error handling.

4. Powerful View Resolution: Spring MVC supports various view technologies, including JSP, Thymeleaf, FreeMarker, and others. It provides a unified and flexible view resolution mechanism, allowing developers to choose the appropriate view technology based on their preference or project requirements. It also supports internationalization and localization of views.

5. Flexible Data Binding: Spring MVC supports flexible data binding between the web request parameters and Java objects. It can automatically bind request parameters to Java object properties, reducing the need for manual data conversion. It also provides mechanisms for handling data binding errors and customization of the data binding process.

6. Interceptor Support: Spring MVC allows the use of interceptors, which are components that can be invoked before and after the execution of a request handler. Interceptors provide a way to implement cross-cutting concerns such as logging, security, and caching. They can modify the request or response, perform pre-processing or post-processing logic, and enable aspects of the application to be applied consistently across multiple requests.

7. Testability: Spring MVC promotes testability by providing a well-defined architecture and separation of concerns. It allows for easy unit testing of controllers by using mock objects for the request and response. Additionally, the framework provides testing utilities and support for integration testing with a test-specific application context.

Flow of Spring Web MVC:

1. Request Handling: When a client sends a request to a Spring MVC application, it is intercepted by the DispatcherServlet, which acts as the front controller. The DispatcherServlet is configured in the application's web.xml or using servlet annotations in Spring Boot.

2. Handler Mapping: The DispatcherServlet consults the configured HandlerMappings to determine which controller should handle the request. HandlerMappings map the request to the appropriate controller based on request mappings defined in the controllers or other configuration mechanisms.

3. Controller Execution: Once the appropriate controller is determined, the DispatcherServlet invokes the appropriate controller method to handle the request. The controller method performs the necessary processing based on the requested operation (GET, POST, etc.) and interacts with the model and services to prepare the data.

4. Data Binding: The controller uses data binding to bind the request parameters or form data to the corresponding model objects. It also performs validation using the validation framework if applicable.

5. Model Update: The controller updates the model objects with the processed data or performs any necessary business logic. It prepares the model data that needs to be passed to the view for rendering.

6. View Resolution: The controller returns a logical view name or a View object that represents the view to be rendered. The DispatcherServlet consults the configured ViewResolvers to determine the actual view implementation based on the logical view
name.

7. View Rendering: The selected view is responsible for rendering the model data and generating the response. The view technology (JSP, Thymeleaf, etc.) processes the model data and generates the HTML or other output to be sent back to the client.

8. Response Handling: The DispatcherServlet sends the rendered response back to the client, completing the request-response cycle.

The above steps represent a simplified overview of the Spring Web MVC flow. The framework provides hooks and extension points at each stage to allow customization and integration with other components or frameworks.

## 9. Explain the Spring Web MVC framework controllers

In the Spring Web MVC framework, controllers play a crucial role in handling and processing incoming requests from clients. They are responsible for accepting requests, executing the necessary business logic, and preparing the model data to be rendered by a view. Controllers act as intermediaries between the client and the server-side components of an application. Here's an explanation of the key aspects of Spring Web MVC controllers:

1. Controller Annotation: In Spring Web MVC, controllers are typically annotated with the `@Controller` annotation. This annotation identifies a class as a controller and enables automatic detection and registration of the controller with the Spring IoC container.

2. Request Mapping: Controllers define the request handling methods that correspond to specific URLs or URL patterns. These methods are annotated with `@RequestMapping` or more specific annotations like `@GetMapping`, `@PostMapping`, etc. The annotations specify the URL pattern to map the request to the corresponding controller method.

3. Request Method Handling: Each request handling method in a controller is responsible for handling a specific HTTP request method, such as GET, POST, PUT, DELETE, etc. The method can accept parameters from the request (path variables, query parameters, request headers, etc.) and return a response (model data, view name, etc.).

4. Model and View: Controllers interact with the model to store and retrieve data required by the view. The model can be accessed using method parameters annotated with `@ModelAttribute` or `@RequestParam`. Controllers prepare the model data and return a view name or a `ModelAndView` object, which represents the view to be rendered and the model data to be passed to the view.

5. Model Attributes: Controllers can use `@ModelAttribute` annotations on method parameters or class-level to bind request parameters or form data to model attributes. These attributes can be accessed in the controller method and used to populate the model.

6. View Resolution: Controllers determine the view to be rendered by returning a logical view name or a `View` object. The logical view name is resolved to an actual view implementation by the configured `ViewResolver`. The view is responsible for rendering the model data and generating the response.

7. Redirects and Forwarding: Controllers can perform redirects or forward requests to other controllers or URLs. This can be achieved by returning a special redirect: or forward: prefix along with the URL in the return value.

8. Exception Handling: Controllers can define exception handling methods to handle specific exceptions that may occur during request processing. These methods are annotated with `@ExceptionHandler` and provide custom logic for handling exceptions and generating appropriate error responses.

9. Controller Advice: Controllers can also use the `@ControllerAdvice` annotation to define global exception handling, request preprocessing, or post-processing logic that is applied to multiple controllers.

Overall, Spring Web MVC controllers provide a flexible and powerful mechanism to handle requests, execute business logic, and prepare the model data for rendering. They form the backbone of the MVC pattern and facilitate the development of robust and maintainable web applications.