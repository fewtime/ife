任务三：三栏式布局
==================

清除浮动
--------

[原文链接](http://stackoverflow.com/questions/211383/which-method-of-clearfix-is-best)

### “重新加载”浮动

把 `display: table` 改为 `display: block`, 有利于不启用容器之间 margin 的冲突

``` css
.container::after {
    content:"";
    display:block;
    clear:both;
}
```

### “打败浮动”，现在浏览器的清理浮动方法

使用现在浏览器时，可以去除 `zoom` 和 `::before` 属性/值，直接使用：

``` css
.container::after {
    content:"";
    display:table;
    clear:both;
}
```

注意：该方法不适用于 **IE6/7**

### 小型清理浮动

最近广泛适用的清除浮动方法：

``` css
.container::before, .container::after {
    content:"";
    display:table;
}
.container::after {
    clear:both;
}
.container {
    zoom:1; /* For IE 6/7 (trigger hasLayout) */
}
```

### 溢出性质

适用于目标内容遮盖了容器的边界

[这里解释了这个方法](http://www.quirksmode.org/css/clearing.html)

``` css
.container {
    overflow: hidden;
    display: inline-block; /* Necessary to trigger "hasLayout" in IE */
    display: block; /* Sets element back to block */
}
```

**IE** 不仅可以使用 `display` 属性，还可以使用其它属性用于 [触发一个元素 `hasLayout` ](http://www.satzansatz.de/cssd/onhavinglayout.html)

``` css
.container {
    overflow: hidden; /* Clearfix! */
    zoom: 1;  /* Triggering "hasLayout" in IE */
    display: block; /* Element must be a block to wrap around contents. Unnecessary if only using block-level elements. */
}
```

还可以这么使用 `_overflow` 属性清除浮动，但只有 **IE** 能识别这个属性，还有 `_zoom` 属性在 **IE** 中用于触发一个元素的 `hasLayout`

``` css
.container {
    overflow: hidden;
    _overflow: visible; /* for IE */
    _zoom: 1; /* for IE */
}
```

### "::after"伪元素

更为古老的清理浮动方法，它允许元素超出其容器边界

<http://www.positioniseverything.net/easyclearing.html>

``` css
.container {
    display: inline-block;
}
.container::after {
    content: "";
    display: block;
    height: 0;
    clear: both;
    overflow: hidden;
    visibility: hidden;
}
.container {
    display: block;
}
```

### 元素中直接使用"clear"属性

最快捷最直接的方法：

``` css
<br style="clear:both" /> <!-- So dirty! -->
```

然而，这不是最理想的方法：

-   主要原因：CSS 应该把相同的标记裕运用不同场景中。(CSS should be used to style the same markup differently in different contexts.

)

-   不要在任何 CSS 代码插入 HTML 代码中。
-   这很业余。
-   将来有其它清除浮动的方法你不需要清除 `<br>` 内原有清除浮动的代码。

三栏布局技巧
------------

<https://zhuanlan.zhihu.com/p/25070186?refer=learncoding>
