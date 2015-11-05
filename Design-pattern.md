###Singleton
---

**Singleton is a class which has only one instance in whole application and provides a getInstance() method to access the singleton instance**. There are many classes in JDK which is implemented using Singleton pattern like **java.lang.Runtime** which provides getRuntime() method to get access of it and used to get free memory and total memory in Java.

Which classes are candidates of Singleton?

**Any class which you want to be available to whole application and whole only one instance is viable is candidate of becoming Singleton**. One example of this is **Runtime** class , since on whole java application only one runtime environment can be possible making Runtime Singleton is right decision. Another example is a utility classes like **Popup in GUI application**, if you want to show popup with message you can have one PopUp class on whole GUI application and anytime just get its instance, and call show() with message. 

Read more: http://javarevisited.blogspot.com/2011/03/10-interview-questions-on-singleton.html#ixzz3qdcME0r6