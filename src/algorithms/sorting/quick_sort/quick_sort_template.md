# 快速排序
给定你一个长度为 `n` 的整数数列。

请你使用快速排序对这个数列按照从小到大进行排序。

并将排好序的数列按顺序输出。

## 输入格式
输入共两行，第一行包含整数` n`。

第二行包含`n` 个整数（所有整数均在 `1∼10^9 `范围内），表示整个数列。

## 输出格式
输出共一行，包含 `n` 个整数，表示排好序的数列。

## 数据范围
1≤ `n ≤  `100000

### 输入样例：

5

3 1 2 4 5



### 输出样例：


1 2 3 4 5

------


算法证明使用算法导论里的循环不变式方法
## 快排的模板（以j为分界）
快排属于分治算法，分治算法都有三步：
- 分成子问题
- 递归处理子问题
- 子问题合并

```java
void quick_sort(int q[], int l, int r)
{
    //递归的终止情况
    if(l >= r) return;
    //第一步：分成子问题
    int i = l - 1, j = r + 1, x = q[l + r >> 1];
    while(i < j)
    {
        do i++; while(q[i] < x);
        do j--; while(q[j] > x);
        if(i < j) swap(q[i], q[j]);
    }
    //第二步：递归处理子问题
    quick_sort(q, l, j), quick_sort(q, j + 1, r);
    //第三步：子问题合并.快排这一步不需要操作，但归并排序的核心在这一步骤
}
```


## 题解代码：

```java
mport java.util.*;
import java.io.*;

class Main{
    static int N = 100010;
    static int[] arr = new int[N];

    public static void quick_sort(int l, int r){
        // 如果是特殊情况直接退出
        if(l >= r) return;
        int i = l - 1, j = r + 1 , x = arr[ l + r >> 1];
        // 判断当前i和j的情况
        while( i < j){
            do i++; while(arr[i] < x);
            do j--; while(arr[j] > x);
            // 如果仍然是符合的，直接进行交换
            if( i < j) swap(i, j);
        }
        // 递归的处理左边和右边
        quick_sort(l, j);
        quick_sort(j + 1, r);
    }

    public static void swap(int i, int j){
        int tmp = arr[i];
        arr[i] = arr[j];
        arr[j] = tmp;
    }
    public static void main(String[] args){
        Scanner sc = new Scanner(new BufferedInputStream(System.in));
        int n = sc.nextInt();
        for(int i = 0; i < n; i ++) arr[i] = sc.nextInt();

        quick_sort(0, n - 1);

        for(int i = 0; i < n; i ++) System.out.print(arr[i] + " ");
    }
}
```