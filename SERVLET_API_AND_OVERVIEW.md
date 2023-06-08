# SERVLET API AND OVERVIEW

## 1. Servlet Life Cycle

- The web container maintains the life cycle of a servlet instance.
- The life cycle of the servlet:

1. Servlet class is loaded.
2. Servlet instance is created.
3. init method is invoked.
4. service method is invoked.
5. destroy method is invoked.

![Servlet Life Cycle](https://static.javatpoint.com/images/servletlife.jpg)

- In the above diagram, there are three states of a servlet: new, ready and end.

- The servlet is in new state if servlet instance is created. After invoking the init() method, Servlet comes in the ready state.

- In the ready state, servlet performs all the tasks.

- When the web container invokes the destroy() method, it shifts to the end state.

### 1. Servlet class is loaded

- The classloader is responsible to load the servlet class.
- The servlet class is loaded when the first request for the servlet is received by the web container.

### 2. Servlet instance is created

- The web container creates the instance of a servlet after loading the servlet class.
- The servlet instance is created only once in the servlet life cycle.

### 3. init method is invoked

- The web container calls the init method only once after creating the servlet instance.
- The init method is used to initialize the servlet.
- It is the life cycle method of the `javax.servlet.Servlet` interface.

### 4. service method is invoked

- The web container calls the service method each time when request for the servlet is received.
- If servlet is not initialized, it follows the first three steps as described above then calls the service method.
- If servlet is initialized, it calls the service method.
- servlet is initialized only once.

### 5. destroy method is invoked

- The web container calls the destroy method before removing the servlet instance from the service.
- It gives the servlet an opportunity to clean up any resource for example memory, thread etc.

<img src="https://media.geeksforgeeks.org/wp-content/uploads/Life-Cycle-Methods-of-a-Servlet.jpg"  height="280">

### Servlet Code

`MyServlet.java`

```java
import java.io.*;
import javax.servlet.*;
public class MyServlet1 extends GenericServlet{
    public void init() throws ServletException{
            //Initailization Code
        }
    public void service(ServletRequest request,ServletResponse response) throws
    ServletException,IOException{
        //Servlet code
    }
    public void destroy(){
        //Finalization Code
    }
}
```

## 2. CGI vs Servlet

| CGI                                                                       | Servlet                                                               |
| ------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| CGI was not portable.                                                     | Servlets are portable.                                                |
| CGI is more expensive than Servlets                                       | Servlets is inexpensive than CGI                                      |
| In CGI each request is handled by heavy weight OS process                 | In Servlets each request is handled by lightweight Java Thread        |
| Session tracking and caching of previous computations cannot be performed | Session tracking and caching of previous computations can be performe |
| CGI cannot handle cookies                                                 | Servlets can handle cookies                                           |
| CGI does not provide sharing property                                     | Servlets can share data among each other                              |

<img src="https://studyglance.in/servlet/images/cgi-process.jpg" alt="cgi" height="280">
<img src="https://studyglance.in/servlet/images/servlet-process.jpg" alt="servlet" height="280">

## 3. DoGet vs DoPost

| DoGet                                                                                                                    | DoPost                                                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| In doGet Method the parameters are appended to the URL and sent along with header information                            | In doPost, parameters are sent in separate line in the body                                                                                                                                               |
| Maximum size of data that can be sent using doget is 240 bytes                                                           | There is no maximum size for data                                                                                                                                                                         |
| Parameters are not encrypted                                                                                             | Parameters are encrypted                                                                                                                                                                                  |
| DoGet method generally is used to query or to get some information from the server                                       | Dopost is generally used to update or post some information to the server                                                                                                                                 |
| DoGet is faster if we set the response content length since the same connection is used. Thus increasing the performance | DoPost is slower compared to doGet since doPost does not write the content length                                                                                                                         |
| DoGet should be idempotent. i.e. doget should be able to be repeated safely many times                                   | This method does not need to be idempotent. Operations requested through POST can have side effects for which the user can be held accountable, for example, updating stored data or buying items online. |
| DoGet should be safe without any side effects for which user is held responsible                                         | This method does not need to be either safe                                                                                                                                                               |

## 4. Differentiate ServletConfig and ServletContext.

|                                          ServletConfig                                           |                                                             ServletContext                                                              |
| :----------------------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------------------: |
|                                ServletConfig is servlet specific                                 |                                                 ServletContext is for whole application                                                 |
| Parameters of servletConfig are present as name-value pair in `<init-param>` inside `<servlet>`. | Parameters of servletContext are present as name-value pair in `<context-param>` which is outside of `<servlet>` and inside `<web-app>` |
|                  ServletConfig object is obtained by getServletConfig() method.                  |                                    ServletContext object is obtained by getServletContext() method.                                     |
|                        Each servlet has got its own ServletConfig object.                        |                          ServletContext object is only one and used by different servlets of the application.                           |
|             Use ServletConfig when only one servlet needs information shared by it.              |                                Use ServletContext when whole application needs information shared by it                                 |

## 5. What is Request Dispatcher? What is the difference between RequestDispatcher’s forward() and include() method? Explain it in detail with program

- The `RequestDispatcher` interface in Java Servlets provides a way to forward the request from one servlet to another or include the response of another servlet in the current servlet's response. It is commonly used for servlet collaboration and dynamic resource sharing within a web application.

- The `forward()` method of `RequestDispatcher` is used to forward the request and response objects from the current servlet to another servlet or JSP. Once the `forward()` method is called, the control is transferred to the new servlet, and it becomes responsible for generating the response. The new servlet receives the same request and response objects as the previous servlet. The client is unaware of the servlet change and perceives it as a single response from the original request.

- The `include()` method of `RequestDispatcher` is used to include the response of another servlet or JSP in the current servlet's response. When `include()` is called, the output of the included servlet or JSP is added to the current servlet's output. After the included servlet or JSP is executed, the control returns to the current servlet, and it continues generating its own response. The final response is a combination of the output from both servlets or JSPs.

- Here's an example that demonstrates the usage of `forward()` and `include()` methods:

- Assume we have two servlets: `FirstServlet` and `SecondServlet`.

**FirstServlet.java:**

```java
import javax.servlet.*;
import javax.servlet.http.*;
import java.io.*;

public class FirstServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {

        // Forwarding the request to SecondServlet
        RequestDispatcher dispatcher = request.getRequestDispatcher("SecondServlet");
        dispatcher.forward(request, response);

        // The control will not return here
    }
}
```

**SecondServlet.java:**

```java
import javax.servlet.*;
import javax.servlet.http.*;
import java.io.*;

public class SecondServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {

        // Writing the response
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();
        out.println("<h2>This is the response from SecondServlet</h2>");
        out.close();
    }
}
```

- In this example, when a client requests `FirstServlet`, the `forward()` method is called to transfer the request and response objects to `SecondServlet`. `SecondServlet` generates a response, and that response is sent back to the client as if it was directly requested from `FirstServlet`.

- On the other hand, if we replace `forward()` with `include()` in `FirstServlet`, the output of `SecondServlet` will be included in the response of `FirstServlet`. The control will return to `FirstServlet` after executing `SecondServlet`, and `FirstServlet` will continue generating its own response.

- Note: Make sure to configure the servlets in the `web.xml` file or use annotations, as per the Servlet version you are using, to map the servlets to their respective URLs.

## 6. What is a session? List out various session management techniques

In Java, a session refers to a mechanism that allows the server to maintain stateful information about a user across multiple requests and responses. It is used to store user-specific data and maintain the user's identity during their interaction with a web application.

Session Management Techniques in Java:

1. Cookies: The most common and widely used technique for session management is through cookies. The server sends a unique session identifier to the client's browser as a cookie, and the browser includes this cookie in subsequent requests. The server then uses the session identifier to retrieve the associated session data.

2. URL Rewriting: This technique involves appending the session identifier as a parameter in the URL of each page. The server extracts the session identifier from the URL to identify and retrieve the session data. However, this technique is less secure and can be vulnerable to session hijacking.

3. Hidden Form Fields: Session data can be embedded in hidden form fields within HTML forms. The server includes the session data in the HTML form, and the browser submits it back to the server with each request. The server uses the hidden form field value to identify and retrieve the session data.

4. HttpSession: Java Servlets provide the HttpSession interface to manage sessions. It stores session data on the server and associates it with a unique session identifier. The session identifier is typically stored as a cookie on the client's browser. The server uses the session identifier to retrieve the corresponding session data.

## 7. What are cookies? Demonstrate the use of cookies in servlet

- Cookies are small pieces of data stored on the client's browser by a web server. They are used to maintain stateful information and track user activity across multiple requests and responses. Cookies are sent back to the server with each subsequent request, allowing the server to personalize the user experience and provide customized content.

- Here's an example that demonstrates the use of cookies in a servlet:

```java
import javax.servlet.*;
import javax.servlet.http.*;
import java.io.*;

public class CookieServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {

        // Get the value of the cookie
        Cookie[] cookies = request.getCookies();
        String username = null;
        if (cookies != null) {
            for (Cookie cookie : cookies) {
                if (cookie.getName().equals("username")) {
                    username = cookie.getValue();
                    break;
                }
            }
        }

        // Set a new cookie if it doesn't exist
        if (username == null) {
            username = "JohnDoe";
            Cookie cookie = new Cookie("username", username);
            cookie.setMaxAge(60 * 60 * 24 * 30); // Cookie expires after 30 days
            response.addCookie(cookie);
        }

        // Generate the response
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();
        out.println("<h2>Welcome, " + username + "!</h2>");
        out.close();
    }
}
```

- In this example, the `doGet()` method of the `CookieServlet` class is overridden to handle GET requests.

- The servlet first checks if the client has sent any cookies by calling `request.getCookies()`. If cookies exist, it searches for a cookie named "username" and retrieves its value.

- If the "username" cookie does not exist, the servlet sets a new cookie using `response.addCookie()`. The cookie is named "username" and its value is set to "JohnDoe". Additionally, the `setMaxAge()` method is used to set the cookie's expiration time to 30 days.

- Finally, the servlet generates the response using a `PrintWriter`. It displays a welcome message using the retrieved or newly set username value.

- Please note that the cookie handling code should be placed in the appropriate methods according to your application's logic and requirements, such as `doGet()`, `doPost()`, or a dedicated method for cookie handling.

## 8. What is filter? How will you configure filter using deployment descriptor?

- In Java, a filter is a component that intercepts and processes requests and responses between a client and a servlet or web application. Filters can perform various tasks such as logging, authentication, authorization, data transformation, or modification of the request/response.

- To configure a filter using the deployment descriptor (`web.xml`) in Java, you need to follow these steps:

1. Open the `web.xml` file, which is typically located in the `WEB-INF` directory of your web application.

2. Define the filter by specifying its name and class in the deployment descriptor. For example:

   ```xml
   <filter>
       <filter-name>MyFilter</filter-name>
       <filter-class>com.example.MyFilter</filter-class>
   </filter>
   ```

3. Configure the filter's initialization parameters, if required. These parameters provide additional configuration options for the filter. For example:

   ```xml
   <filter>
       <filter-name>MyFilter</filter-name>
       <filter-class>com.example.MyFilter</filter-class>
       <init-param>
           <param-name>param1</param-name>
           <param-value>value1</param-value>
       </init-param>
       <init-param>
           <param-name>param2</param-name>
           <param-value>value2</param-value>
       </init-param>
   </filter>
   ```

4. Map the filter to specific servlets or URL patterns that you want the filter to intercept. This determines when the filter will be applied. For example:

   ```xml
   <filter-mapping>
       <filter-name>MyFilter</filter-name>
       <url-pattern>/myServlet/*</url-pattern>
   </filter-mapping>
   ```

   - In the above example, the filter named "MyFilter" is mapped to URLs that start with "/myServlet/". You can also use `<servlet-name>` instead of `<url-pattern>` to map the filter to a specific servlet.

5. Save the `web.xml` file with the changes.

- By configuring the filter in the deployment descriptor (`web.xml`), you define its name, class, initialization parameters, and mapping to the desired servlets or URL patterns. The filter will be invoked automatically when the specified requests are made, allowing you to perform the necessary operations on the requests and responses.

## 9. What is FilterConfig? How will you use it?

- The `FilterConfig` interface in Java Servlets provides configuration information for a filter. It allows the filter to access initialization parameters defined in the deployment descriptor (`web.xml`) and obtain references to the servlet context and the filter's name.

- To use `FilterConfig`, you typically implement the `init()` method of the `Filter` interface and receive the `FilterConfig` object as a parameter. Here's a simple example:

```java
import javax.servlet.*;
import java.io.IOException;

public class MyFilter implements Filter {
    private FilterConfig filterConfig;

    public void init(FilterConfig filterConfig) throws ServletException {
        this.filterConfig = filterConfig;

        // Access initialization parameters
        String paramValue = filterConfig.getInitParameter("paramName");
        System.out.println("Initialization Parameter Value: " + paramValue);

        // Access the servlet context
        ServletContext servletContext = filterConfig.getServletContext();

        // Access the filter name
        String filterName = filterConfig.getFilterName();
        System.out.println("Filter Name: " + filterName);
    }

    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
            throws IOException, ServletException {
        // Filter logic here

        // Pass the request and response to the next filter or servlet in the chain
        chain.doFilter(request, response);
    }

    public void destroy() {
        // Clean up resources
    }
}
```

- In this example, the `init()` method is implemented to access the `FilterConfig` object. The `getInitParameter()` method is used to retrieve the value of an initialization parameter specified in the `web.xml` file. The `getServletContext()` method is used to obtain a reference to the servlet context. The `getFilterName()` method retrieves the name of the filter.

- You can use the retrieved initialization parameter values or the servlet context in your filter's logic to perform tasks such as configuration, initialization, or custom processing based on the specific requirements of your application.

## 10. Write a servlet code which reads the student details from web page and stores it in database

```java
import java.io.*;
import java.sql.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class StudentServlet extends HttpServlet {

    protected void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {

        // Read student details from the request parameters
        String name = request.getParameter("name");
        String rollNo = request.getParameter("rollNo");

        // JDBC database connection
        String jdbcUrl = "jdbc:mysql://localhost:3306/mydatabase";
        String username = "your_username";
        String password = "your_password";

        try {
            // Create database connection
            Connection connection = DriverManager.getConnection(jdbcUrl, username, password);

            // Prepare the SQL statement
            String sql = "INSERT INTO students (name, roll_no) VALUES (?, ?)";
            PreparedStatement statement = connection.prepareStatement(sql);
            statement.setString(1, name);
            statement.setString(2, rollNo);

            // Execute the SQL statement
            statement.executeUpdate();

            // Close the database connection
            statement.close();
            connection.close();

            // Send a response to the client
            response.setContentType("text/html");
            PrintWriter out = response.getWriter();
            out.println("<h2>Student details saved successfully!</h2>");

        } catch (SQLException e) {
            e.printStackTrace();
            // Handle any errors that occur during database connection or SQL execution
            response.setContentType("text/html");
            PrintWriter out = response.getWriter();
            out.println("<h2>Error occurred while saving student details</h2>");
        }
    }
}
```
