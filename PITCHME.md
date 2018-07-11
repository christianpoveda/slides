# Scala and the Actor Model

This is title

---

## Introduction

### What is the actor model?

In the actor/object model, everything is an actor/object.

---

### What is OOP?

OOP is about message passing and isolation and protection of state. Objects and classes are implementations of those ideas. - Alan Kay (Smalltalk)

---

### What is the actor model?

Imagine a world where objects are completely isolated (even on failure) and can only use messages for communicating.

---

## The Actor Model

- Actors perform work in response to messages in an asynchronous way.
- Actors have no methods, they just know how to handle certain messages.
- Actors do not share state.
- Actor instances can start, stop and recover from failures by themselves. Other entities use references to each instance for communication.

---

## Actors exist in your favorite language

- Scala, Java & Kotlin: Akka
- Erlang & Elixir: OTP
- C# & F#: Akka.NET
- Go: Proto.Actor
- C++: CAF

---
