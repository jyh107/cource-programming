# MkDocs

我开始使用的是 [MdBook](https://rust-lang.github.io/mdBook/)，因为缺失一些重要的功能，不得不换到了 [MkDocs](https://squidfunk.github.io/mkdocs-material/)。

这里介绍一些 MkDocs 特有的格式。

尽量不要在标题中使用这些复杂的样式。

## 警告框

```md
!!! warning "警告"
    样式有 ： `octicons` `abstract` `info` `tip` `success` `example` `question` `warning` `failure` `danger` `bug` `quote`

!!! warning ""
    无标题式
```

!!! warning "警告"
    样式有 ： `octicons` `abstract` `info` `tip` `success` `example` `question` `warning` `failure` `danger` `bug` `quote`

!!! warning ""
    无标题式

警告框的形式很丰富，更多种类的示例见 [Admonitions](https://squidfunk.github.io/mkdocs-material/reference/admonitions/)。

## 折叠块

```md
??? bug "折叠"
    折叠

???+ bug "展开"
    展开
```

??? bug "折叠"
    折叠

???+ bug "展开"
    展开

## 代码块

代码块支持了很多额外样式。

    ```python hl_lines="2 3"
    def bubble_sort(items):
        for i in range(len(items)):
            for j in range(len(items) - 1 - i):
                if items[j] > items[j + 1]:
                    items[j], items[j + 1] = items[j + 1], items[j]
    ```

```python hl_lines="2 3"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```

## 标签页

```md
=== "C"

    ``` c
    #include <stdio.h>

    int main(void) {
    printf("Hello world!\n");
    return 0;
    }
    ```

=== "C++"

    ``` c++
    #include <iostream>

    int main(void) {
    std::cout << "Hello world!" << std::endl;
    return 0;
    }
    ```

=== "Haskell"

    偷偷告诉你我不会：）
```

=== "C"

    ``` c
    #include <stdio.h>

    int main(void) {
      printf("Hello world!\n");
      return 0;
    }
    ```

=== "C++"

    ``` c++
    #include <iostream>

    int main(void) {
      std::cout << "Hello world!" << std::endl;
      return 0;
    }
    ```

=== "Haskell"

    偷偷告诉你我不会：）

## 文本样式

支持很多额外的文本样式，有需要请直接查阅 [Formatting](https://squidfunk.github.io/mkdocs-material/reference/formatting/)。
