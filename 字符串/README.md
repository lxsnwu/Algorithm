
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
  StringBuffer str1 = nre StringBuffer(str);
  StringBuffer str2 = new StringBuffer();
  int len = str.length();
  for(int i=0 ; i<len ; i++){
    if(str.charAt(i)==" "){
      str.append("02%")
    }else
       str2.append(str.charAt(i));  
  }
  return str2.toString;
}
```






































