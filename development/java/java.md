# Java

- [Java](#java)
  - [Java Subjects](#java-subjects)
    - [Java 17](#java-17)
    - [Java 11](#java-11)
      - [Java 11 Overview](#java-11-overview)
    - [Java 9](#java-9)
      - [Java Modules](#java-modules)
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
      - [Optional articles - especially the avoiding anti-patterns](#optional-articles---especially-the-avoiding-anti-patterns)
    - [Lambda Expressions](#lambda-expressions)
      - [StreamEx library - enhanced streams in java](#streamex-library---enhanced-streams-in-java)
    - [Dropbox - Tech Docs - Introducing Java 8](#dropbox---tech-docs---introducing-java-8)
      - [Features](#features)
  - [Streams](#streams)
    - [Stream Examples](#stream-examples)
    - [Eclipse Collections vs Lambdas](#eclipse-collections-vs-lambdas)
    - [Streams with an index](#streams-with-an-index)
    - [Streams maps with a lambda with parameters instead of a functional interface method](#streams-maps-with-a-lambda-with-parameters-instead-of-a-functional-interface-method)
    - [Stream to check for existence of something in a collection](#stream-to-check-for-existence-of-something-in-a-collection)
    - [Nested Streams](#nested-streams)
    - [Stream to join Strings](#stream-to-join-strings)
    - [Effectively final vs final](#effectively-final-vs-final)
  - [Quartz Scheduler](#quartz-scheduler)
  - [Regex](#regex)
  - [Logging in Java](#logging-in-java)
    - [Log4J2 and SLF4J](#log4j2-and-slf4j)
    - [Logging and Mapped Diagnostic Context MDC](#logging-and-mapped-diagnostic-context-mdc)
  - [Spring Framework - TO MOVE](#spring-framework---to-move)
    - [REST API with Async calls in Spring](#rest-api-with-async-calls-in-spring)
  - [Java Articles](#java-articles)
  - [Java Language](#java-language)
    - [Strings and Immutability](#strings-and-immutability)
  - [Thread local](#thread-local)
  - [Memory and Garbage Collection](#memory-and-garbage-collection)
    - [Memory leak tooling in Java](#memory-leak-tooling-in-java)
    - [Finding jars and classes loaded during execution](#finding-jars-and-classes-loaded-during-execution)
    - [Statics](#statics)
  - [Serialization](#serialization)
    - [Example of Simple reading in of an object](#example-of-simple-reading-in-of-an-object)
    - [Reading from Standard in using Scanner](#reading-from-standard-in-using-scanner)
  - [File operations](#file-operations)
    - [NIO library example for writing to file](#nio-library-example-for-writing-to-file)
  - [Date and Time](#date-and-time)
    - [Timezone updates for the JDK/JRE](#timezone-updates-for-the-jdkjre)
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
    - [Date formatting in JaxB XML](#date-formatting-in-jaxb-xml)
  - [JAX-RS](#jax-rs)
    - [Server side - build a JSON Response body](#server-side---build-a-json-response-body)
    - [Client side - Reading or Printing a JSON Response body](#client-side---reading-or-printing-a-json-response-body)
  - [Asynchronous Programming - Completable Futures \& Futures](#asynchronous-programming---completable-futures--futures)
    - [thenApply vs thenCompose](#thenapply-vs-thencompose)
    - [ThenApply vs ThenApplyAsync](#thenapply-vs-thenapplyasync)
    - [Exception handling](#exception-handling)
      - [Mocking errors in CompletableFuture](#mocking-errors-in-completablefuture)
    - [Join vs Get in Completable Future](#join-vs-get-in-completable-future)
    - [Thread pooling with Completable Futures](#thread-pooling-with-completable-futures)
  - [Failsafe and fault tolerant JVM patterns](#failsafe-and-fault-tolerant-jvm-patterns)
  - [Lombok](#lombok)
  - [Javadoc](#javadoc)
    - [Referencing methods in javadoc](#referencing-methods-in-javadoc)
  - [Application Servers](#application-servers)
  - [IDEs](#ides)
    - [Intellij](#intellij)

## Java Subjects

### Java 17

- Migration tips for moving to JDK 17 - <https://ahrooran.hashnode.dev/technical-challenges-migrating-from-jdk-8-to-17-and-spring-boot-2x-to-3x>

### Java 11

#### Java 11 Overview

- Really nice overview of java 11 with code examples - <https://dzone.com/articles/whats-new-between-java-11-and-java-17#:~:text=Java%2017%20is%20an%20LTS,for%20production%20and%20commercial%20use.>
  - Stream.toList() instead of Collectors.toList()
  - Helpful Null Pointer Exceptions
    - ``` Cannot invoke "com.blah.GrapeClass.getColor()" because the return value of "java.util.HashMap.get(Object)" is null ```
  - Records - instead of boilerplate or lombok for pojo classes you can define as records with fields

### Java 9

#### Java Modules

- Introduction to Modules - <https://www.javacodegeeks.com/2023/03/java-modules-an-introduction.html>
  - Way of encapsulating project to reduce runtime, explicitly specify dependencies
  - Specify using `module-info.java` file
  - Special way to build and run using the java commands to indicate it's a module
  - Completely different to maven multi-module which is related to compile time dependencies
    - JPMS modules are to do with runtime dependencies

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
- <https://stackoverflow.com/questions/17081063/how-should-we-manage-jdk8-stream-for-null-values>
- <https://www.baeldung.com/java-null-safe-streams-from-collections>

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
// Gets the first value and flatmaps so we get Optional<String> not Optional<Optional<String>>
public Optional<String> optionalListFirst() {
   return getOptionalList()
      .flatMap(list -> list.stream().findFirst());
}
```

#### Optional articles - especially the avoiding anti-patterns

- <https://www.linkedin.com/pulse/java-optional-cookbook-vincent-vauban/>
  - This one is really good -> TODO extract the examples
    - return status.orElse(SOME_VALUE); // use this instead of an if(optional.ispresent())optional.get
    - optional.ifPresent() is good too.
- <https://gradlehero.com/java-optional/#5-when-should-you-_not_-use-optional>

### Lambda Expressions

- way of passing code as parameter to avoid unwieldy anonymous inner
    classes
- Some tips - <https://www.baeldung.com/java-8-lambda-expressions-tips>

#### StreamEx library - enhanced streams in java

- <https://github.com/amaembo/streamex>
- Baeldung article - <https://www.baeldung.com/streamex>

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

### Stream Examples

```java

// Ordering a collection
List<String> list = Arrays.asList("9", "A", "Z", "1", "B", "Y", "4", "a", "c");
List<String> sortedList = list.stream().sorted().collect(Collectors.toList());
sortedList.forEach(System.out::print); // 1 4 9 A B Y Z a c
```

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
              .map(this::sendTiTi); // can do this if sendTiTi(Blah blah)
              .map(b -> sendTiTi(b, someParam)); // OR can do this if sendTiTi(Blah blah, String someParam)
}

private Blah sendTiTi (Blah blah, String someParam) {
    .....
    return blah;
}
```

### Stream to check for existence of something in a collection

- Using stream and "anyMatch" to check for the presence of some value or field etc.

```java
  // Example for a protobuf object in java form
  private static boolean hasFieldsToBuild(Builder brandingBuilder) {
    return Builder.getDescriptor()
        .getFields()
        .stream()
        .anyMatch(brandingBuilder::hasField);
  }
```

### Nested Streams

- <https://stackoverflow.com/questions/51630352/nested-lists-with-streams-in-java8>

To replace something like this:

```java
C c1 = null;
String name = "name1"
for (A a: listOfAObjects) {
    for (B b: a.getList()) {
        for (C c: b.getPr()) {
            if (c.getName().equalsIgnoreCase(name)) {
                c1= c;
                break;
            }
        }
    }
}
```

Can do this:

```java

C c1 = listOfAObjects.stream()
        .flatMap(a -> a.getList().stream())
        .flatMap(b -> b.getPr().stream())
        .filter(c -> c.getName().equalsIgnoreCase(name))
        .findFirst()
        .orElse(null);

```

Can also filter nulls with this:

```java
  .filter(Objects::nonNull)
```

### Stream to join Strings

- Article with example (see below) <https://ivarconr.wordpress.com/2013/11/20/java-8-joining-strings-with-stream-api/>
  - Collectors.joining(<char>) is a helper for this task, the input string is the separator between each value
- More information in the JDK docs about the reduction operations available - <https://docs.oracle.com/javase/tutorial/collections/streams/reduction.html>

```java
  List<Person> persons = new ArrayList<>();
  persons.add(new Person("Ola Hansen", 21));  ..
  
  
  String names = persons.stream()
    .filter(p -> p.getAge() > 18)
    .sorted((p1, p2) -> p1.getAge() - p2.getAge())
    .map(p -> p.getAge() + ":" + p.getName())
    .collect(Collectors.joining(", "));
```

### Effectively final vs final

- <https://www.baeldung.com/java-effectively-final>
  - When working with lambdas, you can't pass regular variables for use inside the lambda expression so you need either a final or effectively final variable.
  - <https://www.baeldung.com/java-8-lambda-expressions-tips>

```java

public void method() {
    String localVariable = "Local";
    Foo foo = parameter -> {
        String localVariable = parameter;
        return localVariable;
    };
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

### Logging and Mapped Diagnostic Context MDC

- <https://www.baeldung.com/mdc-in-log4j-2-logback>
  - Shows how MDC can be used in Log4J, Log4j2, Slf4j etc.
  - Basic idea is to create a context where we can put information when we have it - e.g. transaction ids etc. and then it can be included in logging messages where we may not have access to the context e.g. handle an error or logging a field value
  - Need to setup and then clean the context, especially when using thread pools or there is a risk of stale data being used.

Further reading:

- <https://medium.com/asyncparadigm/logging-in-a-multithreaded-environment-and-with-completablefuture-construct-using-mdc-1c34c691cef0>
- <https://logback.qos.ch/manual/mdc.html>

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

- <http://www.programcreek.com/2013/04/why-string-is-immutable-in-java/>

- Nice baeldung page on string pool and intern() <https://www.baeldung.com/java-string-pool>
  - intern() is useful when using new String("dsfdsf") to create strings since it forces the use of the String Pool whereas otherwise it would result in a new object always.

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
adds items without ever removing them. In this case the objects are
allocated but never de-allocated because they are never in a situation
where they cannot be referenced.

- Description of Memory allocation & garbage collection (Also features
    explanation of the 'set everything to null' myth):
    <http://www.ibm.com/developerworks/java/library/j-jtp01274/index.html>
- Interesting article on types of memory leak:
    <http://blog.dynatrace.com/2011/04/20/the-top-java-memory-problems-part-1/>

### Memory leak tooling in Java

- From Java 11, JFR was non-commercial
  - Baeldung overview - <https://www.baeldung.com/java-flight-recorder-monitoring>
- Articles - <https://inside.java/tag/jfr>
  - JFR with pratical example - <https://inside.java/2020/09/20/jdk-introduction/>
    - direct link to youtube video - <https://www.youtube.com/watch?v=7z_R2Aq-Fl8>

- Java 8 FlightRecorder - <https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/memleaks001.html#CIHHGDJH>
- Online heap dump analyzer - <https://heaphero.io/heap-index.jsp>
- JFR high level archi Overview - <https://www.youtube.com/watch?v=XEKkUpPnf4Q&list=WL&index=88>

- Intellij profiling - <https://blog.jetbrains.com/idea/2020/03/profiling-tools-and-intellij-idea-ultimate/>
- Visual VM - <https://visualvm.github.io/>
- On OpenShift - a JFR tool - <https://cryostat.io/>

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

## Serialization

Method of writing/read objects to or from a stream in order to transfer
them to file/transport etc.

- Serialize to a stream
- Deserialize to an object

Multiple methods of serialization:

- Default Protocol - Interface - implements Serializable
- Customize Default Protocol - Override Object methods - readObject/writeObject
- Custom Protocol - implements Externalizable (very manual)

transient - mark a property that is not to be serialized.

### Example of Simple reading in of an object

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

## File operations

### NIO library example for writing to file

```java
// Simple case with some strings and the NIO Files API
Path path = Paths.get("src/main/resources/question.txt"); 
String question = "To be or not to be?";
Files.write(path, question.getBytes());

// More efficient with large files using a bufferedWriter
Path path = Paths.get("src/main/resources/shakespeare.txt");
try(BufferedWriter writer = Files.newBufferedWriter(path, Charset.forName("UTF-8"))){
  writer.write("To be, or not to be. That is the question.");
}catch(IOException ex){
  ex.printStackTrace();
}
```

## Date and Time

- Java 8 date type replaces joda time - <https://www.baeldung.com/java-8-date-time-intro>

- Using zoned date times in a diff calculation - <https://stackoverflow.com/questions/41077142/java-8-calculate-difference-between-two-zoneddatetime>
  - Basically use [ChronoUnit](https://docs.oracle.com/javase/9/docs/api/java/time/temporal/ChronoUnit.html)
    - ChronoUnit.SECONDS.between(tzdate1, tzdate2);
    - Careful to use same types e.g all timezonedDates or LocalDateTimes

### Timezone updates for the JDK/JRE

- <https://stackoverflow.com/questions/27925035/wrong-offset-for-timezone-casablanca-java>
  - TZUpdater is a tool to update the JDK/JRE with corrected timezone offset, daylight savings etc.
  - Not updating will lead to errors for e.g. moroccan DST change in 2017/2018.

## Threading

Thread and sync changes in java 1.5
<http://onjava.com/onjava/excerpt/jthreads3_ch6/index1.html>

## Collections

Collections Tutorial on Sun/Oracle site:
<http://docs.oracle.com/javase/tutorial/collections/intro/index.html>

My notes here - [Java Collections](Java Collections)

also - estimation of big O notation
<http://www.dreamincode.net/forums/topic/125427-determining-big-o-notation/>

- Creating a list from a group of objects

``` java
  // Java 8
  Arrays.asList(Objects...);

  // Java 9+
  List.of(Objects...);
```

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
<c:import url="http://www.someSite.net/RssReader/GoogleRssReader/RssHelloWorldV4.html"></c:import>
```

## Spring Framework

- TODO - deprecated this one -> Good intro tutorial <http://blog.springsource.com/2011/01/04/green-beans-getting-started-with-spring-mvc/>

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

This will give you a nice xml string output from a JaxB object.

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
  JAXBElement<Employee> jaxbElement = new JAXBElement<Employee>(new QName("", "employee"), Employee.class, employeeObj);
        
  jaxbMarshaller.marshal(jaxbElement, System.out);

```

### Date formatting in JaxB XML

- <https://www.baeldung.com/java-localdate-to-xmlgregoriancalendar>
  - LocalDate to JaxB XML Gregorian Calendar standard

```java
  // DatatypeFactory comes from javax.xml.datatype (same package as XMLGregorianCalendar)

  // Build directly from a date
  LocalDate localDate = LocalDate.of(2019, 4, 25);  
  XMLGregorianCalendar xmlGregorianCalendar = DatatypeFactory.newInstance().newXMLGregorianCalendar(localDate.toString());

  // Build from a formatted string
  String localDate2 = LocalDate.now().plusDays(30).format(DateTimeFormatter.ISO_DATE);
  XMLGregorianCalendar departureDateXmlCalendar = DatatypeFactory.newInstance().newXMLGregorianCalendar(localDate2);
```

## JAX-RS

- Building a JSON response <https://www.baeldung.com/jax-rs-response>
- Validating with JAX-RS rest assured <https://www.baeldung.com/rest-assured-tutorial>
- Example with jersey jax-rs client - <https://www.baeldung.com/jersey-jax-rs-client>

### Server side - build a JSON Response body

- <https://www.baeldung.com/jax-rs-response>

```java
@GET
@Path("/pojo")
public Response getPojoResponse() {

    Person person = new Person("SomeName", "SomePlace");

    return Response
      .status(Response.Status.OK)
      .entity(person)
      .build();
}
```

### Client side - Reading or Printing a JSON Response body

- <https://mkyong.com/webservices/jax-rs/jax-rs-how-to-read-response-body-from-a-post-request/>
- Difference between readEntity(<class>) and getEntity - <https://stackoverflow.com/questions/48781860/getentity-vs-readentity-in-response-javax-ws-rs>
  - Detail of API readEntity() - <https://docs.oracle.com/javaee/7/api/javax/ws/rs/core/Response.html#readEntity-java.lang.Class->
  - ResponseBuilder if needing to add meta-data <https://docs.oracle.com/javaee/7/api/javax/ws/rs/core/Response.ResponseBuilder.html>

```java
  import jakarta.ws.rs.core.Response;

  Response response = //... get the response object

  // Optional - Buffer entity if you want to read response body AND subsequently readEntity to object, otherwise it will fail due to the stream being closed.
  // This is specific to when you want to read response body as say a string and then later read the entity to an object
  response.bufferEntity(); 
  
  // read response body
  String body = response.readEntity(String.class);

  // After reading with readEntity, can use getEntity to retrieve the cached object
  Object obj = response.getEntity();

  // Could also readEntity to a class


```

(See also the Rest page in architecture)

## Asynchronous Programming - Completable Futures & Futures

Involves using Completable Futures and Futures to handle asynchronous programming.

- Baeldung nice guide with explanations of applyAsync() etc. <https://www.baeldung.com/java-completablefuture>
- Also lots of nice examples and explanations - <https://www.callicoder.com/java-8-completablefuture-tutorial/>, <https://www.callicoder.com/java-callable-and-future-tutorial/>
- DZone dump of examples - <https://dzone.com/articles/20-examples-of-using-javas-completablefuture>
- Asynchronous implementation libraries <https://www.baeldung.com/java-asynchronous-programming>
- Another example - <https://www.twilio.com/blog/asynchronous-api-requests-java-completablefutures>
- Java 8 Oreilly - CompletableFuture composable asynchronous programming - <https://learning.oreilly.com/library/view/java-8-in/9781617291999/kindle_split_023.html>

### thenApply vs thenCompose

- Equivalent to map and flatmap
  - map - [1,2,3,4]
  - flatmap - [(1,2), (3,4)]
  - apply - use when a single completable future
  - compose - when a nested completable future

### ThenApply vs ThenApplyAsync

- <https://www.baeldung.com/java-completablefuture-thenapply-thenapplyasync>

### Exception handling

- 3 Ways to Handle Exception In Completable Future - <https://mincong.io/2020/05/30/exception-handling-in-completable-future/>
- Asynchronous Timeouts with CompletableFuture - <https://dzone.com/articles/asynchronous-timeouts>
- <https://www.dariawan.com/tutorials/java/java-12-exception-handling-completionstage-completablefuture/>

#### Mocking errors in CompletableFuture

- Seems better to return a future containing an Exception rather than mockito().throws() - <https://stackoverflow.com/questions/45657008/simulate-completionexception-in-a-test>

```java
CompletableFuture<Long> future = new CompletableFuture<>();
future.completeExceptionally(new Exception("HTTP call failed!"));

Mockito.when(mockClient.getSize())
        .thenReturn(future);

```

### Join vs Get in Completable Future

- <https://www.baeldung.com/java-completablefuture>
- <https://www.baeldung.com/java-completablefuture-join-vs-get>
  - join() - throws unchecked exceptions
  - get() - throws checked exceptions
- <https://www.tedblob.com/completablefuture-join-vs-get/>

### Thread pooling with Completable Futures

- <https://www.baeldung.com/java-completablefuture-threadpool>


## Failsafe and fault tolerant JVM patterns

- <https://failsafe.dev/>
- <https://www.baeldung.com/java-failsafe-fault-tolerance>

## Lombok

- <https://www.baeldung.com/intro-to-project-lombok>


- RequiredArgsConstructor annotation


## Javadoc

### Referencing methods in javadoc

- Nice overview <https://www.baeldung.com/java-method-in-javadoc>
  - Format is ```{@link #methodName(argType)} labelToDisplay```

```java

class SomeClass {
  /**
   * REF a method in the same class
   * Also, check the {@link #move() Move} method for more movement details.
   */
  public void walk() {}

  public void move() {}

  /**
   * REF a method in another package and class (NB - can omit the package if same)
 * Also consider checking {@link com.baeldung.sealed.classes.Vehicle#Vehicle() Vehicle} 
 * constructor to initialize vehicle object.
 */
public void goToWork() {

}
}

```

## Application Servers

- JBoss - different versions
  - JBoss WildFly or JBoss AS (old name) - Open source base version of JBoss
    - JBoss AS renamed to Wildfly starting with version 8
    - JBoss Web - Tomcat based Servlet container Red Hat used in JBoss EAP 6
      - From EAP 7 (WildFly 8+) new Servlet container/http engine called Undertow.
  - JBoss EAP - commercially supported version which eventually absorbs features from the upstream JBoss Wildfly once stable.

- <https://stackoverflow.com/questions/31756933/what-is-the-difference-between-jboss-eap-wildfly-jboss-web-and-jboss-server>


## IDEs 

### Intellij

- if you have issues with "sticky" mouse selection and right-click not working, it might be because you touched the touchscreen of the laptop at the same time as using the mouse/trackpad. Focus on the Intellij window and then touch the touchscreen again to resolve the issue.