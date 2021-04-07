# 选择结构 PTA

我确认这部分的代码可以运行于 gcc、clang 等现代编译器，能通过 PTA 的评测。为了突出主体，我省略了头文件等不重要的内容。

一些题有多解，不必拘于一种写法。鉴于一些题本来就不是选择结构的内容，我决定按照最适合的解法讲解，可能会有部分题用到后面的知识。

水平有限，文中可能有诸多错误，还请谅解。如果有更好的解法，欢迎讨论。后续更正不再发放 PDF。

## 简单判断

这一部分是有关于简单判断的。

### 7-3 春夏秋冬

```c
int main() {
    int n;
    scanf("%d", &n);
    n = n % 100;
    if (n <= 2) {
        printf("winter\n");
    } else if (n <= 5) {
        printf("spring\n");
    } else if (n <= 8) {
        printf("summer\n");
    } else if (n <= 11) {
        printf("autumn\n");
    } else {
        printf("winter\n");
    }
    return 0;
}
```

### 7-4 判断能否被 3，5，7 整除

注意末尾不能有空格，可以通过 `flag` 来判断。

```c
int main() {
    int n;
    scanf("%d", &n);
    int flag = 0;
    if (n % 3 == 0) {
        printf("3");
        flag = 1;
    }
    if (n % 5 == 0) {
        if (flag)
            printf(" ");
        printf("5");
        flag = 1;
    }
    if (n % 7 == 0) {
        if (flag)
            printf(" ");
        printf("7");
        flag = 1;
    }
    if (!flag)
        printf("n");
    return 0;
}
```

### 7-5 有一门课不及格的学生

当低于 $60$ 时 `flag + 1`，只需判断 `flag` 是否恰为 $1$ 。

```c
int main() {
    int a,b;
    scanf("%d %d", &a, &b);
    int flag = 0;
    if (a < 60)
        flag++;
    if (b < 60)
        flag++;
    if (flag == 1)
        printf("1");
    else
        printf("0");
    return 0;
}
```

### 7-6 骑车与走路

设距离为 $x$，则骑车和步行所花的时间分别为

$$\begin{aligned}t_1 &= 27 + x/3 + 23\\t_2&=x/1.2\end{aligned}$$

可以直接据此计算再判断，也可以算出关键点 $x=100$ 再判断。

```c
int main() {
    int n;
    scanf("%d", &n);
    if (n < 100)
        printf("Walk");
    else if(n == 100)
        printf("All");
    else
        printf("Bike");
    return 0;
}
```

### 7-10 于龙加

题目有坑，结果不能以 $0$ 开头。

```c
int main() {
    int a, b;
    scanf("%d %d", &a, &b);
    if (a == 0)
        printf("%d", b);
    else
        printf("%d%d", a, b);
    return 0;
}
```

### 7-13 洛希极限

题目的难点主要在于看不懂，我也帮不了什么（

```c
int main() {
    int type;
    double f1,f2;
    scanf("%lf %d %lf", &f1, &type, &f2);
    if (type == 0) {
        f1 *= 2.455;
    } else {
        f1 *= 1.26;
    }
    printf("%.2lf ", f1);
    if (f1 > f2)
        printf("T_T");
    else
        printf("^_^");
    return 0;
}
```

### 7-14 最简单的 if - else 练习: 乘法还是加法？

```c
int main() {
    double f1,f2;
    scanf("%lf %lf", &f1, &f2);
    int op;
    scanf("%d", &op);
    if (op == 0) {
        printf("%.2lf", f1 + f2);
    } else {
        printf("%.2lf", f1 * f2);
    }
    return 0;
}
```

### 7-21 西安距离

```c
int main() {
    int a, b, c, d;
    scanf("%d %d %d %d", &a, &b, &c, &d);
    printf("%d", abs(a-c) + abs(b-d));
    return 0;
}
```

### 7-24 编程实现两个分数相加

通分，用 gcd 化简。

$$\frac{a}{b}+\frac{c}{d} = \frac{ad+bc}{bd}$$

```c
int gcd(int a, int b) {
    return a ? gcd(b%a, a) : b;
}

int main() {
    int a,b,c,d;
    scanf("%d/%d+%d/%d", &a, &b, &c, &d);
    int e = a*d + b*c;
    int f = b * d;
    int g = gcd(e,f);
    printf("%d/%d+%d/%d=%d/%d", a, b, c, d, e/g, f/g);
    return 0;
}
```

### 7-25 分支结构

题目有坑，非字母无需输出。

```c
int main() {
    char d;
    scanf("%c", &d);
    if ('A' <= d && d <= 'Z') {
        printf("%d\n", d);
    } else if ('a' <= d && d <= 'z') {
        printf("%c\n", d - 32);
    }
    return 0;
}
```

### 7-26 有多少位是7？

取模可以得到末位，除 $10$ 再取模可以得到次末位的数字。因为不超过四位数，反复四次即可。

字符串数组也可以。

```c
int main() {
    int n;
    scanf("%d", &n);
    int ans = 0;
    for (int i = 0; i < 4; i++) {
        if (n % 10 == 7)
            ans++;
        n /= 10;
    }
    printf("%d\n", ans);
    return 0;
}
```

### 7-27 判断体质完整版

```c
int main() {
    double f1, f2;
    scanf("%lf %lf", &f1, &f2);
    double bmi = f1 / f2 / f2;
    if (bmi < 18.5)
        printf("偏瘦");
    else if (bmi < 24)
        printf("正常");
    else if (bmi < 28)
        printf("偏胖");
    else if (bmi < 40)
        printf("肥胖");
    else
        printf("极重度肥胖");
    return 0;
}
```

### 7-29 多分支表达-倍数问题

我想了一会既是 $5$ 的倍数又是 $3$ 的倍数会怎样，没想出来。打算先交一次看看，结果过了。。

```c
int main() {
    int a;
    scanf("%d", &a);
    int f1, f2;
    f1 = f2 = 0;
    if (a % 3 == 0)
        f1 = 1;
    if (a % 5 == 0)
        f2 = 1;
    if (f1 && !f2) {
        printf("%d", a % 5);
    } else if (!f1 && f2) {
        printf("%d", a % 3);
    } else if (!f1 && !f2) {
        printf("%d", a % 15);
    }
    return 0;
}
```

### 7-32 分段计算居民水费

```c
int main() {
    double x;
    scanf("%lf", &x);
    if (x < 0) {
        printf("Input Data error!");
    } else if (x <= 15) {
        printf("%.2lf", 4 * x / 3);
    } else {
        printf("%.2lf", 2.5 * x - 17.5);
    }
    return 0;
}
```

### 7-35 计算分段函数（双分支）

```c
int main() {
    double x;
    scanf("%lf", &x);
    if(x == 0) {
        printf("%.2lf", 0.0);
    } else {
        printf("%.2lf", 1 / x);
    }
    return 0;
}
```

## 最值问题

寻找最值有多种方法，这里介绍一种通用的方法。

关键的，对于数 $a,b$ 取最大值只需

```c
int max(int a, int b) {
    if (a < b)
        return b;
    return a;
}
```

或者简写成三目运算符

```c
return a < b ? b : a;
```

若需要取一个数组的最大值，可以通过反复取 max。

```c
int a[N];
int m = a[0];
for (int i = 0; i < N; i++)
    m = max(a[i], m);
```
### 7-16 找最大数和最小数

```c
int main() {
    int a, b, c;
    scanf("%d %d %d", &a, &b, &c);
    int max = a > b ? a : b;
    max = max > c ? max : c;
    int min = a < b ? a : b;
    min = min < c ? min : c;
    printf("max=%d,min=%d", max, min);
    return 0;
}
```

### 7-31 判断三角形的形状

题目引号没标全，输出 `简单三角形`。可以直接判断，也可以像我一样排序后再判断。

若需取中间值，可以把三数求和后再减去最大最小值，剩下的自然是中间值。若数字范围很大，三数求和会溢出，可以用异或。

```c
int main() {
    int a, b, c;
    scanf("%d %d %d", &a, &b, &c);
    int max = a > b ? a : b;
    max = max > c ? max : c;
    int min = a < b ? a : b;
    min = min < c ? min : c;
    int mid = a + b + c - min - max;
	// 如果怕溢出 int ，请使用异或
    // int mid = a ^ b ^ c ^ min ^ max;
    if (min + mid <= max)
        printf("NO");
    else if (min == max)
        printf("等边");
    else if (min == mid && min*min + mid*mid == max*max)
        printf("等腰直角");
    else if (min == mid || max == mid)
        printf("等腰");
    else if (min*min + mid*mid == max*max)
        printf("直角");
    else
        printf("普通三角形");
    return 0;
}
```

## 嵌套判断

当分类只需简单的一层时，简单的判断即可。当分类错综复杂时，我们需要谨慎的理清它们的关系。

当一族分类完全的包含于一种分类下时，建议使用 `if` 嵌套，利用层次关系组织我们的程序。倘若摊成一层，不但增大了思考的难度，还增加了出问题的概率。

清晰的代码是最好的注释。

### 7-8 简单计算器

简单分类，注意 `%c` 需要严格对应。

```c
int main() {
    int a,b;
    char op;
    scanf("%d %d %c", &a, &b, &op);
    int ans;
    int flag = 1;
    if (op == '+') {
        printf("%d", a + b);
    } else if (op == '-') {
        printf("%d", a - b);
    } else if (op == '*') {
        printf("%d", a * b);
    } else if (op == '/') {
        if (b == 0)
            printf("Divided by zero!\n");
        else
            printf("%d", a / b);
    } else {
        printf("Invalid operator!\n");
    }
    return 0;
}
```

### 7-20 【分支】【--时制转换A--】

题目描述有误，读入需要加冒号，即 `scanf("%d:%d", &h, &m)` 。

注意细节，$12$ 点的情况需要详细考虑。

```c
int main() {
    int h, m;
    scanf("%d:%d", &h, &m);
    if (h < 12) {
        printf("%02d:%02d AM\n", h, m);
    } else if (h == 12) {
        if (m == 0)
            printf("%02d:%02d AM\n", h, m);
        else
            printf("%02d:%02d PM\n", h, m);
    } else {
        printf("%02d:%02d PM\n", h - 12, m);
    }
    return 0;
}
```


### 7-28 多分支表达-数据奇偶判断

```c
int main() {
    int a, b;
    scanf("%d,%d", &a, &b);
    if (a == 0 || b == 0)
        return 0;
    if (a % 2 == 0) {
        if(b % 2 == 0)
            printf("%d+%d=%d", a, b, a + b);
        else
            printf("%d/%d=%d", a, b, a / b);
    } else {
        if(b % 2 == 0)
            printf("%d*%d=%d", a, b, a * b);
        else
            printf("%d-%d=%d", a, b, a - b);
    }
    return 0;
}
```

## 阶梯付费

对于这种阶梯付费的问题，每一档可以记作：超过 $x_i$ 元时，超出部分费率 $k_i$。

于是我们可以令 $f_i$ 为超出价格，有

$$f_i = \begin{cases} p-x_i&,p>x_i\\0&,p \leqslant x_i \end{cases}$$

那么总付费可以表示为 $\sum k_if_i$。


### 7-7 计算邮资

我们知道，C 语言中的除法是向下取整。

$$p/q = \left\lfloor \frac{p}{q} \right\rfloor$$

于是向上取整可以表示为

$$\left\lceil \frac{p}{q} \right\rceil = \left\lfloor \frac{p+q-1}{q} \right\rfloor = \left\lfloor \frac{p-1}{q} \right\rfloor + 1= (p-1)/q + 1$$

如果使用 `if` 判断整除的写法，对于分母为 $1$ 的特例很可能出错，我展示的写法兼容这种特例。

```c
int main() {
    int n;
    char c;
    scanf("%d %c", &n, &c);
    int ans = 8;
    if (n > 1000) {
        n = n - 1000;
        if (n < 0)
            n = 0;
        n = (n - 1) / 500 + 1;
        ans += n * 4;
    }
    if (c == 'y')
        ans += 5;
    printf("%d", ans);
    return 0;
}
```


### 7-15 超市购物打折

```c
int main() {
    double t;
    scanf("%lf", &t);
    double f1, f2, f3;
    f1 = f2 = f3 = 0;
    if (t <= 50) {
        f1 = t;
    } else {
        f1 = 50;
        t -= 50;
        if (t <= 100) {
            f2 = t;
        } else {
            f2 = 100;
            t -= 100;
            f3 = t;
        }
    }
    printf("%.2lf", f1 + f2*.9 + f3*.8);
    return 0;
}
```

### 7-18 计算出租车费

题目有坑，当 $x=0$ 时应当付 $0$ 元。

```c
int main() {
    double x;
    scanf("%lf", &x);
    if (x == 0) {
        printf("0.0");
        return 0;
    }
    double f1, f2;
    f1 = f2 = 0;
    if (x > 3)
        f1 = x - 3;
    if (x > 10)
        f2 = x - 10;
    printf("%.1lf", 11.0 + f1*2.4 + f2*0.96);
    return 0;
}
```

## 利用数组

一部分题其实 `if - else` 或 `switch` 都能做，我只是觉得数组更适合。

### 7-17 帮小明出主意

可以 if - else，也可以 switch，我觉得数组比较好。

```c
char s[][20] = {
    "answer = First",
    "answer = Second",
    "answer = Third",
    "answer = Fourth"
};

int main() {
    int a;
    scanf("%d", &a);
    a = a % 4;
    printf("%s", s[a]);
    return 0;
}
```

### 7-19 小燕爱偶数

使用数组 $a$ 记录所有的偶数，$p$ 是数组的下标。

当遇到偶数 $t$ 时，令 $a_p = t$，自增 $p$。

这样可以实现不断放入，令 $i$ 遍历 $0 \to p$ 输出 $a_i$ 即可。

不要忘了末尾没有空格。

```c
int a[10086], p = 0;

int main() {
    int n;
    scanf("%d", &n);
    for (int i = 0; i < n; i++) {
        int t;
        scanf("%d", &t);
        if (t % 2 == 0)
            a[p++] = t;
    }
    printf("%d\n", p);
    if (p > 0)
        printf("%d", a[0]);
    for (int i = 1; i < p; i++)
        printf(" %d", a[i]);
    return 0;
}
```

### 7-22 前天是哪天

利用 7-9 计算当月天数的方法，当需要退位时计算一下。

```c
int month[] = {0,31,28,31,30,31,30,31,31,30,31,30,31};

int main() {
    int y,m,d;
    scanf("%d %d %d",&y,&m,&d);
    d -= 2;
    if (d <= 0) {
        m--;
        if (m <= 0) {
            y--;
            m = 12;
        }
        int day = month[m];
        int flag = (y % 4 == 0 && y % 100 != 0);
        if (m == 2)
            if (y % 400 == 0 || flag)
                day++;
        d = day + d;
    }
    printf("%d-%d-%d", y, m, d);
    return 0;
}
```
### 7-23 根据输入的数字，输出需要上课的节数

```c
char s[][80] = {
    "",
    "星期一 8节课",
    "星期二 10节课",
    "星期三 6节课",
    "星期四 8节课",
    "星期五 6节课",
    "今天没有课，可以好好休息一下啦！",
    "今天没有课，可以好好休息一下啦！"
};

int main() {
    int d;
    scanf("%d", &d);
    printf("%s", s[d]);
    return 0;
}
```

### 7-30 输入一个数字，输出其对应的星期几的英文单词

```c
char s[][10] = {
    "",
    "Monday",
    "Tuesday",
    "Wednesday",
    "Thursday",
    "Friday",
    "Saturday",
    "Sunday"
};

int main() {
    int a;
    scanf("%d", &a);
    if (1 <= a && a <= 7) {
        printf("%s",s[a]);
    } else {
        printf("输入错误！");
    }
    return 0;
}
```

### 7-33 输出星期名

```c
char s[][10] = {
    "Sunday",
    "Monday",
    "Tuesday",
    "Wednesday",
    "Thursday",
    "Friday",
    "Saturday"
};

int main() {
    int a;
    scanf("%d", &a);
    if (0 <= a && a <= 6) {
        printf("%s", s[a]);
    } else {
        printf("None");
    }
    return 0;
}
```

## 细节处理

这里的题需要些许思考。

### 7-1 今天之前的第 n 天是星期几

求星期 $x$ 的 $n$ 天前是星期几，朴素的想法是对 $x$ 自减 $n$ 次，特判当 $x=1$ 时后继是 $7$。

```c
int main() {
    int x, n;
    scanf("%d %d", &x, &n);
    for (int i = 0; i < n; i++) {
        x--;
        if (x == 0)
            x = 7;
    }
    printf("%d", x);
    return 0;
}
```

很容易想到利用取模来优化。为了方便，将星期一到星期天映射到 $0\sim 6$。那样第 $x-n$ 天是星期几，完全只和其对 $7$ 的余数有关。

唯一的问题是负数取模，它的结果可能与你的想象不同，我们应当避免，感兴趣的可以查看 [cppreference](https://zh.cppreference.com/w/c/language/operator_arithmetic#.E4.BD.99.E6.95.B0)。容易验证

$$x - n \bmod 7 \equiv x - n \pmod 7$$

上式左侧显然大于 $-7$，于是有

```c
int main() {
    int x, n;
    scanf("%d %d", &x, &n);
    n = n % 7;
    x -= 1;
    x = (x - n + 7) % 7;
    printf("%d", x + 1);
    return 0;
}
```

### 7-9 日期识别 2

本题略要思考。首先因为分隔符未知，可以使用 `%c` 吸收掉。

```c
int main() {
    int a,b,c;
    char p;
    scanf("%d%c%d%c%d", &a, &p, &b, &p, &c);
    int flag = 0;
    flag += test(a, b, c);
    flag += test(b, c, a);
    flag += test(c, a, b);
    flag += test(c, b, a);
    flag += test(a, c, b);
    flag += test(b, a, c);
    if(flag)
        printf("%d", flag);
    else
        printf("Invalid Date!\n");
    return 0;
}
```

先特判掉不合法的数字，之后计算当前月份有多少天。

也可以用分支实现，但像这样没什么规律的，还是数组比较好。

```c
int month[] = {
    0,31,28,31,30,31,30,31,31,30,31,30,31
};

int test(int y, int m, int d) {
    if (y < 0)
        return 0;
    if (m <= 0 || m >= 13)
        return 0;
    int day = month[m];
    int flag = (y % 4 == 0 && y % 100 != 0);
    if (m == 2)
        if (y % 400 == 0 || flag)
            day++;
    if (d <= 0 || d > day)
        return 0;
    return 1;
}
```

当一行代码过长时，尽量分开写。过长的代码往往意味着复杂的逻辑，分开有助于理解。

也可以自己实现读入数字，示范如下。一般用这个读数字比 `scanf` 快的多，也叫做快读。

```c
int read() {
    int s = 0;
    char c = getchar();
    while (c >= '0' && c <= '9') {
        s = s * 10 + c - '0';
        c = getchar();
    }
    return s;
}
```


### 7-12 位置关系 A

比较有趣的数学题。定义圆心距 $d$ 为

$$d = \sqrt{(x_1-x_2)^2 + (y_1-y_2)^2}$$

将 $d$ 与 $|r_1+r_2|$ 和 $|r_1-r_2|$ 比较，分类讨论如下

- 当 $|r_1+r_2| < d$，两圆尚未接触，为外离 Separated。
- 当 $d = |r_1+r_2|$，两圆外切 Circumscribed。
- 当 $|r_1-r_2| < d < |r_1+r_2|$，两圆相交 Intersected。
- 当 $d = |r_1-r_2|$，两圆内切 Inscribed。
- 当 $0 \leqslant d < |r_1-r_2|$，两圆内含 Contained。

至于重合，开始特判掉即可。

```c
int main() {
    int x1, y1, r1, x2, y2, r2;
    scanf("%d %d %d", &x1, &y1, &r1);
    scanf("%d %d %d", &x2, &y2, &r2);

    int td = (x1-x2) * (x1-x2) + (y1-y2) * (y1-y2);
    int tr1 = (r1-r2) * (r1-r2);
    int tr2 = (r1+r2) * (r1+r2);

    if (td == 0 && tr1 == 0) {
        printf("Completely Overlapping");
    } else if (td < tr1) {
        printf("Contained");
    } else if (td == tr1) {
        printf("Inscribed");
    } else if (td < tr2) {
        printf("Intersected");
    } else if (td == tr2) {
        printf("Circumscribed");
    } else {
        printf("Separated");
    }
    return 0;
}
```



## 附录 · 私货

其实我正文里写了不少私货了（

### 关于未定义行为

未定义行为是很重要的概念。不知道你是否为这些代码的值苦恼过？

```c
i = ++i + i++;
i = i++ + 1;
f(++i, ++i);
```

未定义行为的含义是，出现什么结果都不奇怪，比如像段错误，程序闪退，电脑死机，系统崩溃，都有可能。甚至在两个电脑上结果不同，都不奇怪。

C 语言并不是教条主义的语言，它是先推广开才进行标准化的，因此 C/C++ 标准都是追述性的。编译器也是程序，我们需要给编译器充足的空间去进行代码优化，而不是做很多无用而详细的限制。

比如运算符的优先级和求值顺序无关，求值顺序是由 [序列点](https://zh.cppreference.com/w/c/language/eval\_order) 概念决定，序列点未指定的则不指定顺序。这属于实现编译器才需要了解的知识，我们没必要了解。我们总是可以通过把程序写的简炼，来避免通过复杂的知识确定程序的运行状况。

任何良好的程序不应该依赖未定义行为，甚至不应该使用不常见的写法。很多复杂的概念，你在编程里用了，除了把自己绕晕以外什么用也没有。但是就是有人以绕晕别人为荣，天天琢磨茴的四种写法，遇到问题最喜欢引经据典，我们一般讽刺作“语言律师”。

说了这么多，一言以蔽之：

> 不要写看不懂的代码。

### 关于代码风格

我的代码风格可能和很多人不同，但只要遵从统一规范的代码都是风格良好的。我比较喜欢大括号放在同一行，因为这样可以一页看更多的代码。

假如不进行格式化，我想你是没有心情看这一串的

```
bool miller_rabbin(int n)
{   int ppp[10] = {2,7,61};
    int a=n-1,b=0,j,v,x;
    if(n<3) return n==2;
    while(1-a&1) a>>=1,++b;
    for(int i=0;i<=2;i++){
    x = ppp[i];
    if(n==x) return true;
    v = power(x,a,n);
    if(v==1||v==n-1) continue;
    for(j=0;j<b;++j) {
    v = v*v%n; if(v==n-1) break; }
    if(j>=b) return false;
    } return true;
}
```

格式化，高亮

```cpp
bool miller_rabbin(int n) {
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
            return true;
        int v = power(x, a, n);
        if (v == 1 || v == n - 1)
            continue;
        int j;
        for (j = 0; j < b; j++) {
            v = v * v % n;
            if (v == n - 1)
                break;
        }
        if (j >= b)
            return false;
    }
    return true;
}
```

良好代码格式能够让程序本身的逻辑一目了然。

除了排版等要求不能太多空白时，采取紧凑的代码风格，其他时候尽可能把代码 **展开** 写。

具体的一些建议：

**1 最基本的是好好缩进**

代码是结构性的，良好的缩进可以体现出这种结构。

左大括号的缩进方式，缩进是用 space 还是 tab，这些争论倒无关紧要。风格统一就行。

**2 不要压行，一行只做一件事**

比如 `if` 条件后换行，内层缩进。

```c
if (condition)
    statement;
```

这样，条件是什么，语句是什么，一目了然。

功能不同的代码片段之间空行。

**3 重要的变量见名知意**

比如一堆 `int a,b,c,d,e,f;`，要费很大劲猜这个变量究竟是什么意思，可读性很差。

**4 尽可能延后变量的定义**

尽可能延后变量的定义，尽可能缩小变量的作用域，声明不要全在开头挤着。

在现代的编辑器中，我们可以很方便的查找出该变量在何处定义，定义时有什么注释。定义的上下文一般都是和这个变量有关的信息，有助于我们理解变量的作用。

同样，声明不要全在开头挤着，用到了再定义。

> 因此将自己的代码格式化再发送是一种礼貌。

### 后续学习

C 语言受底层影响很深。比如 `switch` 需要自己写 `break`，当了解到跳转表 Jump Table 后，反倒觉得很自然了。

归根结底，奇怪的不是 C 语言，而是 CPU 就是那样工作的。缺乏理解时，编程就像念咒语。

估计很多同学 C 语言学的差不多了吧，我介绍一种后续的学习方案。

很多学校在大一的程序设计之后会开一门计算机系统导论（ICS），使用的教材是 [《深入理解计算机系统》](https://book.douban.com/subject/26912767/) （CS:APP）。这门课引进自国外的 [CMU15-213](http://www.cs.cmu.edu/~./213/schedule.html) ，讲述了以程序员的视角（相对的 是系统设计视角）需要了解的计算机系统。读完后，你会去开始思考代码的底层运作原理，而不是把计算机当做黑盒。

这门课只是一门导论，带你领略整个计算机系统的宏观面貌，其细节将会在之后组成原理、操作系统、体系结构、网络等课程深入。

网上也有诸多资料，可以配合学习。

### 求值顺序测试

求值顺序是由 [序列点](https://zh.cppreference.com/w/c/language/eval_order) 概念决定，序列点未指定的则不指定顺序。

为了查看求值顺序，我们测试了如下程序

```c
int x;

int f() {
    int t;
    scanf("%d", &t);
    x = t;
    return t;
}

int main() {
    int ans = f() + f() * f();
    printf("%d %d", ans, x);
    return 0;
}
```

当你输入 `1 2 3` 时，此时 `vc6`，`gcc`，`clang` 都很统一的告诉你答案会是 `7 3`，这与我们的想法不符。这是值得信赖的规律吗？

我们可以让它更混乱一点

```c
int main() {
    printf("%d %d %d", f(), f(), f());
    return 0;
}
```

还是输入 `1 2 3`，答案就有很多种了

```shell
gcc   : 3 2 1
tcc   : 1 2 3
vc6   : 3 2 1
clang : 1 2 3
```

标准中明确指出了，序列点之间的副作用顺序未指定，因此这部分实验没有任何意义。