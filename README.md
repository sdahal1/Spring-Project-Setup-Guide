# Spring Boot Starter Project - Checklist

### Step 1 - Creating a new project

Inside of ` Package Explorer ` right click -> new -> Spring Starter Project

![Create Spring Starter Project](https://github.com/kcwebers/SpringStarterProjectSetUp/blob/main/screencaps/createproj.png "Create Spring Starter Project")

Inside of the Pop-up we need to:

* Create a unique project name, example ` LoginReg `
* Make sure the type is ` Maven `
* Set Java Version to ` 11 `
* Set Packaging to ` War `
* Group name convention... ` com.username ` <-- your username/initials here
* Package name convention... ` com.username.loginreg ` <-- your project name here!

![Spring Tool Starter Project set-up](https://github.com/kcwebers/SpringStarterProjectSetUp/blob/main/screencaps/sp_start.PNG "Spring Tool Starter Project set-up")

Once these are set choose ` Next `

Select/Search for the following packages:

* Spring Boot DevTools
* Spring Web

Last, click ` Finish `

![Spring Tool Starter Project set-up dependencies](https://github.com/sdahal1/Spring-Project-Setup-Guide/blob/main/screencaps/dependencies_1_web.png "Spring Tool Starter Project set-up dependencies")
![Spring Tool Starter Project set-up dependencies](https://github.com/sdahal1/Spring-Project-Setup-Guide/blob/main/screencaps/dependencies_2_devtools.png "Spring Tool Starter Project set-up dependencies")


### If you select these options often, they may appear above in the `Frequently Used` section!

### Step 2 - pom.xml

Your ` pom.xml ` is located at the very bottom of your project's file tree. 

![Pom.xml location](https://github.com/kcwebers/SpringStarterProjectSetUp/blob/main/screencaps/pomxml.png "Pom.xml location")

Add these to the ` <dependencies></dependencies> ` tag in the file and save it

```xml
<dependencies>
    <!--Basics (for general web dev) -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
        <scope>runtime</scope>
        <optional>true</optional>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-tomcat</artifactId>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>

    <!--For handling views (to see your .jsp pages) -->
    <dependency>
        <groupId>org.apache.tomcat.embed</groupId>
        <artifactId>tomcat-embed-jasper</artifactId>
    </dependency>
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>jstl</artifactId>
    </dependency>

    <!-- MySQL -->
    <!-- Comment this section in if you are using MySQL! -->
    <!-- <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <scope>runtime</scope>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency> --> 

    <!--Validations -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-validation</artifactId>
    </dependency>
    
    <!-- Bcrypt -->
    <dependency>
        <groupId>org.mindrot</groupId>
        <artifactId>jbcrypt</artifactId>
        <version>0.4</version>
    </dependency>
</dependencies>
```

If you are having trouble with these dependencies, remove the comments! To confirm that you've properly added the dependencies to your pom.xml, you can open your pom.xml and select the `dependencies` tab to see them listed out!

![Pom dependencies](https://github.com/kcwebers/SpringStarterProjectSetUp/blob/main/screencaps/depend.PNG "Pom dependencies")

### Step 3 - Adding Settings to `application.properties` and connecting to MySQL

Next add this line to the `src/main/resources/application.properties` file

```
spring.mvc.view.prefix=/WEB-INF/


#These lines below are only if you're yousing database and are on the full stack assignments!!! Do not use the lines below if you're not on the full stack assignments

spring.datasource.url=jdbc:mysql://localhost:3306/<<YOUR_SCHEMA>>?&serverTimezone=UTC
spring.datasource.username=<<YOUR_USERNAME>>
spring.datasource.password=<<YOUR_PASSWORD>>
spring.jpa.hibernate.ddl-auto=update

spring.mvc.hiddenmethod.filter.enabled=true

```

Swap out the `<<YOUR_USERNAME>>`, `<<YOUR_PASSWORD>>`, and `<<YOUR_SCHEMA>>` for the details related to your project. 

#### Important!

Don't forget to create a schema for your project in MySQL! you can do so by accessing your workbench and entering your local instance (likely Local Instance at port 3306). After that, select the option to create your schema, name it as you like, and hit `Apply`.

![Adding schema to MySQL to connect to project](https://github.com/kcwebers/SpringStarterProjectSetUp/blob/main/screencaps/createschema.PNG "Adding schema to MySQL to connect to project")

### Step 4 - Create folder for the JSP files and set up a jsp template

Create the folder `src/main/webapp/WEB-INF`. This is where you will store your `.jsp` files! For example:

![WEB-INF folder](https://github.com/kcwebers/SpringStarterProjectSetUp/blob/main/screencaps/webinf.png "WEB-INF folder")

Here is a boiler plate for your this `.jsp` pages:

```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
    
   <!-- c:out ; c:forEach ; c:if -->
 <%@taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%> 
   <!-- Formatting (like dates) -->
 <%@taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt"%>
   <!-- form:form -->
 <%@ taglib prefix="form" uri="http://www.springframework.org/tags/form"%>  
   <!-- for rendering errors on PUT routes -->
 <%@ page isErrorPage="true" %>   
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Title Here</title>
  <!-- Bootstrap -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" 
      rel="stylesheet" 
      integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" 
      crossorigin="anonymous">

</head>
<body>
    <div class="container"> <!-- Beginning of Container -->
        
    </div> <!-- End of Container -->
</body>
</html>
```

This boiler plate has the Bootstrap v4 already attached so you can incorporate css easily! If you prefer v5 you can swap out the link as you like :). Additionally, there are taglibs for your `<form:form>` tags, any `fmt:` tags you may use, and the `core` tag. 

### Step 5 - Creating `packages`

Create your packages! you can leave these empty until you add you files to them as you build out your project.

![Packages](https://github.com/kcwebers/SpringStarterProjectSetUp/blob/main/screencaps/packages.PNG "Packages")

Note that your packages follow the same naming conventions as dictated above.

* Package name convention... ` com.username.loginreg ` <-- your project name here!

As you create your packages, you can add the remainder of the name onto the end. Make sure you have all of the names correct! This helps your data flow through your project correctly! For example:

* ` com.username.loginreg `
* ` com.username.loginreg.controllers `
* ` com.username.loginreg.models `
* ` com.username.loginreg.repositories `
* ` com.username.loginreg.services `
* ` com.username.loginreg.validators `

### Step 6 - Get Building!

you should now have everything you need to work on your project! As a final note, listed below are the appropriate imports for various files in your program :)

Models

![Models imports](https://github.com/kcwebers/SpringStarterProjectSetUp/blob/main/screencaps/model.PNG "Models imports")

Repositories

![Repositories imports](https://github.com/kcwebers/SpringStarterProjectSetUp/blob/main/screencaps/repo.PNG "Repositories imports")

Services

![Services imports](https://github.com/kcwebers/SpringStarterProjectSetUp/blob/main/screencaps/service.PNG "Services imports")

Controllers

![Controllers imports](https://github.com/kcwebers/SpringStarterProjectSetUp/blob/main/screencaps/controller.PNG "Controllers imports")

Validators

![Validators imports](https://github.com/kcwebers/SpringStarterProjectSetUp/blob/main/screencaps/validator.PNG "Validators imports")


Additionally, make sure you're importing the appropriate files related specifically to your project (models, repos, etc) as you use them in additional files!
