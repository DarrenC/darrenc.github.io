# Load Testing - Perf and Profiling stuff

## List of Tools

- JMeter
- Gatling
- JMH - open JDK performance tester with lots of JUnit Parallels -
    <http://openjdk.java.net/projects/code-tools/jmh/>
- YourKit - JDK Profiler
- Really good low latency profilers
  - https://github.com/async-profiler/async-profiler
  - https://github.com/glowroot/glowroot

## Gatling

Open-Source load test runner. Has paid version too called Frontline.
Based on Scala + Akka

- Link to Gatling docs -
    <https://gatling.io/docs/current/http/http_protocol/>
- Interesting article about adding a protocol (maybe old though) -
    <https://www.trivento.io/write-custom-protocol-for-gatling/>
  - <https://github.com/jgordijn/lambda_gatling_test>
- Link to an issue with a jenkins gatling plugin -
    <https://github.com/gatling/gatling/issues/3407>
- And some protocol extensions examples;
  - <https://gatling.io/docs/current/extensions>
    - Git commands one - <https://github.com/GerritForge/gatling-git> 
    - JDBC one - <https://github.com/rbraeunlich/gatling-jdbc>

### Gatling Feeders

Using Feeders we can parameterize tests using various sources of data - DB, file etc.

- Gatling docs - <https://gatling.io/docs/current/session/feeder/>
  - Example in tutorial - <https://gatling.io/docs/current/advanced_tutorial/>
- Examples - <https://chercher.tech/gatling/gatling-feeders>
- <https://stackoverflow.com/questions/35730086/how-can-i-turn-a-simple-iterative-loop-into-a-feeder-in-gatling>

## JMeter

The original open source load tester.

List of TODOs for this section

- Add links to JMeter docs + examples
- Add example of the nice report :)
- Investigate adding a protocol other than http
  - <https://jmeter.apache.org/usermanual/jmeter_tutorial.html>
