

## 斐波那契数列

题目描述
大家都知道斐波那契数列，现在要求输入一个整数n，请你输出斐波那契数列的第n项。

解析：斐波那契数列也有叫它（不死神兔），就是数学规律题，递归版的写法很简单，但是面试时，你写出递归的写法，就相当于0分，从头到脚，从内心到外表，深深地鄙视你......所以为了获得更高的分数，使用动态规划去解才是最好的。当然了，如果你需要缓存所有的结果，就是用额外空间数组进行存储，当然面试官要求只需要结果的话，那么我们就没有必要使用数组进行缓存，只需要使用一个中间变量进行记录结果。
具体公式：F(n) = F(n-1) + F(n-2); F(0) = 0; F(1) = 1; 

### 递归解法

举个小点的例子，n=4，看看程序怎么跑的：
Fibonacci(4) = Fibonacci(3) + Fibonacci(2);
                    = Fibonacci(2) + Fibonacci(1) + Fibonacci(1) + Fibonacci(0);
                    = Fibonacci(1) + Fibonacci(0) + Fibonacci(1) + Fibonacci(1) + Fibonacci(0);
由于我们的代码并没有记录Fibonacci(1)和Fibonacci(0)的结果，对于程序来说它每次递归都是未知的，因此光是n=4时f(1)就重复计算了3次之多。
#### 时间复杂度为二叉树的节点个数：(2^h)-1=O(2^N) ，空间复杂度为树的高度：h即O(N)。
```
 public static int Fibonacci(int n){  //递归解法
   
      if(n==1){  
          return 0;  
      }  
   
      if(n==2){  
          return 1;  
      }  
      return Fibonacci(n-1)+Fibonacci(n-2);  
  } 
```

### 动态规划解法
#### 时间复杂度为：O(N) ，空间复杂度为：O(1)。
```
 public class Solution {  //最优解
     public int Fibonacci(int n) {  
         if(n <= 1){  //代码的鲁棒性
             return n;  
         }  
         int first = 0;  
         int second = 1;
         //记录每一次的结果  
         int result = 0;  
         for(int i = 2;i < n+1;i++){  
             result = first + second;    
             first = second;    
             second = result;    
         }  
         return result;  
     }  
 }  
```








