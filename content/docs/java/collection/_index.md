---
 title: '集合'
---

### 常用集合类
- ArrayList、LinkedList、HashSet、HashMap、TreeMap
 
### 常用集合类的内存结构
- ArrayList：基于数据实现，便于随机读取，可动态扩容（System.arraycopy）
- LinkedList：基于链表实现，便于增加、删除元素
- HashMap：基于数据+链表+红黑树实现，当链表元素大于8个时转换为红黑树
- TreeMap：基于红黑树实现

    **红黑树**

    1、红黑树是一种近似平衡的二叉查找树，满足以下条件:
    - 每个节点要么是黑色，要么是红色
    - 根节点必须是黑色
    - 红色节点不能连续（红色节点的父亲和孩子都不能是红色）
    - 对于每个节点，从根节点到null（树尾端）的任何路径，都包括相同个数的黑色节点

### 集合类的继承关系
- ArrayList、LinkedList实现Collection接口，继承AbstractList类，ArrayList实现RandomAccess接口
- HashMap实现Map接口，继承AbstractMap类
- HashTable继承Dictionary类，实现Map接口

### 线程安全的集合类，如何做到线程安全（内存结构是如何的）
- HashTable：get、put方法上添加synchronized关键字实现，不推荐使用
- Collections.synchronizeXXX，get、put方法都通过synchronized关键字共享变量mutex加锁，效率不高
- ConcurrentHashMap：JDK1.7采用分段锁，对Segment加锁，默认分16段，JDK1.8采用Node数组保存元素，默认Node数组大小16，对Node数组中的元素加锁，采用synchronized和CAS实现，put时，hash值相同，放到Node数组元素的next里，get方法不加锁

### 集合类的常用遍历算法
- List：for-each、for循环、while循环
- Map：Map.EntrySet，用iterator遍历，推荐使用

### 并发包中常用的集合类
- ReenTrantLock：实现锁，使用时需要手动解锁
- CountDownLatch：实现计数器功能，子线程实行countdown后，可继续执行后续操作，父线程等待所有子线程处理完成后再执行
- CyclicBarrier：栅栏，子线程执行await后，需等待，等所有线程都执行await后，统一继续执行；可循环使用
- Semaphore：，控制每次访问次数，一个执行完，另一个即可补位