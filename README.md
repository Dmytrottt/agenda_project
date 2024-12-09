# Topics

1. Build the simple zio-cli project
2. Pack the project using `sbt-assembly`

## **1. Build the simple zio-cli project**

- Create simple application
- Add zio and zio-cli dependencies:
Change `project/Dependencies.scala` file
```scala
import sbt._

object Dependencies {
  lazy val Zio = "dev.zio" %% "zio" % "2.0.0"
  lazy val ZioCli = "dev.zio" %% "zio-cli" % "0.7.0"
}
```
Change `build.sbt` file
```scala
import Dependencies._

// ... some code here

lazy val agenda = (project in file("."))
  .settings(
    name := "agenda",
    libraryDependencies += Zio,
    libraryDependencies += ZioCli,
  )
```
- follow the instruction: [ziocli documentation](https://zio.dev/zio-cli/):
 - extend ZIOCliDefault
 - Create Command
 - Create Subcommand
 - Add subcommand
 - Handle subcommand
 
## 2. Pack the project using `sbt-assembly`

- Dependency for sbt-assembly
Add the following code to `project/plugins.sbt`
```scala
addSbtPlugin("com.eed3si9n" % "sbt-assembly" % "2.3.0")
```
- Import Build
- Execute sbt
```sh
sbt
sbt:agenda> assembly
```
- Set executable permissions
Find `.jar` file in the `target/scala-2.13` directory
```sh
chmod +x agenda-assembly-0.1.1-SNAPSHOT.jar
sudo mv target/scala-2.13/agenda-assembly-0.1.1-SNAPSHOT.jar /usr/bin/agenda.jar
```
- Create wrapper file `agenda` with content:
```script
#!/bin/bash
java -jar /usr/bin/agenda.jar $@
```
```sh
sudo chmod +x /usr/bin/agenda
which agenda 
```
