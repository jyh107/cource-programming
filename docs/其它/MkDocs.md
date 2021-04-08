# MkDocs

我开始使用的是 [MdBook](https://rust-lang.github.io/mdBook/)，因为缺失一些重要的功能，不得不换到了 [MkDocs](https://squidfunk.github.io/mkdocs-material/)。

这里介绍一些 MkDocs 特有的格式。

更详细的请阅读 [Cyent](https://cyent.github.io/markdown-with-mkdocs-material/syntax/main/)。

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

代码块支持背景高亮，支持更改代码起始行号。

    ```python hl_lines="2 3" linenums="2"
    def bubble_sort(items):
        for i in range(len(items)):
            for j in range(len(items) - 1 - i):
                if items[j] > items[j + 1]:
                    items[j], items[j + 1] = items[j + 1], items[j]
    ```

```python hl_lines="2 3" linenums="2"
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

额外的文本样式，有需要请直接查阅 [Formatting](https://squidfunk.github.io/mkdocs-material/reference/formatting/)。

## Primary Color

鼠标点击即可临时改变当前页主体颜色

<button data-md-color-primary="red">Red</button>
<button data-md-color-primary="pink">Pink</button>
<button data-md-color-primary="purple">Purple</button>
<button data-md-color-primary="deep-purple">Deep Purple</button>
<button data-md-color-primary="indigo">Indigo</button>
<button data-md-color-primary="blue">Blue</button>
<button data-md-color-primary="light-blue">Light Blue</button>
<button data-md-color-primary="cyan">Cyan</button>
<button data-md-color-primary="teal">Teal</button>
<button data-md-color-primary="green">Green</button>
<button data-md-color-primary="light-green">Light Green</button>
<button data-md-color-primary="lime">Lime</button>
<button data-md-color-primary="yellow">Yellow</button>
<button data-md-color-primary="amber">Amber</button>
<button data-md-color-primary="orange">Orange</button>
<button data-md-color-primary="deep-orange">Deep Orange</button>
<button data-md-color-primary="brown">Brown</button>
<button data-md-color-primary="grey">Grey</button>
<button data-md-color-primary="blue-grey">Blue Grey</button>

<script>
  var buttons = document.querySelectorAll("button[data-md-color-primary]");
  Array.prototype.forEach.call(buttons, function(button) {
    button.addEventListener("click", function() {
      document.body.dataset.mdColorPrimary = this.dataset.mdColorPrimary;
    })
  })
</script>

## Accent Color

鼠标点击即可临时改变当前页鼠标悬停超链接文字颜色

<button data-md-color-accent="red">Red</button>
<button data-md-color-accent="pink">Pink</button>
<button data-md-color-accent="purple">Purple</button>
<button data-md-color-accent="deep-purple">Deep Purple</button>
<button data-md-color-accent="indigo">Indigo</button>
<button data-md-color-accent="blue">Blue</button>
<button data-md-color-accent="light-blue">Light Blue</button>
<button data-md-color-accent="cyan">Cyan</button>
<button data-md-color-accent="teal">Teal</button>
<button data-md-color-accent="green">Green</button>
<button data-md-color-accent="light-green">Light Green</button>
<button data-md-color-accent="lime">Lime</button>
<button data-md-color-accent="yellow">Yellow</button>
<button data-md-color-accent="amber">Amber</button>
<button data-md-color-accent="orange">Orange</button>
<button data-md-color-accent="deep-orange">Deep Orange</button>

<script>
  var buttons = document.querySelectorAll("button[data-md-color-accent]");
  Array.prototype.forEach.call(buttons, function(button) {
    button.addEventListener("click", function() {
      document.body.dataset.mdColorAccent = this.dataset.mdColorAccent;
    })
  })
</script>
