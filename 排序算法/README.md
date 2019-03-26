
## 冒泡排序

设数组的长度为N： 
（1）比较前后相邻的二个数据，如果前面数据大于后面的数据，就将这二个数据交换。
（2）这样对数组的第0个数据到N-1个数据进行一次遍历后，最大的一个数据就“沉”到数组第N-1个位置。
（3）N=N-1，如果N不为0就重复前面二步，否则排序完成。
```
public static viod bubbleSort(int[] arr){
  int n = arr.length;
  for(int i=0;i<n-1;i++){
    for(int j=0;j<n-1-i;j++){
      if(arr[j]>arr[j+1]){
        int temp = arr[j];
        arr[j] = arr[j+1];
        arr[j+1] = temp;
      }
    }
  }
}
```
性能分析：若记录序列的初始状态为"正序"，则冒泡排序过程只需进行一趟排序，在排序过程中只需进行n-1次比较，且不移动记录；反之，若记录序列的初始状态为"逆序"，则需进行n(n-1）/2次比较和记录移动。因此冒泡排序总的时间复杂度为O(n*n)。

算法优化：
冒泡排序法存在的不足及改进方法：
第一，在排序过程中，执行完最后的排序后，虽然数据已全部排序完备，但程序无法判断是否完成排序，为了解决这一不足，可设置一个标志位flag，将其初始值设置为非0，表示被排序的表是一个无序的表，每一次排序开始前设置flag值为0，在进行数据交换时，修改flag为非0。在新一轮排序开始时，检查此标志，若此标志为0，表示上一次没有做过交换数据，则结束排序；否则进行排序；
```
public static void BubbleSort(int[] arr) {
    boolean flag = true;
    while(flag){
       int temp;//定义一个临时变量
       for(int i=0;i<arr.length-1;i++){//冒泡趟数，n-1趟
           for(int j=0;j<arr.length-i-1;j++){
               f(arr[j+1]<arr[j]){
                   temp = arr[j];
                   arr[j] = arr[j+1];
                   arr[j+1] = temp;
                   flag = true;
                }
           }
       if(!flag){
           break;//若果没有发生交换，则退出循环
       }
     }
   }
}
```



## 快速排序

```
public class QuickSort {
    public static void quickSort(int[] arr,int low,int high){
        int i,j,temp,t;
        if(low>high){
            return;
        }
        i=low;
        j=high;
        //temp就是基准位
        temp = arr[low];

        while (i<j) {
            //先看右边，依次往左递减
            while (temp<=arr[j]&&i<j) {
                j--;
            }
            //再看左边，依次往右递增
            while (temp>=arr[i]&&i<j) {
                i++;
            }
            //如果满足条件则交换
            if (i<j) {
                t = arr[j];
                arr[j] = arr[i];
                arr[i] = t;
            }

        }
        //最后将基准为与i和j相等位置的数字交换
         arr[low] = arr[i];
         arr[i] = temp;
        //递归调用左半数组
        quickSort(arr, low, j-1);
        //递归调用右半数组
        quickSort(arr, j+1, high);
    }
```


















