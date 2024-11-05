> 关于HW

分开Order和OrderItem。
如果使用REQUIRES NEW，看不到没落盘的Order，会失败。
但是Order可以成功过。
再次下，能看到，就会成功。

所以必须在一个事务里写进去。


# Memory Consistency Errors

Java 的多线程编程是通过**`Thread`** 类或 **`Runnable`** 接口来实现的。Java 提供了许多强大的工具和库来简化多线程编程，帮助你充分利用现代多核处理器的性能。

### 1. **创建线程的方式**

在 Java 中，有几种创建和管理线程的方式：

#### (1) 继承 `Thread` 类

你可以通过继承 `Thread` 类，并重写 `run` 方法来定义线程的行为。

java

复制代码

`class MyThread extends Thread {     public void run() {         // 线程要执行的代码         System.out.println("Thread is running...");     } }  public class Main {     public static void main(String[] args) {         MyThread t1 = new MyThread();         t1.start(); // 启动线程     } }`

`start()` 方法启动线程，执行 `run()` 中的代码。

#### (2) 实现 `Runnable` 接口

推荐的方式是实现 `Runnable` 接口，然后将 `Runnable` 对象传递给 `Thread` 的构造函数。

java

复制代码

`class MyRunnable implements Runnable {     public void run() {         System.out.println("Thread is running...");     } }  public class Main {     public static void main(String[] args) {         MyRunnable runnable = new MyRunnable();         Thread thread = new Thread(runnable);         thread.start();     } }`

相比继承 `Thread` 类，`Runnable` 的好处是你可以继承其他类，并且不需要单独创建新类。

#### (3) 使用 `Callable` 和 `Future`

`Callable` 是 `Runnable` 的增强版，它可以返回结果，并且可以抛出异常。结合 `Future`，可以获取线程的结果。

java

复制代码

`import java.util.concurrent.Callable; import java.util.concurrent.ExecutionException; import java.util.concurrent.FutureTask;  class MyCallable implements Callable<Integer> {     public Integer call() throws Exception {         return 123;     } }  public class Main {     public static void main(String[] args) throws ExecutionException, InterruptedException {         MyCallable callable = new MyCallable();         FutureTask<Integer> futureTask = new FutureTask<>(callable);         Thread thread = new Thread(futureTask);         thread.start();          // 等待线程完成并获取结果         Integer result = futureTask.get();         System.out.println("Result: " + result);     } }`

### 2. **线程同步**

在多线程编程中，数据的共享和同步非常重要。Java 提供了几种机制来确保线程安全。

#### (1) `synchronized` 关键字

`Synchronized` 用于锁定方法或代码块，确保同一时间只有一个线程可以访问同步代码块。

java

复制代码

`class Counter {     private int count = 0;      // 同步方法     public synchronized void increment() {         count++;     }      public int getCount() {         return count;     } }  public class Main {     public static void main(String[] args) throws InterruptedException {         Counter counter = new Counter();          Thread t1 = new Thread(() -> {             for (int i = 0; i < 1000; i++) {                 counter.increment();             }         });          Thread t2 = new Thread(() -> {             for (int i = 0; i < 1000; i++) {                 counter.increment();             }         });          t1.start();         t2.start();          t1.join();         t2.join();          System.out.println("Final count: " + counter.getCount());     } }`

#### (2) `ReentrantLock`

`ReentrantLock` 是一个比 `synchronized` 更灵活的同步机制，可以显式地获取和释放锁。

java

复制代码

`import java.util.concurrent.locks.Lock; import java.util.concurrent.locks.ReentrantLock;  class Counter {     private int count = 0;     private Lock lock = new ReentrantLock();      public void increment() {         lock.lock(); // 获取锁         try {             count++;         } finally {             lock.unlock(); // 确保最终释放锁         }     }      public int getCount() {         return count;     } }`

### 3. **线程池**

Java 提供了 `ExecutorService` 来简化线程管理。你可以通过线程池有效管理线程的创建和销毁，避免频繁创建新线程带来的开销。

java

复制代码

`import java.util.concurrent.ExecutorService; import java.util.concurrent.Executors;  public class Main {     public static void main(String[] args) {         ExecutorService executor = Executors.newFixedThreadPool(5); // 创建一个有 5 个线程的线程池          for (int i = 0; i < 10; i++) {             executor.submit(() -> {                 System.out.println(Thread.currentThread().getName() + " is running");             });         }          executor.shutdown(); // 关闭线程池     } }`

线程池有多种类型，如 `CachedThreadPool`、`ScheduledThreadPool`、`SingleThreadExecutor` 等，可以根据不同需求选择。

### 4. **线程间通信**

线程间的协调可以使用 **`wait()`**、**`notify()`** 和 **`notifyAll()`** 等方法，它们通常和 `synchronized` 关键字一起使用，来控制线程的等待和唤醒。

java

复制代码

`class SharedResource {     private boolean available = false;      public synchronized void produce() throws InterruptedException {         while (available) {             wait(); // 等待资源被消费         }         System.out.println("Producing...");         available = true;         notify(); // 通知消费者     }      public synchronized void consume() throws InterruptedException {         while (!available) {             wait(); // 等待资源被生产         }         System.out.println("Consuming...");         available = false;         notify(); // 通知生产者     } }  public class Main {     public static void main(String[] args) {         SharedResource resource = new SharedResource();          Thread producer = new Thread(() -> {             try {                 resource.produce();             } catch (InterruptedException e) {                 Thread.currentThread().interrupt();             }         });          Thread consumer = new Thread(() -> {             try {                 resource.consume();             } catch (InterruptedException e) {                 Thread.currentThread().interrupt();             }         });          producer.start();         consumer.start();     } }`

### 总结

Java 的多线程编程提供了各种机制来创建和管理线程，并提供了工具来解决同步和通信问题。无论你是创建简单的线程，还是使用线程池或锁，Java 的多线程编程模型都很强大，并且相对易于理解。


### **Key Takeaways:**

1. **Synchronized Instance Methods**: The lock is on the **object instance**, and only one thread can execute synchronized methods on the same object instance at a time.
    
2. **Synchronized Static Methods**: The lock is on the **Class object** of the class, not on any individual instance. This prevents concurrent access to static fields and methods of the class, regardless of the number of instances.
