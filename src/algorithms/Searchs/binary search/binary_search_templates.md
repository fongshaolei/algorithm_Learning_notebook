二分模板一共有两个，分别适用于不同情况。
----
算法思路：假设目标值在闭区间`[l, r]`中， 每次将区间长度缩小一半，当`l = r`时，我们就找到了目标值。

## 版本1
当我们将区间`[l, r]`划分成`[l, mid]`和`[mid + 1, r]`时，其更新操作是`r = mid`或者`l = mid + 1`;，计算`mid`时不需要加`1`。

### C++ 代码模板：
```c++
int bsearch_1(int l, int r)
{
    while (l < r)
    {
        int mid = l + r >> 1;
        if (check(mid)) r = mid;
        else l = mid + 1;
    }
    return l;
}
```
## 版本2
当我们将区间`[l, r]`划分成`[l, mid - 1]`和`[mid, r]`时，其更新操作是`r = mid - 1`或者`l = mid`;，此时为了防止死循环，计算`mid`时需要加1。

### C++ 代码模板：
```c++
int bsearch_2(int l, int r)
{
    while (l < r)
    {
        int mid = l + r + 1 >> 1;
        if (check(mid)) l = mid;
        else r = mid - 1;
    }
    return l;
}
```

--------
# 数的范围

给定一个按照升序排列的长度为 `n `的整数数组，以及 `q` 个查询。

对于每个查询，返回一个元素 `k `的起始位置和终止位置（位置从` 0` 开始计数）。

如果数组中不存在该元素，则返回 `-1 -1`。

## 输入格式
第一行包含整数 `n` 和 `q`，表示数组长度和询问个数。

第二行包含 `n` 个整数（均在 `1∼10000 `范围内），表示完整数组。

接下来 `q `行，每行包含一个整数 `k`，表示一个询问元素。

输出格式
共`q` 行，每行包含两个整数，表示所求元素的起始位置和终止位置。

如果数组中不存在该元素，则返回 `-1 -1`。

## 数据范围
1≤n≤100000

1≤q≤10000

1≤k≤10000
### 输入样例：
6 3

1 2 2 3 3 4

3

4

5
#### 输出样例：
3 4

5 5

-1 -1

### 解题代码
```java
import java.util.*;

class Main{
    static int N = 100010;
    static int[] arr = new int[N];
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int q = sc.nextInt();
        for(int i = 0; i < n; i ++) arr[i] = sc.nextInt();
        while(q -- > 0){
            int k = sc.nextInt();
            int l = 0, r = n - 1;
            while(l < r){
                int mid = l + r >> 1;
                if(arr[mid] >= k) r = mid;
                else l = mid + 1;
            }
            if(arr[l] != k) System.out.println("-1 -1");
            else{
                System.out.print(l + " ");
                l = 0;r = n - 1;
                while(l < r){
                    int mid = l + r + 1>> 1;
                    if(arr[mid] <= k) l = mid;
                    else r = mid - 1;
                }
                System.out.println(l);
            }
        }
    }
}
```
