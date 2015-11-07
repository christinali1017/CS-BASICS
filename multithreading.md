###Basic
---
https://www.youtube.com/watch?v=O_Ojfq-OIpM

Examples:

- Computer games are the best examples for applying multithreading.
- Download files. Suppose we have several files to download. 


Process and threads:

- A office word opened on your computer can be considered as a process.A error check can be considered as a thread.
- Even when you do not create threads there is a main thread execute the program
- Os schedules the threads to be processed by the process.


Creating threads:

```java
Thread t = new Thread();
```

At this point, you just creates a thread object. You need to call 

```java
t.start();
```

But there is no guarantee that the thread willl start immediately when start is invoked.

At this point, java.lang.Thread has no idea about what we want to do. **Thus we need to extends Thread and override the Run method**. Or **implements Runnable interface.**

Example:

Extends Thread class:


```java
class Downloader extends Thread {
    private String url;
    public Downloader(String url) {
        this.url = url;
    }
    
    public void run() {
        FileDowndloader fd = new FileDownloader();
        fd.download(this.url);
    }
}
```

Implement Runnable:

```java
Class Downloader implements Runnanle {
    private String url;
    public Downloader(String url) {
        this.url = url;
    }
    
    public void run() {
        FileDowndloader fd = new FileDownloader();
        fd.download(this.url);
    }
}


//When use it:
Downloader d = new Downloader();
Thread t = new Thread(d);
t.start();
```

###Thread constructor
---

You can specified Runnable target, thread name, thread group, etc.

- Thread()

- Thread(Runnable target)

- Thread(Runnable target, String name)

- Thread(String name)

- Thread(ThreadGroup group, Runnable target)

- Thread(ThreadGroup group, Runnable target, String name)

- Thread(ThreadGroup group, Runnable target, String name, long stackSize)

- Thread(ThreadGroup group, String name)


###Thread states
---

- **New**  Thread t = new Thread()
- **Runnable**   t.start()
- **Running**   the thread is actually executeing the code.
- **Sleep / waiting / blocked**
- **Dead**   cannot start again on this object once it is dead.


###Thread priority
---

- All threads in java carry normal priority unless specified.
- Priority specified 1 to 10
- Priority should be set before start is called

**Yield**:

Yield method tells the currently running thread to give chance to other threads with equal priority in the thread pool. 


**Join**:

Waits for this thread to die.

So t1.join() is called to wait for the t1 thread to finish. Then t2.join() is called to wait for the t2 thread to finish. The 2 threads have been running in parallel but the thread that started them (probably the main thread) needs to wait for them to finish before continuing. That's a common pattern. When the main thread calls t1.join() it will stop running and wait for the t1 thread to finish.

http://stackoverflow.com/questions/15956231/what-does-this-thread-join-code-mean


###Thread safety
---

- Remember to keep the instance variables marked as private in multithread environment to avoid manipulating them by threads.
- Unnecessary code synchronization will affect the application's performance.

Simple example of **Synchronized**

```java
package multithreading;

/**
 * In this example, for increment count, we use synchronized to maintain the atomic of increment.
 * 
 * If we just put count++ in run method, the result can not guarantee to be 20000. Because 
 * to do count++, it has 3 operations, we need first read count, then count + 1, then write 
 * back. 
 * 
 * Because these three operations can not guarantee atomic, thus there is possibility that 
 * the final result is < 20000.
 *
 */

public class SynchronizedExample {
    private int count =0;
    public synchronized void increment() {
        count++;
    }
    public static void main(String[] args) {
        SynchronizedExample e = new SynchronizedExample();
        e.doWork();
    }
    public void doWork() {
        Thread t1 = new Thread(new Runnable() {
            public void run() {
                for (int i = 0; i < 10000; i++) {
                    increment();
                }
            }
        });
        
        Thread t2 = new Thread(new Runnable() {
            public void run() {
                for (int i = 0; i < 10000; i++) {
                    increment();
                }
            }
        });
        
        t1.start();
        t2.start();
        
        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        
        System.out.println("Count is " + count);
    }
}

```

In the above method, if we add synchronized on a method, then it synchronized on "this" class object.















