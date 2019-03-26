
![avatar](https://images0.cnblogs.com/blog2015/694841/201506/231749553615077.png)

## 字符流中第一个不重复的字符

问题描述：请实现一个函数用来找出字符流中第一个只出现一次的字符。例如，当从字符流中只读出前两个字符"go"时，第一个只出现一次的字符是"g"。当从该字符流中读出前六个字符“google"时，第一个只出现一次的字符是"l"。

思路：申请一个128大小的数组来实现一个简易的哈希表。所以创建一个大小为128的整形数组，因为一个字符不会超过8位创建一个List，存放只出现一次的字符。insert时先对该字符所在数组位置数量+1，再判断该位置的值是否为1，如果为1，就添加到List中，不为1，则表示该字符已出现不止1次，然后从List中移除，取出时先判断List的size是否为0，不为0直接List.get(0)，就可以得到结果，否则返回‘#’
```
public class Solution{

  StringBuffer str = new StringBuffer();
  int[] table = new int[128];

  public viod Insert(char ch){
    //把字符添加到字符串中，并使数组对应的位置加1。
    s.append(ch);
    table[ch]++;
  }
  
  public char getOnceChar(){
    char[] char1 = s.toString.charArray();
    for(char c : char1){
      if(table[c] == 1)
        return c;
    }
    return #;
  }
}
```
方法二：利用LinkedHashMap的有序性

```
public class Solution {
    private Map<Character, Integer> map = new LinkedHashMap<>();
     
    //添加char到map
    public void Insert(char ch) {
        if (map.containsKey(ch)) {
            map.put(ch, map.get(ch) + 1);
        } else {
            map.put(ch, 0);
        }
    }
     
    //返回字符
    public char getOnceChar() {
        //根据entrySet遍历map。
        for (Map.Entry<Character, Integer> set : map.entrySet()) {
            if (set.getValue() == 0) {
                return set.getKey();
            }
        }
        return '#';
    }
}

```

## 翻转字符串

方法一：利用栈
```
public static string reverseString(String str){
  Stack<Character> stack = new Stack<Character>();
  char[] c = new char[str.length()];
  char[] temp = new char[str.length()];
  c = str.toCharArray();
  
  for(int i=0;i<str.length;i++){
    stack.push(c[i]);
  }
  for(int i=0;i<str.length;i++){
    temp[i] = stack.pop();
  }
  retrun String.valueOf(temp);
}
```

方法二：利用StringBuffer中的reverse()
```
public static String reverseString(String str){
  StringBuffer str2 = new StringBuffer(str);
  return str2.reverse().toString;
}
```

## 替换空格

问题描述：请实现一个函数，将一个字符串中的每个空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

```
public String replaceSpace(String str){
    StringBuffer str1 = new StringBuffer();
  int len = str.length();
  for(int i=0 ; i<len ; i++){
    if(str.charAt(i)==' '){
      str1.append("02%")
    }else
      str1.append(str.charAt(i));  
  }
  return str1.toString;
}
```
## 是否为回文串

问题描述：给定一个字符串，验证它是否是回文串，只考虑字母和数字字符，可以忽略字母的大小写。说明：本题中，我们将空字符串定义为有效的回文串。
![avatar](https://upload-images.jianshu.io/upload_images/1670644-f5d13bd20d6d5168.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)


```
public boolean isPalindrome(String str){
  str = str.toLowerCase();
  int len = str.length();
  StringBuffer str2 = new StringBuffer(str); 
  char
  for(char c : str.toCharArray())
    if((c>='0' && c<='9') || (c>='a' && c<='z')){
      str2.append(c);
    }
  }
  return str2.toString.equals(str2.reverse().toString());
}

```



## 最长回文串

问题描述：给定一个包含大写字母和小写字母的字符串，找到通过这些字母构造成的最长的回文串。在构造过程中，请注意区分大小写。比如 "Aa" 不能当做一个回文字符串。
![avatar](https://upload-images.jianshu.io/upload_images/1670644-e1c1219dc0d109f6.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)

思路解析：统计字母出现的次数即可，双数才能构成回文。因为允许中间一个数单独出现，比如“abcba”，所以如果最后有字母落单，总长度可以加 1。

```
public int longestPalindrome(String str){
  int len = str.length();
  if(len == 0)  return 0;
  int count = 0;
  HashSet<Character> ch = new HashSet<Character>();
  for(int i=0;i<len;i++){
    if(ch.contains(s.charAt(i))){
      ch.remove(s.charAt(i));
      count ++;
    }
    else ch.add(s.charAt(i));
  }
  return !ch.isEmpty()? count*2 : count*2 + 1;
}

```

## 第一次只出现一次的字符

题目描述：在一个字符串(0<=字符串长度<=10000，全部由字母组成)中找到第一个只出现一次的字符,并返回它的位置, 如果没有则返回 -1.

思路解析：先在hash表中统计各字母出现次数，第二次扫描直接访问hash表获得次数。也可以用数组代替hash表。

```
public int FirstNotRepeatingChar(String str){
  int len = str.length();
  HashMap<Character> hash = new HashMap<Character>();
  for(int i = 0 ; i<len ; i++){
    if(hash.containsKey(str.charAt(i))){
      int val = hash.get(charAt(i));
      hash.put(str.charAt(i),val+1);
    } else
    hash.put(str.charAt(i),1);
  }

  for(int i =0; i<len; i++){
    if(hash.get(str.charAt(i))==1);
    return str.charAt(i);
  }
  retrun -1;
} 

```






























