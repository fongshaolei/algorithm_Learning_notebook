# 高精度加法
给定两个正整数（不含前导 0），计算它们的和。

## 输入格式
共两行，每行包含一个整数。

## 输出格式
共一行，包含所求的和。

## 数据范围
1≤整数长度≤100000
### 输入样例：
12

23
### 输出样例：
35

-----

### 
```java
import java.util.*;

class Main{
    static int N = 100010;
    static int[] A = new int[N];
    static int[] B = new int[N];
    static int[] C = new int[N];
    static int ka,kb,kc;
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        String a = sc.next();
        String b = sc.next();
        // 将字符串转成数组操作
        for(int i = a.length() - 1; i >= 0; i--) A[ka++] = a.charAt(i) - '0';
        for(int i = b.length() - 1; i >= 0; i--) B[kb++] = b.charAt(i) - '0';
        add(A,B);
        
        for(int i = kc - 1; i >= 0; i --) System.out.print(C[i]);
    }
    
    public static void add(int[] a, int[] b){
        int t = 0; // 进位信息
        for(int i = 0; i < ka || i < kb; i ++){
            if(i < ka) t += a[i];
            if(i < kb) t += b[i];
            C[kc++] = t % 10;
            t /= 10;
        }
        // 处理最后一个进位
        if(t != 0) C[kc++] = t;
    }
}
```

# 高精度减法

```java
import java.util.*;

class Main{

    static int N = 100010;
    static int[] A = new int[N];
    static int[] B = new int[N];
    static int[] C = new int[N];
    static int ka, kb, kc;
    // 判断是否是a>=b
    public static boolean cmp(int[] a, int[] b){
        if(ka != kb) return ka > kb;
        // 从高位开始判断
        for(int i = ka - 1; i >= 0; i--) 
            if(a[i] != b[i]) return a[i] >= b[i];
        return true;
    }

    public static void sub(int[] a, int[] b){
        // 一定要注意这个按道理，应该是最大的那个长度
        for(int i = 0, t = 0; i < ka || i < kb; i ++){
            t = a[i] - t; // 当前为减去进位
            if(i < kb) t -= b[i]; // 如果b还有值话
            // 保留当前位置
            C[kc ++] = (t + 10) % 10;
            if(t < 0) t = 1; // 之前的进位加上一个1
            else t = 0;
        }
        // 最后取出前导零的操作
        while(kc > 1 && C[kc - 1] == 0) kc --;
    }

    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        String a = sc.next();
        String b = sc.next();
        // 转成数组
        for(int i = a.length() - 1; i >= 0; i--) A[ka ++] = a.charAt(i) - '0';
        for(int i = b.length() - 1; i >= 0; i--) B[kb ++] = b.charAt(i) - '0';
        if(cmp(A,B)){
            sub(A,B);
        }else{
            sub(B,A);
            System.out.print("-");
        }
        // 直接输出
        for(int i = kc - 1; i >= 0; i--) System.out.print(C[i]);
    }

}

```

# 高精度乘法



# 高精度除法

