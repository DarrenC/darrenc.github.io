# Testing

- [Testing](#testing)
  - [Interesting articles](#interesting-articles)
  - [Selenium](#selenium)
  - [JUnit testing with Java](#junit-testing-with-java)
    - [JUnit 5](#junit-5)
    - [Using Tag to include/exclude tests](#using-tag-to-includeexclude-tests)
  - [Frameworks](#frameworks)
    - [Mockito](#mockito)
    - [PowerMock](#powermock)
    - [Geb Testing Framework](#geb-testing-framework)
  - [JUnit etc. - TODO  merge with sections above](#junit-etc---todo--merge-with-sections-above)
    - [Mockito - Partial Mocking and Spying](#mockito---partial-mocking-and-spying)
    - [Mockito - any() and raw values](#mockito---any-and-raw-values)
    - [Mockito - stub() when() and given() - when to use what](#mockito---stub-when-and-given---when-to-use-what)
    - [JUNIT Testing Hamcrest](#junit-testing-hamcrest)
    - [Mockito and Dependency Injection](#mockito-and-dependency-injection)
  - [Miscellaneous Testing](#miscellaneous-testing)
    - [Load Testing](#load-testing)
    - [Restful Resources Testing - Postman and Newman](#restful-resources-testing---postman-and-newman)

## Interesting articles

- How different companies do their testing - <https://github.com/abhivaikar/howtheytest>

## Selenium

Selenium IDE - Firefox add on to provide simple GUI for creating tests
Selenium RC/Web Driver - Java API for creating browser executed tests

Good Blog on Testing stuff: <http://www.nearinfinity.com/blogs/testing/>

When using the Selenium Web Driver you have to keep up to date on the
libs to allow you to launch the latest versions of Firefox etc.

Below is an example taken from the selenium website of a basic scenario
using the WebDriver.

```java
package selenium;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.firefox.FirefoxDriver;

public class Selenium2Example {

    public static void main(String[] args) {
        // Create a new instance of the Firefox driver
        // Notice that the remainder of the code relies on the interface, 
        // not the implementation.
        WebDriver driver = new FirefoxDriver();

        // And now use this to visit Google
        driver.get("http://www.google.com");

        // Find the text input element by its name
        WebElement element = driver.findElement(By.name("q"));

        // Enter something to search for
        element.sendKeys("Cheese!");

        // Now submit the form. WebDriver will find the form for us from the element
        element.submit();

        // Check the title of the page
        System.out.println("Page title is: " + driver.getTitle());

        //Close the browser
        //driver.quit();
    }

}
```

## JUnit testing with Java

### JUnit 5

- link to main JUnit5 documentation:
    <https://junit.org/junit5/docs/current/user-guide/#overview>
- TODO also - check out parameterized tests\....

### Using Tag to include/exclude tests

- Tag("integration-test") - can tag unit tests with Tag annotation to allow you to group tests
- Intellij JUnit configuration can use "Test Kind" drop-down with "Tag" value to allow filtering by tags for running tests
- Can exclude a tag with "!my-tag-name"

## Frameworks

### Mockito

Principle is to mock dependencies and provide expected results

```java
  @Test
  public void testGetIssueCurrency() {
    final String CURRENCY_EUR = "EUR";
    AmountInfoForAllPax amountInfoForAllPax = new AmountInfoForAllPax();
    ItineraryAmounts mockItineraryAmounts = Mockito.mock(ItineraryAmounts.class);
    Mockito.when(mockItineraryAmounts.getCurrencyMonetaryDetailByType(anyString())).thenReturn(CURRENCY_EUR);

    amountInfoForAllPax.setItineraryAmounts(mockItineraryAmounts);
    assertEquals(amountInfoForAllPax.getIssueCurrency(), CURRENCY_EUR);
  }
```

- Can also use **verify()** to make sure that certain methods are
    called.

### PowerMock

TODO - but maybe less useful since manipulating classes

### Geb Testing Framework

<http://www.gebish.org/>

From the site: \<pre\> Geb is a browser automation solution.

It brings together the power of WebDriver, the elegance of jQuery
content selection, the robustness of Page Object modelling and the
expressiveness of the Groovy language.

It can be used for scripting, scraping and general automation --- or
equally as a functional/web/acceptance testing solution via integration
with testing frameworks such as Spock, JUnit & TestNG.

The Book of Geb contains all the information you need to get started
with Geb. \</pre\>

## JUnit etc. - TODO  merge with sections above

### Mockito - Partial Mocking and Spying

- Partial Mocking - call Mock for all methods unless a method is
    explicitly marked as calling real method
- Spying - call real for all methods unless a method is explicitly
    marked as being mocked.

See the Mockito documentation on partial mocks for more information.

```java
Stock stock = mock(Stock.class);
when(stock.getPrice()).thenReturn(100.00); // Mock implementation
when(stock.getQuantity()).thenReturn(200); // Mock implementation
when(stock.getValue()).thenCallRealMethod(); // Real implementation
```

In that case, each method implementation is mocked, unless specify
thenCallRealMethod() in the when(..) clause. There is also a possibility
the other way arround with spy instead of mock:

```java
Stock stock = spy(Stock.class);
when(stock.getPrice()).thenReturn(100.00);    // Mock implementation
when(stock.getQuantity()).thenReturn(200);    // Mock implementation// All other method call will use the real implementations
```

There is one important pitfall when you use when(Object) with spy like
in the previous example. The real method will be called (because
stock.getPrice() is evaluated before when(..) at runtime). This can be a
problem if your method contains logic that should not be called. You can
write the previous example like this:

```java
Stock stock = spy(Stock.class);
doReturn(100.00).when(stock).getPrice();    // Mock implementation
doReturn(200).when(stock).getQuantity();    // Mock implementation// All other method call will use the real implementations
```

### Mockito - any() and raw values

When using the any() (e.g. anyInt()) in a Mockito matcher, all
parameters must be matchers, you can\'t use raw values (like -
Constants.SOME_STRING). To get around this, the eq() method will allow
you to use the constant values.

```java
when(someObj.someMethod(eq(metas), any(List.class), anyInt(), any(Config.class))).thenReturn(someResponse);
```

### Mockito - stub() when() and given() - when to use what

<http://stackoverflow.com/questions/14736219/difference-between-stub-and-when-in-mockito>

- stub() - original version
- when() - when interactions became fashionable
- given() - now that BDD is fashionable

Mockito - with mocking Class\<?\> style objects
<http://stackoverflow.com/questions/7366237/mockito-stubbing-methods-that-return-type-with-bounded-wild-cards>

### JUNIT Testing Hamcrest

- Using the hamcrest form of asserts

```java
import static org.hamcrest.Matchers.is;
import static org.hamcrest.Matchers.nullValue;

    Assert.assertThat(preferencesList, is(nullValue()));
```

### Mockito and Dependency Injection

<https://blog.jayway.com/2012/02/25/mockito-and-dependency-injection/>

```java
@RunWith(MockitoJUnitRunner.class)
public class ExampleTest {

    @Mock
    Delegate delegateMock;

    @InjectMocks
    Example example;

    @Test
    public void testDoIt() {
        example.doIt();
        verify(delegateMock).execute();
    }
}
```

## Miscellaneous Testing

- <http://docs.spockframework.org/en/latest/introduction.html> - Spock testing and specification framework
- <http://www.codeaffine.com/2012/11/26/working-efficiently-with-junit-in-eclipse-2/>
- Infinitest - Runs all tests that could be impacted when you change code - <http://infinitest.github.io/>
- Article critical of TDD -
    <http://ravimohan.blogspot.fr/2007/04/learning-from-sudoku-solvers.html>
- Maximising return on Testing effort
    <http://zeroturnaround.com/rebellabs/dont-test-blindly-the-right-methods-for-unit-testing-your-java-apps/>
- <https://dzone.com/articles/the-evolution-of-software-quality-processes-and-to>
- <https://www.cqse.eu/en/blog/i-will-clean-up-next-time/>
- <https://www.cqse.eu/en/products/teamscale/landing/> - Rival to
    SonarQube
- Rollbar - Error monitoring and consolidation - <https://rollbar.com/>
- mutation testing -<http://blog.cleancoder.com/uncle-bob/2016/06/10/MutationTesting.html>
- <http://moreunit.sourceforge.net/>
- <https://infinitest.github.io/>
- <http://codurance.com/practices/extreme-programming/2016/06/14/mastering-TDD/>
- Very important - how to avoid big steps in refactoring - <https://blog.8thlight.com/uncle-bob/2013/05/27/TheTransformationPriorityPremise.html>
- Reducing Software Defects - <http://www.daedtech.com/how-to-actually-reduce-software-defects/>
- ZOMBIES for TDD - <http://blog.wingman-sw.com/archives/677>

### Load Testing

- Link to new page for load testing -
    <http://www.iamdarren.net/wikidc/doku.php?id=testing:loadtesting>

### Restful Resources Testing - Postman and Newman

- link to postman page -
    <http://www.iamdarren.net/wikidc/doku.php?id=testing:postman>
