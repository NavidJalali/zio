---
id: zio-http
title: "ZIO HTTP"
---

[ZIO HTTP](https://github.com/dream11/zio-http) is a scala library to write HTTP applications.

## Introduction

ZIO HTTP is a Scala library for building HTTP applications. It is powered by ZIO and netty and aims at being the defacto solution for writing, highly scalable, and performant web applications using idiomatic scala.

## Installation

In order to use this library, we need to add the following lines in our `build.sbt` file:

```scala
libraryDependencies += "io.d11" %% "zhttp"      % "1.0.0.0-RC13"
libraryDependencies += "io.d11" %% "zhttp-test" % "1.0.0.0-RC13" % Test
```

## Example

```scala
import zhttp.http._
import zhttp.service.Server
import zio._

object ZIOHTTPExample extends zio.App {

  // Create HTTP route
  val app: HttpApp[Any, Nothing] = HttpApp.collect {
    case Method.GET -> Root / "text" => Response.text("Hello World!")
    case Method.GET -> Root / "json" => Response.jsonString("""{"greetings": "Hello World!"}""")
  }

  // Run it like any simple app
  override def run(args: List[String]): URIO[zio.ZEnv, ExitCode] =
    Server.start(8090, app.silent).exitCode
}
```

## Resources

- [ZIO World - ZIO HTTP](https://www.youtube.com/watch?v=dVggks9_1Qk&t=257s) by Tushar Mathur (March 2020) — At ZIO World Tushar Mathur unveiled a new open-source library 'ZIO HTTP' that gives you better performance than Vert.x, but with pure functional Scala and native ZIO integration.