---
title: Java学习笔记2
date: 2019-02-11 10:35:11
tags: Java
categories: Java
---
## io 多线程  网络编程  XML
<!-- more -->
* IO流
    1.字符流,字节流
    字符输入流：共同的父类Reader  比如FileReader,BufferedReader
        功能：读取一个字符，读取一个字符数组(一部分)，读取一个字符串
    字符输出流：共同的父类Writer  比如FileWriter,BufferedWriter
        功能：写一个字符，写一个字符数组(一部分)，写一个字符串
    字节输入流：共同父类 InputStream  比如：FileInputStream,BufferInputStream    读取一个字节   读取一个字节数组
    字节输出流：共同父类 OutputStream  比如：FileOutputStream,BufferOutputStream    写一个字节   写一个字节数组
    2.OutputStream:字节输出流的根类，这是一个抽象类
    public void close();
    public void flush(); //刷新流
    public void write(int b); //写一个字节
    public void write(byte[] bs); //写一个字节数组
    public void writre(byte[] bs,int startIndex, int lenght);//写一个字节数组的一部分
    3.续写和换行
    FileOutputStream fos = new FileOutputStream("2.txt",true);
    fos.write("\r\nhello".getBytes());
    fos.close();
    4.InputStream:字节输入流的根类，这是一个抽象类
    1.public int read();、、读取一个字节，返回是码值
    2.public int read(byte[] bs);//读取一个字节数组，返回值表示实际读取到的字节数
    我们用InputStream具体子类：FileInputStream
    一次读取一个字节
    FileIntputStream fis = new FileIntputStream(new File("1.txt"));
    int b = 0;
    while(b=fis.read()!=-1)
    {
        System.out.println((char)b);
    }
    fis.close();
    一次读取一个字节数组
    byte[] bs = new byte[4];
    int len = fis.read(bs);
    System.out.println(len); //实际字节数
    System.out.println(new String(bs));  
    标准：
    while((len = fis.read(bs)!=-1))
    {
        System.out.println(new String(bs,0,len))
    }
    复制文件：
    long s= System.currentTimeMillis(); //系统时间
    while((len = fis.read(bs)!=-1))
    {
        fos.writ(bs,0,len);
    }
    字节缓冲流：
    BufferedOutputStream bos = new BufferedOutputStream(new FileOutputaStream("1.txt"));
    字节流读取中文的乱码问题：读取中文读了一半
    解决问题：字符流  转化流
    字符编码表(字符集)
    ASCII码表
    在GBK码表中一个中文2个字节 在UTF-8中一个中文 3个字节
    OutputStreamWriter  是字符流通向字节流的桥梁，查码表(编码)
    OutputStreamWriter osw = new OutputStreamWriter(new FileOutputStream("1.txt"));
    osw.close();
    字节->解码->字符： InputStreamReader
    字符->编码->字节： OutputStreamWriter
    transient关键字：
    用来修饰成员变量 用不用没有影响
    序列化的时候有用，如果一个成员变量被transient修饰，那么序列化的时候会忽略该成员变量
    static:关键字 他也具有和transient一样的功能
    打印流：
    PrintWriter:打印字符流
    PrintyStream:打印字节流

    使用第三方框架的步骤
    1.导入classpath
    a.在工程根目录下 建立一个目录"lib"
    b.把要使用的第三方框架的jar包拷贝过来
    c.添加构建路径 右键单击jar包---->Build Path ----> Add to Build Path
    以FileUtils为例

* 多线程
    1. 内存RAM  硬盘ROM
    多线程程序并不能提高程序的运行速度，但能够提高程序运行速率，让cpu的使用率更高。
    main方法所在线程  我们就称为主线程
    Thread类：线程类
    public Thread();//创建一个默认名字的线程对象
    public Thread(String name);//创建一个指定名字的线程对象
    第一种：继承
    class 子线程类 extends Thread{
        run(){
            任务代码
        }
    }
    子线程类 t = new 子线程类();
    t.start();
    第二种：声明实现Runable接口的类，重写run方法，创建实现类对象，创建Thread对象，并把刚刚的实现类对象 作为参数传递，启动这个Thread对象
    从耦合性分析用第二种
    扩展性:第一种继承Thread，那么子线程类就不能继承别的类
    第二种方式  由于是实现了接口，同时可以继承别的类
    匿名内部类创建线程对象
    1. new Thread(){
        public void run(){
            /////////
        }
    }.start();
    2. new Thread(new Runnable(){
        public void run(){
            /////
        }
    }).start();
    线程安全问题：1.同步锁  synchronized(obj)
    2.同步方法:
    public synchronized void sale()
    {
    }
    这里同步方法使用的锁对象  叫做this对象
    这里同步方法是静态方法，那么他的锁对象是当前类.class
    3.lock接口方式
    实现类：ReentrantLock

* 网络编程  udp  tcp
    InetAddress

* XML语法
    文档说明：
    <?xml version="1.0 encoding="TTF-8"?>
    作用：存放数据  配置文件
    CDATA区 <![CDATA[]]>



