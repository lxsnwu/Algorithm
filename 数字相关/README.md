
## 只出现一次的数字
leetcode136
```
示例 1:
输入: [2,2,1]
输出: 1

示例 2:
输入: [4,1,2,1,2]
输出: 4
```
解题思路：
可能一开始会想到使用hashmap，但是如何不使用额外空间来实现呢？

首先我们需要知道：
1.交换律：a ^ b ^ c <=> a ^ c ^ b
2.任何数于0异或为任何数 0 ^ n => n
3.相同的数异或为0: n ^ n => 0

```
int singleNumber(vector<int>& nums) {
       int len = nums.size();
        int result=0;
       for(int i=0;i<len;i++){
           result ^=nums[i];
       } 
        return result;
 }
```

## 寻找重复数

```
示例 1:
输入: [1,3,4,2,2]
输出: 2
示例 2:

输入: [3,1,3,4,2]
输出: 3

说明：
1.不能更改原数组（假设数组是只读的）。
2.只能使用额外的 O(1) 的空间。
3.时间复杂度小于 O(n2) 。
4.数组中只有一个重复的数字，但它可能不止重复出现一次。
```
解题思路：
	快慢指针思想, fast 和 slow 是指针, nums[slow] 表示取指针对应的元素,注意 nums 数组中的数字都是在 1 到 n 之间的(在数组中进行游走不会越界),
因为有重复数字的出现, 所以这个游走必然是成环的, 环的入口就是重复的元素, 即按照寻找链表环入口的思路来做。

```
public int findDuplicate(int[] nums) {

	int fast = 0, slow = 0;
	while(true) {
		fast = nums[nums[fast]];
		slow = nums[slow];
		if(slow == fast) {
			fast = 0;
			while(nums[slow] != nums[fast]) {
				fast = nums[fast];
				slow = nums[slow];
			}
		return nums[slow];
		}
	}
}
```



## 位1的个数
leetcode191

```
示例 1：
输入：00000000000000000000000010000000
输出：1
解释：输入的二进制串 00000000000000000000000010000000 中，共有一位为 '1'。

示例 2：
输入：11111111111111111111111111111101
输出：31
解释：输入的二进制串 11111111111111111111111111111101 中，共有 31 位为 '1'。
```
思路一：将n和1与（&）运算，然后再右移；其中，如果运算结果是1则表明n的最后一位是1，count+1；否则就是最后一位是0，count不变.
缺陷：这种没有考虑到n是负数的时候。在计算机中负数存储成补码，右移的时候补位是1而不是0，所以1会一直存在，这样会造成一直循环，导致陷入死循环。

思路二：将n和1与（&）运算，可以n不动，让1左移，其中，如果运算结果是1则表明n的最后一位是1，count+1；否则就是最后一位是0，count不变.
```
public int numberOf1(int n){
  int count = 0;
  int flag = 1;
  while(flag!=0){
    if((n&flag)!=0){
      count++;
    }
    flag = flag<<1;
  }
return count;
}
```

思路三：一个整数减去1，相当于把这个数最右边的1的后边的变成0,0变成1；1的前边的0,1不变。举例说明：1100，减去1，变成1011。将这两个数做与&运算，1100&1011会得到1000，可以看出把1100最右边的1变成了0，所以我们可以用n&（n-1）来计算有多少个1；n能运行多少次这样的操作，就有多少个1.
```
public int NumberOf1(int n) {
        int count=0;
		while(n!=0){
            ++count;
            n=n&(n-1);
        }
        return count;
    }
```

## 缺失数字
leetcode268
```
给定一个包含 0, 1, 2, ..., n 中 n 个数的序列，找出 0 .. n 中没有出现在序列中的那个数。

示例 1:
输入: [3,0,1]
输出: 2

示例 2:
输入: [9,6,4,2,3,5,7,0,1]
输出: 8

说明:你的算法应具有线性时间复杂度。你能否仅使用额外常数空间来实现?
```
和上面的一道题（只出现一次的数字）有异曲同工之处。看了大家的题解，异或操作（^）是一种很好的方式，不用考虑sum越界问题。

举个例子：
0 ^ 4 = 4
4 ^ 4 = 0
那么，就可以不用求和，直接使用异或运算^进行 抵消，剩下的数字就是缺失的了。

再举个例子：
1^1^2^2^3 = 3
```
int missingNumber(int[] nums) {
    int len = nums.length;
    for (int i = 0; i < nums.length; i++){
        len ^= nums[i];
        len ^= i;
    }
    return sum;
}
```

还有一个很直观的解法：求出0-n的和，然后求出数组所有数的和，两个和相减，得到结果。

```
int missingNumber(int[] nums) {
	int sum = 0;
	for (int elem : nums) {
		sum += elem;
	}
	return ((1 + nums.length) * nums.length / 2) - sum;
}
```

## 3的幂
leetcode326
```
给定一个整数，写一个函数来判断它是否是 3 的幂次方。
示例 1:
输入: 27
输出: true

示例 2:
输入: 0
输出: false
```
进阶：你能不使用循环或者递归来完成本题吗？

通过查看相关解析，发现了这个解法，用到了数论的知识，3的幂次的质因子只有3，而所给出的n如果也是3的幂次，故而题目中所给整数范围内最大的3的幂次的因子只能是3的幂次，1162261467是3的19次幂，是整数范围内最大的3的幂次

```
class Solution {
    public boolean isPowerOfThree(int n) {
        return n > 0 && 1162261467%n == 0;
    }
}
```
皮：
```
public boolean isPowerOfThree(int n) {
	if(n==0)
	return false;
	if(n==Math.pow(3,0)|n==Math.pow(3,2)|n==Math.pow(3,1)|n==Math.pow(3,2)|n==Math.pow(3,3)|n==Math.pow(3,4)|
n==Math.pow(3,5)|n==Math.pow(3,6)|n==Math.pow(3,7)|n==Math.pow(3,8)|n==Math.pow(3,9)|n==Math.pow(3,10)|
n==Math.pow(3,11)|n==Math.pow(3,12)|n==Math.pow(3,13)|n==Math.pow(3,14)|n==Math.pow(3,15)|n==Math.pow(3,16)|
n==Math.pow(3,17)|n==Math.pow(3,18)|n==Math.pow(3,19)|n==Math.pow(3,20))
	return true;
	return false;
}
```

## 寻找峰值
```
峰值元素是指其值大于左右相邻值的元素。
给定一个输入数组 nums，其中 nums[i] ≠ nums[i+1]，找到峰值元素并返回其索引。
数组可能包含多个峰值，在这种情况下，返回任何一个峰值所在位置即可。
你可以假设 nums[-1] = nums[n] = -∞。

示例 1:
输入: nums = [1,2,3,1]
输出: 2
解释: 3 是峰值元素，你的函数应该返回其索引 2。

示例 2:
输入: nums = [1,2,1,3,5,6,4]
输出: 1 或 5 
解释: 你的函数可以返回索引 1，其峰值元素为 2；
     或者返回索引 5， 其峰值元素为 6。	 
```
思路解析：用二分法来寻找峰值
为什么二分查找大的那一半一定会有峰值呢？（即nums[mid]<nums[mid+1]时，mid+1~N一定存在峰值） 我的理解是，首先已知 nums[mid+1]>nums[mid]，那么mid+2只有两种可能，一个是大于mid+1，一个是小于mid+1，小于mid+1的情况，那么mid+1就是峰值，大于mid+1的情况，继续向右推，如果一直到数组的末尾都是大于的，那么可以肯定最后一个元素是峰值，因为nums[nums.length]=负无穷
```
class Solution {
    public int findPeakElement(int[] nums) {
        
      if(nums.length == 1)
          return 0;
      if(nums[0] > nums[1])
          return 0;
      if(nums[nums.length - 1] > nums[nums.length - 2])
          return nums.length - 1;
      return binary(nums, 1 , nums.length - 2);
    }
    
    public int binary(int nums[], int left, int right){
        
        if(left > right)
            return -1;
        int mid = (left + right) / 2;
        if(nums[mid] > nums[mid - 1] && nums[mid] > nums[mid + 1])
            return mid;
        int value = binary(nums, left, mid - 1);
        if(value == -1)
            return binary(nums, mid + 1, right);
        else
            return value;
    }
}
```


## x的平方根
leetcode.69

实现 int sqrt(int x) 函数。
计算并返回 x 的平方根，其中 x 是非负整数。
由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。
```
class Solution {
    public int mySqrt(int x) {
        int i;
        if(x==1){
            return 1;
        }
        for(i=1;i<x;i++){
            if((long)i*i>x){
                break;
            }
        }
        return i-1;
   }
}
```

















