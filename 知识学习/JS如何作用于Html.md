## document和window的区别？
就是简而言之，dom是一个对象，win也是一个对象。他们都是Web API里的一个不同角色。

### window对象
- window对象  
window就是窗口吗，它代表浏览器的一个窗口或标签页，并且是 JavaScript 中的全局对象。它提供了许多控制浏览器窗口的方法和属性。  
作用域：window 是最顶层的对象，在浏览器中的任何 JavaScript 代码中都可以直接访问 window 及其属性和方法，无需任何限定前缀。  
功能：window 对象包含了**浏览器窗口的属性，如窗口的大小、位置等**，同时也提供了**一些方法来控制浏览器窗口的行为，如打开新窗口、定时器函数（setTimeout、setInterval）、浏览器历史控制等。此外，它还是所有全局变量和全局函数的宿主**。
### document对象
- document对象  
定义：document 对象是 window 对象的一个属性，它代表了加载在窗口中的 HTML 文档，是 Document Object Model（DOM）的入口点。  
作用域：document 对象**专门用于操作和访问文档的内容**，比如 HTML 元素、CSS 样式等。  
功能：document 对象提供了**许多方法来访问和修改文档内容**，如获取和设置元素的内容、创建新的 HTML 元素、查询选择器等。通过 document 对象，可以实现对页面内容的动态修改和交互。  

总的来说，window 对象代表了浏览器窗口本身，是所有全局JavaScript对象、函数和变量的父级对象，而 document 对象代表了窗口中加载的文档，是所有HTML文档元素的容器。在实际开发中，根据需要操作的是浏览器窗口本身还是窗口中的文档内容，来决定使用 window 还是 document。  
就简单而言，dom对象操控的是文档的内容，而window对象操控的是浏览器窗口的属性和方法。So,如果你想开定时器，监控窗口的变化你需要用到的是windows对象，如果你想要改变文档的内容那你则需要使用document对象。  
所以当时**其实甘特图最主要的问题**是，我不知道windows API和document API的区别。我不懂原生的html，**当这块知识缺失了自然是不会去设计这个逻辑的**。
所以本质上就是会用封装好的API。

## Dom流API学习
### 如何获取元素
在DOM中获取元素主要涉及以下几个API：

1. `getElementById()`
    - 通过元素的ID获取单个元素。ID在一个HTML文档中应该是唯一的。

    ```javascript
    let element = document.getElementById('elementId'); // 通过ID获取元素
    ```

2. `getElementsByClassName()`
    - 通过元素的类名获取一个元素集合。这个方法返回的是一个类数组对象，包含所有匹配指定类名的元素。

    ```javascript
    let elements = document.getElementsByClassName('className'); // 通过类名获取元素集合
    ```

3. `getElementsByTagName()`
    - 通过元素的标签名（如`div`, `p`, `a`等）获取元素集合。同样返回一个类数组对象，包含所有匹配指定标签名的元素。

    ```javascript
    let elements = document.getElementsByTagName('tagName'); // 通过标签名获取元素集合
    ```

4. `querySelector()`
    - 使用CSS选择器获取第一个匹配的元素。这是一个非常强大的方法，可以使用**复杂的CSS选择器**来定位元素。

    ```javascript
    let element = document.querySelector('.className'); // 通过CSS选择器获取第一个匹配的元素
    ```

5. `querySelectorAll()`
    - 使用CSS选择器获取所有匹配的元素集合。这个方法返回的是一个`NodeList`对象，包含**所有匹配指定CSS选择器的元素**。

    ```javascript
    let elements = document.querySelectorAll('.className'); // 通过CSS选择器获取所有匹配的元素
    ```

6. `closest()`
    - 从元素本身开始，在其祖先元素中（包括自己），找到第一个匹配给定CSS选择器的元素。这个方法对于寻找元素的最近父级匹配非常有用。自下向上寻找。

    ```javascript
    let closestElement = element.closest('.className'); // 在元素的祖先中找到最近的匹配给定选择器的元素
    ```
7. `children`
    - 获取一个元素的子元素集合，不包括文本和注释节点。这是一个元素对象的属性，返回直接子元素的HTML集合。

    ```javascript
    let childElements = parentElement.children; // 获取parentElement的所有直接子元素
    ```

8. `childNodes`
    - 获取一个元素的所有子节点，包括元素节点、文本节点和注释节点。这同样是元素对象的一个属性，返回一个节点列表。

    ```javascript
    let childNodes = parentElement.childNodes; // 获取parentElement的所有子节点，包括文本和注释
    ```

9. `parentElement` 和 `parentNode`
    - 通过一个元素获取其父元素。`parentElement` 返回父级元素节点，而 `parentNode` 可以返回任何类型的父节点，包括文本节点和注释节点。

    ```javascript
    let parent = childElement.parentElement; // 获取childElement的父元素
    let parentNode = childElement.parentNode; // 获取childElement的父节点
    ```

10. `nextSibling` 和 `previousSibling`
    - 分别获取元素的下一个和上一个同级节点。这两个属性返回的可以是任何类型的节点，包括元素节点、文本节点和注释节点。

    ```javascript
    let nextNode = element.nextSibling; // 获取element的下一个同级节点
    let prevNode = element.previousSibling; // 获取element的上一个同级节点
    ```

11. `nextElementSibling` 和 `previousElementSibling`
    - 类似于 `nextSibling` 和 `previousSibling`，但这两个属性只返回元素节点，忽略文本节点和注释节点。

    ```javascript
    let nextElement = element.nextElementSibling; // 获取element的下一个同级元素
    let prevElement = element.previousElementSibling; // 获取element的上一个同级元素
    ```

12. `firstChild` 和 `lastChild`
    - 分别获取元素的第一个和最后一个子节点。这些子节点可以是任何类型的节点，包括元素节点、文本节点和注释节点。

    ```javascript
    let first = parentElement.firstChild; // 获取parentElement的第一个子节点
    let last = parentElement.lastChild; // 获取parentElement的最后一个子节点
    ```

13. `firstElementChild` 和 `lastElementChild`
    - 类似于 `firstChild` 和 `lastChild`，但这两个属性只返回元素节点，忽略文本节点和注释节点。

    ```javascript
    let firstElement = parentElement.firstElementChild; // 获取parentElement的第一个子元素
    let lastElement = parentElement.lastElementChild; // 获取parentElement的最后一个子元素
    ```

通过综合运用这些API，可以有效地遍历和操作DOM树，实现对页面结构的灵活控制。

通过这些API，可以根据不同的条件和需求，在DOM树中灵活地获取单个或多个元素。

---
### 如何创建元素
#### 创建元素
```javascript
document.createElement('tag')
```
#### 创建文本节点
```javascript
document.createTextNode('text')
```
什么是文本节点？  
文本节点就是html中的文本，比如p标签中的文本，a标签中的文本等等。
createTextNode怎么使用？  
```javascript
var text = document.createTextNode('text')
```
这是什么效果？
```javascript
<p>text</p>
```
text在这里面是他文字的内容。

---
### 如何添加元素
#### 添加元素
```javascript
parent.appendChild(child)
```
什么效果？
```javascript
<div>
  <p>text</p>
</div>
```
#### 插入元素
```javascript
parent.insertBefore(newNode, referenceNode)
```
举个例子
```javascript
var parent = document.getElementById('parent')
var newNode = document.createElement('p')
var referenceNode = document.getElementById('reference')
parent.insertBefore(newNode, referenceNode)
```
这个效果是什么？
```javascript
<div id="parent">
  <p>newNode</p>
  <p id="reference">referenceNode</p>
</div>
```
referenceNode起了什么作用？
referenceNode是一个参考节点，他的作用是在参考节点之前插入新的节点。
### 如何删除元素
#### 删除元素
```javascript
parent.removeChild(child)
```
举个例子
```javascript
var parent = document.getElementById('parent')
var child = document.getElementById('child')
parent.removeChild(child)
```
这个效果是什么？给出对比
```javascript
<div id="parent">
  <p id="child">child</p>
</div>
```
```javascript
<div id="parent">
</div>
```
### 如何修改元素内容？
在DOM（文档对象模型）中修改元素内容主要涉及以下几个常用的API：

1. `innerText` 和 `textContent`
   这两个属性都可以用来获取或设置一个元素的文本内容。`innerText` 反映了元素及其子元素的“渲染”文本内容，即按照样式显示在页面上的内容，而 `textContent` 则获取或设置元素内所有子节点的内容，包括 `<script>` 和 `<style>` 标签内的文本。

    ```javascript
    element.innerText = '新的文本内容'; // 设置元素的可见文本
    let content = element.innerText; // 获取元素的可见文本

    element.textContent = '新的全部文本内容'; // 设置元素的全部文本，包含所有子节点
    let fullContent = element.textContent; // 获取元素的全部文本，包含所有子节点
    ```

2. `innerHTML`
   `innerHTML` 属性可以用来获取或设置元素内的HTML内容。与 `innerText` 和 `textContent` 不同，`innerHTML` 会包含所有的HTML标签。

    ```javascript
    element.innerHTML = '<strong>加粗的文本</strong>'; // 设置元素内的HTML内容
    let htmlContent = element.innerHTML; // 获取元素内的HTML内容
    ```

3. `outerHTML`
   `outerHTML` 属性可以获取或设置包含元素本身及其所有子节点的HTML。

    ```javascript
    element.outerHTML = '<div><strong>新元素及其内容</strong></div>'; // 替换元素及其内容
    ```

4. `createElement` 和 `appendChild` / `replaceChild`
   这些方法用于创建新的DOM元素并将其插入到文档中。`createElement` 用于创建一个新的元素节点，`appendChild` 用于将创建的节点添加到父节点的子节点列表的末尾，`replaceChild` 用于替换父节点的一个子节点。

    ```javascript
    let newElement = document.createElement('div'); // 创建一个新的div元素
    newElement.innerText = '这是新创建的元素'; // 设置新元素的文本内容
    parentElement.appendChild(newElement); // 将新元素添加为parentElement的子节点

    let anotherElement = document.createElement('span'); // 创建另一个元素
    parentElement.replaceChild(anotherElement, newElement); // 替换父元素中的子元素
    ```

通过这些API，可以方便地在DOM中修改元素的内容和结构。
在DOM中修改元素的样式和属性主要涉及以下几个API：

1. 修改样式：`style` 属性
    - 每个DOM元素都有一个 `style` 属性，它允许你通过JavaScript直接修改元素的样式。可以通过设置元素的 `style` 属性中的CSS属性来改变样式。

    ```javascript
    element.style.backgroundColor = 'red'; // 直接设置元素的背景颜色为红色
    element.style.fontSize = '20px'; // 设置元素的字体大小为20像素
    ```

2. 修改类：`classList` 属性
    - `classList` 提供了一种简单的方法来操作元素的类名集合。常用的方法包括 `add()`, `remove()`, `toggle()` 和 `contains()`。

    ```javascript
    element.classList.add('new-class'); // 添加一个新的类名
    element.classList.remove('old-class'); // 移除一个类名
    element.classList.toggle('active'); // 如果存在则删除该类名，不存在则添加
    ```

3. 设置和获取属性：`setAttribute()` 和 `getAttribute()`
    - 这两个方法分别用于设置和获取元素的属性。属性可以是标准的HTML属性，如 `id`, `src`, `href` 等，也可以是自定义属性。

    ```javascript
    element.setAttribute('data-custom', 'value'); // 设置一个自定义属性
    let value = element.getAttribute('data-custom'); // 获取这个自定义属性的值
    ```

4. 直接修改属性
    - 对于一些常用的HTML属性，如 `id`, `src`, `href` 等，可以直接通过元素对象来获取和设置。

    ```javascript
    element.href = 'https://example.com'; // 直接设置元素的href属性
    let elementId = element.id; // 直接获取元素的id属性
    ```

通过这些API，可以方便地在JavaScript中修改DOM元素的样式和属性，以实现动态的页面效果。
### 如何替换元素
#### 替换元素
在DOM操作中，替换元素涉及以下几个常用的API：

1. `replaceChild(newChild, oldChild)`
    - 这是一个在父节点上调用的方法，用于将父节点中的一个旧子节点替换为一个新的子节点。`newChild` 是要插入的新节点，而 `oldChild` 是要被替换的旧节点。

    ```javascript
    parentNode.replaceChild(newElement, oldElement); // 将parentNode中的oldElement替换为newElement
    ```

2. `replaceWith(...)`
    - `replaceWith()` 方法允许你将一个DOM节点（或多个节点）替换为指定的节点或者一段HTML或文本字符串。这个方法是直接在要被替换的节点上调用的。

    ```javascript
    oldElement.replaceWith(newElement); // 将oldElement替换为newElement
    ```

3. 使用 `insertBefore()` 配合 `removeChild()` 或 `remove()` 来实现替换
    - 虽然不是直接的替换方法，但可以通过先插入新节点到旧节点之前，然后移除旧节点，达到替换的效果。

    ```javascript
    parentNode.insertBefore(newElement, oldElement); // 将newElement插入到oldElement之前
    parentNode.removeChild(oldElement); // 移除oldElement，实现替换效果
    // 或者使用更简洁的 oldElement.remove()，如果环境支持
    oldElement.remove();
    ```

4. 使用 `outerHTML`
    - 通过设置元素的 `outerHTML` 属性，可以直接替换整个元素，包括元素本身及其内容。这种方法不需要先获取父节点。

    ```javascript
    oldElement.outerHTML = '<div id="newElement">新内容</div>'; // 用新的HTML内容替换oldElement，包括元素本身
    ```

这些API提供了灵活的方式来替换DOM中的元素，可以根据不同的场景和需求选择合适的方法。




### 如何给元素添加事件
在DOM中处理元素事件主要涉及以下几个API：

1. `addEventListener(event, handler, [options])`
    - 用于在指定元素上添加一个事件监听器。`event` 是要监听的事件类型（如 `"click"`, `"mouseover"` 等），`handler` 是事件发生时调用的函数，`options` 是一个可选的参数，用于指定更详细的事件监听行为。

    ```javascript
    element.addEventListener('click', function() {
      console.log('元素被点击了');
    });
    ```

2. `removeEventListener(event, handler, [options])`
    - 用于移除之前通过 `addEventListener` 添加的事件监听器。需要注意的是，`handler` 必须与添加监听器时使用的是同一个函数引用。

    ```javascript
    function handleClick() {
      console.log('元素被点击了');
    }

    element.addEventListener('click', handleClick);
    // 稍后移除监听器
    element.removeEventListener('click', handleClick);
    ```

3. `dispatchEvent(event)`
    - 用于触发指定元素上的事件。`event` 是一个 `Event` 对象的实例，可以通过 `new Event()` 来创建。

    ```javascript
    let event = new Event('customEvent');
    element.dispatchEvent(event); // 触发自定义事件
    ```

4. 通过属性直接分配事件处理器
    - 可以直接将事件处理函数分配给元素的事件处理属性。例如，`onclick` 对应于点击事件。

    ```javascript
    element.onclick = function() {
      console.log('元素被点击了');
    };
    ```

5. 使用 `on` 前缀的属性来设置事件处理函数
    - 除了 `onclick`，还有许多其他的事件可以通过设置以 `on` 开头的属性来添加处理函数，例如 `onmouseover`、`onkeydown` 等。

    ```javascript
    element.onmouseover = function() {
      console.log('鼠标悬停在元素上');
    };
    ```

6. 使用 `Event` 对象
    - 事件处理函数中的 `event` 参数是一个 `Event` 对象的实例，它提供了关于事件的信息，如触发事件的元素、事件类型以及其他与特定事件相关的属性和方法。

    ```javascript
    element.addEventListener('click', function(event) {
      console.log('点击发生在 ' + event.target.tagName + ' 元素上');
    });
    ```
7. `preventDefault()`
    - 事件对象的 `preventDefault()` 方法用于阻止事件的默认行为。这在处理如点击链接时不希望页面跳转，或在提交表单时不希望页面重新加载等场景下非常有用。

    ```javascript
    element.addEventListener('click', function(event) {
      event.preventDefault(); // 阻止链接默认的跳转行为
    });
    ```

8. `stopPropagation()`
    - 用于阻止事件冒泡到父元素。事件冒泡是指事件从最深的节点开始，然后逐级向上传播到较为浅的节点的过程。

    ```javascript
    element.addEventListener('click', function(event) {
      event.stopPropagation(); // 阻止事件继续冒泡
    });
    ```

9. 事件委托
    - 利用事件冒泡的特性，可以将事件监听器设置在父元素上，而不是每个子元素上。当事件在子元素上触发并冒泡到父元素时，可以通过检查事件的 `target` 属性来确定是哪个子元素触发的事件。

    ```javascript
    parentElement.addEventListener('click', function(event) {
      if (event.target && event.target.matches('button.child')) {
        console.log('子按钮被点击');
      }
    });
    ```

10. `capture` 事件捕获
    - 在事件处理的第三个参数 `options` 中，可以设置 `capture` 为 `true` 来指定事件处理器在捕获阶段而不是冒泡阶段执行。事件捕获是指事件从最外层开始，然后逐级向下传播到最深的节点的过程。

    ```javascript
    element.addEventListener('click', function() {
      console.log('捕获阶段的事件处理');
    }, {capture: true});
    ```

11. `once` 选项
    - 在 `addEventListener` 的第三个参数中，设置 `once: true` 可以让事件处理器只执行一次，然后自动移除。

    ```javascript
    element.addEventListener('click', function() {
      console.log('这个事件处理器只会执行一次');
    }, {once: true});
    ```

通过这些API，可以灵活地为DOM元素添加、移除和触发事件，实现丰富的交互效果。

### 生命周期
DOM（文档对象模型）和Window对象在Web页面的生命周期中扮演着重要的角色。下面介绍一些与DOM和Window生命周期相关的API：

1. Window的生命周期事件：

    - `load` 事件
        - 当整个页面及所有依赖资源如样式表和图片都已完成加载时，`window` 对象会触发 `load` 事件。

        ```javascript
        window.addEventListener('load', function() {
            console.log('页面完全加载完毕');
        });
        ```

    - `DOMContentLoaded` 事件
        - 当初始的HTML文档被完全加载和解析完成，不需要等待样式表、图片和子框架完成加载，`document` 对象会触发 `DOMContentLoaded` 事件。

        ```javascript
        document.addEventListener('DOMContentLoaded', function() {
            console.log('DOM内容加载完毕');
        });
        ```

    - `unload` 事件
        - 当用户离开当前页面，`window` 对象会触发 `unload` 事件。这个事件可以用于清理工作，如关闭弹出窗口等。

        ```javascript
        window.addEventListener('unload', function() {
            console.log('用户离开页面');
        });
        ```

    - `beforeunload` 事件
        - 在窗口、文档或其资源即将卸载时触发。可以用来询问用户是否确定离开当前页面，通常用于提示用户保存未保存的更改。

        ```javascript
        window.addEventListener('beforeunload', function(event) {
            event.returnValue = '您有未保存的更改，确定要离开吗？';
        });
        ```

2. 请求动画帧（Request Animation Frame）:
    - `requestAnimationFrame(callback)`
        - 提供了一种在浏览器重绘之前调用特定代码的方法，用于执行动画或页面重绘等。这个方法比传统的 `setInterval` 更高效，可以更平滑地执行动画。

        ```javascript
        function animate() {
            // 动画代码
            requestAnimationFrame(animate);
        }
        requestAnimationFrame(animate);
        ```
3. 页面可见性 API（Page Visibility API）:
    - 这个API提供了`visibilitychange`事件，以及`document.hidden`属性，用于检测页面是否对用户可见。这在优化页面性能和用户体验方面特别有用，比如可以在页面不可见时暂停视频播放或停止执行动画。

    ```javascript
    document.addEventListener('visibilitychange', function() {
        if (document.hidden) {
            console.log('页面不可见');
        } else {
            console.log('页面可见');
        }
    });
    ```

4. 性能监测 API（Performance API）:
    - `performance`对象允许访问与当前页面相关的性能数据。例如，可以使用`performance.timing`来分析不同阶段的耗时，如页面加载、解析等。

    ```javascript
    window.addEventListener('load', function() {
        setTimeout(function() {
            const timing = performance.timing;
            const loadTime = timing.loadEventEnd - timing.navigationStart;
            console.log('页面加载时间：' + loadTime);
        }, 0);
    });
    ```

5. `resize` 事件:
    - 当浏览器窗口被调整大小时，`window`对象会触发`resize`事件。可以用来调整页面布局或执行其他响应窗口大小变化的操作。

    ```javascript
    window.addEventListener('resize', function() {
        console.log('窗口大小变化了');
    });
    ```

6. `scroll` 事件:
    - 当用户滚动页面时，会触发`scroll`事件。这可以用于实现“懒加载”（延迟加载图片等内容），或者动态改变导航条的样式等。

    ```javascript
    window.addEventListener('scroll', function() {
        console.log('页面被滚动了');
    });
    ```

7. `focus` 和 `blur` 事件:
    - 当页面或页面内的元素获得或失去焦点时，会触发`focus`和`blur`事件。这可以用于改善表单输入的用户体验，或在应用中管理键盘快捷键。

    ```javascript
    window.addEventListener('focus', function() {
        console.log('窗口获得了焦点');
    });

    window.addEventListener('blur', function() {
        console.log('窗口失去了焦点');
    });
    ```

通过结合使用这些API，开发者可以更精细地控制和优化Web应用的行为和性能，提升用户的互动体验。

通过监听和处理这些生命周期事件，可以更好地控制Web页面的加载、渲染和卸载过程，提高用户体验。
