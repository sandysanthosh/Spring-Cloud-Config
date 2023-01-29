# Pivotal-Cloud-Foundry

How to Deploy Spring Boot Application to Cloud Foundry Platform

#### Technology Stack:

We will use below technology stack for the spring boot application development and testing.

* Spring Boot
* Spring REST
* Maven
* Eclipse
* Cloud Foundry CLI
* Web Browser


#### Spring Boot application with Cloud Configuration using Spring Cloud Config:


```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-config-client</artifactId>
</dependency>

```

#### Next, you will need to configure your application to connect to a Spring Cloud Config Server. You can do this by adding the following to your 
#### application.properties or application.yml file:

```

spring.cloud.config.uri=http://localhost:8888
```

#### class MyConfig:

```
@Configuration
@RefreshScope
public class MyConfig {

    @Value("${my.config.property}")
    private String myConfigProperty;

    public String getMyConfigProperty() {
        return myConfigProperty;
    }
}


```

#### Create a REST controller class to handle HTTP requests and inject the Configuration class:

```

@RestController
public class MyController {

    @Autowired
    private MyConfig myConfig;

    @GetMapping("/config")
    public String getConfig() {
        return myConfig.getMyConfigProperty();
    }
}

```

To deploy the application to the cloud, you can use a service like Heroku, AWS, or Google Cloud Platform. You will need to configure the necessary dependencies and settings for your chosen platform.

Finally, use Spring Cloud Config to externalize your application configuration, so that you can manage it in a central location, rather than hard-coding it in the application itself.
