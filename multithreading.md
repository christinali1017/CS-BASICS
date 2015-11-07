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

###Thread states
---

- New  Thread t = new Thread()
- Runnable   t.start()
- Running   the thread is actually executeing the code.
- Sleep / waiting / blocked 









