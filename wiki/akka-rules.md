# Akka rules package [rules/akka](/rules/akka/src)

These rules should apply to code that uses the Akka framework. The provided rules require the libraries
```scala
"com.typesafe.akka" %% "akka-actor" % "2.3.3"
"com.typesafe.akka" %% "akka-stream-experimental" % "0.4"
```

TODO: this requirement should be made more flexible by people who know more about Akka than I do!

## Sender method called in deferred block

name : **sender-in-future**  
source : [SenderInFuture](/rules/akka/src/main/scala/com/typesafe/abide/akka/SenderInFuture.scala)

The `sender()` method should _never_ be called inside of a code block that won't be executed immediately in the `receive` method since the resulting sender might not be the right one anymore when the deferred code is actually executed. For example, the code
```scala
class ExampleActor extends Actor {
  def receive = {
    case "Hi" => future {
      sender() ! "Hello"
    }
  }
}
```
should be written as
```scala
class ExampleActor extends Actor {
  def receive = {
    case "Hi" => 
      val s = sender()
      future { s ! "Hello" }
  }
}
```
to make sure the sender we use to reply is indeed the one associated to the received message.
