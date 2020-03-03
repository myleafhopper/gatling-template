# gatling-template

The following must be installed on your machine before you can being gatling development & execution:

1. JAVA
2. Maven

## VsCode Development Setup ##

To use VsCode as the primary IDE for gatling script development & execution you must:

1. Install the following VsCode plugin: `Scala (Metals)`
2. Install the following VsCode plugin: `Maven for Java`
3. Update maven archetypes using the command pallette (View > Command Pallette): `Maven: Update Maven Archetype Catalog`
4. Create a new maven project using the command pallette (View > Command Pallette):
    - `Maven: Create Maven Project`
    - `more`
    - `gatling-highcharts-maven-archetype`
5. Select the directory where your project root directory will be created.
6. For the `groupId` type in your project name.
7. For the `artifactId` type in your project name.
8. Accept the default snapshot version.
9. Accept the default package.
10. Confirm all selections.
11. Open the project using VsCode.
12. Open the `METALS` plugin and select `Import Build` under the ***BUILD*** tab.
13. From the project root create a folder called `sample` in the following directory: `src` > `test` > `scala`
14. In the `sample` folder create a file called: `BasicSimulation.scala`
    - Note: Basic simulation code can be found as the end of this guild.

---

```
package sample

import io.gatling.core.Predef._
import io.gatling.http.Predef._
import scala.concurrent.duration._

class BasicSimulation extends Simulation {

  val httpProtocol = http
    .baseUrl("http://computer-database.gatling.io") // Here is the root for all relative URLs
    .acceptHeader(
      "text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8"
    ) // Here are the common headers
    .acceptEncodingHeader("gzip, deflate")
    .acceptLanguageHeader("en-US,en;q=0.5")
    .userAgentHeader(
      "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.8; rv:16.0) Gecko/20100101 Firefox/16.0"
    )

  val scn =
    scenario("Scenario Name") // A scenario is a chain of requests and pauses
      .exec(
        http("request_1")
          .get("/")
      )
      .pause(7) // Note that Gatling has recorder real time pauses

  setUp(scn.inject(atOnceUsers(1)).protocols(httpProtocol))
}
```
