---
title: Java学习笔记2
date: 2019-02-08 8:35:42
tags: Java
categories: Java
---
# 项目（秒杀系统）
<!-- more -->
* 集合(collection)：
    数组的长度是固定的，集合的长度是可变的。
    每一个容器的数据结构不一样  
    Collection接口定义着集合框架中最最共性的内容  
    size(); add(); remove(); clear(); contains(); toArray();  
    集合的遍历：
    在根接口中使用了一种公共的遍历方式，迭代器遍历
    1. 获取一个集合的迭代器对象(迭代器对象不是我们创建的，而是每个集合自带的) 是一个接口
    ```
    Iterator<String> it = names.iterator();
    while(it.hasnext()){
        String s = it.next();
        System.out.println(s);
    }
    ```
    java规定，如果一个集合使用迭代器遍历，那么遍历的过程中，不允许修改集合长度
    2. 增强for循环
    Collection<String> names = new ArrayList<String>();
    for(数据类型 变量名：数组/集合){
        syso(变量名);
    }
    使用增强for循环遍历集合的时候，不能修改集合的长度
    3. 泛型:E实际上是一个“变量”  用来保存一种数据类型
        <E>,<K,V>
        可以用在类，方法，接口上。
        泛型通配符
        ？：代表任意类型
    4. Collections.shuffle(cards); //洗牌
    5. 栈，队列
       数组结构  Arraylist   Vector   查询快，增删慢
       链表结构：一般使用双向链表   
       哈希表结构：查询快 增删快
    6. List接口特点：有下标，有序的，可重复
    实现类：ArrayList,LinkedList,Vector 安全
    List结构中的方法：
    增：add(E e);  add(int index,E e)
    删：remove(Object obj);remove(int index);
    改：set(int index,E e);
    查：get(int index);
    其他：
        size();clear(),contains(Object obj),toArray();
        iterator();isEmpty();
    1.ArrayList:方法基本和List一致  
    
    2.LinkedList:还有大量的首尾操作方法
    void addFirst(E e);
    E removeFirst();
    E getFirst();
    E pop();  和removeFirst一致
    void push(E e);   推入  和addFirst一致
    7. Set接口
       a.无下标
       b.无序的
       c.不可重复
       实现类：
       HashSet：底层采用哈希表结构，查询快，增删快，无序的
       LinkedHashSet:链表＋哈希表，查询快，增删快，有序
       Set接口中的特有方法和Collection基本一致
       TreeSet:红黑树
    8. 哈希表
    哈希值：每一个对象都具有哈希值
    地址值实际是哈希值的16进制
    String对象的哈希值：重写了Object类中的hashCode
    不再通过地址值计算 只和字符串内容相关
    哈希表结构，添加元素判断是否重复
    1.先判断新旧元素的哈希值
    2.再判断新旧元素的equals
    自定义类，要使用HashSet存储
    保证元素唯一性：
        必须重写自定义类的两个方法  hashcode   equals
    定义一个标准得类：
    1.封装
    2.构造
    3.toString
    4.hashCode equals
    contains方法：
    ArrayList:names.contains("abc");
    HashSet:set.contains("abc");
    9. Map接口
    Map<K,V>集合常用方法： 、
    HashMap
    增：put(K key,V value);  //向集合中添加键值对
    //如果集合中已存在该键，覆盖整个键值对，并返回被覆盖的键值对的值
    判断k是不是空
       哈希表结构，添加元素判断是否重复
    1.先判断新旧元素的哈希值
    2.再判断新旧元素的equals
    删：v remove(object key);  //返回被删除的键值对的值
    改：==put
    查：V get(K key);  判断是不是空
    Map集合遍历：   LinkedHashMap   HashMap
    getKey();
    getValue();
    1.keySet遍历
    Set<Student> keys = students.keySet();  //放在set集合中
    map.KeySet(); Iterator  hasnext  
    for(String key : keys)
    {
        String value = students.get(key);
    }
    2.
    Set<Map.Entry<String String>> entrySet = map.entrySet();
    Iterator<Map.Entry<String,String>> it = entrySet.iterator();
    while(it.hasNext(){
        Map.Entry<String, String> entry = it.next();
        String key = entry.getKey();
        String value = entry.getValue();
        system.out.println(key+"="+value)；
    })
    ```
import java.util.HashMap;
import java.util.Iterator;
import java.util.Map;
import java.util.Map.Entry;
import java.util.Set;
  
public class MapTest {
    public static void main(String[] args) {
        Map<Integer, String> map = new HashMap<>();
        //map集合存入数据
        map.put(1, "第一个value");
        map.put(2, "第二个value");
        map.put(3, "第三个value");
         
        //通过keySet取出map数据[for-each循环]
        System.out.println("-------[for-each循环遍历]通过keySet取出map数据-------");
        Set<Integer> keys = map.keySet();  //此行可省略，直接将map.keySet()写在for-each循环的条件中
        for(Integer key:keys){
            System.out.println("key值："+key+" value值："+map.get(key));
        }
         
        //通过EntrySet取出map数据[for-each循环]
        System.out.println("-------[for-each循环遍历]通过EntrySet取出map数据-------");
        Set<Entry<Integer, String>> entrys = map.entrySet(); //此行可省略，直接将map.entrySet()写在for-each循环的条件中
        for(Entry<Integer, String> entry:entrys){
            System.out.println("key值："+entry.getKey()+" value值："+entry.getValue());
        }
         
        //通过keySet取出map数据[Iterator遍历]
        System.out.println("-------[Iterator循环遍历]通过keySet取出map数据---------");
        Iterator<Integer> it = map.keySet().iterator(); //map.keySet()得到的是set集合，可以使用迭代器遍历
        while(it.hasNext()){
            Integer key = it.next();
            System.out.println("key值："+key+" value值："+map.get(key));
        }
         
        //通过EntrySet取出map数据[Iterator遍历]
        System.out.println("-------[Iterator循环遍历]通过EntrySet取出map数据---------");          
        Iterator<Entry<Integer, String>> iterator = map.entrySet().iterator(); //map.entrySet()得到的是set集合，可以使用迭代器遍历
        while(iterator.hasNext()){
            Entry<Integer, String> entry = iterator.next();
            System.out.println("key值："+entry.getKey()+" value值："+entry.getValue());
        }
    }   
}
```
    内部类：
    OutClass.InterClass ic = new OutClass.new InterClass();
    内部接口    实现谁，重写谁
    如果Map中的键是自定义类型，那么要保证键的唯一性，必须重写键对应类的hashCode和equals方法
    3.Properties类
    本质就是一个Map集合
    持久的属性集  
    ps.store(new FileWriter("phones.properties"),"");//存
    ps.load(new FileReader("phones.properties)); //读取
    没有泛型
    具有Map接口的一切方法，以及自己特有的
    getProperty();
    setProperty();
    public Set<String> stringPropertyNames();//和KeySet一样
    Properties ps = new Properties();
    可变参数：
    public static int add(int...a){
        return 0;
    }
    //类型不能改变，多个参数时，可变参数在最后面
    本质：数组  for(int i : a)
    Collections：(集合工具类)中的静态方法：
    public static void shuffle(List list);//打乱顺序
    public static void sort(List list);//把集合元素按照自然顺序排序
    Arrays:数组工具类
    public static List asList(数组/可变参数); //把数组转化为List集合
    Arrays.sort(nums);
    Arrays.toString(nums);
    Map集合的嵌套：

* File类
    1. File类可以表示文件  也可以表示文件夹
    构造：
        1.public File(String filepath);
        绝对路径：以盘符开头的路径
        相对路径：相对当前项目的根目录
        2.public File(String parent ,String child);
        3.public File(File parent,String child);
    2. File对象的获取方法
    public String getAbsolutePath();//获取绝对路径
    getName();  getPath();
    public long length(); //获取File对象(文件)的字节数  不能计算文件夹
    3. File对象的删除和创建方法：
    1.创建方法
        创建文件：
            public boolean creatNewFile(); //创建新的文件
        创建文件夹
            public boolean mkdir();
    2.判断方法
        判断是否是文件
            public boolean isFile();
        判断是否是文件夹
            public boolean isDirectory();
        判断是否存在
            public boolean exists();
    3.删除
            public boolean delete();
    4.File类下的list和listFiles方法(文件夹)
        1.public String[] list();
        2.public File[] listFiles();
        只能列出当前文件下的一级子文件或者子文件夹
        扩展：删除先删文件再删文件夹
    5.递归打印目录下的所有文件
    6.文件过滤器：FileFilter
    在list和listFiles方法中使用

    

        