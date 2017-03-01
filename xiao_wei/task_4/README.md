任务四：定位和居中问题
======================

HTML 和 CSS 高级指南之二－－定位详解
------------------------------------

[原文链接](http://www.w3cplus.com/css/advanced-html-css-lesson2-detailed-css-positioning.html)

### 包含浮动

当元素浮动时，一个元素的位置依赖于放置在他周边的其他元素。

浮动问题：一个父元素包含了多个浮动的子元素。 浮动元素不会影响父元素的宽度。这样做会让父元素塌陷，从而使父元素的高度为"0"，以及忽略其它的属性。

嵌套的元素不会正确的排列，也会有错误的样式出现。

1.  clear:both

    在容器结束标签前添加一个空标签，在空标签上直接设置样式 `clear:both` 缺点：不太适合语义化，容易造成页面上空标签迅速堆积，页面中没有上下文内容。

2.  overflow 技巧

    在具有浮动元素的父容器中设置 `overflow` 的属性值为 `auto` 注意：

    1.  IE6 里父元素需设置 `width` 和 `height`
    2.  IE 会添加滚动条 `> 最好直接使用 =overflow:hidden;`

    优点：父容器就会有一个高度存在 缺点：

    1.  子元素会被限制在父元素内
    2.  不同的浏览器对 `overflow` 属性解析不一样

3.  clearfix 技巧

    clearfix 技巧是基于父元素上使用 `:before` 和 `:after` 两个伪类。 `:before` 伪类是用来防止子元素顶部的外边距塌陷 `:after` 伪类是用来防止子元素的底部的外边距塌陷，以及用来清除元素的浮动 注意：加上 `*zoom` 属性来触发父元素的 `hasLayout` 的机制

4.  有效的包含浮动

    一个常见的方法是将定义一个类名，把这个类名加到需要清除浮动的容器上。 例如使用“clearfix”清除浮动，Dan Cederholm 为容器设置了一个类名“group”。在需要清除浮动的容器上添加这个类名“group”。

    ``` css
    .group:before,
    .group:after {
      content: "";
      display: table;
    }
    .group:after {
      clear: both;
    }
    .group {
      *zoom: 1;
    } 
    ```

    > **单个伪类** 每个元素只有一个 `:before` 和 `:after` 伪类

    在上面的例子中，clearfix 的样式不应该直接插入到“.box-set”类中，应该是给需要清除浮动的元素中添加类名“group”。

### 定位属性

[MDN -- position 教程](https://developer.mozilla.org/en-US/docs/Web/CSS/position)

> **盒子位移属性是如何工作？** 盒子的位移属性有四个“top、right、bottom 和 left”，用来指定元素的定位位置和方向。这些属性只能在元素的“position”属性设置了“relative、absolute 和 fixed”属性值，才生效。 对于相对定位元素，这些属性的设置让元素从默认位置移动。 对于绝对定位和固定定位鲜红，这些属性指定了元素与父元素边缘之间的距离。

1.  Position relative

    设置了位移属性的相对定位元素，他在页面中仍然是正常的、静态的，仍属于自然流。在这种情况下，其他元素不会占用相对定们元素当初的位置。此外，其他元素没有进行位置移动时，相对定伴元素可能会和其他元素重叠。

    一个相对定位元素同时设置了“top”和“bottom”位移属性值，实际上“top”优先级高于“bottom”。然而，一个相对定位元素同时设置了“left”和“right”位移属性，他们的优先级取决于页面使用的是哪种语言。

2.  Position absolute

    绝对定位元素也具有盒子位移属性，然而，绝对定位元素会脱离文档流。绝对定位元素直接从文档流中移出，绝对定位元素的位置直接和父容器是否设置了相对定位（绝对定位）有直接关系。绝对定位元素需要至少一个祖先元素设置了相对定位（绝对定位），不然元素定位会相对于页面的主体进行定位。

    使用绝对定位的元素可以指定垂直和水平的位移属性，使绝对定位元素相对于设置了相对定们的祖先元素边缘进行移位。

    然而，使用了绝对定位的元素并没有进行任何盒子位移属性设置，那么绝对定位元素的顶部和左部会和设置了相对定位的父元素的顶边和左边重合。

    一个绝对定位元素同时设置了“top”和“bottom”位移属性值，实际上“top”优先级高于“bottom”。然而，一个相对定位元素同时设置了“left”和“right”位移属性，他们的优先级取决于页面使用的是哪种语言。

3.  Position fixed

    固定定位和绝对定位很类似，但是他定位是相对于浏览器窗口，并且不会随滚动条进行滚动。也就是说，不管用户停留在页面那个地方，固定定位的元素将始终停留在页面的一个地方。

    注意：IE6 不能使用 `position: fixed`

    固定定位元素的盒子位移属性的使用和绝对定位的一样。

4.  固定页头和页脚

    ``` html
    <footer>Fixed Footer </footer>    
    ```

    ``` css
    footer {
      bottom: 0;
      left: 0;
      position: fixed;
      right: 0;
    } 
    ```

### z-index 属性

页面元素是一个[怎样的层叠顺序](http://www.impressivewebs.com/a-detailed-look-at-the-z-index-css-property/) -&gt; `z-index` 属性来控制

在 Dom 中，元素在顶部的要低于底部。

`z-index` 值越高，将会出现在越上面，不管元素在 Dom 哪个位置上。

元素上设置了 `position` 属性值为 `relative`, `absolute`, `fixed` -&gt; 盒子位移属性、设置 `z-index` 属性

CSS 居中方案
------------

[原文链接](https://css-tricks.com/centering-css-complete-guide/)

### 水平

1.  元素为行元素

    适用于 `inline`, `inline-block`, `inline-table`, `inline-flex`, 等等。

    ``` css
    .center-children {
      text-align: center;
    }
    ```

2.  一个元素且为块元素

    无论多宽，目标元素都会在父元素中央。

    ``` css
    .center-me {
      margin: 0 auto;
    }
    ```

    注意：不能适用 `float` 来居中。[为什么？](http://css-tricks.com/float-center/)

3.  多个元素且为块元素

    要使多个块元素在一行中居中，需要改变它们 `display` 属性，例如全部改为 `inline-block`

    要是你是要每个元素都在每一行独自居中，则可以使用 `margin: 0 auto`

### 垂直

1.  元素为行元素

    1.  一行？

        ``` css
        .link {
          padding-top: 30px;
          padding-bottom: 30px;
        }
        ```

        要是 `padding` 无效，可以使用：

        ``` css
        .center-text-trick {
          height: 100px;
          line-height: 100px;
          white-space: nowrap;
        }
        ```

    2.  多行？

        使用一行中 `padding` 方法。

        要是无效，如在表格类元素中，用 `vertical-align` 属性

        要是都没有效果，可以使用 `flex`

        ``` css
        .flex-center-vertically {
          display: flex;
          justify-content: center;
          flex-direction: column;
          height: 400px;
        }
        ```

        要是都没有效果，可以创建一个空元素，设置完全高度并包裹元素。

        ``` css
        .ghost-center {
          position: relative;
        }
        .ghost-center::before {
          content: " ";
          display: inline-block;
          height: 100%;
          width: 1%;
          vertical-align: middle;
        }
        .ghost-center p {
          display: inline-block;
          vertical-align: middle;
        }
        ```

2.  一个块元素

    1.  知道高度

        ``` css
        .parent {
          position: relative;
        }
        .child {
          position: absolute;
          top: 50%;
          height: 100px;
          margin-top: -50px; /* account for padding and border if not using box-sizing: border-box; */
        }
        ```

    2.  不知道高度

        ``` css
        .parent {
          position: relative;
        }
        .child {
          position: absolute;
          top: 50%;
          transform: translateY(-50%);
        }
        ```

    3.  使用 flexbox

        ``` css
        .parent {
          display: flex;
          flex-direction: column;
          justify-content: center;
        }
        ```

### 水平和垂直都要居中

1.  元素固定高宽

    ``` css
    .parent {
      position: relative;
    }

    .child {
      width: 300px;
      height: 100px;
      padding: 20px;

      position: absolute;
      top: 50%;
      left: 50%;

      margin: -70px 0 0 -170px;
    }
    ```

2.  不知道元素高宽

    ``` css
    .parent {
      position: relative;
    }
    .child {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
    ```

3.  使用 flexbox

    ``` css
    .parent {
      display: flex;
      justify-content: center;
      align-items: center;
    }
    ```

### 使用做作弊器

<http://howtocenterincss.com/>
