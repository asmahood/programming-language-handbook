# Servlets
A Java servlet is a Java class whose sole purpose is to receive a network request and response object (typically HTTP) and construct the necessary response. To start working with servlets you'll need a web server and a servlet container. **Tomcat** gives both for free.

## Prerequisites

- Install and start Tomcat
- Verify Tomcat was started successfully by navigating to `http://localhost:8080` in a browser
- Create a new directory in the Tomcat `webapps/` directory
- Setup the project like so:
  - `WEB-INF/`
    - `src/` - Contains Java source files (`.java`)
    - `classes/` - Contains Java bytecode files (`.class`)
    - `lib/` - Cotanins JARs needed by our web application
    - `web.xml` - An XML deployment descriptor file needed by Tomcat to deploy our servlets. We can define things like servlets, URL mappings, and more.
  - HTML files

## Creating a Servlet

Java provides the `GenericServlet` and `HttpServlet` classes which can be extended to create a custom servlet. Using a protocol-specific subclass (like `HTTPServlet`) is recommended. To start, you need several imports:
```java
import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
```
Then define a class that extends `HttpServlet` class and a `private static final serialVersionUID`:
```java
public class HomeServlet extends HttpServlet {
  private static final long serialVersionUID = 100L;  // Used for serialization since `HttpServlet` implements `Serializable`. 
}
```
Next, implement the `doGet` method:
```java
public void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
  PrintWriter out = response.getWriter();
  out.println("<html>");
  out.println("<head><title>My Icecream Shop!</title></head>");
  out.println("<body>");
  out.println("<h1>Welcome To My Ice Cream Parlor</h1>");
  out.println("</body></html>");
}
```
To make the servlet "visible" to the server, modify the `web.xml` file:
```xml
  <servlet>
    <servlet-name>homeServlet</servlet-name>
    <servlet-class>HomeServlet</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>homeServlet</servlet-name>
    <url-pattern>/home</url-pattern>
  </servlet-mapping>
```

### Request Parameters and Dynamic Responses
To access the body of a request, you can use the `getParameter(String paramName)` method on `HTTPServletRequest`:
```java
public void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
  String cupOrCone = request.getParameter("cupOrCone");
  String size = request.getParameter("size");
  String flavor = request.getParameter("flavor");

  PrintWriter out = response.getWriter();   // Get the response PrintWriter
  out.println("<html>");
  out.println("<head><title>My Icecream Shop!</title></head>");
  out.println("<body>");
  out.println(String.format("<h1>Here is your %s %s ice cream in a %s. Enjoy!</h1>", size, flavor, cupOrCone));
  out.println("</body></html>");
}
```

### Redirecting Request and Sending Responses
To handle redirects and responding with errors, the `HTTPServletResponse` objects provide `sendRedirect` and `sendError` methods:

```java
public void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
  response.sendRedirect("https://wwww.google.com"); 
  return; 
}

// OR to a static page
public void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
  response.sendRedirect("/icecream-app/example.html"); 
  return; 
}
```

To send an error:

```java
public void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
  response.sendError(HttpServletResponse.SC_BAD_REQUEST, "There was an error in your request.");
  return; 
}
```

### Sessions
To start a new session, use the `getSession` method on `HttpServletRequest`:
```java
public void doPost(HttpServletRequest request, HttpServletResponse response) throws  ServletException, IOException {
  HttpSession session = request.getSession(true);
}
```
This will return the session associated with the client or creates one if it doesn't exist when we provide `true` as an argument. If `false` is provided, the method would return an `HTTPSession` if it already exists or return null if it doesn't. To store information in the session, use the `setAttribute` and `getAttribute` methods:
```java
public void doPost(HttpServletRequest request, HttpServletResponse response) throws  ServletException, IOException {
  String cupOrCone = request.getParameter("cupOrCone");
  String size = request.getParameter("size");
  String flavor = request.getParameter("flavor");
  HttpSession session = request.getSession(true);  // Get or create session object

  String prevSize = session.getAttribute("size");  // Get previously saved size value or null if none was set.
  String prevFlavor = session.getAttribute("flavor");  // Get previously saved flavor value
  String prevCupOrCone = session.getAttribute("cupOrCone");  // Get previously saved cupOrCone value

  session.setAttribute("size", size);  // Update size option
  session.setAttribute("flavor", flavor);  // Update flavor option
  session.setAttribute("cupOrCone", cupOrCone);  // Update cupOrCone option
}
```


## Testing the Servlet
Navigate to the `bin` directory of the Tomcat install, and run the following example command:
```bash
javac -cp lib/servlet-api.jar -d webapps/icecream-app/WEB-INF/classes webapps/icecream-app/WEB-INF/src/HomeServlet.java 
```
- `javac` - The java compiler command-line tool.
- `-cp lib/servlet-api.jar` - The javac option to specify where the compiler can look for our imported classes (like HttpServlet).
- `-d webapps/icecream-app/WEB-INF/classes` - The javac option to specify where to place the generated .class file.
- `webapps/icecream-app/WEB-INF/src/HomeServlet.java` - The path to our .java file that we wish to compile.

Then start Tomcat and navigate to the webpage. For example: `http://localhost:8080/icecream-app/home`.

## CGI vs Java Servlets
Prior to servlets, a server could respond to user requests using the CGI. The CGI architecture worked okay but had some major drawbacks:

- CGI programs were OS-dependent scripts (.bat for Windows and .sh for Linux).
- Since client requests would require the execution of a script, a new process is created on every request.
- More memory is needed on the server as each process needs its own memory space; this causes a scalability issue.
- Since the CGI ran scripts on the web server, there was a high-security risk if any user input was not properly sanitized.

Java servlets addressed many of the issues related to CGI in the following ways:

- Being OS-independent as it runs on the JVM.
- Requests are processed in new threads, which require less overhead to create than processes.
- Less memory is needed on the webserver as threads share memory.
- Servlets are written in Java and inherit all of the built-in security features making them more resilient to attacks.

## Servlet Container
The servlet container is a program that runs on the web server, and its job is to run and manage servlets. The servlet container keeps track of all the servlets in what is known as the servlet context. The servlet container receives a request from the web server and does the necessary network and protocol (like HTTP) processing to make the equest and response objects easily available to the servlet that should handle the request.

## Servlet Lifecycle
The management of servlets involves initialization, invocation, and destruction. The servlet API exposes methods for the container to use the like `init()`, `service()`, and `destroy()`. The container will:

- Check if an instance of the requested servlet is available
- If an instance is not available it will load the servlet class, create an instance of it, and call `init`. Note that once a servlet is initialized it stays initialized until destroyed.
- Once an isntance of a servlet is available and initialized, it will call the `service()` method which, in the case of an `HTTPServlet`, takes care of calling the appropriate (GET, POST, etc) methods.

Once a servlet needs to be removed, for example when we shut down our web server, it takes care of shutting down the servlet by calling its `destroy()` method.

*Note: A servlet's `init` and `destroy` methods can be overridden to implement custom initialization and destruction like setting up a database connection or removing a database connection respectively.*
