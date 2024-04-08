## 创建动画的API
在CSS中创建动画主要依赖于以下几个关键的API：

1. `@keyframes` 规则
     - 用于定义动画的中间步骤（关键帧）。在 `@keyframes` 规则中，可以设定在动画过程中某个或某些时刻元素的样式。

    ```css
    @keyframes example {
      from {background-color: red;}
      to {background-color: yellow;}
    }
    ```

   或者使用百分比来指定多个关键帧：

    ```css
    @keyframes example {
      0%   {background-color: red;}
      50%  {background-color: blue;}
      100% {background-color: yellow;}
    }
    ```
   `@keyframes` 规则什么时候出发？
     - 当元素绑定了 `animation-name` 属性，并且动画开始时，`@keyframes` 规则中定义的关键帧将按照指定的时间和速度曲线进行执行。
     - 例如，上面的 `example` 动画在 `animation-name` 属性中绑定到元素后，将按照 `animation-duration` 和 `animation-timing-function` 属性的设置进行执行。
2. `animation-name` 属性
     - 指定需要绑定到选择器的 `@keyframes` 名称。

    ```css
    .element {
      animation-name: example;
    }
    ```

3. `animation-duration` 属性
     - 定义动画完成一个周期所花费的时间，例如秒或毫秒。

    ```css
    .element {
      animation-duration: 2s;
    }
    ```

4. `animation-timing-function` 属性
     - 定义动画的速度曲线，例如 `linear`, `ease`, `ease-in`, `ease-out`, `ease-in-out`, 或者 `cubic-bezier` 函数。

    ```css
    .element {
      animation-timing-function: ease-in-out;
    }
    ```
   在CSS动画中，可以通过指定动画的速度曲线来控制动画的变化速度。以下是一些常用的速度曲线：
   1. `linear`
       - 动画从头到尾的速度是相同的。这意味着动画以恒定速度平滑地进行，没有加速或减速的过程。

   2. `ease`
       - 默认的速度曲线。动画以低速开始，然后加速，最后再减速。这使得动画看起来更自然，因为它模拟了现实世界中物体的运动状态。

   3. `ease-in`
       - 动画以低速开始，随着动画的进行，速度逐渐增加，直到结束。这种曲线适用于需要强调动作开始阶段的场景。

   4. `ease-out`
       - 动画以全速开始，然后逐渐减速直到停止。这种曲线适用于需要强调动作结束阶段的场景。

   5. `ease-in-out`
       - 动画以低速开始和结束，中间部分以较快的速度运动。这种速度曲线是`ease-in`和`ease-out`的结合，适用于需要平滑过渡的场景。

   6. `cubic-bezier(n,n,n,n)`
       - 允许你自定义一个速度曲线。`cubic-bezier`函数接受四个参数，这些参数定义了一个三次贝塞尔曲线，可以精确控制动画的加速和减速过程。CSS提供了一个`cubic-bezier`工具，帮助你可视化和调整这四个参数。
   ease-n. 容易；舒适，自在
        v. 减轻，缓和，放松；缓缓移动；使容易；降低；使离职；熟悉



5. `animation-delay` 属性
     - 设置动画在启动前的延迟时间。

    ```css
    .element {
      animation-delay: 1s;
    }
    ```

6. `animation-iteration-count` 属性
     - 定义动画应该播放的次数，可以是数字或者 `infinite` 表示无限次重复。

    ```css
    .element {
      animation-iteration-count: infinite;
    }
    ```

7. `animation-direction` 属性
     - 指定动画是否应该轮流反向播放。常见值有 `normal`, `reverse`, `alternate`, `alternate-reverse`。

    ```css
    .element {
      animation-direction: alternate;
    }
    ```

8. `animation-fill-mode` 属性
     - 指定在动画执行之前和之后如何为目标元素应用样式。例如，`forwards` 保留最后一帧的样式。

    ```css
    .element {
      animation-fill-mode: forwards;
    }
    ```
   `animation-fill-mode` 属性在CSS动画中用来指定一个动画在执行之前和之后如何将样式应用到其目标元素上。简而言之，它决定了动画执行前后元素的样式表现。`animation-fill-mode` 属性接受以下几个值：
   
   1. `none`
       - 默认值。不改变默认行为。动画不会将任何样式应用于目标元素，动画结束后元素会回到动画未执行时的状态。
   
   2. `forwards`
       - 动画完成后，元素将保留由动画的最后一个关键帧计算值决定的样式。即动画结束后元素会保留动画结束时的样式。
   
   3. `backwards`
       - 动画将在应用于元素的那一刻立即应用第一关键帧的样式，即使动画延迟开始。这意味着元素会立即获得动画初始状态的样式，直到动画真正开始。
   
   4. `both`
       - 动画遵循`forwards`和`backwards`的规则，意味着动画会在延迟期间应用第一关键帧的样式，并在动画结束后保留最后一个关键帧的样式。
   
   例如，如果你有一个淡出动画，你可能希望动画结束后元素保持透明

9. `animation` 简写属性
     - 可以使用 `animation` 简写属性同时设置所有动画属性。

    ```css
    .element {
      animation: example 2s infinite ease-in-out;
    }
    ```
10. `animation-play-state` 属性
    - 控制动画的播放状态。可以设置为 `paused` 暂停动画，或者 `running` 继续播放动画。

    ```css
    .element {
      animation-play-state: paused;
    }
    ```

11. 使用CSS变量控制动画
    - CSS变量（自定义属性）可以与动画结合使用，为动画提供动态值或实现主题定制。

    ```css
    :root {
       --animation-duration: 2s;
    }

    .element {
      animation-duration: var(--animation-duration);
    }
    ```

12. 使用`@media` 查询和动画
    - 可以结合媒体查询来应用不同的动画效果，使动画响应不同的屏幕尺寸或设备特性。

    ```css
    @media (max-width: 600px) {
      .element {
        animation-name: exampleSmallScreen;
      }
    }
    ```

13. `will-change` 属性
    - 提前告知浏览器元素将要进行的变化，以优化性能。虽然不是直接控制动画的属性，但适当使用可以提高动画的流畅度。

    ```css
    .element {
      will-change: transform, opacity;
    }
    ```

14. 利用CSS动画实现性能优化
     - 在可能的情况下，使用transform和opacity动画，因为它们可以通过硬件加速，提高动画的性能。

15. 动画事件
     - 虽然CSS本身不直接提供事件监听机制，但在JavaScript中，可以监听动画相关的事件，如 `animationstart`, `animationend`, 和 `animationiteration`，以在动画的不同阶段执行脚本。

    ```javascript
    document.querySelector('.element').addEventListener('animationend', function() {
      console.log('动画结束');
    });
    ```



## 动画API的实践
### 1. keyframes的使用
```css
.button {
  cursor: pointer;
  animation-duration: 3ms;
}
@keyframes button {
  0% {
    background-color: aqua;
  }
  100% {
    background-color: bisque;
  }
}
```
问题：它无法触发，动画一般何时触发？
```CSS
.button {
   cursor: pointer;
   animation-duration: 3s;
   animation-name: bgcolor;
   animation-delay: 0s;
   animation-timing-function: ease-in;
   background-color: aqua;
   animation-fill-mode: both;
   animation-iteration-count: infinite;
}
@keyframes bgcolor {
   0% {
      background-color: rgb(0, 140, 140);
   }
   100% {
      background-color: rgb(208, 127, 29);
   }
}

```
- animation-name属性就是将keyframes的名字赋值给它，这样就可以触发动画了。然后他是默认第一次加载的时候就会触发一次的。如果你绑定上。
- animation-duration属性是表示动画持续时间；
- animation-delay属性是表示动画延迟时间；
- animation-timing-function是动画时间函数，就是这个动画它是以什么函数执行的；linner，ease，ease-in，ease-in-out等。而ease就是轻松，减轻的意思，ease-in就是慢慢进。
- animation-iteration-count是动画的次数,iteration就是迭代重复的意思，count就是次数的意思。所以这个属性就是表示动画的次数。然后他设置的参数可以是1,2,3,4,5...也可以是infinite，表示无限次重复。
- animation-play-state是动画的播放状态，paused就是暂停的意思，running就是运行的意思。
- animation-fill-mode是动画的填充模式，forwards就是向前的意思，在这里是应用最后一帧的设置，backwards就是向后的意思在这里是应用第一帧率的设置，一般这个第一帧是它原来的设置而不是动画帧的第一个0%，both就是两者都有的意思，这里差不多和forwards相似。

### 2. 实现一个hover属性
- keyframers悬停动画的实现
```CSS
.button {
   cursor: pointer;

   background-color: antiquewhite;
}
.button :hover {
   animation-name: bgcolor;
   animation-duration: 3s;
   background-color: antiquewhite;
}

@keyframes bgcolor {
   0% {
      background-color: rgb(0, 140, 140);
   }
   100% {
      background-color: rgb(208, 127, 29);
   }
}
```
- 问题：为什么悬停动画没有实现？
- 解决：将button :hover改为.button:hover，因为问题出在`.button :hover`选择器上。在CSS选择器中，`.button :hover`表示选择`.button`内部的任何元素在悬停时的状态，而不是`.button`本身在悬停时的状态。这是因为`.button`和`:hover`之间有一个空格，这代表了一个后代选择器，意味着它将选择`.button`的子元素的悬停状态，而不是`.button`本身。
```CSS
.button {
  cursor: pointer;

  background-color: antiquewhite;
}
.button:hover {
  animation-name: bgcolor;
  animation-duration: 3s;
  background-color: antiquewhite;
  animation-iteration-count: infinite;
}

@keyframes bgcolor {
  0% {
    background-color: rgb(0, 140, 140);
  }
  50% {
    background-color: rgb(208, 127, 29);
  }
  100% {
    background-color: rgb(0, 140, 140);
  }
}
```



### 3. 实现一个点击事件
为什么我点击后没有反馈？
```css
.button {
  cursor: pointer;

  background-color: antiquewhite;
}
.button:checked {
  animation-name: bgcolor;
  animation-duration: 3s;
  background-color: antiquewhite;
  animation-iteration-count: infinite;
}

@keyframes bgcolor {
  0% {
    background-color: rgb(0, 140, 140);
  }
  50% {
    background-color: rgb(208, 127, 29);
  }
  100% {
    background-color: rgb(0, 140, 140);
  }
}

```
问题在于使用了 `.button:checked` 选择器，这个选择器通常用于表单元素（如复选框、单选按钮等）的选中状态，而不是用于常规的按钮元素。如果你的 `.button` 是一个 `<button>` 或 `<div>` 元素，`:checked` 伪类选择器是不适用的，因此点击时不会有任何效果。

如果你想在点击按钮后触发动画，可以考虑以下几种方法：

1. 使用 JavaScript 在点击事件发生时添加一个类，然后通过这个类来触发动画。
2. 如果是希望有点击（或触摸）的即时反馈，可以考虑使用 `:active` 伪类。但请注意，`:active` 状态仅在元素被激活（即鼠标按下期间）时生效，一旦鼠标松开，元素就会立刻回到正常状态。
3. 对于能够切换状态的按钮（如开关按钮），可以使用隐藏的复选框（checkbox）和标签（label）来实现。用户点击标签时会改变复选框的选中状态，从而通过复选框的 `:checked` 伪类来控制动画。

改为active之后是激活状态，但是松开鼠标就会回到原来的状态。就是说你鼠标一直按着的时候它是执行动画的，松开就不执行了。  
这不应该是点击事件，应该叫：**按住事件**。

那如何实现点击事件动画呢？
```css
.button {
   cursor: pointer;
   background-color: antiquewhite;
}

.animate {
   animation-name: bgcolor;
   animation-duration: 3s;
   animation-iteration-count: infinite;
}

@keyframes bgcolor {
   0% {
      background-color: rgb(0, 140, 140);
   }
   50% {
      background-color: rgb(208, 127, 29);
   }
   100% {
      background-color: rgb(0, 140, 140);
   }
}
```
```js
document.getElementById('animatedButton').addEventListener('click', function() {
this.classList.add('animate');
});

```


### 4.实现其他动画效果，旋转，放大缩小，移动等
CSS的`transform`属性允许你对元素进行移动、缩放、旋转、倾斜等变形操作。以下是一些常用的`transform`函数：

1. **平移（Translate）**：
    - `translate(x, y)`：沿X轴和Y轴移动元素。
    - `translateX(x)`：只沿X轴移动元素。
    - `translateY(y)`：只沿Y轴移动元素。

    ```css
    .translate {
      transform: translate(50px, 100px); /* 向右移动50px，向下移动100px */
    }
    ```

2. **缩放（Scale）**：
    - `scale(x, y)`：沿X轴和Y轴缩放元素。
    - `scaleX(x)`：只沿X轴缩放元素。
    - `scaleY(y)`：只沿Y轴缩放元素。

    ```css
    .scale {
      transform: scale(2, 3); /* 宽度放大2倍，高度放大3倍 */
    }
    ```

3. **旋转（Rotate）**：
    - `rotate(angle)`：旋转元素，`angle`是旋转角度，单位可以是`deg`（度）、`rad`（弧度）等。

    ```css
    .rotate {
      transform: rotate(45deg); /* 顺时针旋转45度 */
    }
    ```

4. **倾斜（Skew）**：
    - `skew(x-angle, y-angle)`：沿X轴和Y轴倾斜元素。
    - `skewX(angle)`：只沿X轴倾斜元素。
    - `skewY(angle)`：只沿Y轴倾斜元素。

    ```css
    .skew {
      transform: skew(30deg, 20deg); /* 沿X轴倾斜30度，沿Y轴倾斜20度 */
    }
    ```

5. **组合使用**：
    - `transform`属性可以组合使用多个变形函数，按照指定的顺序应用于元素。

    ```css
    .combine {
      transform: rotate(30deg) translate(100px, 50px) scale(1.5);
    }
    ```

    这个例子中，`.combine`类的元素首先被旋转30度，然后沿X轴和Y轴移动，最后整体放大1.5倍。
6. `matrix`变换在CSS中是一个非常强大的变换工具，它可以通过一个6值的矩阵来组合所有的2D变换效果（平移、旋转、缩放、倾斜）。这个矩阵是这样的：
   - `scaleX()`和`scaleY()`分别代表沿X轴和Y轴的缩放比例。
   - `skewX()`和`skewY()`分别代表沿X轴和Y轴的倾斜角度。
   - `translateX()`和`translateY()`分别代表沿X轴和Y轴的平移距离。
   - `matrix(scaleX(), skewY(), skewX(), scaleY(), translateX(), translateY())`
   使用`matrix`变换可以实现包括平移、缩放、旋转、倾斜在内的所有2D变换效果，但它不直观，需要一定的数学知识来构造合适的矩阵值。
   但是，要注意的是，`matrix`变换本身只适用于2D变换，对于3D变换（如在Z轴的平移或旋转），则需要使用`matrix3d`或其他3D变换相关的函数（如`translateZ()`, `rotateX()`, `rotateY()`, `rotateZ()`, `perspective()`等）。因此，如果你的问题是询问`matrix`是否可以处理3D变换，那么答案是不能。对于3D变换，你应该使用`matrix3d`或者组合使用其他3D变换函数。



使用`transform`属性可以在不影响页面布局的情况下对元素进行视觉上的变形，是实现复杂动画和布局效果的强大工具。此外，`transform`通常配合`transition`或`animation`属性一起使用，以实现平滑的过渡效果。
。

```CSS
.button {
  cursor: pointer;

  background-color: antiquewhite;
}
.button:active {
  animation-name: bgcolor;
  animation-duration: 3s;
  background-color: antiquewhite;
  animation-iteration-count: infinite;
}
.button:hover {
  animation-name: aaa;
  animation-duration: 3s;
  background-color: antiquewhite;
  animation-iteration-count: infinite;
}

@keyframes bgcolor {
  form {
    transform: rotate(32deg);
  }
  to {
    transform: rotate(90deg);
  }
}
@keyframes aaa2 {
  form {
    transform: scale(1);
  }
  to {
    transform: scale(2);
  }
}
@keyframes aa21a {
  form {
    transform: skew(2deg);
  }
  to {
    transform: skew(60deg);
  }
}
@keyframes aaa {
  form {
    transform: translate(0px, 0px);
  }
  to {
    transform: translate(0px, 250px);
  }
}
```

### 5.渐变过渡动画效果
- transition 实现渐变动画
```CSS
.button {
  width: 20px;
  cursor: pointer;
  transform: none;
  transition-property: transform width;
  transition-duration: 2s;
  background-color: antiquewhite;
}

.button:hover {
  width: 230px;
  transform: rotate(49deg);
}

```
- transform 转变动画
```CSS
.button {
  cursor: pointer;
  transform: none;
  transition: 2s;
  background-color: antiquewhite;
}

.button:hover {
  transform: rotate(49deg);
}
```
他们本质上都是通过transtion实现的渐变动画。transform也是css的属性一部分而已。

### 6. **构造`@keyframes`动画：**
   - 使用JavaScript构造一个完整的`@keyframes`动画，并将其插入到文档的`<style>`标签中。
   - 示例：
     ```javascript
     var duration = '2s';
     var fromPosition = '-100%';
     var toPosition = '0';
     var styleSheet = document.createElement('style');
     styleSheet.type = 'text/css';
     styleSheet.innerHTML = `@keyframes dynamicSlideIn {
       from { transform: translateX(${fromPosition}); }
       to { transform: translateX(${toPosition}); }
     }`;
     document.head.appendChild(styleSheet);
     
     var elem = document.getElementById('myElement');
     elem.style.animationName = 'dynamicSlideIn';
     elem.style.animationDuration = duration;
     elem.style.animationFillMode = 'forwards';
     ```
