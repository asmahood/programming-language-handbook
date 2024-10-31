# Threading

## Implementing Threading

The `Thread` class is part of the `java.lang` package and can be imported as normal. Note that all threads will run *concurrently*, not in parallel.

### Extending the `Thread` Class
The first way we can implement threading is by extending the `Thread` class and overriding the `run` method. These are the only two requirements. The `run` method performs the work that the thread is responsible for. To start the thread, create an instance of the class and call the `start` method. For example:
```java
public class HugeProblemSolver extends Thread{

  public HugeProblemSolver(){
    // Required constructor used for passing information to the start() method.
  }

  private static void solveComputation(){
    // Solves random computation
    // Takes anywhere from 1 second to 10 minutes
  }

  @Override
  public void run(){
    solveComputation();
System.out.println("The answer is: 42");
  }

  public static void main(String[] args){
    HugeProblemSolver m1 = new HugeProblemSolver();
    HugeProblemSolver m2 = new HugeProblemSolver();
    m1.start();
    m2.start();
  }
}
```

### Implementing the Runnable Interface
You can also create threaded classes by implementing the `Runnable` interface. This approach is prefereed becasue we are only allowed toe xtend one class, and wasiting it on `Thread` might not be beneficial. Thus implementing `Runnable` and passing in the object into a new `Thread` object is the preferred way of implementing multithreading. For example:
```java
public class Factorial implements Runnable {
 private int n;
 
 public Factorial(int n) {
   this.n = n;
 }
 
 public int compute(int n) {
   // ... the code to compute factorials
 }
 
 public void run() {
   System.out.print("Factorial of " + String.valueOf(this.n) + ":")
   System.out.println(this.compute(this.n));
 }
 
 public static void main(String[] args) {
   Factorial f = new Factorial(25);
   Factorial g = new Factorial(10);
   Thread t1 = new Thread(f);
   Thread t2 = new Thread(f);
   t1.start();
   t2.start();
 }
}
```
A more succint way of using the `Runnable` interface is to use `lambda` expressions:
```java
public class Factorial {
 public int compute(int n) {
   // ... the code to compute factorials
 }
 
 public static void main(String[] args) {
   Factorial f = new Factorial();
 
   // the lambda function replacing the run method
   new Thread(() -> {
     System.out.println(f.compute(25));
   }).start();
 
   // the lambda function replacing the run method
   new Thread(() -> {
     System.out.println(f.compute(10));
   }).start();
 }
}
```

## Supervising a Thread
To see the status of threads during their execution, use a **supervisor thread**. This is a pattern where the main thread (or another thread) is able to watch and check on th epgrogess of another thread, as lonmg as it has access to the corresponding `Thread` instance. Supervisor threads are oftne used for updating the user of our program on the progress of an ongoing task.

One `Thread` method that a supervisor thread may use to monitor another thread is the `isAlive` method. This method returns `true` if the thread is still running, and `false ` if it has terminated. A supervisor might continously poll this value until it changes, and then notify the user that the thread has changed state. For example:
```java
import java.time.Instant;
import java.time.Duration;
 
public class Factorial{
 public int compute(int n){
   // the existing method to compute factorials
 }
 
 // utility method to create a supervisor thread
 public static Thread createSupervisor(Thread t){
   Thread supervisor = new Thread(() -> {
     Instant startTime = Instant.now();
     // supervisor is polling for t's status
     while (t.isAlive()) {
       System.out.println(Thread.currentThread().getName() + " - Computation still running...");
       Thread.sleep(1000);
     }
   });
 
   // setting a custom name for the supervisor thread
   supervisor.setName("supervisor");
   return supervisor;
 
 }
 
 public static void main(String[] args){
   Factorial f = new Factorial();
 
   Thread t1 = new Thread(() -> {
     System.out.println("25 factorial is...");
     System.out.println(f.compute(25));
   });
 
 
   Thread supervisor = createSupervisor(t1);
 
   t1.start();
   supervisor.start();
 
   System.out.println("Supervisor " + supervisor.getName() + " watching worker " + t1.getName());
 }
}
```

Additionally, the `getName` method will return a unique name for a thread in the current context.  This is useful when debugging multithreaded programs. Threads can also be named using the `setName` method of the `Thread` class.

## Waiting for Thread Completion
The concept of waiting for a thread to complete is known as *"waiting for the thread to join"* in Java. When a thread join,s it means that the thread's task is complete and the process that was initally forked off ahs been "joined" back into the main thread. This is useful when we need to wait for prerequisite tasks to complete before starting another. To do this, we can use the `join` method to wait for a thread to complete before continuing with execution. For example:
```java
import java.lang.Thread;
public class BurgerMaker {
 
 public void toastBuns() {
   try {
     System.out.println("Toasting buns...");
     Thread.sleep(2000);
   } catch (InterruptedException e) {
     System.out.println(e);
   }
 }

 public void grillPatty() {
   System.out.println("Grilling patty...");
   Thread.sleep(1500);
 }

 public void meltCheese() {
   System.out.println("Melting cheese...");
   Thread.sleep(800);
 }

 public void fryOnions() {
   System.out.println("Frying onions...");
   Thread.sleep(1000);
 }

 public void assembleBurger() {
   System.out.println("Assembling burger...");
   Thread.sleep(1500);
 }

 public static void main(String[] args) {
   BurgerMaker burgerMaker = new BurgerMaker();
   Thread t1 = new Thread(() -> burgerMaker.toastBuns());
   Thread t2 = new Thread(() -> burgerMaker.grillPatty());
   Thread t3 = new Thread(() -> burgerMaker.meltCheese());
   Thread t4 = new Thread(() -> burgerMaker.fryOnions());
   Thread t5 = new Thread(() -> burgerMaker.assembleBurger());
 
   t1.start();
   t2.start();
   t4.start();
   t2.join(); // must grill patty before melting cheese on it
   t3.start(); // ready to melt cheese
   t1.join();
   t3.join();
   t4.join();
   // must complete all other steps before assembling burger
   t5.start();
   t5.join(); // waiting for the burger assembly task to complete
   System.out.println("Burger complete!");
 }
 
}
```

### Thread Synchronization
When accessing the same data from two different threads, we may cause a **race condition**. A race condition occurs when some inconsistency is caused by two threads tring to access the same shared data at the same time. We can prevent race conditions on shread data by using the `synchronized` keyword. In a threaded program, when we add `synchronized` to the definition of a function, it will ensure that for a given instance of a class, only one thread can run that method at a time. We can make a function synchronzied like so:
```java
public synchronized void incrementElement(int i, int j){
    array[i] += j;
}
```

### Communicating Between Threads
To control thread execution from within other threads, we can use the `wait`, `notify`, and `notifyAll` methods. These are primarily used to protect shared resoruces from being used by two threads at the same time or to wait until some condition has changed in a thread.

When using `wait` and `notifyAll`, it is important to do so in a `synchronized(this)` block. When we create a `synchronized(this)` block, we are telling Java that we want it to be the only thread accessing the fields of the class at a given moment. In the `synchronized(this)` we must:

1. Check the condition on which to wait
2. Decide whether to `wait` (block the execution of the current thread) or `notifyAll` (allow other threads to check their condition again and proceed)

For example:
```java
import java.lang.Thread;

public class OrderDinnerProcess {
 private boolean foodArrived = false;

 private void printTask(String task) {
   System.out.println(Thread.currentThread().getName() + " - " + task);
 }

 public void eatFood() {
   printTask("Wow, I am starving!");
   try {
     synchronized (this) {
       while (!this.foodArrived) {
         printTask("Waiting for the food to arrive...");
         wait();
       }
     }
   } catch (InterruptedException e) {
     System.out.println(e);
   }
   printTask("Finally! Yum yum yum!!!");
 }

 public void deliverFood() {
   printTask("Driving food over...");
   try {
     Thread.sleep(5000);
     synchronized (this) {
       this.foodArrived = true;
       printTask("Arrived!");
       notifyAll();
     }
   } catch (InterruptedException e) {
     System.out.println(e);
   }
 }

 public static void main(String[] args) {
   OrderDinnerProcess p = new OrderDinnerProcess();
   try {
     for (int i = 0; i < 5; i++) {
       Thread eatFood = new Thread(() -> p.eatFood());
       eatFood.start();
     }
     Thread.sleep(1000);
     Thread delivery = new Thread(() -> p.deliverFood());
     delivery.start();
   } catch (InterruptedException e) {
     System.out.println(e);
   }
 }
}
```

## Virtual Threading
To improve efficiency, virtual threads group several tasks and are executed on one platform thread instead of reserving one thread for each separate task. A task is mounted on a thread when it is ready to execute its function and is unmounted when it is awaiting an external response. When a task is unmounted the resources are released and allocated to another task that is ready to finish executing. With this mechanism, every task behaves as if it were its own thread (hence the **virtual thread**). The Java Virtual Machine handles thr grouping, mounting, and unmounting of the tasks on a platform thread.

To start a virtual thread:
```java
Thread.ofVirtual().start(Runnable someThread);
```
Since virtual threads belong to the `Thread` class, we can use `join` to block a parent thread from exiting until a child thread has completed executing as we would for a traditional platform thread. For example, the following code will run 10,000 threads:
```java
public class SoManyThreads { 
  public static void main(String[] args) { 
    int numberOfThreads = 10000; 
    for (int i = 0; i < numberOfThreads; i++) { 
      Thread thread = Thread.ofVirtual().start(new Runnable() { 
        @Override 
        public void run() { 
          System.out.println(Thread.currentThread().threadId() + " is running"); 
        } 
      }); 
    } 
  } 
} 
```
Since many threads run on one platform thread, `Thread.currentThread().threadId()` will print out the ID of the virtual thread's parent platform thread. The previous code created virtual threads and ran them immediately because of the call to `start`. To create virtual threads now and start them later:
```java
public class SoManyThreads { 
  public static void main(String[] args) { 
    int numberOfThreads = 10000; 
    for (int i = 0; i < numberOfThreads; i++) { 
      Thread thread = Thread.ofVirtual().unstarted(new Runnable() { 
        @Override 
        public void run() { 
          System.out.println(Thread.currentThread().threadId() + " is running"); 
        } 
      }); 
    } 
  } 
} 
```
We can start running all of the threads by calling the `start` method:
```java
thread.start();
```

### Using Structured Concurrency with Virtual Threads
Concurrency is implemented using the `ExecutorService` class. For example:
```java
public class ConcurrencyExample { 
  public static void main(String[] args) { 
    ExecutorService executorService = Executors.newFixedThreadPool(3); 
    // We can assume the fetch functions have the relevant information of a user. 
    Future<String> userName = executorService.submit(fetchUserName()); 
    Future<String> userID = executorService.submit(fetchUserID()); 
    Future<String> orderNumber = executorService.submit(fetchOrderNumber()); 
    executorService.shutdown(); 
    // Get results from the completed tasks 
    try { 
      String result1 = userName.get(); 
      String result2 = userID.get(); 
      String result3 = orderNumber.get(); 
    } catch (InterruptedException | ExecutionException e) { 
      e.printStackTrace(); 
    } 
  } 
} 
```
This is a form of unstructured concurrency. Fetching a user's username, ID, and order number can be independent operations. However, the followinbg problem exists: if, for some reason, the user does not have a registered `userName` (meaning they are not registered on the site), the tasks of `fetchID` and `fetchOrder` will continue to execute in search of information for a non-existent user thereby wasting time and other resources. This inherent problem of unstructured concurrency leads to code that is hard to maintain and debug. To fix this problem, it is preferable to use structured concurrency instead. Structured concurrency combines the benefits of a consecutive code (if one step fails, the whole code fails) with the time-saving benefits of running concurrent code.

Virtual threads are excellent candidates for running structured concurrency as they can run several tasks on one platform thread. Virtual threads are used for structured concurrency by using the following Java code: 
```java
Executors.newVirtualThreadPerTaskExecutor()
```
The previous code refactored to use structured concurrency via virtual threads:
```java
public class ConcurrencyExample{ 
  public static void main(String[] args) { 
    try (ExecutorService executorService = Executors.newVirtualThreadPerTaskExecutor()) { 
      // We can assume the fetch functions have the relevant information of a user 
      Future<String> userName = executorService.submit(fetchUserName()); 
      Future<String> userID = executorService.submit(fetchUserID()); 
      Future<String> orderNumber = executorService.submit(fetchOrderNumber()); 
    } 
  } 
} 
```

### Sharing Data using Scoped Values
While tasks are running, there may be a case where data between threads must be shared. In concurrent programming, the way to do this was to use a `ThreadLocal` variable. A `ThreadLocal` variable is a public static variable that belongs to the class, but a separate instance of which is created in each thread. The problem with a `ThreadLocal` variable used in virtual threads is that because virtual threads allow the creation of many threads, there will consequently be many instances of a `ThreadLocal` variable, rendering them to unmanageable due to their amount. To solve this problem, it is preferable to use a `ScopedValue` variable instead. A `ScopedValue` variable belongs to the class and does not allow the creation of multiple instances of itself.

To use a `ScopedValue` variable, syntax similar to the following should be added to any code using virtual threads:
```java
private static final ScopedValue<String> someString = ScopedValue.newInstance(); 
ScopedValue.where(someString, "StringValue", virtualThread);
```

### Advantages and Disadvantages of Virtual Threads
Virtual threads have proven to be helpful in applications where several tasks are slated to run concurrently, and each task awaits some form of external response, such as IO or a network call. However, there are situations in which a virtual thread cannot be used. In the case where a thread must run some form of complex calculation, it does not make sense to use a virtual thread because the task will not be idle as the CPU is under constant use. When this is the case, there is no other choice but to rely on a standard platform thread. A second scenario when a virtual thread can’t be used is when a task executes a `synchronized` block of code. A `synchronized` block of code prevents other threads from accessing a specific piece of data in the interest of protecting it from being incorrectly processed. When a virtual thread executes `synchronized` code, the virtual thread cannot be unmounted until the block of code is finished executing, even if the thread is idle. When this happens, we say the virtual thread is pinned to the parent platform thread. When this is the case, we lose the advantages we gain from unmounting an idle thread. In this case, we again are forced to use standard platform threads.

## Thread Pooling
A thread pool manages a pool of worker threads that connect to a work queue of `Runnable` tasks waiting to be executed. In a thread pool, added threads idle until given work. A Blocking Queue is used to manage this work. Idling threads will process enqueued tasks on a first come first serve basis. Once a thread finishes its task, it simply returns to watching the queue.

### The Executor Framework
The `Executor` framework implements thread pooling through an `Executor` interface. The `Executor` interfaces include:
- `Executor`: launch a `Runnable` object task
- `ExecutorService`: manages the lifecycle of tasks in a sub-interface of `Executor`
- `ScheduledExecutor`: schedules the execution of tasks in a sub-interface of `ExecutorService`.

To use the `Executor` framework, we will need the following imports:
```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
```
To use an `Executor`, we need to create an `ExecutorService` object and pass it the number of threads we'll be alloting it:
```java
private static final int N = 10;
ExecutorService executor = Executors.newFixedThreadPool(N);
```
To pass tasks to the executor:
```java
Runnable task = new RunnableTask(); // RunnableTask is a custom class that implements Runnable
executor.execute(task);
```
To prevent new tasks from being added, call the `shutdown` method:
```java
executor.shutdown();
```
To wait for the thread pool to finish all of its tasks:
```java
executor.awaitTermination(time, timeUnit);
```
The `awaitTermination` will wait for an allotted amount of maximum time for the tasks to finish. If they do not finish before the time passes, an `InterruptedExecption` will be thrown
