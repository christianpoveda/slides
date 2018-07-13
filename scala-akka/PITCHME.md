## Actors in Scala

MISO-4207

---

## Introduction

+++

### What is the actor model?

In the actor model, everything is an actor.

+++

### What is OOP?

_OOP is about message passing and isolation and protection of state. Objects and classes are implementations of those ideas_ - Alan Kay (Smalltalk)

+++

### The Actor Model

@ul
- Actors perform work in response to __messages__ in an __asynchronous__ way.
- Actors can send __messages__ to other actors.
- Actors do __not share state__ (no data races).
- __Creating actors__ and __sending messages__ is __location independant__.
@ulend

+++

### Actors in your favorite language

@ul
- Scala & Java: Akka
- C# & F#: Akka.NET
- Go: Proto.Actor
- Erlang & Elixir: OTP
- C++: CAF
@ulend

---

## Scala and Akka

+++

### The Akka actor model

@ul
- Actor System: Creates and locates actors.
- Actor Class: Describes the state and behavior of an Actor.
- Actor Instance: Exists at runtime and receive messages.
- Message: Unit of communication between instances.
@ulend

+++

### The Akka actor model
![Akka System](scala-akka/images/akka_system.png)

---

## Hello World

+++

```scala
object Printer {
  def props: Props = Props(new Printer)
  final case class PrintMsg(text: String)
}

class Printer extends Actor {
  import Printer._

  def receive = {
    case PrintMsg(text) => println(text)
    case _ => println("Unexpected message")
  }
}
```
@[6](Actor classes inherit from `akka.actor.Actor`)
@[1-4](Companion object has the `Props` factory and the messages)
@[9-12](the `receive` method handles messages)
@[3](This message...)
@[10](Is handled here)

+++

```scala
object HelloWorld extends App {
  implicit val system: ActorSystem =
    ActorSystem("mySystem")

  val printer: ActorRef = 
   system.actorOf(Printer.props, "printerActor")

  printer ! Printer.PrintMsg("Hello, world!")

  system.terminate()
}
```
@[2-3](Create an `ActorSystem`)
@[10](Terminate the `ActorSystem`)
@[5-6](Create an actor instance in the system)
@[8](Sends a message using the `!` operator)

