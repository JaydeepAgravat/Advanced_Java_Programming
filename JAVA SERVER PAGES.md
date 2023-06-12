# JAVA SERVER PAGES

## 1. What is difference between include directive and jsp:include action tag?

In JavaServer Pages (JSP), there are two ways to include the content of another resource within a JSP page: using the include directive (`<%@ include %>`) and the `<jsp:include>` action tag. While both achieve a similar purpose, there are some differences between them:

1. Syntax: The syntax of the include directive and `<jsp:include>` action tag is different:
   - Include Directive: The include directive is a static include and is written using the `<%@ include file="includedFile.jsp" %>` syntax. It is processed during the JSP translation phase, and the content of the included file is directly inserted into the JSP page.
   - `<jsp:include>` Action Tag: The `<jsp:include>` action tag is a dynamic include and is written using the `<jsp:include page="includedFile.jsp" />` syntax. It is processed during the JSP execution phase, and the content of the included file is fetched and executed during runtime.

2. Time of Processing: The include directive is processed during the JSP translation phase, while the `<jsp:include>` action tag is processed during the JSP execution phase. This means that the content included using the include directive becomes a part of the JSP page at the time of translation, whereas the content included using the `<jsp:include>` action tag is fetched and included during runtime.

3. Dynamic Behavior: The `<jsp:include>` action tag allows for dynamic behavior. This means that the inclusion of content can be conditional and determined during the execution phase. For example, you can include different files based on certain conditions or parameters. On the other hand, the include directive is a static inclusion and cannot be dynamically changed based on runtime conditions.

4. Request Dispatch: The `<jsp:include>` action tag performs a request dispatch to the included resource. This means that the included resource is treated as a separate request, and the control returns to the calling JSP page after the included resource is executed. The response of the included resource is included in the output of the calling JSP page. In contrast, the include directive directly inserts the content of the included file into the calling JSP page without performing a request dispatch.

In summary, the main differences between the include directive and `<jsp:include>` action tag in JSP are their processing time, dynamic behavior, and request dispatch behavior. The include directive is processed during translation, provides static inclusion, and does not perform a request dispatch. On the other hand, the `<jsp:include>` action tag is processed during runtime, allows for dynamic behavior, and performs a request dispatch to the included resource.

## 2. Explain any four implicit objects of JSP

In JSP (JavaServer Pages), implicit objects are predefined objects that are automatically available to developers without the need for explicit declaration or initialization. These objects provide easy access to various aspects of the JSP page and the web application environment. Here are four commonly used implicit objects in JSP:

1. `request`: The `request` object represents the client's HTTP request sent to the server. It provides methods to access request parameters, headers, cookies, session, and other attributes. For example, `request.getParameter("paramName")` retrieves the value of a request parameter.

2. `response`: The `response` object represents the server's HTTP response that will be sent back to the client. It provides methods to set response headers, cookies, and write content to the response output stream. For example, `response.getWriter().println("Hello, World!")` sends the text "Hello, World!" as the response content.

3. `session`: The `session` object represents the user's session, which maintains state information across multiple requests from the same client. It provides methods to store and retrieve session attributes. For example, `session.setAttribute("username", "John")` stores the value "John" with the attribute name "username" in the session.

4. `application`: The `application` object represents the servlet context or application-wide context of the web application. It provides methods to store and retrieve application-level attributes, such as shared data or configuration parameters. For example, `application.setAttribute("appName", "MyApp")` stores the value "MyApp" with the attribute name "appName" in the application context.

These implicit objects are automatically available in every JSP page, allowing developers to access and manipulate various aspects of the request, response, session, and application context without explicitly retrieving them from the Servlet API. Implicit objects simplify development and promote rapid development of dynamic web applications by providing easy access to essential information and functionalities.

## 3. Explain JSP page directives with example

JSP (JavaServer Pages) page directives are instructions that provide configuration information to the JSP container or modify the default behavior of the JSP page. They are specified using special tags that start with `<%@` and end with `%>`. Page directives are typically placed at the top of the JSP page, before any Java code or HTML content. Here are some commonly used JSP page directives:

1. `page`: The `page` directive is used to define various attributes and settings for the JSP page. Some of the commonly used attributes are:

   - `import`: Specifies a list of Java import statements that will be added to the generated servlet class. This allows you to use specific Java classes and libraries in your JSP code.

     ```java
     <%@ page import="java.util.List, java.util.ArrayList" %>
     ```

   - `session`: Specifies whether the JSP page requires a session. If set to "true" (default), the JSP container ensures that a session is available for the page.

     ```java
     <%@ page session="false" %>
     ```

   - `contentType`: Specifies the MIME type and character encoding of the response generated by the JSP page.

     ```java
     <%@ page contentType="text/html; charset=UTF-8" %>
     ```

2. `include`: The `include` directive is used to include the content of an external file during the JSP translation phase. It is similar to the `<%@ include file="includedFile.jsp" %>` directive. The included file is directly inserted into the JSP page during translation.

   ```java
   <%@ include file="header.jsp" %>
   ```

3. `taglib`: The `taglib` directive is used to declare and configure custom tag libraries that will be used in the JSP page. It specifies the URI of the tag library and the location of the tag library descriptor (TLD) file.

   ```java
   <%@ taglib uri="http://example.com/mytags" prefix="my" %>
   ```

4. `extends`: The `extends` directive is used to specify the class that the generated servlet for the JSP page should extend. It allows you to provide a custom base class for the JSP page's servlet.

   ```java
   <%@ page extends="com.example.MyCustomServlet" %>
   ```

These are just a few examples of JSP page directives. Page directives allow you to configure various aspects of the JSP page, import Java classes, define custom tag libraries, and more. They provide flexibility and control over the behavior and execution of the JSP page.

## 4. What are the implicit objects of JSP? Write a JSP page to demonstrate the use them

The implicit objects in JSP are predefined objects that are automatically available to developers without the need for explicit declaration or initialization. These objects provide easy access to various aspects of the JSP page and the web application environment. The commonly used implicit objects in JSP are `request`, `response`, `session`, `application`, `out`, and `pageContext`. Here's an example of a JSP page that demonstrates the use of these implicit objects:

```java
<%@ page contentType="text/html; charset=UTF-8" %>
<!DOCTYPE html>
<html>
<head>
  <title>Implicit Objects Example</title>
</head>
<body>
  <h1>Implicit Objects Example</h1>
  
  <%-- Accessing the implicit objects --%>
  
  <h2>Request Object:</h2>
  <p>Server Name: <%= request.getServerName() %></p>
  <p>Request URI: <%= request.getRequestURI() %></p>
  
  <h2>Response Object:</h2>
  <p>Response Content Type: <%= response.getContentType() %></p>
  
  <h2>Session Object:</h2>
  <p>Session ID: <%= session.getId() %></p>
  
  <h2>Application Object:</h2>
  <p>Application Name: <%= application.getInitParameter("appName") %></p>
  
  <h2>Out Object:</h2>
  <% out.println("Hello from the out object!"); %>
  
  <h2>PageContext Object:</h2>
  <% pageContext.setAttribute("message", "Welcome to JSP!"); %>
  <p><%= pageContext.getAttribute("message") %></p>
</body>
</html>
```

In this example, the JSP page starts with the page directive specifying the content type as HTML. Then, the implicit objects are accessed and their properties or methods are used to display information on the page. The `request` object is used to retrieve the server name and request URI. The `response` object is used to get the content type of the response. The `session` object is used to retrieve the session ID. The `application` object is used to access an application-level parameter. The `out` object is used to print a message to the response output stream. The `pageContext` object is used to set an attribute and retrieve its value.

When the JSP page is rendered, the information from the implicit objects is displayed on the page, demonstrating their usage and providing access to various aspects of the JSP page and the web application environment.

## 5. What are the directive tags of JSP? Write a JSP page to demonstrate the use of them

In JSP (JavaServer Pages), directive tags are used to provide instructions to the JSP container regarding the configuration and behavior of the JSP page. There are three types of directive tags in JSP: `page`, `include`, and `taglib`. Here's an example of a JSP page that demonstrates the use of these directive tags:

```java
<%@ page contentType="text/html; charset=UTF-8" %>
<%@ include file="header.jsp" %>
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<!DOCTYPE html>
<html>
<head>
  <title>Directive Tags Example</title>
</head>
<body>
  <h1>Directive Tags Example</h1>
  
  <%-- Using directive tags --%>
  
  <%-- Page Directive --%>
  <p>This is a JSP page directive example.</p>
  
  <%-- Include Directive --%>
  <%-- The header.jsp file is included here --%>
  
  <%-- Taglib Directive --%>
  <c:forEach var="num" begin="1" end="5">
    <p>Iteration <%= num %></p>
  </c:forEach>
  
  <%-- Rest of the JSP page content --%>
  
  <h2>Page Content</h2>
  <p>This is the content of the JSP page.</p>
  
  <%-- The footer.jsp file is included here --%>
  <%@ include file="footer.jsp" %>
</body>
</html>
```

In this example, the JSP page begins with the `page` directive, which sets the content type of the page to HTML. The `include` directive is used to include the contents of the `header.jsp` and `footer.jsp` files into the JSP page. The `taglib` directive is used to declare the usage of the JSTL (JavaServer Pages Standard Tag Library) core tag library, which provides additional functionality to the JSP page.

Within the JSP page, the directive tags are used within JSP comments (`<%-- --%>`) to differentiate them from regular JSP code. The `page` directive provides instructions related to the JSP page itself. The `include` directive is used to include the contents of external files during JSP translation. The `taglib` directive declares the usage of a tag library and associates it with a prefix that can be used to access the tags defined in that library.

The rest of the JSP page contains regular HTML and JSP code. In this example, the JSTL `forEach` tag from the declared tag library is used to iterate over a range of numbers and display them on the page.

The example demonstrates the usage of the `page`, `include`, and `taglib` directive tags in a JSP page, showing how they provide instructions to the JSP container and enable the inclusion of external files and the usage of tag libraries.

## 6. What are the attributes for the JSP page directive?

The `page` directive in JSP (JavaServer Pages) is used to provide configuration settings and attributes for the JSP page. It is specified using the `<%@ page %>` syntax. Here are some commonly used attributes for the `page` directive:

1. `import`: This attribute is used to specify a list of Java import statements that will be added to the generated servlet class for the JSP page. It allows you to import specific Java classes and packages that you need to use in your JSP code.

   Example: `<%@ page import="java.util.List, java.util.ArrayList" %>`

2. `session`: This attribute specifies whether the JSP page requires a session. If set to `"true"` (default), the JSP container ensures that a session is available for the page. If set to `"false"`, the JSP container may or may not create a session for the page.

   Example: `<%@ page session="false" %>`

3. `contentType`: This attribute is used to specify the MIME type and character encoding of the response generated by the JSP page. The `contentType` value typically consists of the MIME type and the character encoding.

   Example: `<%@ page contentType="text/html; charset=UTF-8" %>`

4. `isErrorPage`: This attribute is used to indicate whether the JSP page should be treated as an error page. If set to `"true"`, the JSP container treats the page as an error page, and it can handle uncaught exceptions and display error information.

   Example: `<%@ page isErrorPage="true" %>`

5. `errorPage`: This attribute is used to specify the URL of another JSP page or servlet that will handle the exceptions thrown on the current JSP page when it is configured as an error page.

   Example: `<%@ page errorPage="/error.jsp" %>`

6. `extends`: This attribute is used to specify the fully qualified name of the class that the generated servlet for the JSP page should extend. It allows you to provide a custom base class for the generated servlet.

   Example: `<%@ page extends="com.example.MyCustomServlet" %>`

These are some of the commonly used attributes for the `page` directive in JSP. The `page` directive provides various configuration options and settings to control the behavior of the JSP page and customize its generated servlet class.

## 7. What is Expression Language EL in JSP explain with suitable example program?

Expression Language (EL) is a simplified scripting language introduced in JSP (JavaServer Pages) to simplify the expression evaluation and data manipulation within JSP pages. EL provides a convenient way to access data stored in various scopes (such as request, session, application, and page) and perform operations on that data without the need for Java code.

Here's an example program that demonstrates the usage of Expression Language in JSP:

```java
<%@ page contentType="text/html; charset=UTF-8" %>
<!DOCTYPE html>
<html>
<head>
  <title>Expression Language Example</title>
</head>
<body>
  <h1>Expression Language Example</h1>
  
  <%-- Setting request attributes --%>
  <% request.setAttribute("name", "John Doe"); %>
  <% request.setAttribute("age", 30); %>
  
  <%-- Accessing request attributes using EL --%>
  <h2>Request Attributes:</h2>
  <p>Name: ${requestScope.name}</p>
  <p>Age: ${requestScope.age}</p>
  
  <%-- Calculating and displaying values using EL --%>
  <h2>Calculated Values:</h2>
  <p>Sum: ${10 + 20}</p>
  <p>Product: ${5 * 4}</p>
  
  <%-- Accessing session attributes using EL --%>
  <% session.setAttribute("username", "johndoe"); %>
  <h2>Session Attribute:</h2>
  <p>Username: ${sessionScope.username}</p>
  
  <%-- Accessing application attributes using EL --%>
  <% application.setAttribute("appName", "MyApp"); %>
  <h2>Application Attribute:</h2>
  <p>App Name: ${applicationScope.appName}</p>
</body>
</html>
```

In this example, the JSP page starts with the page directive specifying the content type as HTML. Inside the JSP code, request attributes (`name` and `age`) are set using Java code.

Using EL, we can access these attributes directly within the HTML content without writing any Java code. `${requestScope.name}` and `${requestScope.age}` access the corresponding request attributes and display their values.

EL can also perform calculations and display the results. `${10 + 20}` and `${5 * 4}` calculate the sum and product, respectively, and display them.

The example also demonstrates the usage of EL with session and application attributes. The session attribute `username` and application attribute `appName` are set using Java code and accessed using `${sessionScope.username}` and `${applicationScope.appName}`, respectively.

When the JSP page is rendered, the values of request attributes, calculated values, and attributes from session and application scopes are displayed on the page using EL expressions. EL simplifies data access and expression evaluation within JSP pages, reducing the need for explicit Java code and making the page more readable and maintainable.

## 8. Which action tags are used to access the JavaBeans from a JSP page?

In JSP (JavaServer Pages), there are two action tags used to access JavaBeans from a JSP page: `<jsp:useBean>` and `<jsp:getProperty>`. These action tags provide a convenient way to work with JavaBeans within JSP pages.

1. `<jsp:useBean>`:
   - The `<jsp:useBean>` action tag is used to instantiate a JavaBean or locate an existing instance of a JavaBean in the specified scope.
   - It has attributes such as `id`, `class`, `scope`, and `type` that define the behavior and characteristics of the JavaBean.
   - The `<jsp:useBean>` tag typically appears at the top of the JSP page or in the `<body>` section before using the bean's properties or methods.
   - Example usage: `<jsp:useBean id="userBean" class="com.example.UserBean" scope="request" />`

2. `<jsp:getProperty>`:
   - The `<jsp:getProperty>` action tag is used to retrieve the value of a property from a JavaBean and display it in the JSP page.
   - It takes the `name` attribute, which specifies the name of the bean, and the `property` attribute, which specifies the name of the property to retrieve.
   - The `<jsp:getProperty>` tag can be used within HTML tags to display the value dynamically.
   - Example usage: `<jsp:getProperty name="userBean" property="username" />`

Here's an example that demonstrates the usage of both action tags together:

```java
<%@ page contentType="text/html; charset=UTF-8" %>
<!DOCTYPE html>
<html>
<head>
  <title>Accessing JavaBeans Example</title>
</head>
<body>
  <h1>Accessing JavaBeans Example</h1>
  
  <%-- Instantiating the JavaBean using <jsp:useBean> --%>
  <jsp:useBean id="userBean" class="com.example.UserBean" scope="request" />
  
  <%-- Accessing and displaying JavaBean properties using <jsp:getProperty> --%>
  <h2>User Information:</h2>
  <p>Username: <jsp:getProperty name="userBean" property="username" /></p>
  <p>Email: <jsp:getProperty name="userBean" property="email" /></p>
  <p>Age: <jsp:getProperty name="userBean" property="age" /></p>
</body>
</html>
```

In this example, the `<jsp:useBean>` tag is used to instantiate a `UserBean` object with the id `userBean` and store it in the request scope. Then, the `<jsp:getProperty>` tags retrieve and display the values of `username`, `email`, and `age` properties from the `userBean` object.

These action tags allow easy integration and interaction with JavaBeans in JSP pages, providing a convenient way to access and display data stored in JavaBean objects.

## 9. Explain JSP inbuilt objects with their use in application

JSP (JavaServer Pages) provides several inbuilt objects that are automatically available in every JSP page. These objects are pre-initialized by the JSP container and provide access to various aspects of the JSP environment, request processing, and web application functionality. Here are some commonly used inbuilt objects in JSP and their uses in an application:

1. `request`: The `request` object represents the client's request to the server and provides access to request-related information and functionality. It allows you to retrieve parameters, headers, cookies, and other request attributes. It can also be used to forward or include other resources in the request processing flow.

   Example uses:
   - Accessing request parameters: `String name = request.getParameter("name");`
   - Forwarding to another resource: `request.getRequestDispatcher("/somePage.jsp").forward(request, response);`

2. `response`: The `response` object represents the server's response to the client and provides methods to manipulate the response content and send it back to the client. It allows you to set response headers, write response content, and control the response behavior.

   Example uses:
   - Setting response content type: `response.setContentType("text/html");`
   - Writing response content: `response.getWriter().println("Hello, World!");`

3. `session`: The `session` object represents the user's session and provides a way to store and retrieve session-related data. It allows you to create, invalidate, and manage user sessions. Data stored in the session is accessible across multiple requests from the same user.

   Example uses:
   - Storing session attributes: `session.setAttribute("username", "john");`
   - Retrieving session attributes: `String username = (String) session.getAttribute("username");`

4. `application`: The `application` object represents the web application and provides access to application-level data and functionality. It allows you to store global information and share it across multiple users and requests within the same application.

   Example uses:
   - Storing application attributes: `application.setAttribute("appName", "MyApp");`
   - Retrieving application attributes: `String appName = (String) application.getAttribute("appName");`

5. `out`: The `out` object represents the output stream to which the response is written. It provides methods to write content to the response output stream. It is typically used to send dynamic content to the client.

   Example uses:
   - Writing content to the response: `out.println("Hello, World!");`

These inbuilt objects in JSP provide easy access to various aspects of the JSP environment and web application functionality. They simplify request processing, response handling, session management, and content generation within JSP pages, making it convenient to develop dynamic web applications.

## 10. What is a custom tag? Explain the life cycle of tag handler

A custom tag in JSP (JavaServer Pages) is a user-defined tag that encapsulates specific functionality and can be used within JSP pages. Custom tags allow you to create reusable components or functionalities that can be easily included in multiple JSP pages. They provide a way to separate the presentation logic from the content of the JSP page, promoting modular and maintainable code.

The life cycle of a tag handler, which is responsible for handling the custom tag, consists of several phases:

1. Tag Instantiation: When a custom tag is encountered in a JSP page, the tag handler class associated with the tag is instantiated by the JSP container. This happens once for each occurrence of the tag in the JSP page.

2. Setting Tag Attributes: After instantiation, the container sets the attributes of the tag by invoking setter methods on the tag handler class. These attributes can be defined in the tag's attribute directives or provided as runtime attributes in the JSP page.

3. Invoking Tag Handler Methods: Once the tag attributes are set, the container calls various methods on the tag handler class to perform tag-specific processing. The most commonly used methods are:

   - `doStartTag()`: This method is invoked at the start of the tag and is responsible for any setup or initialization required before processing the tag's content.
   - `doEndTag()`: This method is invoked at the end of the tag and is responsible for any cleanup or final processing after processing the tag's content.
   - `doAfterBody()`: This method is invoked if the tag has a body content and is responsible for processing the body content iteratively if needed.

   These methods allow you to define the behavior of the custom tag, such as generating content, interacting with the JSP environment, and controlling the flow of the JSP page.

4. Evaluating Tag Body: If the custom tag has a body content, the JSP container evaluates the body content and passes it to the tag handler class for processing. The body content can be processed iteratively using the `doAfterBody()` method.

5. Releasing Resources: After the tag is processed, the container calls the `release()` method on the tag handler class. This method is responsible for releasing any resources held by the tag handler, such as closing database connections or freeing up memory.

The life cycle of a tag handler allows you to define custom behavior and logic that can be seamlessly integrated into JSP pages. It provides a way to extend the functionality of JSP by encapsulating specific functionality into reusable components, making JSP development more modular, readable, and maintainable.
