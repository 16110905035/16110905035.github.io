---
layout: post
title: 基础算法之素数,gcd
tags: 基础算法
---
### 概述：
> * 建议大家在学之前请分清素数,合数的区别.数字的几种分类.
> * 线性求素数应该算是数论里面知识点的基础，掌握后就可以看一看
  >> * 分解素因子算法，算数基本定理（唯一分解定理），区间求素数， 欧拉函数等（为甚么，因为后面的我有学，这只是总结贴而已.(0_0)!!!）。
> * Ps: 笔者在这只写了java的版本,所以其他相关的知识点,请各位自行查阅.
> * 推荐网址：　线性求素数（传送门)[https://www.zhihu.com/question/24942373]
> * gcd函数(求最大公约数),exgcd(欧几里得算法,扩展gcd,不定方程组,中国剩余定理)ps:自查
> * 祝大家都有所收获!

## 素数:

### c++版本：

  ```
  #include <bits/stdc++.h>
  using namespace std;
  const int maxn =1e6+5;
  bool vis[maxn];
  int cnt ;//统计prime 个数
  int prime[maxn];//存储prime
  /***
  前提说明：这个算法的时间复杂度是可以优化的，
  如何优化，请自行百度。
  ***/
  void is_prime() // 求prime
  {
      long long i,j,k;
      fill(vis,vis+maxn,0);
      cnt =0 ;
      for (i =2 ;i<maxn;i++)
      {
           if (!vis[i])
           {
               prime[cnt++]=i;
           }
           for (j=i*i;j<maxn;j+=i)
           {
               vis[j]=1;
           }
           vis[0]=vis[1]=1; // 0,1 不是素数
      }
  }
  int main ()
  {
       is_prime();
       for (int i = 0;i< 100;i++)
       {
           if (i<10)
              cout<<prime[i]<<"\t";
           else
              cout<<prime[i]<<endl;
       }
      return 0;
  }

  ```


### Java版本：

  ```
  import java.util.Scanner;
  import java.util.Arrays;
  public class Main {
  	public static void main(String[] args) {
  		Scanner in = new Scanner(System.in);
  		Prime a = new Prime(10000000);
  		int cnt = 0;
  		int num[] = new int[100];
  		for (int i = 100; i < 201; i++) {
        //		int x = in.nextInt();
  			if (a.isPrime[i] == true) {
  				num[cnt++] = i;
  			}
  		}
  		System.out.println(cnt);
  		int i;
  		for (i = 0; i < cnt - 1; i++) {
  			System.out.printf("%d ", num[i]);
  		}
  		System.out.println(num[i]);
  	}
  }

  class Prime {
  	/*
  	 * 偶数一定不是素数，排除，默认所有的奇数为素数，在此基础上进行筛选 推荐网址：
  	 * https://www.zhihu.com/question/24942373 PS： 2是素数
  	 * 待添加的函数： 范围内求素数数量，输出
  	 * 判断素数。
  	 * java没有类似c++直接声名全局变量求得方式，可能这就是面向对象与面向过程的一点点区别吧
  	 */
  	boolean isPrime[];
  	int rangeNum;

  	Prime(int num) {
  		rangeNum = num + 1;
  		isPrime = new boolean[rangeNum];
  		// for (int i =0;i<rangeNum;i++) //不用自己初始化，boolean类型默认为false
  		// isPrime[i]=false ;
  		for (int i = 3; i < rangeNum; i += 2)
  			isPrime[i] = true;
  		isPrime[2] = true;
  		for (int i = 3; i * i < rangeNum; i++) // 必须是 i*i<rangeNum. 否则的化会撑爆int上限，本来想用long表示，不过java不予许从long 到int
  												// 。。至少我现在不知道。。
  		{
  			if (isPrime[i] == true) {
  				for (int j = i * i; j < rangeNum; j += i)
  					isPrime[j] = false;
  			}
  		}
  	}

  	int calculatNumber(int maxn) { // 计算在maxn范围内素数的个数
  		int cnt = 0;
  		for (int i = 2; i < maxn; i++)
  			if (isPrime[i])
  				cnt++;
  		return cnt;
  	}

  	boolean judge(int x) {
  		return isPrime[x];
  	}
  }
  ```
## gcd函数(java版本):

  ```
  import java.util.Scanner;
  import java.util.Arrays;

  public class Main {
  	public static void main(String[] args) {
  		Scanner in = new Scanner(System.in);
  		while(in.hasNext())
  		{int x = in.nextInt();

  		int y = in.nextInt();
  		int ret= gcd(x, y);
  		int  ans =x*y/ret;
  		System.out.printf("%d\n%d\n",ret,ans);
  		}

  	}
  	static int gcd(int a, int b)
  	{
  		if (a==0)
  			return  b;
  		else
  			return gcd(b%a,a);
  	}
  	// 扩展gcd算法。。不定方程
  }
  ```


### 注意:
以上内容，作者一字一句码出来的，纯属不易，欢迎大家转载，转载是还请您表明出处。另外如果我有侵权行为，请在下方留言，确认后我会及时撤销相应内容，谢谢大家！

PS:欢迎大家来到我的小站,和我一起记录属于我们自己的大学！
