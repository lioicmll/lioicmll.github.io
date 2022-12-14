### 线程日志 
``` shell
/data/jdk/bin/jstack -l 8870 >jvm_list.txt
```

### 堆内存信息 
```shell
/data/jdk/bin/jmap -F -dump:live,format=b,file=/home/tomcat/heap001 8870 
```
### JAVA程序内存/Cpu 过高问题排插流程

```shell
# 查看此进程中的线程
ps p 5664  -L -o pcpu,pmem,pid,tid,time,tname,cmd
# 将最高的TID转换成16进制 
printf "%x\n" tid 
# jstack查询 
jstack -l 5664 | grep 16进制tid -A 30
```
### Java堆和栈的区别
栈与堆都是Java用来在Ram中存放数据的地方.
与C++不同，Java自动管理栈和堆，程序员不 能直接地设置栈或堆。 

Java的堆是一个运行时数据区,类的对象从中分配空间。这些对象通过new、newarray、 anewarray和 multianewarray等指令建立，它们不需要程序代码来显式的释放。堆是由垃圾 回收来负责的，堆的优势是可以动态地分配内存大小，生存期也不必事先告诉编译器，因为 它是在运行时动态分配内存的，Java的垃圾收集器会自动收走这些不再使用的数据。但缺点 是，由于要在运行时动态分配内存，存取速度较慢。 

栈的优势是，存取速度比堆要快，仅次于寄存器，栈数据可以共享。但缺点是，存在栈中的 数据大小与生存期必须是确定的，缺乏灵活性。

栈中主要存放一些基本类型的变量（,int, short, long, byte, float, double, boolean, char）和对象句柄。
栈有一个很重要的特殊性，就是存在栈中的数据可以共享。假设我们同时定义： int a = 3; int b = 3； 编译器先处理int a = 3；首先它会在栈中创建一个变量为a的引用，然后查找栈中是否有3 这个值，如果没找到，就将3存放进来，然后将a指向3。接着处理int b = 3；在创建完b的 引用变量后，因为在栈中已经有3这个值，便将b直接指向3。这样，就出现了a与b同时均指 向3的情况。
这时，如果再令a=4；那么编译器会重新搜索栈中是否有4值，如果没有，则将4存放进来， 并令a指向4；如果已经有了，则直接将a指向这个地址。因此a值的改变不会影响到b的值。 要注意这种数据的共享与两个对象的引用同时指向一个对象的这种共享是不同的，因为这种 情况a的修改并不会影响到b, 它是由编译器完成的，它有利于节省空间。而一个对象引用变 量修改了这个对象的内部状态，会影响到另一个对象引用变量。

## jcmd

```shll
# 查看帮助
./jdk1.8.0_73/bin/jcmd 1 help

#获取堆信息, 与jmap效果一样
./jdk1.8.0_73/bin/jcmd 1 GC.heap_dump /usr/local/service-singularity/logs/heap_dump
```

