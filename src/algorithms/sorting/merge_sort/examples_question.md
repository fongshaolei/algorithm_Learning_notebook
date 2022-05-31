# 逆序对的数量
给定一个长度为 n 的整数数列，请你计算数列中的逆序对的数量。

逆序对的定义如下：对于数列的第 i 个和第 j 个元素，如果满足` i<j `且 `a[i]>a[j]`，则其为一个逆序对；否则不是。

## 输入格式
第一行包含整数 n，表示数列的长度。

第二行包含 n 个整数，表示整个数列。

## 输出格式
输出一个整数，表示逆序对的个数。

## 数据范围
1≤n≤100000，

数列中的元素的取值范围 [1,10^9]。

### 输入样例：
6

2 3 4 5 6 1
### 输出样例：
5

------
```java
import java.util.*;

class Main{
    static int N = 100010;
    static int[] q = new int[N];
    static int[] tmp = new int[N];
    // 返回逆序对数量
    public static long merge_sort(int l, int r){
        if(l >= r) return 0;
        int mid = l + r >> 1;
        long ret = merge_sort(l, mid) + merge_sort(mid + 1, r);
        int i = l, j = mid + 1, k = 0;
        while(i <= mid && j <= r){
            if(q[i] <= q[j]) tmp[k++] = q[i++];
            else{
                // 记录逆序对的数量
                ret += (mid + 1 - i);
                tmp[k++] = q[j++];
            }
        }
        // 扫尾工作
        while(i <= mid) tmp[k++] = q[i++];
        while(j <= r) tmp[k++] = q[j++];
        
        for(i = l, k = 0; i <= r; i ++) q[i] = tmp[k++];
        // 返回结果集
        return ret;
    }
    
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        for(int i = 0; i < n; i ++) q[i] = sc.nextInt();
        System.out.println(merge_sort(0, n - 1));
    }
}
```