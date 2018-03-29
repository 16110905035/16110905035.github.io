---
layout: post
title: Java学习笔记之水题日志
tags: Java_Basic_Knowledge
---


### java 之arrays
>
  *  导入模板： import java.util.Arrays;
  *  常用函数：
    *   排序： 			Arrays.sort(a,start,end );
    *  转化成字符串： 	Arrays.toString(a);
    * 复制数组： 		Arrays.copyOfRanges(a,start,end);
    *  二分查找：   	Arrays.binarySearch(a,x);  // 返回索引，即数组下标，找不到时返回-1;

### java 之 格式化输出：
> * java 格式化输出浮点类型：
>> *  方法一：
		double d1 = 123.635;  
		double d2 = 123.6;   
		System.out.printf("%#.2f %#.2f/n", d1, d2);  // 記住是%f，而不是%lf
>> * 方法二：
		double d1 = 123.635;  
		double d2 = 123.6;  
		DecimalFormat df = new DecimalFormat(".00");  
		System.out.println(df.format(d1) + " " + df.format(d2));

### java 接受用戶輸入：

>
* 导入模板： import java.util.Scanner;
* 接受用戶輸入：
		Scanner in =new Scanner(System.in);
		in.hasNext(); //判断用户是否有下一次的输入
		int x =in.nextInt(); // x接收用户输入的int类型数据
PS: java 基本数据类型： 真正赋值 ，对象则是引用

### java String类 java api

```
 	   string  s ;
		 char[] arr = s.toCharArray();
		 s.equals(str);// 判断s 与str是否相等，相等返回 true，否则false
		 s.equalsIgnoreCase(str);// 忽略大小写
		 s.split(String regex) ; //差分字符
		 s.replace(str1,str2);//用str2替换s中的str1
		 s.indexof(str);//返回str在s中第一次出现的位置，没有返回-1
		 s.substring(int start,int end);// 返回一个s[start,end)的字符串
```
### java 接口的区别：
>* Interface是用来定义类的，I并且是一个极度抽象的类，因为它允许人们通过创建一个能够被向上转型为多种基类的类型，来实现某种类似多种继承变种的特性。
* Interface接口仅包含方法的声明，而不包含其实现。也就是说，实现接口的每个类都必须为该接口中声明的每个方法提供实现。
Interface接口方法定义不能包含任何属性（如 public 或 private），但在实现接口的类的定义中，已实现的方法必须标记为 public。
* 通过 extends 语句可以使用一个接口继承多个接口，通过 implements 语句可以使用一个类继承多个接口。
* 通俗的讲：interface 只能定义，不能实现，implements可以实现
* 引自：[传送门](https://www.cnblogs.com/hljarmy/archive/2013/10/30/3396606.html)

### java 多级自定义排序: (ｕｐｄａｔｅ: 2018-03-29)
> * 前提说明:
 >> 输入学生姓名,年龄,以及成绩
 >> 以成绩降序,年龄升序的形式输出.
> * Ps：如果你学过ｃ＋＋，也用ｃ++写过线性求素数，仔细比较下，你会发现这两者之间存在的区别．（⊙ｖ⊙）嗯，就是这样！



```
/**
 * @author  John Nash
 * @date Crate time：2018年3月26日下午10:26:03
 */
import java.util.Scanner;
import java.util.Arrays;

class Person implements Comparable<Person> {
	String name;
	int score ;
	int age ;

	public int compareTo(Person b) // 返回值有三种 1，0，-1
	{
		if (score!=b.score)
		return b.score - score;
		else
			return age -b.age;
	}

}
public class Main {
	public static void main(String[] args) {

		Scanner in = new Scanner(System.in);
		while (in.hasNext()) {
			int n = in.nextInt();
			Person a[] = new Person[n];
			for (int i = 0; i < n; i++) {
				a[i] = new Person();
				a[i].name = in.next();
				a[i].score = in.nextInt();
				a[i].age =in.nextInt();
			}
			Arrays.sort(a);//
			for (int i = 0; i < n; i++) {
				System.out.println(a[i].name + " " + a[i].score+ " "+a[i].age);
			}
		}
	}
}
```

### 注意:
以上内容，作者一字一句码出来的，纯属不易，欢迎大家转载，转载是还请您表明出处。另外如果我有侵权行为，请在下方留言，确认后我会及时撤销相应内容，谢谢大家！

PS:欢迎大家来到我的小站,和我一起记录属于我们自己的大学！
