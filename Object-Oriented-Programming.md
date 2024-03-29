###Interface vs Abstract class
---
An interface is a contract: the guy writing the interface says, "hey, I accept things looking that way", and the guy using the interface says "Ok, the class I write looks that way".

**An interface is an empty shell, there are only the signatures of the methods, which implies that the methods do not have a body**. The interface can't do anything. It's just a pattern.


Abstract classes

Abstract classes, unlike interfaces, are classes. They are more expensive to use because there is a look-up to do when you inherit from them.

Abstract classes look a lot like interfaces, but they have something more : **you can define a behavior for them.** **It's more about a guy saying, "these classes should look like that, and they have that in common, so fill in the blanks!".**

http://stackoverflow.com/questions/1913098/what-is-the-difference-between-an-interface-and-abstract-class



1.Main difference is methods of a Java interface are implicitly abstract and cannot have implementations. A Java abstract class can have instance methods that implements a default behavior.

2.Variables declared in a Java interface is by default final. An abstract class may contain non-final variables.

3.Members of a Java interface are public by default. A Java abstract class can have the usual flavors of class members like private, protected, etc..

4.Java interface should be implemented using keyword “implements”; A Java abstract class should be extended using keyword “extends”.

5.An interface can extend another Java interface only, an abstract class can extend another Java class and implement multiple Java interfaces.

6.A Java class can implement multiple interfaces but it can extend only one abstract class.

7.Interface is absolutely abstract and cannot be instantiated; A Java abstract class also cannot be instantiated, but can be invoked if a main() exists.

8.In comparison with java abstract classes, java interfaces are slow as it requires extra indirection.

http://javapapers.com/core-java/abstract-and-interface-core-java-2/difference-between-a-java-interface-and-a-java-abstract-class/


###Polymorphism
---

http://stackoverflow.com/questions/1031273/what-is-polymorphism-what-is-it-for-and-how-is-it-used


**Polymorphism describes a pattern in object oriented programming in which classes have different functionality while sharing a common interface.**

The beauty of polymorphism is that the code working with the different classes does not need to know which class it is using since they’re all used the same way. A real world analogy for polymorphism is a button. Everyone knows how to use a button: you simply apply pressure to it. What a button “does,” however, depends on what it is connected to and the context in which it is used — but the result does not affect how it is used. If your boss tells you to press a button, you already have all the information needed to perform the task.

In the programming world, polymorphism is used to make applications more modular and extensible. Instead of messy conditional statements describing different courses of action, you create interchangeable objects that you select based on your needs. That is the basic goal of polymorphism.