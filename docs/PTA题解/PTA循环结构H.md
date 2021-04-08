# 循环结构 PTA

PTA 循环结构 HARD。

## 加点优化

掌握一些常见的算法很有必要，部分较难的算法仅仅给出代码示例，感兴趣的可以自行学习。

如果看不懂，不必死磕。

### 7-2 含 8 的数字的个数

暴力是显然的，为 $O(n \log n)$。

```c
int main() {
    int a, b;
    scanf("%d %d", &a, &b);
    int sum = 0;
    for (int i = a; i <= b; i++) {
        int ti = i;
        while(ti > 0) {
            if(ti % 10 == 8) {
                sum++;
                break;
            }
            ti /= 10;
        }
    }
    printf("%d", sum);
    return 0;
}
```

假如输入的是 `1 123456987`，在我的电脑上大概需要运行 10 秒钟，用 PTA 在线测试则会超时。

这里通过另一道题 [P1980 计数问题](https://www.luogu.com.cn/problem/P1980)，来引出 **数位 DP** 。

> 在 $[1,n]$ 的所有整数中，数码 $x$ 出现了几次？

注意 $888$ 在原题中算出现 $1$ 次，在这题算出现 $3$ 次。

利用小学奥数中的一些计数技巧，不用计算机我们也可以求出答案。

> 假设 $n=728,x=7$。
> 
> 个位：$73$ 个，$7$，$17$，$\cdots$，$727$。
> 
> 十位：$70$ 个，$70\sim79$，$170\sim179$，$\cdots$，$670\sim679$。
> 
> 百位：$29$ 个，$700 \sim 728$。
> 
> 故总计为 $73+70+29 = 172$。

据此，我们可以写出 $x\ne 0$ 的解。不难看出是 $O(\log n)$ 的。

```c
int addup(int n, int x) {
    int ans = 0, m = 1;
    while(m <= n){
        int a=n/(m*10), b=n/m%10, c=n%m;
        if(b > x)
            ans += a * m + m;
        else if(b == x)
            ans += a * m + c + 1;
        else
            ans += a * m;
        m *= 10;
    }
    return ans;
}
```

回到原题，我们可以用同样的思想。记 $f_x(n) = f(x)$ 是 $1$ 到 $n$ 中数码 $x$ 出现的次数，所求即 $f_8(b) - f_8(a-1)$。

第一步是预处理 $f(10^t)$，后面将把任意的 $n$ 分解为一系列 $10^t$  的组合。

- 首先 $f(10) = 1$。对于 $10 \sim 19$ 和 $20 \sim 29$，因为首位数不贡献，可把这些区间看作相似的。只有 $80 \sim 89$ 是特殊的。

- 对于 $f(10^2)$，除了特殊的 $80$ 至 $89$，剩下都可看作相似的 $9$ 个 $f(10)$，共记 $9f(10) + 10 = 19$。

- 同样的对于 $f(10^3)$，除了特殊的 $800$ 至 $899$，剩下都可看作相似的 $9$ 个 $f(10)$，共记 $9f(10^2) + 10^2 = 272$。

记 $a_i = f(10^i)$，可以抽象出递推关系，提前预处理

$$a_{i+1} = 9a_{i} + 10^i, a_1 = 1$$

假如要计算的 $x=123456987$，从高到低位逐位分析。

- 首先，最高位的 $1$ 表示有 $1$ 个 $f(10^8)$。

- 次高位的 $2$ 表示有 $2$ 个 $f(10^7)$。

- 直到 $9$，表示有 $8$ 个 $f(10^2)$ 和特殊的 $100$ 个 $800\sim 899$。

- 接下来是 $8$ ，表示有 $8$ 个 $f(10)$，以及特殊且被截断的 $80\sim 87$。因为截断已经计数了，跳出循环。

综上，我们可以写出代码，它的复杂度是 $O(\log n)$。

```c
int aa[20] = {0};

int addup(int n, int x) {
    int m = 1, i = 0;
    while(m <= n) {
        i++; m *= 10;
    }
    int ans = 0;
    while(m > 0) {
        int t = n / m;
        n = n % m;
        if (t < x) {
            ans += t * aa[i];
        } else if (t > x) {
            ans += (t - 1) * aa[i] + m;
        } else {
            ans += t * aa[i] + n + 1;
        }
        i--; m /= 10;
    }
    return ans;
}

int main() {
    int a,b;
    scanf("%d %d", &a, &b);
    int m = 1;
    for(int i = 1; i <= 9; i++) {
        aa[i] = aa[i-1] * 9 + m;
        m *= 10;
    }
    int ans = addup(b,8) - addup(a-1, 8);
    printf("%d", ans);
    return 0;
}
```

### 7-5 输出 2 到 n 之间的全部素数

暴力试除法是能过的，为 $O(n\sqrt n)$。

```c
int isprime(int n) {
    if(n < 3)
        return n == 2;
    if(n % 2 == 0)
        return 0;
    int sn = (int)sqrt(n*1.0);
    for(int i = 3;i <= sn; i += 2)
        if(n % i == 0)
            return 0;
    return 1;
}

int cnt,prime[20000001];
void init(int n) {
    for(int i = 2; i <= n; i++) {
        if(isprime(i)) {
            prime[++cnt] = i;
        }
    }
}

int main() {
    int n;
    scanf("%d", &n);
    init(n);
    for(int i = 1; i <= cnt - 1; i++) {
        printf("%6d", prime[i]);
        if(i % 10 == 0)
            printf("\n");
    }
    printf("%6d", prime[cnt]);
    return 0;
}
```

接下来介绍筛法，把 $1 \sim n$ 的所有数字对应到一个数组，在数组上做标记来表示这个数不是质数，即筛去。剩下的自然都是质数。

首先是埃氏筛，它的复杂度是 $O(n\log\log n)$。我们从 $2$ 开始，将 $2$ 的倍数筛去；其次是 $3$，将 $3$ 的倍数筛去；$4$ 已经被筛去了，接下来是 $5$，把 $5$ 的倍数筛去……一直筛到 $n$。

放个维基的 GIF

![Eratosthenes](https://pic.leetcode-cn.com/1606932458-HgVOnW-Sieve_of_Eratosthenes_animation.gif)

实现如下

```c
int notp[10000001];
int prime[2000001], cnt;
void init(int n) {
    for (int i = 2; i <= n; i++) {
        if (!notn[i]) {
            prime[++cnt] = i;
            int tn = n / i;
            for (int j = i; i <= tn; i++)
                notn[i * j] = 1;
        }
    }
}
```

线性筛的复杂度更为优秀，是 $O(n)$，因为每个数只会被筛一次。

```c
int notp[10000001];
int prime[2000001], cnt;
void init(int n) {
    for (int i = 2; i <= n; i++) {
        if (!notp[i])
            prime[++cnt] = i;
        int t = n / i;
        for (int j = 1; i <= cnt; i++) {
            if(prime[j] > t)
                break;
            notp[i * prime[j]] = 1;
            if (i%prime[j] == 0)
                break;
        }
    }
}
```

### 7-26 判断素数

试除法不再详述

```c
int isprime(int n) {
    if(n < 3)
        return n == 2;
    if(n % 2 == 0)
        return 0;
    int sn = (int)sqrt(n*1.0);
    for(int i = 3;i <= sn; i += 2)
        if(n % i == 0)
            return 0;
    return 1;
}
```

常见的素性测试方法还有 Miller-Rabbin 方法，通过快速幂利用二次探测定理， $O(\log n)$。

需要些许数论知识，仅在此示范不做讲解

```c
ll power(ll a, ll b, ll p) {
    ll rst = 1 % p;
    for(; b > 0; b >>= 1) {
        a = a * a % p;
        if (b & 1)
            rst = a * rst % p;
    }
    return rst;
}

int miller_rabbin(int n) {
    if (n < 3)
        return (n == 2);
    int a = n - 1, b = 0;
    while (1 - (a & 1)) {
        a >>= 1;
        ++b;
    }
    int prime[10] = {2, 7, 61};
    for (int i = 0; i <= 2; i++) {
        int x = prime[i];
        if (n == x)
            return 1;
        ll v = power(x, a, n);
        if (v == 1 || v == n - 1)
            continue;
        int j;
        for (j = 0; j < b; j++) {
            v = v * v % n;
            if (v == n - 1)
                break;
        }
        if (j >= b)
            return 0;
    }
    return 1;
}
```