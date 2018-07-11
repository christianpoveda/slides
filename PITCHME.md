## Scala and the Actor Model

MISO-4207

---

## Introduction

+++

### What is the actor model?

In the actor model, everything is an actor.

+++

### What is OOP?

_OOP is about message passing and isolation and protection of state. Objects and classes are implementations of those ideas._ 
Alan Kay (Smalltalk)

+++

### What is the actor model?

Imagine a world where objects are __completely isolated__ (even on failure) and can only use __messages__ for communicating.

+++

## The Actor Model

- Actors perform work in response to __messages__ in an __asynchronous__ way.
- Actors have no methods, they just know how to __handle__ certain __messages__.
- Actors do __not share state__.
- Actor instances can __start__, __stop__ and __recover from failures__ by __themselves__.

+++

## Actors in your favorite language

- Scala, Java & Kotlin: Akka
- Erlang & Elixir: OTP
- C# & F#: Akka.NET
- Go: Proto.Actor
- C++: CAF

