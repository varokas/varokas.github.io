---
layout:	post
title:	"Concurrency Model: Actors"
date:	2017-10-28
---

  Actors could be considered tiny micro services within our application. They consist of **Actors** that act on predefined set of **Messages **when received. Notable example is [Akka Actors](https://doc.akka.io/docs/akka/2.5.4/scala/actors.html).

#### Akka Actors

A **Message** is simply a Scala case class which carries information

case class Message(info: String)An **Actor** receives messages that are sent directly to it

class MyActor extends Actor {  
 def receive = {  
 case Message(info) => println(s"received: $info")  
 case \_ => println("unknown message")  
 }  
}To send a message, use an exclamation mark (!). This could be done from anywhere. Usually it is from an external event or another actor.

myActor ! myMessageBefore using actors, we need to create the system and the actors within. It is important to keep references to all the actors and that will be used for message passing later on.

val system = ActorSystem("actors")  
val myActor = system.actorOf(Props[MyActor])#### Good For

* Simulation of interaction between real-world objects, systems, or software processes
* When we know exactly who is the entity (actor) responsible for processing the message
#### Not Good For

* When there are multiple receivers of the same message, which usually would be dynamically created and removed.
  