---
title: 剑指offer(2)
date: 2020-01-22 21:35:42
tags: 算法
categories: 算法
---
---------
* 请实现一个函数，将一个字符串中的每个空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。  
---------
<!-- more -->
```
public class Solution {
    public String replaceSpace(StringBuffer str) {
    	String str1 = str.toString();
        if(str1.equals(""))
        {
            return(str1);
        }
        char [] strArray = str1.toCharArray();
        int lengthSpace = 0;
        for(int i = 0;i<strArray.length;i++)
        {
            if(strArray[i]==' ')
            {
                lengthSpace++;
            }
        }
        int newStrLength = strArray.length + lengthSpace*2;
        char [] newstrArray = new char[newStrLength];
        int count = 0;
        for(int i = 0;i<strArray.length;i++)
        {
            if(strArray[i]!=' ')
            {
                newstrArray[i+count*2] = strArray[i];
            }
            else{
                newstrArray[i+2*count]='%';
                newstrArray[i+2*count+1]='2';
                newstrArray[i+2*count+2]='0';
                count++;
            }
                
        }
        return new String(newstrArray);
    }
}
```
-----
```
public class Solution {
public String replaceSpace(StringBuffer str) {
return str.toString().replaceAll("\\s", "%20");
}
}
```
题解：如果建新数组的话，从后往前还是从前往后都是一样的。???
1. charAt(),deleteCharAt()   
   >s1.charAt(3);  
    s1.deleteCharAt(3); 
2. setCharAt();   
   替换所引出的char值
   >str.setCharAt(indexnew, '0');
3. append();  
   >StringBuffer s1 = new StringBuffer().append("bbb");  
    s1.append("aaa");  
    System.out.println(s1.toString());
4. replace两种用法：  
   >replace(int start，int end, String str)  
   replace(char oldchar, char newchar)
5. toString()  toCharArray()  
   >StringBuffer s1 = new StringBuffer();  
   s1.toString();  
   String s2 = new String();
   s2.toCharArray();
6. delete(); insert(); indexOf(); lastIndexOf(); reverse(); length();    
indexOf()返回指定字符串的开始字符索引位置，还可以从某个字符索引位置开始向后匹配，没有找到匹配的就会返回-1    
lastIndexOf()是从后往前匹配，也支持从指定索引开始从后往前去匹配
   >s1.delete(2,4);  
   s1.insert(2,"cc");  
   System.out.println(s1.indexOf("ba"));  
   System.out.println(s1.indexOf("ba",2));  
   System.out.println(s1.reverse());  
   System.out.println(s1.length());
5. String,StringBuffer,StringBuilder三者的使用方法和区别  
String适用于少量的字符串操作的情况  
StringBuilder适用于单线程下在字符缓冲区进行大量操作的情况  
StringBuffer适用多线程下在字符缓冲区进行大量操作的情况
   





6. 一.java数据类型
 1.基本数据类型
 byte(1) boolean(1) short(2) char(2) int(4) float(4) long(8)double (8)
 2.引用数据类型
 string,数组，集合ArrayList,Scanner,Random,自定义类型
 3.引用类型String中的方法
 第一组：判断方法
   boolean equals(String str);  //比较两个字符串是否相等
   boolean equalsIgnoreCase(String str);  //比较两个内容是否相等 （忽略大小写）
   boolean startsWith(String subStr); //判断某个字符串是否以指定的子串开头
   boolean endsWith(String subStr); //判断某个字符串是否以指定的子串结尾
 第二组：获取方法
   int length();//获取字符串中字符个数
   char charAt(int index); //获取字符串中某一个字符
   String substring(int startIndex);//从指定下标开始截取字符串，直到字符串结尾
   substring(int startIndex,int endIndex); //包括开头不包括结尾？
   int indexof(String subStr); //获取子串第一次出现的下标
 第三组：转换方法
   String toLowerCase(); //转成小写串
   String toUpperCase);  //转成大写串
   Char[] toCharArray(); //变成字符数组
 第四组：其他方法
   String trim();//去掉字符串两端的空格
   String[] split(String str); //切割字符串
  三：读写文件
  输出流：数据从java程序 到  文件中
  FilWriter：文件的字符输出流，写数据  （一个字符，一个字符串，一个字符数组）
     write(int ch);// 写一个字符
     write(char[] chs); //写一个字符数组
     write(String s);// 写一个字符串
     write(char[] chs,int startInex,int len);// 写一个字符数组的一部分
     write(String s,int startInex,int len); //写一个字符串的一部分
  输入流：数据从文件  到  java程序中
  FileReader:文件的字符输入流,读数据（一个字符，一个字符数组）
  	int read();//读取一个字符  ASCII
  	int read(char[] chs); //一次读取一个字符数组，返回值是读取的字符的个数
  文件的路径分为两种：
  1.相对路径：
          相对于当前项目而言的
  2.绝对路径：
          以盘符开头

