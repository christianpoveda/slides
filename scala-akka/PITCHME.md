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

+++

### Real world usage
 
@ul
- Akka has its own http library [`akka-http`](https://doc.akka.io/docs/akka-http/current/) 
- Akka has its own streaming library [`akka-stream`](https://doc.akka.io/docs/akka/current/stream/) 

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
@[3, 10](This message is handled here)
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
  
  scala.io.StdIn.readLine()
  system.terminate()
}
```
@[2-3](Create an `ActorSystem`)
@[11](Terminate the `ActorSystem`)
@[5-6](Create an actor instance in the system)
@[8](Sends a message using the `!` operator)
@[8](This is a non blocking operation)
@[1-12]

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
@[8, 2](The `props` factory has the same argument)
@[11](The `last` attribute is mutable)
@[4-5](This actor handles two kind of messages)
@[1-13]

+++

### An stateful actor

```scala
  ...
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
@[9-12](Say Hello and store the name)
@[3-8](Say the last name)
@[1-13]

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

scala.io.StdIn.readLine()
system.terminate()
```
@[4](Create a new actor using the `props` factory)
@[6-10](Have fun!)
@[1-13](What should happen at runtime?)

+++

### No data races

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

  scala.io.StdIn.readLine()
  system.terminate()
```

+++

### Now do it yourself

Change the `Printer` actor so that it only prints after receiving 5 messages

---

## Patterns

+++

### A mnemonist actor

```scala
object Mnemonist {
  def props: Props = Props(new Mnemonist)

  final case class RememberMsg(name: String)
  final case class RecallMsg()
  final case class NamesMsg(names: List[String])
}

class Mnemonist() extends Actor {
  import Mnemonist._

  var names: List[String] = List.empty[String]

  def receive = {
    case RememberMsg(name) => names = name::names
    case RecallMsg => sender ! NamesMsg(names)
  }
}
```
@[12](Stores all the received names)
@[4, 15](Adds the name to `names`)
@[5-6, 16](Sends back `names`)
@[5-6, 16](`sender` is a reference to the sender)
@[1-18]

+++

### Fixing amnesia

```scala
object Amnesiac {
  def props(printer: ActorRef, mnemonist: ActorRef) = 
    Props(new Amnesiac(printer, mnemonist))
  ...
  final case class FirstMsg()
}
```
@[2-3](Now we have a reference to `mnemonist`)
@[5](We can use `mnemonist` to recall the first name)
@[1-6]

+++

### Fixing amnesia

```scala
class Amnesiac(val printer: ActorRef, val mnemonist: ActorRef) extends Actor {
  ...
  implicit val timeout = Timeout(30 seconds)

  def receive = {
    case FirstMsg => {
      val future = (mnemonist ? Mnemonist.RecallMsg).mapTo[Mnemonist.NamesMsg] 
      
      future.map({ msg: Mnemonist.NamesMsg => msg.names.lastOption match {
        case Some(name) => Printer.PrintMsg(s"The first person who talked to me was $name\n")
        case None => Printer.PrintMsg(s"No one has talked to me :(\n")
      }}).pipeTo(printer)
    ...
```
@[1](Modify the class arguments accordingly)
@[6-12](Handles the new message)
@[7](`?` or `ask` allow us to receive something back)
@[3, 7](It needs a timeout)
@[7](The result is a `Future`)
@[9-11](`map` let us transform a `Future`)
@[12](`pipeTo` sends a `Future` to an actor)
@[1-13]

+++

### The main app

```scala
object Patterns extends App {
  implicit val system: ActorSystem = ActorSystem("mySystem")

  val printer: ActorRef = system.actorOf(Printer.props, "printerActor")
  val mnemonist: ActorRef = system.actorOf(Mnemonist.props, "mnemonistActor")
  val amnesiac: ActorRef = system.actorOf(Amnesiac.props(printer, mnemonist), "amnesiacActor")

  amnesiac ! Amnesiac.HelloMsg("Alice")
  amnesiac ! Amnesiac.HelloMsg("Bob")
  amnesiac ! Amnesiac.HelloMsg("Charlie")
  amnesiac ! Amnesiac.HelloMsg("David")
  amnesiac ! Amnesiac.LastMsg
  amnesiac ! Amnesiac.FirstMsg

  scala.io.StdIn.readLine()
  system.terminate()
}
```

---

### Where to learn more
- [The akka website](https://akka.io/)
- [Learning Concurrent Programming in Scala](https://www.amazon.com/Learning-Concurrent-Programming-Aleksandar-Prokopec/dp/1783281413)
- [Programming Erlang](https://pragprog.com/book/jaerlang2/programming-erlang)
- [The Little Elixir & OTP Guidebook](https://www.manning.com/books/the-little-elixir-and-otp-guidebook)
