# Spring Getting Started Build with Gradle

## Learn what you can do with Spring Boot

Spring Boot offers a fast way to build applications. It looks at your classpath and at beans you have configured, makes reasonable assumptions about what you’re missing, and adds it. With Spring Boot you can focus more on business features and less on infrastructure.   

### For Example:

- Got Spring MVC? There are several specific beans you almost always need, and Spring Boot adds them automatically. A Spring MVC app also needs a servlet container, so Spring Boot automatically configures embedded Tomcat.
- Got Jetty? If so, you probably do NOT want Tomcat, but instead embedded Jetty. Spring Boot handles that for you.
- Got Thymeleaf? There are a few beans that must always be added to your application context; Spring Boot adds them for you.

These are just a few examples of the automatic configuration Spring Boot provides. At the same time, Spring Boot doesn’t get in your way. For example, if Thymeleaf is on your path, Spring Boot adds a `SpringTemplateEngine` to your application context automatically. But if you define your own `SpringTemplateEngine` with your own settings, then Spring Boot won’t add one. This leaves you in control with little effort on your part.

> Spring Boot doesn’t generate code or make edits to your files. Instead, when you start up your application, Spring Boot dynamically wires up beans and settings and applies them to your application context.

## Create a simple web application

Now you can create a web controller for a simple web application.

## Fail to Run the application

There's no gradlew file.

<details>

### The Gradle Wrapper

The recommended way to execute any Gradle build is with the help of the Gradle Wrapper (in short just “Wrapper”). The Wrapper is a script that invokes a declared version of Gradle, downloading it beforehand if necessary. As a result, developers can get up and running with a Gradle project quickly without having to follow manual installation processes saving your company time and money.

![The Wrapper workflow](https://docs.gradle.org/current/userguide/img/wrapper-workflow.png)

**In a nutshell you gain the following benefits:**

- Standardizes a project on a given Gradle version, leading to more reliable and robust builds.
- Provisioning a new Gradle version to different users and execution environment (e.g. IDEs or Continuous Integration servers) is as simple as changing the Wrapper definition.

**So how does it work? For a user there are typically three different workflows:**

- You set up a new Gradle project and want to add the Wrapper to it.
- You want to run a project with the Wrapper that already provides it.
- You want to upgrade the Wrapper to a new version of Gradle.

The following sections explain each of these use cases in more detail.

#### Adding the Gradle Wrapper

Generating the Wrapper files requires an installed version of the Gradle runtime on your machine as described in Installation. Thankfully, generating the initial Wrapper files is a one-time process.

Every vanilla Gradle build comes with a built-in task called wrapper. You’ll be able to find the task listed under the group "Build Setup tasks" when listing the tasks. Executing the wrapper task generates the necessary Wrapper files in the project directory.

**Running the Wrapper task**

```shell script
$ gradle wrapper
> Task :wrapper

BUILD SUCCESSFUL in 0s
1 actionable task: 1 executed
```

As a result you can find the desired information in the Wrapper properties file.

**Example: The generated distribution URL**

```properties
distributionUrl=https\://services.gradle.org/distributions/gradle-6.0.1-all.zip
```

Let’s have a look at the following project layout to illustrate the expected Wrapper files:

```
.
├── build.gradle
├── settings.gradle
├── gradle
│   └── wrapper
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── gradlew
└── gradlew.bat
```

A Gradle project typically provides a `build.gradle` and a `settings.gradle` file. The Wrapper files live alongside in the gradle directory and the root directory of the project. The following list explains their purpose.

##### `gradle-wrapper.jar`
The Wrapper JAR file containing code for downloading the Gradle distribution.

##### `gradle-wrapper.properties`
A properties file responsible for configuring the Wrapper runtime behavior e.g. the Gradle version compatible with this version. Note that more generic settings, like configuring the Wrapper to use a proxy, need to go into a different file.

##### `gradlew`, `gradlew.bat`
A shell script and a Windows batch script for executing the build with the Wrapper.

You can go ahead and execute the build with the Wrapper without having to install the Gradle runtime. If the project you are working on does not contain those Wrapper files then you’ll need to generate them.

</details>

## Run the application

To run the application, execute:
   
```shell script
./gradlew build && java -jar build/libs/gs-spring-boot-0.1.0.jar
```

If you are using Maven, execute:
   
```shell script
mvn package && java -jar target/gs-spring-boot-0.1.0.jar
```

You should see some output like this:
   
```
Let's inspect the beans provided by Spring Boot:
application
beanNameHandlerMapping
defaultServletHandlerMapping
dispatcherServlet
embeddedServletContainerCustomizerBeanPostProcessor
handlerExceptionResolver
helloController
httpRequestHandlerAdapter
messageSource
mvcContentNegotiationManager
mvcConversionService
mvcValidator
org.springframework.boot.autoconfigure.MessageSourceAutoConfiguration
org.springframework.boot.autoconfigure.PropertyPlaceholderAutoConfiguration
org.springframework.boot.autoconfigure.web.EmbeddedServletContainerAutoConfiguration
org.springframework.boot.autoconfigure.web.EmbeddedServletContainerAutoConfiguration$DispatcherServletConfiguration
org.springframework.boot.autoconfigure.web.EmbeddedServletContainerAutoConfiguration$EmbeddedTomcat
org.springframework.boot.autoconfigure.web.ServerPropertiesAutoConfiguration
org.springframework.boot.context.embedded.properties.ServerProperties
org.springframework.context.annotation.ConfigurationClassPostProcessor.enhancedConfigurationProcessor
org.springframework.context.annotation.ConfigurationClassPostProcessor.importAwareProcessor
org.springframework.context.annotation.internalAutowiredAnnotationProcessor
org.springframework.context.annotation.internalCommonAnnotationProcessor
org.springframework.context.annotation.internalConfigurationAnnotationProcessor
org.springframework.context.annotation.internalRequiredAnnotationProcessor
org.springframework.web.servlet.config.annotation.DelegatingWebMvcConfiguration
propertySourcesBinder
propertySourcesPlaceholderConfigurer
requestMappingHandlerAdapter
requestMappingHandlerMapping
resourceHandlerMapping
simpleControllerHandlerAdapter
tomcatEmbeddedServletContainerFactory
viewControllerHandlerMapping
```
   
You can clearly see **org.springframework.boot.autoconfigure** beans. There is also a tomcatEmbeddedServletContainerFactory.
   
Check out the service.

```shell script
$ curl localhost:8080
Greetings from Spring Boot!
```
