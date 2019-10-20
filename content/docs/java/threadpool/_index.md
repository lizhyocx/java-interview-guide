---
 title: '线程池'
---

### 如何创建线程
- 继承Thread类
- 实现Runnable接口
- 实现Callable接口
- 使用线程池

### Java常用线程池及适用场景
- 使用ThreadPoolExecutor类创建线程池，Executors提供的方法不建议使用，其实质也是实例化的ThreadPoolExecutor类，只是传递的参数不同

### 线程池的参数影响
- corePoolSize：核心线程数，初始化时为0，执行任务时，在corePoolSise大小的范围内，新建线程，执行任务
- maxPoolSize，最大线程数，配合队列参数使用，当超过核心线程数，且队列也满了，此时才会创建新的线程
- keepAliveTime，空闲时间，当线程大于核心线程数，且空闲达到空闲时间时，会销毁线程，如果小于核心线程数，不会销毁线程
- queue，阻塞队列，当线程大于等于核心线程数时，新增任务时，会将任务放到队列中等待执行。一般情况下，一定要给阻塞队列指定大小，否则任务堆积造成内存溢出。常用的阻塞队列有：

    - ArrayBlockingQueue：有界队列
    - LinkedBlockingQueue：无界队列
    - SynchronousQueue：一般生产者消费者场景，队列只保存一个任务。是一个双栈双队列算法，无空间的队列或栈，任何一个对SynchronousQueue写需要等到一个对SynchronousQueue的读操作，反之亦然。一个读操作需要等待一个写操作，相当于是交换通道，提供者和消费者是需要组队完成工作，缺少一个将会阻塞线程，知道等到配对为止。
- rejectHandler，拒绝策略，当线程达到最大线程数，且队列也满了，此时还有新的任务提交，此时会触发拒绝策略。默认提供4种拒绝策略：

    - AbortPolicy：终止当前提交的任务，并抛出异常
    - DiscardOldestPolicy：丢弃最早提交的任务
    - DiscardPolicy：丢弃当前提交的任务
    - CallerRunsPolicy：由调用者线程进行执行（线程池的父线程）

    **阻塞队列**

    常用的方法：
    
    - put：放元素，没有空间时，阻塞等待
    - take：取元素，没有数据时，阻塞等待

    - add：放元素，没有空间时，抛出异常
    - offer：放元素，没有空间时，等待超时后返回false
    - poll：取元素，没有数据时，等待超时后返回null


