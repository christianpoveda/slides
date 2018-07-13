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
- Actors have no methods, they just know how to __handle__ certain __messages__.
- Actors do __not share state__ (no data races).
- Actors can __start__, __stop__ and __recover from failures__ by __themselves__.
@ulend

+++

### Let it crash

_Is better to let an actor crash and then decide what to do with the error_

+++

### Sequential programming

@ul
- There is a __single process__.
- If that process crash, the whole aplication crash.
- We try to __prevent errors__ (defensive programming).
@ulend

+++

### Concurrent programming

@ul
- There are __several processes__.
- If one process crash, we can handle the error.
- We try to __recover from errors__ (corrective programming).    
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
- Actor System: Create and locate actors.
- Actor Class: Describes the state and behavior of an Actor.
- Actor Instance: Exist at runtime and receive messages.
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
@[1-4](Companion object has the recipe and the messages)
@[9-12](the `receive` method handles messages)
@[3](This message...)
@[10](Is handled here)
