# 归并排序
给定你一个长度为 n 的整数数列。

请你使用归并排序对这个数列按照从小到大进行排序。

并将排好序的数列按顺序输出。

## 输入格式
输入共两行，第一行包含整数 n。

第二行包含 n 个整数（所有整数均在 1∼109 范围内），表示整个数列。

## 输出格式
输出共一行，包含 n 个整数，表示排好序的数列。

## 数据范围
1≤n≤100000
### 输入样例：
5

3 1 2 4 5
### 输出样例：
1 2 3 4 5

----

### 分析
归并模板
归并属于分治算法，有三个步骤
```java
void merge_sort(int q[], int l, int r)
{
    //递归的终止情况
    if(l >= r) return;

    //第一步：分成子问题
    int mid = l + r >> 1;

    //第二步：递归处理子问题
    merge_sort(q, l, mid ), merge_sort(q, mid + 1, r);

    //第三步：合并子问题
    int k = 0, i = l, j = mid + 1, tmp[r - l + 1];
    while(i <= mid && j <= r)
        if(q[i] <= q[j]) tmp[k++] = q[i++];
        else tmp[k++] = q[j++];
    while(i <= mid) tmp[k++] = q[i++];
    while(j <= r) tmp[k++] = q[j++];

    for(k = 0, i = l; i <= r; k++, i++) q[i] = tmp[k];
}
```

### 题解
```java
import java.util.*;

class Main{
    static int N = 100010;
    static int[] q = new int[N];
    static int[] tmp = new int[N];
    public static void merge_sort(int l, int r){
        if(l >= r) return;
        int mid = l + r >> 1;
        // 分别merge左右两边
        merge_sort(l, mid); merge_sort(mid + 1, r);
        // 开始合并的逻辑
        int i = l, j = mid + 1, k = 0;
        while(i <= mid && j <= r){
            if(q[i] <= q[j]) tmp[k++] = q[i++];
            else tmp[k++] = q[j++];
        }
        // 扫尾工作
        while(i <= mid) tmp[k++] = q[i++];
        while(j <= r) tmp[k++] = q[j++];
        
        // 赋值
        for(i=l, k = 0; i <= r; i++) q[i] = tmp[k++];
    }
    
    
    
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        for(int i = 0; i < n; i ++) q[i] = sc.nextInt();
        merge_sort(0, n - 1);
        for(int i = 0; i < n; i ++) System.out.print(q[i] + " ");
    }
}
```