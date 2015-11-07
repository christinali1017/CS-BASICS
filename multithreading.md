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


**Wait**:
wait will release the lock.

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

In the above method, **if we add synchronized on a method, then it synchronized on "this" class object.**


**Multi lock example**:

In the following example, we have two threads to add element to two list. If we add synchronized to stageOne and stageTwo method, it's thread safe. But it takes around 5 seconds to finish adding. 

Because we add synchronized on the two methods. Thus the two method can not be executed on the same time. Because they both have lock on "class object". 

```java
package multithreading;

import java.util.ArrayList;
import java.util.List;
import java.util.Random;

public class MultilockExample {
    private List<Integer> list1 = new ArrayList<>();
    private List<Integer> list2 = new ArrayList<>();

    private Random random = new Random();
    
    public synchronized void stageOne() {
        try {
            Thread.sleep(1);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        list1.add(random.nextInt(100));
    }

    public synchronized void stageTwo() {
        try {
            Thread.sleep(1);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        list2.add(random.nextInt(100));
    }

    public void process() {
        for (int i = 0; i < 1000; i++) {
            stageOne();
            stageTwo();
        }
    }

    public static void main(String[] args) {
        MultilockExample m = new MultilockExample();
        System.out.println("Starting...");
        long start = System.currentTimeMillis();
        Thread t1 = new Thread(new Runnable() {
            @Override
            public void run() {
                m.process();
            }
        });
        Thread t2 = new Thread(new Runnable() {
            @Override
            public void run() {
                m.process();
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
        long end = System.currentTimeMillis();
        System.out.println("Time take " + (end - start));
        System.out.println("List 1: " + m.list1.size() + "; list 2 : " + m.list2.size());
    }
}
```

Run result:

```
Starting...
Time take 5417
List 1: 2000; list 2 : 2000```

How to make it faster? What we can do to execute the two method at the same time? 

We can use synchronized block. See the following example:

```java
package multithreading;

import java.util.ArrayList;
import java.util.List;
import java.util.Random;

public class MultilockExample {
    private List<Integer> list1 = new ArrayList<>();
    private List<Integer> list2 = new ArrayList<>();

    private Object lock1 = new Object();
    private Object lock2 = new Object();

    private Random random = new Random();
    
    public void stageOne() {
        synchronized (lock1) {
            try {
                Thread.sleep(1);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            
            list1.add(random.nextInt(100));
        }
    }

    public void stageTwo() {
        synchronized (lock2) {
            try {
                Thread.sleep(1);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
    
            list2.add(random.nextInt(100));
        }
    }

    public void process() {
        for (int i = 0; i < 1000; i++) {
            stageOne();
            stageTwo();
        }
    }

    public static void main(String[] args) {
        MultilockExample m = new MultilockExample();
        System.out.println("Starting...");
        long start = System.currentTimeMillis();
        Thread t1 = new Thread(new Runnable() {
            @Override
            public void run() {
                m.process();
            }
        });
        Thread t2 = new Thread(new Runnable() {
            @Override
            public void run() {
                m.process();
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
        long end = System.currentTimeMillis();
        System.out.println("Time take " + (end - start));
        System.out.println("List 1: " + m.list1.size() + "; list 2 : " + m.list2.size());
    }
}

```

This time it takes around 2 seconds to run the result. 

```
Starting...
Time take 2728
List 1: 2000; list 2 : 2000
```

###Thread pool
---

Use Executors.newFixedThreadPool(num) to create thread pool.

See the following example:

```java
package multithreading;

import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.TimeUnit;

class Processor implements Runnable{

    private int id;

    public Processor(int id) {
        this.id = id;
    }

    @Override
    public void run() {
        System.out.println("Starting: " + id);

        try {
            Thread.sleep(5000);
        } catch (InterruptedException e) {
        }
        System.out.println("Completed: " + id);
    }

}

public class ThreadPool {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(2);
        for (int i = 0; i < 5; i++) {
            executor.submit(new Processor(i));
        }
        executor.shutdown();

        try {
            executor.awaitTermination(1, TimeUnit.DAYS);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("All tasks submitted");
    }
}


```

https://www.youtube.com/watch?v=lotAYC3hLVo&list=PLBB24CFB073F1048E&index=3


###CountDownLatch
---

A synchronization aid that allows one or more threads to wait until a set of operations being performed in other threads completes.
A CountDownLatch is initialized with a given count. **The await methods block until the current count reaches zero due to invocations of the countDown() method, after which all waiting threads are released and any subsequent invocations of await return immediately**. This is a one-shot phenomenon -- the count cannot be reset. If you need a version that resets the count, consider using a CyclicBarrier.

A CountDownLatch is a versatile synchronization tool and can be used for a number of purposes. A CountDownLatch initialized with a count of one serves as a simple on/off latch, or gate: all threads invoking await wait at the gate until it is opened by a thread invoking countDown(). A CountDownLatch initialized to N can be used to make one thread wait until N threads have completed some action, or some action has been completed N times.

A useful property of a CountDownLatch is that it doesn't require that threads calling countDown wait for the count to reach zero before proceeding, it simply prevents any thread from proceeding past an await until all threads could pass.

Example:


```java
package multithreading;

import java.util.concurrent.CountDownLatch;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

class Process implements Runnable {
    private CountDownLatch latch;

    public Process(CountDownLatch latch) {
        this.latch = latch;
    }

    public void run() {
        System.out.println("Started.");

        try {
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        latch.countDown();
    }
    
}

public class CountDownLatchExample {
    public static void main(String[] args) {
        CountDownLatch latch = new CountDownLatch(3);
        ExecutorService executor = Executors.newFixedThreadPool(3);
        for (int i = 0; i < 3; i++) {
            executor.submit(new Process(latch));
        }
        try {
            latch.await();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Completed");
        executor.shutdown();
    }
}

```

Result:

```java
Started.
Started.
Started.
Completed
```

It will sleep 3 seconds, then countDown, then completed is printed.


###Producer and Consumer
---

The below example use java BlockingQueue libary.

```java
package multithreading;

import java.util.Random;
import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.BlockingQueue;

public class ProducerAndConsumer {
    private BlockingQueue<Integer> queue = new ArrayBlockingQueue<>(10);

    private void producer() throws InterruptedException {
        Random random = new Random();
        while (true) {
            //put will wait until queue is not full
            queue.put(random.nextInt(100));
        }
    }

    private void consumer() throws InterruptedException {
        Random random = new Random();
        while (true) {
            Thread.sleep(100);
            if (random.nextInt(10) == 0) {
                //take will wait until queue is not empty.
                Integer value = queue.take();
                System.out.println("Taken value: " + value + ", queue size is: " + queue.size());
            }
        }
    }
    
    public static void main(String[] args) {
        ProducerAndConsumer p = new ProducerAndConsumer();
        Thread t1 = new Thread(new Runnable() {
            @Override
            public void run() {
                try {
                    p.producer();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            
        });

        Thread t2 = new Thread(new Runnable() {
            @Override
            public void run() {
                try {
                    p.consumer();
                } catch (InterruptedException e) {
                    e.printStackTrace();
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
    }
}

```

















