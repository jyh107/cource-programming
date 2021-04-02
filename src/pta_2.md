# 循环结构 PTA

我确认这部分的代码可以运行于 gcc、clang 等现代编译器，能通过 PTA 的评测。为了突出主体，我省略了头文件等不重要的内容。

一些题有多解，不必拘于一种写法。鉴于一些题本来就不是循环结构的内容，我决定按照最适合的解法讲解，可能会有部分题用到后面的知识。

水平有限，文中可能有诸多错误，还请谅解。如果有更好的解法，欢迎讨论。后续更正不再发放 PDF。

## 约定

随着程序逐渐复杂，我决定介绍一些算法竞赛中常用的定义，来简化我们的程序。

```c
typedef long long ll;
#define _fora(i,a,n) for(int i=(a);i<=(n);i++)
#define _forz(i,a,n) for(int i=(a);i>=(n);i--)
```

即 `ll` 是 `long long` 类型的简写，能够带来比 `int` 更大的范围。

同样， `_fora` 和 `_forz` ，我尽量避免在讲解中使用它，感兴趣的可以尝试。

## 时间复杂度

可能已经有同学察觉到，尽管很多写法都可以通过测试，可它们并不是一样快的。

比如，求 

\\[\sum_{i=1}^n\sum_{j=1}^ij = \sum_{i=1}^n\frac{i(i+1)}{2} = \frac{1}{6}n(n+1)(n+2)\\]

我们可以写出四种写法

```c
int sum0(int n) { // 不会真有人这么写吧
    int sum = 0;
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= i; j++)
            for (int k = 1; k <= j; k++)
                sum++;
    return sum;
}

int sum1(int n) {
    int sum = 0;
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= i; j++)
            sum += j;
    return sum;
}

int sum2(int n) {
    int sum = 0;
    for (int i = 1; i <= n; i++)
        sum += i * (i + 1) / 2;
    return sum;
}

int sum3(int n) {
    return n * (n + 1) * (n + 2) / 6;
}
```

可以得出， `sum0` 累加执行的次数是 、\\(\dfrac{1}{6}(n^3+3n^2+2n)\\) ， `sum1` 累加执行的次数是 \\(\dfrac{1}{2}(n^2+n)\\) ，而 `sum2` 需要 \\(n\\) 次运算， `sum3` 只需要 \\(1\\) 次。

尽管电脑的运行速度很快，可并不是无限快。当 \\(n\\) 较大时， 比如 \\(n=10000\\)，`sum0` 需要接近 \\(10^{12}\\) 次，`sum1` 大致 \\(10^8\\) 次，`sum2` 大致 \\(10^4\\)，而 `sum3` 还是 \\(1\\) 次，差距非常明显。

为了凸显算法的运行时间和 \\(n\\) 的关系，在表示算法的时间复杂度时常常略去常数和低阶项，系数也会被忽略。比如

\\[\dfrac{1}{6}(n^3+3n^2+2n) \sim \dfrac{1}{6}n^3 \sim n^3\\]

我们可将上述四种算法的时间复杂度记为 \\(O(n^3)\\)， \\(O(n^2)\\)，\\(O(n)\\) 和 \\(O(1)\\)。常见的一些时间复杂度还有 \\(O(2^n)\\)，\\(O(\log n)\\)，\\(O(n\log n)\\) 等等。

时间复杂度本身是很复杂的概念，有兴趣的可以查阅资料。因为时间很容易测不准，不能简单的以运行时间评判程序的优劣，尤其运行时间极其短时。

相对于充斥着各种奇妙优化的算法，朴素的算法常称为暴力。

我们应尽量思考，尝试发现更优的解法。

## 简单循环

大部分题还是常规的。

### 7-1 输出等腰杨辉三角

样例有毒，仔细读题。应该没有人会真的写循环吧（

连续的字符常量自动合并，示范如下。

```c
int main() {
    printf(
        "             1\n"
        "           1   1\n"
        "         1   2   1\n"
        "       1   3   3   1\n"
        "     1   4   6   4   1\n"
        "   1   5  10  10   5   1\n"
    );
    return 0;
}
```

### 7-4 统计单词数量

没给数据，猜一手 `1000086`。

```c
int isAlpha(int x) {
    if ('A' <= x && x <= 'Z')
        return 1;
    else if ('a' <= x && x <= 'z')
        return 1;
    return 0;
}

char s[1000086];

int main() {
    gets(s);
    int len = strlen(s);
    int p = isAlpha(s[0]);
    int sum = 0;
    for (int i = 1; i <= len; i++) {
        int t = isAlpha(s[i]);
        if (p && !t)
            sum++;
        p = t;
    }
    printf("%d", sum);
    return 0;
}
```

## 加点优化

掌握一些常见的算法很有必要，部分较难的算法仅仅给出代码示例，感兴趣的可以自行学习。

如果看不懂，不必死磕。

### 7-2 含 8 的数字的个数

暴力是显然的，为 \\(O(n \log n)\\)。

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

假如输入的是 `1 123456987`，在我的电脑上大概需要 10 秒钟，用 PTA 在线测试时会超时。

这里给出另一道题 [P1980 计数问题](https://www.luogu.com.cn/problem/P1980)，引出 **数位 DP** 。

> 在 \\([1,n]\\) 的所有整数中，数码 \\(x\\) 出现了几次？

注意 \\(888\\) 在原题中算 \\(1\\) 次，在这题算 \\(3\\) 次。

利用小学奥数中的一些计数技巧，不用计算机我们也可以求出答案。

> 假设 \\(n=728,x=7\\)。
> 
> 个位：\\(73\\) 个，\\(7\\)，\\(17\\)，\\(\cdots\\)，\\(727\\)。
> 
> 十位：\\(70\\) 个，\\(70\sim79\\)，\\(170\sim179\\)，\\(\cdots\\)，\\(670\sim679\\)。
> 
> 百位：\\(29\\) 个，\\(700 \sim 728\\)。
> 
> 故总计为 \\(73+70+29 = 172\\)。

据此，我们可以写出 \\(x\ne 0\\) 的解。不难看出是 \\(O(\log n)\\) 的。

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

回到原题，我们可以用同样的思想。第一步预处理 \\(10^n\\) 中 \\(8\\) 出现的次数。

- 首先 \\(10\\) 的预处理是 \\(1\\)。

- \\(100\\) 则是由 \\(9\\) 个类似 \\(10\\) 的小块和 \\(10\\) 个的 \\(80\sim 89\\)，共记 \\(9 \times 1 + 10 = 19\\)。

- \\(1000\\) 则是由 \\(9\\) 个类似 \\(100\\) 的小块和 \\(100\\) 个的 \\(800\sim 899\\) 的数，共记 \\(9 \times 19 + 100 = 271\\)。

可以抽象出递推关系，提前预处理

\\[a_{i+1} = 9a_{i} + 10^i,a_1 = 1\\]

假如要计算的 \\(x=123456987\\)，从高到低位逐位分析。

- 首先高位的 \\(1\\) 表示有 \\(1\\) 个 \\(10^8\\) 的预处理。

- 次高位的 \\(2\\) 表示有 \\(2\\) 个 \\(10^7\\) 的预处理。

- 直到 \\(9\\)，表示有 \\(8\\) 个 \\(10^2\\) 的预处理和 \\(100\\) 个的 \\(800\sim 899\\)。

- 接下来是 \\(8\\) ，表示有 \\(8\\) 个 \\(10\\) 的预处理，以及被截断的 \\(80\sim 87\\)。因为是 \\(8\\)，直接跳出。

综上，我们可以写出代码，它的复杂度是 \\(O(\log n)\\)。

```c
int aa[20] = {0};

int addup(int n, int x) {
    int m = 1, i = 0;
    while(m <= n) {
        i++; m *= 10;
    }
    int ans = 0;
    while(m) {
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

暴力试除法是能过的，为 \\(O(n\sqrt n)\\)。

```c
int isprime(int n) {
    if(n < 3)
        return n == 2;
    if(n % 2 == 0)
        return 0;
    for(int i = 3;i <= (int)sqrt(n*1.0); i += 2)
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

接下来介绍筛法，把 \\(1 \sim n\\) 的所有数字对应到一个数组，在数组上做标记来表示这个数不是质数，即筛去。剩下的自然都是质数。

首先是埃氏筛，它的复杂度是 \\(O(n\log\log n)\\)。我们从 \\(2\\) 开始，将 \\(2\\) 的倍数筛去；其次是 \\(3\\)，将 \\(3\\) 的倍数筛去；\\(4\\) 已经被筛去了，接下来是 \\(5\\)，把 \\(5\\) 的倍数筛去……一直筛到 \\(n\\)。

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

线性筛的复杂度更为优秀，是 \\(O(n)\\)，因为每个数只会被筛一次。

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
    for(int i = 3;i <= (int)sqrt(n*1.0); i += 2)
        if(n % i == 0)
            return 0;
    return 1;
}
```

常见的素性测试方法还有 Miller-Rabbin 方法，通过快速幂利用二次探测定理， \\(O(\log n)\\)。

需要些许数论知识，仅在此示范不做讲解

```c
ll power(ll a,ll b,ll p) {
    ll rst = 1%p;
    for(;b>0;b>>=1) {
        a=a*a%p;
        if(b&1)
            rst=a*rst%p;
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