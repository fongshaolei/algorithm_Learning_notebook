# 第k个数
给定一个长度为 n 的整数数列，以及一个整数 k，请用快速选择算法求出数列从小到大排序后的第 k 个数。

## 输入格式
第一行包含两个整数 n 和 k。

第二行包含 n 个整数（所有整数均在 1∼109 范围内），表示整数数列。

## 输出格式
输出一个整数，表示数列的第 k 小数。

## 数据范围
1≤`n`≤100000,

1≤`k`≤`n`

### 输入样例：
5 3

2 4 1 5 3
### 输出样例：
3

------

### 题解
```java
import java.util.*;

class Main{
    static int N = 100010;
    static int[] q = new int[N];
    public static int quick_sort(int l, int r, int k){
        if(l >= r) return q[l];
        int i = l - 1,j = r + 1, x = q[l + r >> 1];
        while(i < j){
            while(q[++i] < x);
            while(q[--j] > x);
            if(i < j){
                int t = q[i];
                q[i] = q[j];
                q[j] = t;
            }
        }
        if((j - l + 1) >= k) return quick_sort(l, j, k);
        else return quick_sort(j + 1, r, k - (j - l + 1));
    }
    
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int k = sc.nextInt();
        for(int i = 0; i < n; i ++) q[i] = sc.nextInt();
        System.out.println(quick_sort(0, n - 1, k));
    }
}
```