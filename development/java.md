# Java

- [Java](#java)
  - [Java Subjects](#java-subjects)
    - [Javalin framework](#javalin-framework)
    - [JSR 303](#jsr-303)
    - [Apache StringUtils](#apache-stringutils)
    - [Java 8 stuff](#java-8-stuff)
    - [Java 8 - Loops replaced by streams](#java-8---loops-replaced-by-streams)
    - [**Old style loop**](#old-style-loop)
    - [**Java 8 Style**](#java-8-style)
    - [**Example of :: operator**](#example-of--operator)
    - [Java 8 from Evernote](#java-8-from-evernote)
    - [Articles](#articles)
    - [Using Optional to avoid NullPointerExceptions, Null Checks etc](#using-optional-to-avoid-nullpointerexceptions-null-checks-etc)
    - [Lambda Expressions](#lambda-expressions)
    - [Dropbox - Tech Docs - Introducing Java 8](#dropbox---tech-docs---introducing-java-8)
      - [Features](#features)
  - [Streams](#streams)
    - [Eclipse Collections vs Lambdas](#eclipse-collections-vs-lambdas)
    - [Streams with an index](#streams-with-an-index)
    - [Streams maps with a lambda with parameters instead of a functional interface method](#streams-maps-with-a-lambda-with-parameters-instead-of-a-functional-interface-method)
  - [Quartz Scheduler](#quartz-scheduler)
  - [Regex](#regex)
  - [Logging in Java](#logging-in-java)
    - [Log4J2 and SLF4J](#log4j2-and-slf4j)
  - [Spring Framework - TO MOVE](#spring-framework---to-move)
    - [REST API with Async calls in Spring](#rest-api-with-async-calls-in-spring)
  - [Java Articles](#java-articles)
  - [Java Language](#java-language)
    - [Strings and Immutability](#strings-and-immutability)
  - [Thread local](#thread-local)
  - [Memory and Garbage Collection](#memory-and-garbage-collection)
    - [Finding jars and classes loaded during execution](#finding-jars-and-classes-loaded-during-execution)
    - [Statics](#statics)
    - [Serialization](#serialization)
      - [Example of Simple reading in of an object](#example-of-simple-reading-in-of-an-object)
    - [Reading from Standard in using Scanner](#reading-from-standard-in-using-scanner)
    - [Date and Time](#date-and-time)
    - [Threading](#threading)
  - [Collections](#collections)
    - [Searching](#searching)
    - [JavaMail](#javamail)
    - [Testing with Initial Context](#testing-with-initial-context)
      - [Testing with an initialContext outside a container](#testing-with-an-initialcontext-outside-a-container)
  - [Web Stuff - JSP, Servlet etc](#web-stuff---jsp-servlet-etc)
    - [Ajax Response - JSON](#ajax-response---json)
  - [JSP](#jsp)
  - [Spring Framework](#spring-framework)
    - [Spring with Groovy](#spring-with-groovy)
    - [Spring Articles](#spring-articles)
    - [Spring MVC](#spring-mvc)
      - [Resource mapping](#resource-mapping)
        - [JSP Displaying JSON List](#jsp-displaying-json-list)
        - [Spring MVC and Ajax](#spring-mvc-and-ajax)
        - [Patterns in Spring](#patterns-in-spring)
  - [J2EE](#j2ee)
    - [Transactions in J2EE](#transactions-in-j2ee)
    - [JNDI](#jndi)
  - [JAXB](#jaxb)
    - [Generate an XSD if you just have a plain XML example file](#generate-an-xsd-if-you-just-have-a-plain-xml-example-file)
    - [Use your XSD along with a binding file to generate some Java objects via the XJC compiler](#use-your-xsd-along-with-a-binding-file-to-generate-some-java-objects-via-the-xjc-compiler)
    - [Marshal unmarshall in JaxB](#marshal-unmarshall-in-jaxb)
  - [JAX-RS](#jax-rs)
  - [Asynchronous Programming](#asynchronous-programming)

## Java Subjects

### Javalin framework

An alternative to Spring using Kotlin - aims to be much more lightweight
and could be easier to use than Springboot.

### JSR 303

- [java bean validation JSR 303 Bean validation](/development/JSR303)

### Apache StringUtils

Lots of really nice utils for String manipulation (TODO - check the
perf)

- Get first index of character not in a set (i.e. first non digit, non
    alpha etc.)
    <https://commons.apache.org/proper/commons-lang/apidocs/org/apache/commons/lang3/StringUtils.html#indexOfAnyBut-java.lang.CharSequence-char>...-
- Could split by digit etc.
  - <https://commons.apache.org/proper/commons-lang/apidocs/org/apache/commons/lang3/StringUtils.html#splitByCharacterType-java.lang.String>-

### Java 8 stuff

- Java 8 overview - <https://mkyong.com/tutorials/java-8-tutorials/>
- Java 8 comparator to use for Ordering -
    <https://mkyong.com/java8/java-8-lambda-comparator-example/>
- Java 8 Streams with filters -
    <https://mkyong.com/java8/java-8-streams-filter-examples/>
- Merging two lists -
    <https://www.baeldung.com/java-combine-multiple-collections>

### Java 8 - Loops replaced by streams

- <http://www.deadcoderising.com/java-8-no-more-loops/>

### **Old style loop**

```java
public List<Article> getAllJavaArticles() {

      List<Article> result = new ArrayList<>();
      for (Article article : articles) {
          if (article.getTags().contains("Java")) {
              result.add(article);
          }
      }
      return result;

}
```

### **Java 8 Style**

``` java
public List<Article>
getAllJavaArticles() {

    return articles.stream()
        .filter(article -> article.getTags().contains("Java"))
        .collect(Collectors.toList());

}
```

### **Example of :: operator**

```java
    private void initializeContext() {
      Context = SomeResponse.getStuffList().stream()
          .collect(Collectors.toMap(Stuff::getStuffId, stuff -> GetStuffBuilderContext.createSwaggerStuffId(stuff)));
          .collect(Collectors.toMap(Stuff::getStuffId, GetOfferBuilderContext::createSwaggerStuffId));
    }
```

### Java 8 from Evernote

### Articles

- <http://winterbe.com/posts/2014/03/16/java-8-tutorial/>
- <http://www.javacodegeeks.com/2014/05/java-8-features-tutorial.html>
- <http://www.coreservlets.com/java-8-tutorial/#streams-1>
- Streams and Optionals:
    <http://www.baeldung.com/java-filter-stream-of-optional>

### Using Optional to avoid NullPointerExceptions, Null Checks etc

- <http://www.oracle.com/technetwork/articles/java/java8-optional-2175753.html>
- <http://winterbe.com/posts/2015/03/15/avoid-null-checks-in-java/>

- Nice example of a nested mapping approach with Optional - <https://lprakashv.medium.com/handling-nulls-in-nested-objects-java-7079b9413ec9>

```java
public static String safeGreetOptionalWay(RootObject rootObject) {
  return Optional.ofNullable(rootObject)
        .map(r -> r.getFirstLevelObject())
        .map(f -> f.getSecondLevelObject())
        .map(s -> s.getThirdLevelObject())
        .map(t -> t.getName())
        .map(n -> "Hello " + n)
        .orElse("Hey There!");
}
```

- More examples here - <https://www.baeldung.com/java-avoid-null-check>

```java
// Get's the first value and flatmaps so we get Optional<String> not Optional<Optional<String>>
public Optional<String> optionalListFirst() {
   return getOptionalList()
      .flatMap(list -> list.stream().findFirst());
}
```

### Lambda Expressions

- way of passing code as parameter to avoid unwieldy anonymous inner
    classes

### Dropbox - Tech Docs - Introducing Java 8

Notes -

Some Main Objectives:

- Tackle verbosity + readability issues in Java
          e.g. lambdas to reduce boilerplate
          Streams API - handle data processing -> SQL like syntax
- Allow exploitation of Multi-core processors
          Parallel Streams

#### Features

- Lambda Expressions -
  - pass pieces of code in a concise way
  - Special syntax "->" e.g. new Thread( () ->
        System.out.println("Hi") ).start();
- Method Refs -
  - linked to lambdas, can pass a ref to an existing method of a
        class - e.g. compareToIgnoreCase()
  - Special syntax ::
- Streams -
  - Major change to working with Collections
  - Fluent API way of chaining calls
  - Lots of new methods
    - filter
    - sorted
    - reversed
    - map
    - collect
  - linked with Big Data, Map-Reduce etc.
- Enhanced Interfaces -
  - Default Methods - allow backward compatible Java API changes -
        e.g. List.sort() with default impl
              NB - now a form of Multiple inheritance since classes can imp multiple ifaces, Strict Java rules (todo -what rules???)
    - Static Methods
              e.g. Collection iface and Collections class to provide static utility methods -> now can be in 1 interface
    - New Date and Time API
          Domain Driven design - new notions of date and time (based on but somewhat different to Joda)
          Fluent style with chaining.
          Immutable objects to make them Thread safe and avoid accidental updates
    - CompletableFuture
          Asynch programming - linked with Streams
          Improvement of Future class
          Can compose and process multiple asynch tasks and combine results
    - Optional
          Allow better modelling when a value can be there or not.
          Helps avoid NullPointerExceptions - good for nested retrieves and providing alternative values

## Streams

NB - not like the network IO streams - concept based on functional
programming and map reduce stuff

- Tutorials -
  - winterbe.com/posts/2014/07/31/java8-stream-tutorial-examples/
  - The old faithful - <https://www.baeldung.com/java-8-streams>

- Example with replacing for loops - <https://dzone.com/articles/java-8-concepts-fp-lambda-expressions-and-streams>

### Eclipse Collections vs Lambdas

NB - Eclipse Collections has some really nice examples of efficient
searches, even compared to lambdas

Example 1 - Filter a list (here it's based on finding IError.getType()
equal to ErrorType.WARNING)

```java
MutableList<IError> warnings = myResponse.getErrors().select(e ->e.getType().equals(ErrorType.WARNING));

// vs Lambdas
myResponse.getErrors().stream().filter(e -> e.getType().equals(ErrorType.WARNING)).collect(Collectors.toList());

// Example 2 - Check for any occurrence in a list
boolean areThereErrors =
myResponse.getErrors().anySatisfy(e -> e.getType().equals(ERROR));

myResponse.getErrors().stream().anyMatch(e ->
e.getType().equals(ERROR));

```

### Streams with an index

How to have an index i instead of having to use a for loop(int i=0 ....

- <https://www.geeksforgeeks.org/program-to-iterate-over-a-stream-with-indices-in-java-8/>
- <https://stackoverflow.com/questions/18552005/is-there-a-concise-way-to-iterate-over-a-stream-with-indices-in-java-8>

### Streams maps with a lambda with parameters instead of a functional interface method

- How to make a .map() call in a stream if we need to call a method that takes parameters -> use a lambda call
  - <https://stackoverflow.com/questions/44848086/java-8-streams-maps-with-parameters/44848118>

```java
void toto (String someParam) {
  collectionOfStuff.stream()
              .filter (blah -> blah.getLevels().contains(someParam))
              .map(this::sendTiTi); // can do this if sendSMS(Blah blah)
              .map(b -> sendTiTi(b, someParam)); // OR can do this if sendSMS(Blah blah, String someParam)
}

private Blah sendTiTi (Blah blah, String someParam) {
    .....
    return blah;
}
```

## Quartz Scheduler

Quartz Scheduler

<http://www.quartz-scheduler.org/>

TODO - Corrections for their readmes and also add BCC to sendMailJob

## Regex

Regex Tester - really handy tool <https://www.debuggex.com/>

Examples:

- Match 2 char string alphanumeric CSV, ignoring whitespace -

```java
^(([0-9a-zA-Z]{2},\s*)*([0-9a-zA-Z]{2}))$
```

## Logging in Java

- <https://www.baeldung.com/java-logging-intro>
- <https://www.marcobehler.com/guides/a-guide-to-logging-in-java> -
    very nice concise overview of the current popular libraries

### Log4J2 and SLF4J

Log4J2 seems to be the latest incarnation of the java logging
"standard" and provides an api + impl and seems to have good java 8
support. SLF4J is still very popular and viewed as an independent way to
have a logging api with a lot of features. There are flame wars :)

Here's an example of using log4J2 as the primary api + implementation
with a bridge to allow a third party jar using SLF4J to log under the
log4J2 config

- <https://github.com/DarrenC/openapi2puml/commit/6474f408770231f4ec0527c436fed1ed2a10b4e5>

## Spring Framework - TO MOVE

### REST API with Async calls in Spring

- Rest API with Async calls in Spring -
    <https://howtodoinjava.com/spring-boot2/rest/enableasync-async-controller/>
- <https://spring.io/guides/gs/async-method/>
- <https://www.baeldung.com/spring-async>

## Java Articles

<http://www.intertech.com/Blog/Post/Top-10-Nasty-Java-Bugs.aspx>

## Java Language

- [Java 8](Java 8)

### Strings and Immutability

**Why are Strings immutable?**

A few reasons:

- String Pool - allows caching of Strings in the String pool
- Performance - no need to recalculate hashes
- Thread Safe - can share between different threads without risk of
    modification

NB - immutable through it's public API. Can still manipulate by
reflection.

<http://www.programcreek.com/2013/04/why-string-is-immutable-in-java/>

## Thread local

Way of giving threads their own copy of variable without making it local

```java
public class Foo
{
    // SimpleDateFormat is not thread-safe, so give one to each thread
    private static final ThreadLocal<SimpleDateFormat> formatter = new ThreadLocal<SimpleDateFormat>(){
        @Override
        protected SimpleDateFormat initialValue()
        {
            return new SimpleDateFormat("yyyyMMdd HHmm");
        }
    };

    public String formatIt(Date date)
    {
        return formatter.get().format(date);
    }
}
```

## Memory and Garbage Collection

Garbage Collection can be requested but never guaranteed to run.
Simplest memory leak example is a static List where the app continually
adds items without every removing them. In this case the objects are
allocated but never deallocated because they are never in a situation
where they cannot be referenced.

- Description of Memory allocation & garbage collection (Also features
    explanation of the 'set everything to null' myth):
    <http://www.ibm.com/developerworks/java/library/j-jtp01274/index.html>
- Interesting article on types of memory leak:
    <http://blog.dynatrace.com/2011/04/20/the-top-java-memory-problems-part-1/>

### Finding jars and classes loaded during execution

If you add -verbose:class to the arguments for the JVM for launching,
you get a list of the classes loaded during execution and also what jars
they come from. Can be very useful for figuring out the dependencies
needed at runtime.

### Statics

Static properties are class level properties, not unique to an instance.

The static method "override" question pops up sometimes: Basically you
can't override, it's a redefinition and the object reference type
determines the method called.

### Serialization

Method of writing/read objects to or from a stream in order to transfer
them to file/transport etc.

Multiple methods of serialization:

- Default Protocol - Interface - implements Serializable
- Customize Default Protocol - Override Object methods - readObject/writeObject
- Custom Protocol - implements Externalizable (very manual)

transient - mark a property that is not to be serialized.

#### Example of Simple reading in of an object

```java
try
{
     fis = new FileInputStream(filename);
     in = new ObjectInputStream(fis);
     time = (PersistentTime)in.readObject();
     in.close();
}catch(IOException ex){
    //blah
}
```



### Reading from Standard in using Scanner

- <https://www.reddit.com/r/javahelp/wiki/scanner>

link to article on serialization:
<http://java.sun.com/developer/technicalArticles/Programming/serialization/>

### Date and Time

Joda time is becoming more of a standard

<http://www.odi.ch/prog/design/datetime.php>

### Threading

Thread and sync changes in java 1.5
<http://onjava.com/onjava/excerpt/jthreads3_ch6/index1.html>

## Collections

Collections Tutorial on Sun/Oracle site:
<http://docs.oracle.com/javase/tutorial/collections/intro/index.html>

My notes here - [Java Collections](Java Collections)

also - estimation of big O notation
<http://www.dreamincode.net/forums/topic/125427-determining-big-o-notation/>

- Iterable to Collection examples - <https://www.baeldung.com/java-iterable-to-collection>

```java
    // handy snippet
    List<String> result = new ArrayList<String>();
    iterable.forEach(result::add);
```

### Searching

Big O Notation links:
<http://www.leepoint.net/notes-java/algorithms/big-oh/bigoh.html>
<http://rob-bell.net/2009/06/a-beginners-guide-to-big-o-notation/>

### JavaMail

JavaMail with text, html and attachments

<http://mlyly.wordpress.com/2011/05/13/hello-world/>
<http://www.thatsjava.com/java-enterprise/4355/>

### Testing with Initial Context

#### Testing with an initialContext outside a container

Basically creating the intial context for JDBC, constants etc.

```java
/**
 - Test classe pour generation de fichier xml de vente avec JaxB.
 - Cette classe utilise un InitialContext pour trouver les chemins vers les fichiers qui sont normalement en web.xml
 - NB - Pour executer il faut ajouter tomcat-juli.jar au classpath du run configuration (qui se trouve dans $TOMCAT_HOME/bin).
 - @author d.costello
 *
 */
public class TestJaxBClient {

    public static void main(String[] args) throws Exception {
        try {
            // Create initial context
            System.setProperty(Context.INITIAL_CONTEXT_FACTORY, "org.apache.naming.java.javaURLContextFactory");
            System.setProperty(Context.URL_PKG_PREFIXES, "org.apache.naming");
            InitialContext ic = new InitialContext();

            ic.createSubcontext("java:");
            ic.createSubcontext("java:comp");
            ic.createSubcontext("java:comp/env");

            ic.bind("java:comp/env/ressRetailProOutDirClient", "");
            ic.bind("java:comp/env/ressRetailProOutDirPurchase", "");

            TestJaxBClient testJaxB = new TestJaxBClient();
        }catch(Exception e){
            // TODO
        }
    }
}
```

## Web Stuff - JSP, Servlet etc

good explanation on WebApp and JSTL/JSP versions:
<http://www.mularien.com/blog/2008/04/24/how-to-reference-and-use-jstl-in-your-web-application/>

### Ajax Response - JSON

- Jackson
- GSON - google version of JSON

## JSP

Code for importing an external file into a JSP Page

```jsp
<c:import url="http://www.iamdarren.net/RssReader/GoogleRssReader/RssHelloWorldV4.html"></c:import>
```

## Spring Framework

Good intro tutorial
<http://blog.springsource.com/2011/01/04/green-beans-getting-started-with-spring-mvc/>

### Spring with Groovy

If you want to wire in a Groovy class as a Bean, you have to have it
implement a Java interface, you use the interface name in the Java class
that wants to use it, and your Groovy Bean gets declared in the App
Context using the special Groovy syntax.

<http://forum.springsource.org/showthread.php?35351-Autowiring-does-not-work-with-Groovy>

### Spring Articles

- Discussion on using Annotations vs Programmatic instantiation:
    <http://www.linkedin.com/groups/Yesterday-onsite-Pivotal-Engineers-recommend-46964.S.5814893164166660096?view=&srchtype=discussedNews&gid=46964&item=5814893164166660096&type=member&trk=eml-anet_dig-b_pd-ttl-cn&fromEmail=&ut=12Onp1-vEGuS41>

### Spring MVC

#### Resource mapping

```xml
<mvc:resources mapping="/css/**" location="/resources/css/"/>
```

##### JSP Displaying JSON List

<http://stackoverflow.com/questions/20756970/how-to-display-json-object-in-jsp>
<http://stackoverflow.com/questions/20756970/how-to-display-json-object-in-jsp>

##### Spring MVC and Ajax

<http://spring.io/blog/2010/01/25/ajax-simplifications-in-spring-3-0/>

##### Patterns in Spring

<http://stackoverflow.com/questions/755563/what-are-the-design-patterns-which-used-in-spring-framework\#!>

## J2EE

<http://java.sun.com/javaee/5/docs/tutorial/doc/bnbly.html>

This is a good introduction to EJB3 using Netbeans and Glassfish which
creates a simple stateless session bean and connects to it using a
Servlet and a client.
<http://wiki.netbeans.org/CreatingEJB3UsingNetbeansAndGlassfish>

This is a fuller example
<http://netbeans.org/kb/docs/javaee/javaee-entapp-ejb.html>

### Transactions in J2EE

Q&A from Sun site
<http://java.sun.com/blueprints/qanda/transaction_management/index.html>

### JNDI

Sun Tutorial for JNDI (TODO)
<http://java.sun.com/products/jndi/tutorial/trailmap.html>

## JAXB

To get some nice objects that you can marshall or unmarshall here are some tips.

### Generate an XSD if you just have a plain XML example file

```bash
$/Dev/Java/Libraries/xmlbeans-2.5.0/bin/inst2xsd test01.xml
```

### Use your XSD along with a binding file to generate some Java objects via the XJC compiler

XJC is included with the Java6 install in the /bin directory. It can be
invoked on the command line but can also (using an extra jar) be
incorporated into an ANT task.

```bash
$xjc -b binding.xml -p com.yourcompany.generated test_0.xsd
```

### Marshal unmarshall in JaxB

This will give you a nice xml string output from a JaxB object.s

```java

/**
 * Marshall input object to a formatted XML String
 */
protected <T> String marshal(T input) throws JAXBException {
    StringWriter writer = new StringWriter();

    JAXBContext jc = JAXBContext.newInstance(input.getClass());
    Marshaller marshaller = jc.createMarshaller();
    marshaller.setProperty(Marshaller.JAXB_FORMATTED_OUTPUT, Boolean.TRUE);
    marshaller.marshal(input, writer);
    return writer.toString();
}
```

If for some reason we don't have a full XML schema object stack from the root, we can still marshal.
For example you only want to marshal part of a jaxb object.

```java
          //If we DO NOT have JAXB annotated class
          JAXBElement<Employee> jaxbElement = 
            new JAXBElement<Employee>( new QName("", "employee"), 
                      Employee.class, 
                      employeeObj);
             
          jaxbMarshaller.marshal(jaxbElement, System.out);

```

## JAX-RS

- Building a JSON response <https://www.baeldung.com/jax-rs-response>
- Validating with JAX-RS rest assured <https://www.baeldung.com/rest-assured-tutorial>

## Asynchronous Programming

Involves using Completable Futures and Futures to handle asynchronous programming.

- Baeldung nice guide with explanations of applyAsync() etc. <https://www.baeldung.com/java-completablefuture>
- Also lots of nice examples and explanations - <https://www.callicoder.com/java-8-completablefuture-tutorial/>, <https://www.callicoder.com/java-callable-and-future-tutorial/>
- DZone dump of examples - <https://dzone.com/articles/20-examples-of-using-javas-completablefuture>
- Asynchronous implementation libraries <https://www.baeldung.com/java-asynchronous-programming>