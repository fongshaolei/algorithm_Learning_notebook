<!--
 * @Descripttion: 
 * @version: 
 * @Author: William Fang
 * @Date: 2022-05-31 20:50:23
 * @LastEditors: 输入自己姓名
 * @LastEditTime: 2022-05-31 20:53:16
-->
# 数的三次方根

给定一个浮点数 n，求它的三次方根。

## 输入格式
共一行，包含一个浮点数 n。

## 输出格式
共一行，包含一个浮点数，表示问题的解。

注意，结果保留 6 位小数。

## 数据范围
−10000≤n≤10000
### 输入样例：
1000.00
### 输出样例：
10.000000

-----

### 题解代码
```java
import java.util.*;
import java.io.*;

class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(new BufferedInputStream(System.in));
        double n = sc.nextDouble();
        
        double l = -1000, r = 1000;
        // 左右两边距离要非常的小
        while(r - l > 1e-8){
            double mid = (l + r ) / 2;
            if(mid * mid * mid < n) l = mid;
            else r = mid;
        }
        
        System.out.printf("%.6f", l);
    }
}
```

需要注意的是，这里和我们二分的思路不太一样。之前二分的思路是需要改变左右两边的`l`和`r`，但是。对于浮点数，我们不需要。

而且，对于`while`中，由于是浮点数，所以需要通过:`r - l > 1e-8`来进行控制。
