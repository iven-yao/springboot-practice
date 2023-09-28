# springboot-practice
spring boot 


## notes
- java class **record**
  ```java
  public record User(String name, long id){}
  ```
  is equivalent to
  ```java
  public User(String name, long id) {
    this.name = name;
    this.id = id;
  }
  ```
  with record, you could instantiate objects as usual
  ```java
  User user = new User("Iven",5566);
  ```
  there are getter methods ready to use as follow:
  ```java
  user.name(); // return "Iven"
  user.id(); // return 5566
  ```
  equals method, will only return true if all fields are the same
  
  and hashCode method, will guarantee that objects with exact same values get same hashcode
  ```java
  User user2 = new User("Iven",2266);
  User user3 = new User("Iven",5566);
  user.equals(user2); // return false
  user.equals(user3); // return true

  if(user.hashCode() == user3.hashCode()){...} // true
  ```
  Lastly, the toString method
  ```java
  user.toString(); // return User[name=Iven, id=5566]
  ```
- Controller:

  building a RESTful web service in Spring, HTTP requests are handled by a controller. and should annotated as @RestController.

  furthermore, using @GetMapping, @PostMapping etc for mapping the request endpoint with certain functions.

  @RequestParam will bind the query param `name` with method variable `name`
  ```java
  package com.example.restservice;

  import java.util.concurrent.atomic.AtomicLong;
  
  import org.springframework.web.bind.annotation.GetMapping;
  import org.springframework.web.bind.annotation.RequestParam;
  import org.springframework.web.bind.annotation.RestController;
  
  @RestController
  public class GreetingController {
    
    private static final String template = "Hello, %s!";
    private final AtomicLong counter = new AtomicLong();

    @GetMapping("/greeting")
    public Greeting greeting(@RequestParam(value = "name", defaultValue = "World") String name) {
        return new Greeting(counter.incrementAndGet(), String.format(template, name));
    }
  }

  ```

- to generate .mvn/wrapper
  ```
  mvn -N io.takari:maven:wrapper
  ```

- to run this application
  ```
  ./mvnw spring-boot:run
  ```
  Alternatively,
  ```
  ./mvnw clean package
  java -jar target/demo-0.0.1-SNAPSHOT.jar
  ```

## helpful links
[Maven Installation](https://www.digitalocean.com/community/tutorials/install-maven-mac-os)

[SpringBoot Tutorials](https://spring.io/projects/spring-boot#learn)
