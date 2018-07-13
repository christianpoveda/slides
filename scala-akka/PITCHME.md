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

### The actor model

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

### A printer actor

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
@[1-4](Companion object has the `props` factory and the messages)
@[9-12](the `receive` method handles messages)
@[3](This message...)
@[10](Is handled here)
@[1-13]

+++

### The main app

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
@[8](This is a non blocking operation)
@[1-11]

---

## Messages between actors

+++

### An stateful actor

```scala
object Amnesiac {
  def props(printer: ActorRef): Props = Props(new Amnesiac(printer))
  
  final case class LastMsg()
  final case class HelloMsg(name: String)
}

class Amnesiac(val printer: ActorRef) extends Actor {
  import Amnesiac._

  var last: Option[String] = None
  ...
}
```
@[8](The class has an `ActorRef` as argument)
@[2](The `props` factory has the same argument)
@[11](The `last` attribute is mutable)
@[4-5](This actor handles two kind of messages)
@[1-13]

+++

### An stateful actor

```scala
  def receive = {
    case LastMsg => last match {
      case Some(name) =>
        printer ! Printer.PrintMsg(s"The last person who talked to me was $name\n")
      case None =>
        printer ! Printer.PrintMsg(s"No one has talked to me :(\n")
    }
    case HelloMsg(name) => {
      printer ! Printer.PrintMsg(s"Hello $name!")
      last = Some(name);
    }
  }
```
@[8-11](Say Hello and store the name)
@[2-7](Say the last name)
@[1-12]

+++

### The main app

```scala
implicit val system: ActorSystem = ActorSystem("mySystem")

val printer = system.actorOf(Printer.props, "printerActor")
val amnesiac = system.actorOf(Amnesiac.props(printer), "amnesiacActor")

amnesiac ! Amnesiac.LastMsg
amnesiac ! Amnesiac.HelloMsg("Alice")
amnesiac ! Amnesiac.LastMsg
amnesiac ! Amnesiac.HelloMsg("Bob")
amnesiac ! Amnesiac.LastMsg

system.terminate()
```
@[4](Create a new actor using the `props` factory)
@[6-10](Have fun!)
@[1-12](What should happen at runtime?)

+++

### Now do it yourself

Change the `Printer` actor so that it only prints after receiving 5 messages

---

## No data races

+++

### The thready main app
```scala
  implicit val system = ActorSystem("mySystem")

  val printer = system.actorOf(Printer.props, "printerActor")
  val amnesiac = system.actorOf(Amnesiac.props(printer), "amnesiacActor")

  val aliceThread = new Thread {
    override def run = {
      for(_ <- 1 to 10) {
        amnesiac ! Amnesiac.HelloMsg("Alice")
        Thread.sleep(100)
      } 
    }
  }

  val bobThread = new Thread {
    override def run = {
      for(_ <- 1 to 10) {
        amnesiac ! Amnesiac.HelloMsg("Bob")
        Thread.sleep(100)
      } 
    }
  }

  val lastThread = new Thread {
    override def run = {
      for(_ <- 1 to 10) {
        amnesiac ! Amnesiac.LastMsg
        Thread.sleep(100)
      } 
    }
  }

  aliceThread.start
  bobThread.start
  lastThread.start

  system.terminate()
```
