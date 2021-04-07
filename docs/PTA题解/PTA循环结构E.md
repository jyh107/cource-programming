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