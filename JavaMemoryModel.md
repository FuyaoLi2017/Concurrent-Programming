#JMM
- 线程什么时候能看到变量

### Thread
- 2个线程访问一个heap对象不同的对象，2个线程拥有该成员变量的私有拷贝
### 内存

- CPU(REGISTER) -> CPU memory cache -> RAM - Main memory
- stack可能在3个里面
- heap可能在后面2个里面

### 同步的八种操作
- lock: 作用于主内存的变量， 把一个变量标识为线程独占
- unlock：把锁定状态的变量释放
- read: 主内存 ->工作缓存
- load:从主内存的变量值放到工作内存的变量副本
- use: 工作内存的变量值传递给执行引擎
- assign: 作用于工作内存，把一个从执行引擎接收到的值赋值给工作内存的变量
- store: 把工作内存的值传送到主内存，以便write
- write: 作用于主内存，把store操作从工作内存中一个变量的值传到主内存的变量中
### 同步操作与规则
lock     read              load               use
**主内存 ------> Save/load -----> 多个工作内存 ------> 多个Java Thread**
unlock   write<-          store<-           assign<-    
- 一个变量在同一个时间只能有一个线程进行lock操作
- lock时候，清空工作内存中变量值，需要重新使用时候要重新load, assign
- unlock前必须同步回主内存

### 特殊规则
final修饰的值无法修改
