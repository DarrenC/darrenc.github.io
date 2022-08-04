# Web Services

- [Web Services](#web-services)
  - [Introduction articles](#introduction-articles)
  - [Definitions](#definitions)
  - [CXF](#cxf)
  - [JAX WS](#jax-ws)
    - [Asynchronous JAX-WS](#asynchronous-jax-ws)
      - [Basic Procedure Notes](#basic-procedure-notes)
      - [Examples of async calls](#examples-of-async-calls)
    - [Tools](#tools)
    - [Handling SOAP exceptions](#handling-soap-exceptions)

## Introduction articles

- Very old intro - <http://onjava.com/pub/a/onjava/2001/08/07/webservices.html>
- JAXB Introduction article - <http://java.sun.com/developer/technicalArticles/WebServices/jaxb/>
- SOAP humour - <http://wanderingbarque.com/nonintersecting/2006/11/15/the-s-stands-for-simple/>

## Definitions

- JAX-B - Java Architecture for XML Binding
- JAX-WS - Java API for XML Web Services
- JAX-P - Java API for XML Binding
- JAX-RPC - Java API forXML-based RPC (deprecated in Java6)
- JAX-RS - Java API for Rest services

## CXF

- <http://www.benmccann.com/dev-blog/web-services-tutorial-with-apache-cxf/>
- <http://cxf.apache.org/docs/defining-contract-first-webservices-with-wsdl-generation-from-java.html>
- <http://www.jroller.com/gmazza/entry/soap_client_tutorial>

Can return PDFs from webservice as a byte[] array

## JAX WS

Can create JAX-WS services either from code or from a WSDL. WSDL is better supported by tools but either is possible :).

### Asynchronous JAX-WS

- Nice example of a simple async ws <https://godatadriven.com/blog/reactive-web-service-client-with-jax-ws/>

#### Basic Procedure Notes

- To go from a simple method to async you need to define 2 more methods which are called <methodName>Async
  - One is a polling method which is blocking+async, the other is a callback handler which is non-blocking+async
  - It's tricky because of the future interface to have a really non-blocking implementation, most examples show a future.get() or .isDone() + sleep style aproach waiting for the response to be available
    - We have a CompletableFuture based approach which can work for the case where you don't need to process the response in the handler (see below)

```java
public interface GreeterAsync {
 
  // Blocking Synchronous call 
  public java.lang.String greetMeSometime( String requestType );

  // Blocking Async call, you poll for a response
  public Response<GreetMeSometimeResponse> greetMeSometimeAsync(String requestType);  

  // Non-Blocking async call, callback handler to get the response when available
  public Future<?> greetMeSometimeAsync( String requestType, AsyncHandler<GreetMeSometimeResponse> asyncHandler );
  
}
```

#### Examples of async calls

- This one is the best one since it should be really non-blocking anywhere

```java
    // Calling the webservice in full async (paraphrased from code)
    long timeout = 5000;
    CompletableFuture<GreeterResponse> async = new CompletableFuture<>();
    final GreeterAsyncHandler handler = new GreeterAsyncHandler(async, timeout);
    
    greeterWebservice.greetMeSometimeAsync(greeterRequest, handler);
    return async.orTimeout(timeout, TimeUnit.MILLISECONDS);
```

```java

// async handler code

package blah;

import java.util.concurrent.CompletableFuture;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.TimeUnit;
import java.util.concurrent.TimeoutException;

import javax.xml.ws.AsyncHandler;
import javax.xml.ws.Response;

public class GreeterAsyncHandler implements AsyncHandler<GreeterResponse> {

  private final CompletableFuture<GreeterResponse> cf;
  private final long timeout;

  public GreeterAsyncHandler(CompletableFuture<GreeterResponse> cf, long timeout) {
    this.timeout = timeout;
    this.cf = cf;
  }

  @Override
  public void handleResponse(Response<GreeterResponse> response) {
    try {
      // call in a completable future which will be used elsewhere
      // This works because our handler doesn't need to do anything to the response, we can just delegate to the completable future
      cf.complete(response.get(timeout, TimeUnit.MILLISECONDS));
    } catch (InterruptedException | ExecutionException e) {      
      Thread.currentThread().interrupt();
    } catch (TimeoutException te) {
      // blah
    }
  }
}

```

- This one is okay but still has a sleep on a thread + then a blocking get() call to future

```java

/**
 * ASYNC HANDLER CLASS
 */
package demo.hw.client;
 
import javax.xml.ws.AsyncHandler;
import javax.xml.ws.Response;
 
import org.apache.hello_world_async_soap_http.types.GreetMeSometimeResponse;
 
public class TestAsyncHandler implements AsyncHandler<GreetMeSometimeResponse> {
  private GreetMeSometimeResponse reply;
 
  public void handleResponse(Response<GreetMeSometimeResponse> response) {
    try {
      reply = response.get();
    } catch (Exception ex) {
      ex.printStackTrace();
    }
  }
 
  public String getResponse() {
    return reply.getResponseType();
  }
}

/**
 * And the calling code
 */

package demo.hw.client;
 
import java.io.File;
import java.util.concurrent.Future;
 
import javax.xml.namespace.QName;
import javax.xml.ws.Response;
 
import org.apache.hello_world_async_soap_http.GreeterAsync;
import org.apache.hello_world_async_soap_http.SOAPService;
import org.apache.hello_world_async_soap_http.types.GreetMeSometimeResponse;
 
public final class Client {
  private static final QName SERVICE_NAME = new QName("http://apache.org/hello_world_async_soap_http", "SOAPService");
 
  private Client() {}
 
  public static void main(String args[]) throws Exception {
        
    TestAsyncHandler testAsyncHandler = new TestAsyncHandler();
    
    // Call the WS and get back a future
    Future<?> response = port.greetMeSometimeAsync(System.getProperty("user.name"), testAsyncHandler);
    
    // sleep in a loop until the future is done (or even future.get() for complete block)
    while (!response.isDone()) {
      Thread.sleep(100);
    }

    // Call the async handler to get a response object
    resp = testAsyncHandler.getResponse();
    ...
    System.exit(0);
  }
}
```

### Tools

- CXF
  - wsdl2java - from a WSDL, generate the java classes for the WS (client stubs and server code)
  - java2ws - from java classes, generate a wsdl
  - These plugins are called via the cxf codegen plugin 

TODO -> Example from the CXF examples showing both directions



### Handling SOAP exceptions

- Handling SOAP Exceptions in JaxWS: <http://io.typepad.com/eben_hewitt_on_java/2009/07/using-soap-faults-and-exceptions-in-java-jaxws-web-services.html>
