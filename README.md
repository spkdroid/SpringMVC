# SpringMVC

**Prerequisites:**
- Java Development Kit (JDK) installed
- Apache Maven installed (optional but recommended)

**Step 1: Set Up a Spring MVC Project**

You can create a Spring MVC project using Maven or any IDE that supports Spring. Here, we'll use Maven.

**Option 1: Using Maven Archetype (Recommended)**

Maven offers a Spring MVC project archetype that simplifies project setup:

```bash
mvn archetype:generate -DgroupId=com.example -DartifactId=spring-mvc-demo -DarchetypeArtifactId=maven-archetype-webapp -DinteractiveMode=false
```

**Option 2: Using an IDE**

Alternatively, you can use an IDE like Eclipse or IntelliJ IDEA to create a new Spring project with Spring MVC support.

**Step 2: Add Spring MVC Dependencies**

If you're using Maven, your project's `pom.xml` should already have the necessary dependencies for Spring Web MVC. If not, you can add them manually:

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-web</artifactId>
        <version>5.3.9</version> <!-- Use the latest version -->
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.3.9</version> <!-- Use the latest version -->
    </dependency>
</dependencies>
```

**Step 3: Create a Controller**

Create a simple controller class to handle requests. For example, let's create a `HelloController.java`:

```java
package com.example.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class HelloController {

    @RequestMapping("/hello")
    public String hello(Model model) {
        model.addAttribute("message", "Hello, World!");
        return "hello";
    }
}
```

**Step 4: Create a View**

Create a JSP view to display the "Hello, World!" message. Create a file named `hello.jsp` in the `src/main/webapp/WEB-INF/views` directory:

```jsp
<!DOCTYPE html>
<html>
<head>
    <title>Hello World</title>
</head>
<body>
    <h1>${message}</h1>
</body>
</html>
```

**Step 5: Configure Spring MVC**

Create a Spring MVC configuration file, such as `spring-servlet.xml`, in the `src/main/webapp/WEB-INF` directory:

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="
           http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

    <context:component-scan base-package="com.example.controller" />

    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/views/" />
        <property name="suffix" value=".jsp" />
    </bean>

</beans>
```

**Step 6: Configure Web Deployment Descriptor**

Create a `web.xml` file in the `src/main/webapp/WEB-INF` directory:

```xml
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <servlet>
        <servlet-name>spring</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>/WEB-INF/spring-servlet.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>

    <servlet-mapping>
        <servlet-name>spring</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>

</web-app>
```

**Step 7: Run the Application**

You can deploy the application to a servlet container (e.g., Apache Tomcat) and access it at `http://localhost:8080/your-app-context/hello`.

That's it! You've created a basic Spring MVC application. You can expand on this foundation to build more complex web applications with Spring MVC.**
