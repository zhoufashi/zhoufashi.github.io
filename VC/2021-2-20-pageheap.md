# 使用PageHeap.EXE或GFlags.EXE检查内存越界错误


## PageHeap的使用中有几点值得注意：

1:启用PageHeap不能够影响正在运行中的应用程序。如果你需要启用一些正在运行且不能重启的程序的PageHeap，那请运行PageHeap启用后，重新启动机器。

2:要想查看PageHeap把信息放到哪里了，请打开你的注册表，来到

   /HKEY_LOCAL_MACHINE/SOFTWARE/Microsoft/Windows NT
       
/CurrentVersion/Image File Execution Options

你将会看到你的应用程序也在这个项下面。你的应用程序的GlobalFlag被设置为了0x02000000，PageHeapFlags被设置为了0x01。

3：PageHeap的原理是这样，它在已分配的内存的后面放上几个守护字节（Guard Bytes），再跟上一个标记为PAGE_NOACCESS的内存页。这样，已分配内存的后面如果被重写了，那么守护字节就会被改变，于是当内存被释放时，PageHeap就会引发一个AV(Access Violation)。大体上就是这样。所以只有最后释放这块问题内存时，才会有PageHeap的报告！这就是PageHeap的局限性吧。

启用pageheap很容易检查操作delete后的内存的错误（包括2次delete）

## 使用：
1，把pageheap.exe放到需要监控的程序目录下
2，以系统管理员身份执行cmd，cd到pageheap.exe目录
3，PageHeap /enable YourApplicationName.exe 0x01。
4，执行“pageheap”语句来查看是否将YourApplicationName.exe加到了pageheap的列表中
5，运行结束后，执行“pageheap /disable XX.exe”来终止监控。

0x01 flags，通过 PageHeap /?  查看 

参数0x01的含义：

FLAGS hex value (0x...) has the following structure:

    B7-B0   Bit flags    1 - enable page heap

   01 - enable page heap. If zero normal heap is used. In 99% of the cases you will want this to be set.
   02 - collect stack traces (default on checked builds)
   04 - minimize memory impact
   08 - minimize randomly(1)/based on size range(0)
   10 - catch backward overruns

可以设置参数为0x10，从而可以检查内存向前的越界写！  
[返回2](../) 