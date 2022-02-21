# Spring Framework Stuff

- [Spring Framework Stuff](#spring-framework-stuff)
  - [Overview](#overview)
  - [Getting Started with Spring MVC (OUTDATED)](#getting-started-with-spring-mvc-outdated)
    - [Examples](#examples)
    - [Links](#links)
  - [Spring Mail](#spring-mail)
    - [Main Class](#main-class)
    - [Abstract class for mail sending](#abstract-class-for-mail-sending)
    - [Implementation class that uses the Spring Java mail class](#implementation-class-that-uses-the-spring-java-mail-class)
  - [SpringBoot on Heroku](#springboot-on-heroku)
  - [Spring examples](#spring-examples)
    - [Mappings in web.xml](#mappings-in-webxml)
    - [Mapping in @Annotated Controller](#mapping-in-annotated-controller)
    - [Paralleling requests in Spring](#paralleling-requests-in-spring)
    - [Consuming REST service from Spring Server Example](#consuming-rest-service-from-spring-server-example)
    - [@Autowired vs @Inject and Constructor injection annotations](#autowired-vs-inject-and-constructor-injection-annotations)
    - [Constructor Injection example](#constructor-injection-example)
  - [Spring Boot](#spring-boot)
    - [Testing MVC in Spring Boot](#testing-mvc-in-spring-boot)

## Overview

- **What is it**
  - Lightweight Framework for Java applications which lets you rapidly develop applications without creating dependencies on any J2EE framework stuff.
- **Main Concept**
  - Dependency injection and inversion of control to stop your apps having a bunch of stuff you don't need just because it comes with a framework.

- [Martin Fowler's article on Inversion of Control/Dependency Injection](http://www.martinfowler.com/articles/injection.html)

## Getting Started with Spring MVC (OUTDATED)

- Maven archetype for Spring 4 + Java 1.8 - <blog.codeleak.pl/2014/12/spring-mvc-4-quickstart-maven-archetype.html>
- Maven archetype std webapp with Spring added after -
    <http://examples.javacodegeeks.com/enterprise-java/spring/mvc/spring-4-rest-hello-world-example/>
- Tomcat Install on Mac - <http://wolfpaulus.com/jounal/mac/tomcat8/>

### Examples

### Links

- Below is a link to an article about the Spring Framework 2.0 XML Schema. This basically allows the use of standard tags instead of everything being a \<bean> tag.

```xml
Eg
        <jee:jndi-lookup id="dataSource" jndi-name="java:comp/env/jdbc/petclinic"/>
instead of
        <bean id="dataSource" class="org.springframework.jndi.JndiObjectFactoryBean">
         <property name="jndiName" value="jdbc/MyDataSource"/>
        </bean>
```

- <http://static.springsource.org/spring/docs/2.5.6/reference/xsd-config.html>
- <http://www.theserverside.com/feature/Comparing-Spring-vs-Google-Guice-By-Example>

## Spring Mail

This is a simple mail runner that uses spring classes to programmatically send a mail. There's no config via xml or otherwise.
Stay tuned for an xml config version.

### Main Class

```java
    package springmailtest;

    /**
     * Test of sending mail using Spring
     * Using example in ProSpring p521
     * @author Darren
     */
    public class Main {
        private static final String TO = "youraddress@gmail.com";
        private static final String TEXT = "this is a call";

        /**
         * @param args the command line arguments
         */
        public static void main(String[] args) {
            SimpleMailSender sender = new JavaMailSimpleMailSender();

            sender.sendMessage(TO, TEXT);
        }

    }
```

### Abstract class for mail sending

```java

    package springmailtest;

    import org.springframework.mail.MailSender;
    import org.springframework.mail.SimpleMailMessage;

    /**
     *
     * @author Darren
     */
    public abstract class SimpleMailSender {
        protected abstract MailSender getMailSender();

        public final void sendMessage(String to, String text){
            SimpleMailMessage msg = new SimpleMailMessage();
            msg.setTo(to);
            msg.setSubject("Test Message");
            msg.setFrom("test@test.net");
            msg.setText(text);

            MailSender sender = getMailSender();
            sender.send(msg);
        }
    }
```

### Implementation class that uses the Spring Java mail class

```java

    package springmailtest;

    import java.util.Properties;
    import org.springframework.mail.MailSender;
    import org.springframework.mail.javamail.JavaMailSenderImpl;

    /**
     *
     * @author Darren
     */
    public class JavaMailSimpleMailSender extends SimpleMailSender{
        protected MailSender getMailSender(){
            JavaMailSenderImpl sender = new JavaMailSenderImpl();

            // Set the java mail properties
            Properties p = new Properties();
            p.put("mail.smtp.auth", "true");
            sender.setJavaMailProperties(p);

            sender.setHost("mail.smtpServer.net");
            sender.setPort(26);
            sender.setUsername("user@yourdomain.net");
            sender.setPassword("THe passsword");
            return sender;
        }
    }
```

## SpringBoot on Heroku

- <http://nicholaspaulsmith.com/spring-boot-on-heroku/>

## Spring examples

### Mappings in web.xml

```xml
<listener>

    <listener-class> org.springframework.web.context.ContextLoaderListener</listener-class>

</listener>

<servlet>

    <servlet-name> springrest</servlet-name>
    <servlet-class> org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <load-on-startup> 1</load-on-startup>

</servlet>

<servlet-mapping\>

    <servlet-name> springrest</servlet-name>
    <url-pattern> /spring/*</url-pattern>

</servlet-mapping>
```

### Mapping in @Annotated Controller

```java
@Controller
public class SpringRestController {

    @RequestMapping("/displayDog")
    public @ResponseBody SmallDog displayDog(Model model) {

        System.out.println("Display Dog called......wooof");

        SmallDog roddy = new SmallDog();
        roddy.setName("Roddy Boland");
        roddy.setHungry(true);
        roddy.setNumberofLegs(4);

        return roddy;
    }
}
```

- URL used to call this:
  - GWT Internal Jetty: <http://127.0.0.1:8888/spring/displayDog>
  - Regular Web App: <http://localhost:8080/MyWebAppName/spring/displayDog>

This setup allows us to have both GWT and Spring apps deployed in the
same server

### Paralleling requests in Spring

- non blocking REST Controllers - <http://callistaenterprise.se/blogg/teknik/2014/04/22/c10k-developing-non-blocking-rest-services-with-spring-mvc/>
- web service with concurrent requests - <http://forum.spring.io/forum/spring-projects/web-services/91790-how-to-write-a-concurrent-web-service-client>

### Consuming REST service from Spring Server Example

- Simple REST cosuming RESTFUL Service from Spring server using RestfulTemplate - <https://spring.io/guides/gs/consuming-rest/>

### @Autowired vs @Inject and Constructor injection annotations

Same thing just Spring vs JSR

### Constructor Injection example

In this case the SearchService must be provided for the bean or it will fail at startup

```java
private SearchService service;

@Inject public MyClass(SearchService service){
    this.service = service;
}
```

- Document from JBoss with example: <https://docs.jboss.org/weld/reference/1.1.0.Final/en-US/html/injection.html>

## Spring Boot

- Linked in Course - <https://www.linkedin.com/learning/learning-spring-with-spring-boot-2/summary-of-the-web-application-2?u=75507506>

### Testing MVC in Spring Boot

- Shows the use of the latest JUnit5 + Spring boot for testing - <https://rieckpil.de/guide-to-testing-spring-boot-applications-with-mockmvc/>
  - No "@RunWith" anymore - taken care of by @SpringBootTest

```java
@WebMvcTest(RoomReservationWebController.class)
class RoomReservationWebControllerTest {
  @MockBean
  private ReservationService reservationService;

  @Autowired
  private MockMvc mockMvc;

  @Test
  public void getReservations() throws Exception{
    String dateString = "2020-01-01";
    Date date = DateUtils.createDateFromDateString(dateString);
    List<RoomReservation> roomReservations = new ArrayList<>();
    RoomReservation roomReservation = new RoomReservation();
    roomReservation.setLastName("Unit");
    roomReservation.setFirstName("Junit");
    roomReservation.setDate(date);
    roomReservation.setGuestId(1);
    roomReservation.setRoomId(100);
    roomReservation.setRoomName("Junit Room");
    roomReservation.setRoomNumber("J1");
    roomReservations.add(roomReservation);
    given(reservationService.getRoomReservationsForDate(date)).willReturn(roomReservations);

    this.mockMvc.perform(get("/reservations?date=2020-01-01"))
        .andExpect(status().isOk())
        .andExpect(content().string(containsString("Unit, Junit")));
  }
}
```