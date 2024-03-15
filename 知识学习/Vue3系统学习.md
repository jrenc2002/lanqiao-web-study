# Vue3系统学习
## 1. Vue3基础
### 1.1 循环渲染
```vue
<div v-for="item in items" :key="item.id">
  <!-- 内容 -->
</div>
```
讲一讲key，为什么要加key？  
key是用于管理状态的，就是说你v-for去绑定一个列表，一个数组吗。  
在默认模式中，就是不加key的时候如果你的数据顺序发生变化，vue不会移动dom流的顺序，而是会重新更新每个元素。
单如果你的列表渲染的输出结果要**依赖子组件状态或者临时dom状态（列如表单输入值的情况**。  
为了给 Vue 一个提示，以便**它可以跟踪每个节点的标识**，从而重用和重新排序现有的元素，你需要为每个元素对应的块提供一个唯一的 key attribute。

### 1.2 事件处理
事件处理器 (handler) 的值可以是：  
- 内联事件处理器：事件被触发时执行的内联 JavaScript 语句 (与 onclick 类似)。  
- 方法事件处理器：一个指向组件上定义的方法的属性名或是路径。

#### 什么是内联事件处理器和方法事件处理器？
内联事件处理器和方法事件处理器是JavaScript中用于处理HTML元素事件的两种主要方式。

内联事件处理器  
内联事件处理器直接在HTML元素的标签内部指定。当用户对该元素进行操作时（如点击），就会触发相应的事件。内联事件处理器的一个典型示例是`onclick`属性，它可以直接在元素的HTML标签中设置。例如：

    <button onclick="alert('你点击了按钮！')">点击我</button>

这段代码中的`onclick`属性就是一个内联事件处理器，它定义了当按钮被点击时应该执行的JavaScript代码。

方法事件处理器  
方法事件处理器则是通过JavaScript代码来为元素绑定事件处理函数。这种方式通常更灵活，也更易于管理，特别是对于复杂的应用程序。你可以在JavaScript中使用`addEventListener`方法为元素添加事件处理器。例如：
```javascript
    const name = ref('Vue.js')

    function greet(event) {
    alert(`Hello ${name.value}!`)
    // `event` 是 DOM 原生事件
    if (event) {
    alert(event.target.tagName)
    }
    }
```
```html
<!-- `greet` 是上面定义过的方法名 -->
<button @click="greet">Greet</button>
```

这段代码首先通过`getElementById`获取ID为`myButton`的元素，然后使用`addEventListener`为该元素添加了一个点击事件处理器。当按钮被点击时，就会弹出一个警告框。

总的来说，内联事件处理器易于快速实现但难以维护，尤其是在较大的项目中；而方法事件处理器虽然需要编写更多的JavaScript代码，但提供了更高的灵活性和可维护性。

### 1.3 表单输入绑定
v-model绑定数值、字符串、布尔值、数组、对象、自定义组件等。  
- 文本
  - 字符串形式
- 多行文本
  - 字符串形式
- 复选框
  - 绑定单一的布尔类型值
- 多个复选框
  - 多个复选框绑定到同一个数组或集合的值
  - ```html
    <div>Checked names: {{ checkedNames }}</div>

    <input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
    <label for="jack">Jack</label>
    
    <input type="checkbox" id="john" value="John" v-model="checkedNames">
    <label for="john">John</label>
    
    <input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
    <label for="mike">Mike</label>
    ```
- 单选按钮
  - 绑定到单一的值
  - ```
    <div>Picked: {{ picked }}</div>
    <input type="radio" id="one" value="One" v-model="picked" />
    <label for="one">One</label>
    
    <input type="radio" id="two" value="Two" v-model="picked" />
    <label for="two">Two</label>
    ```
- 选择器
  - 如果 v-model 表达式的初始值不匹配任何一个选择项，`<select>` 元素会渲染成一个“未选择”的状态。在 iOS 上，这将导致用户无法选择第一项，因为 iOS 在这种情况下不会触发一个 change 事件。因此，我们建议提供一个空值的禁用选项，如上面的例子所示。
    - ```
        <select v-model="selected">
        <option disabled value="">Please select one</option>
        <option>A</option>
        <option>B</option>
        <option>C</option>
        </select>
        <span>Selected: {{ selected }}</span>
        ```


## 2. 组件系统学习
### 2.1 组件数据传递
组件与组件之间的数据传递有两种方式：
- 父组件向子组件传递数据
  通过defineProps去实现数据的传递:
    ```vue
    // 在父组件中
      <template>
          <ChildComponent :title="title" />
      </template>
    
      <script>
      import ChildComponent from './ChildComponent.vue'
      </script>
    ```
    ```vue
    // 在子组件中
      <script setup>
      import { defineProps } from 'vue'
      const props = defineProps({
          title: String
      })
      </script>
    ```
- 子组件向父组件传递数据
  - 通过自定义事件向父组件传递数据
    在Vue 3中，子组件可以通过自定义事件向父组件传递数据。这个过程通常涉及以下几个步骤：

    1. **子组件中**：使用`emit`方法触发一个自定义事件，并将数据作为参数传递。

       ```vue
        // 在子组件中
        <!-- BlogPost.vue, 省略了 <script> -->
        <template>
          <div class="blog-post">
            <h4>{{ title }}</h4>
            <button @click="$emit('enlarge-text')">Enlarge text</button>
          </div>
        </template>
         
       ```
  在Vue中，自定义组件可以通过事件来实现数据的传输。在你的例子中，组件通过`$emit`方法触发了一个`enlarge-text`事件。如果你需要在触发事件的同时传递数据给父组件，你可以将数据作为`$emit`方法的第二个参数传递。
  
  下面是如何修改你的组件模板，以便在触发`enlarge-text`事件时携带数据：
  
  ```vue
  <template>
    <div class="blog-post">
      <h4>{{ title }}</h4>
      <!-- 添加数据作为$emit的第二个参数 -->
      <button @click="$emit('enlarge-text', someData)">Enlarge text</button>
    </div>
  </template>
  ```

    2. **父组件中**：监听这个自定义事件，并通过事件处理函数接收数据。

       ```vue
        <BlogPost
        ...
        @enlarge-text="postFontSize += 0.1"
        />
       ```
    ```vue
       <!-- 父组件模板 -->
      <template>
        <div>
          <your-component @enlarge-text="handleEnlargeText"></your-component>
        </div>
      </template>
      
      <script>
      export default {
        methods: {
          // 事件处理器方法接收传递的数据作为参数
          handleEnlargeText(data) {
            // 在这里处理接收到的数据
            console.log(data);
          }
        }
      }
      </script>
  ```

  因为有了 @enlarge-text="postFontSize += 0.1" 的监听，父组件会接收这一事件，从而更新 postFontSize 的值。  
  简而言之就是，在vue里key通过emit来将**自定义事件**和**操作**关联起来，然后在父组件中**通过@监听这个自定义** 事件，然后 **在监听的事件中** 去处理数据。    
  所以如果你想在Vue里去写一个组件的触发，就使用$emit去定义一个组件的触发。

  - 通过双向绑定向父组件传递数据
  ```vue
    <!-- Child.vue -->
    <script setup>
    const model = defineModel()
    
    function update() {
      model.value++
    }
    </script>
    
    <template>
      <div>parent bound v-model is: {{ model }}</div>
    </template>
  ```
  ```vue
    <!-- Parent.vue -->
  <Child v-model="count" />
  ```
  defineModel() 返回的值是一个 ref。它可以像其他 ref 一样被访问以及修改，不过它能起到在父组件和当前变量之间的双向绑定的作用：

  它的 .value 和父组件的 v-model 的值同步；
  当它被子组件变更了，会触发父组件绑定的值一起更新。  
 v-model接受一个参数
  组件上的 v-model 也可以接受一个参数：

  ```html
  <UserName
  v-model:first-name="first"
  v-model:last-name="last"/>
  <MyComponent v-model:title="bookTitle" />
  在子组件中，我们可以通过将字符串作为第一个参数传递给 defineModel() 来支持相应的参数：
  ```
  ```vue
  <!-- MyComponent.vue -->
  <script setup>
  const title = defineModel('title')
  </script>
  
  <template>
    <input type="text" v-model="title" />
  </template>
  
  
  <script setup>
  const firstName = defineModel('firstName')
  const lastName = defineModel('lastName')
  </script>
  
  <template>
    <input type="text" v-model="firstName" />
    <input type="text" v-model="lastName" />
  </template>
  ```

### 2.2 组件事件学习
 1. 通过$emit的方法将事件绑定，下面这个就是将按钮的触碰和someEvent这个事件绑定了。
 ```html
 <!-- MyComponent -->
<button @click="$emit('someEvent')">click me</button>
 ```
 ```html
 父组件key通过@/v-on去监听事件
 <MyComponent @some-event="callback" />
 <MyComponent @some-event.once="callback" />
 ```
 而通过这个父组件的监听可以实现让子组件去触发父组件的回调的功能。  
 2. 如果我想让这个组件触发父组件**回调时带一数据**的话怎么办？
 ```html
  <button @click="$emit('increaseBy', 1)">
    Increase by 1
  </button>
 ```
 ```vue
    <MyButton @increase-by="(n) => count += n" />
    or
    <MyButton @increase-by="increaseCount" />

    function increaseCount(n) {
    count.value += n
      }   
 ```
 就是说在emit的第二个参数就是它回调会携带的一个数值，我们可以用一个函数参数接受，第一种方法是箭头函数，第二种是组件方法。  
 所有传入 $emit() 的额外参数都会被直接传向监听器。举例来说，$emit('foo', 1, 2, 3) 触发后，**监听器函数将会收到这三个参数值**。
 然后我们可以用三个参数去接受它传入的回调。

 3. 现在我想，这个事件只能通过click触发是有限制的，我想通过js判断条件，如果满足再去触发这个事件我该怎么实现？
 在子组件里定义defineEmits()来声明我要触发的时间，然后生命后可以通过emit去触发。
 ```vue
  <script setup>
    const emit =defineEmits(['inFouse','submit'])
    function buttonClick(){
        emit('submit')
    }
  </script>
 ```
4. OK,那基本就都说清楚了，在vue的temp中触发就`@click='$emit('名字'，参数)'`,而defineEmit后用emit('名字')就是在js触发。

### 2.3 Props组件数据传递
 Props是父组件先子组件传递数据的解决方案。他的作用是显式声明它所接受d的props。  
 1. 如何传入props?  
 首先应该在子组件里去声明，就是说一声我这边都需要接受什么数据。声明可以通过数组的方式声明也可以通过对象的方式声明。
 ```vue
  <script setup>
    const props = defineProps(['foo'])
    const props = defineProps({
      title: String,
      likes: Number
    })
    console.log(props.foo)
  </script>
 ```
 父组件中如果想要传输数据就：
 ```vue
  <BlogPost title="My journey with Vue" likes="2"/>
  <BlogPost title="Blogging with Vue" likes="2" />
  <BlogPost title="Why Vue is so fun" likes="2" />
 ```
 2. 传入的数据的值能不能是动态呢，就是父组件给的值是变化的？
 ```vue
  <!-- 根据一个变量的值动态传入 -->
  <BlogPost :title="post.title" />
  
  <!-- 根据一个更复杂表达式的值动态传入 -->
  <BlogPost :title="post.title + ' by ' + post.author.name" />
 ```
 通过这种方式，可以将一个动态的值传入，这个值变化，子组件的也会变化。  
 3. 传递不同类型的值，传值可以为number，boolean，array等等，但是基于他的语法可能它有时是反直觉的。
    ```vue
    传入Number类型的值
    <!-- 虽然 `42` 是个常量，我们还是需要使用 v-bind -->
    <!-- 因为这是一个 JavaScript 表达式而不是一个字符串 -->
    <BlogPost :likes="42" />
    
    <!-- 根据一个变量的值动态传入 -->
    <BlogPost :likes="post.likes" />
  
    传入boolean值
    <!-- 仅写上 prop 但不传值，会隐式转换为 `true` -->
    <BlogPost is-published />
    
    <!-- 虽然 `false` 是静态的值，我们还是需要使用 v-bind -->
    <!-- 因为这是一个 JavaScript 表达式而不是一个字符串 -->
    <BlogPost :is-published="false" />
    
    <!-- 根据一个变量的值动态传入 -->
    <BlogPost :is-published="post.isPublished" />
  
    传入Array值
    <!-- 虽然这个数组是个常量，我们还是需要使用 v-bind -->
    <!-- 因为这是一个 JavaScript 表达式而不是一个字符串 -->
    <BlogPost :comment-ids="[234, 266, 273]" />
    
    <!-- 根据一个变量的值动态传入 -->
    <BlogPost :comment-ids="post.commentIds" />
  
    传入Object值
    <!-- 虽然这个对象字面量是个常量，我们还是需要使用 v-bind -->
    <!-- 因为这是一个 JavaScript 表达式而不是一个字符串 -->
    <BlogPost
            :author="{
        name: 'Veronica',
        company: 'Veridian Dynamics'
      }"
    />
    
    <!-- 根据一个变量的值动态传入 -->
    <BlogPost :author="post.author" />
    ```
    就简而言之来说，你传入值如果你想表达一个字符串的就用props的属性，如果你想表达的是一个表达式就用:props的属性。
 4. 然后props是一个单向数据流，就是只能父组件往子组件里传数据，子组件没法通过props向父组件传。  
 但是我们很多时候其实是想要改变这个props的数据的，比如我想要获得一个**props局部数据的情况**/我想对**props的数据进行转换的情况**。





### 2.4 v-model组件数据传递
v-model是一个语法糖，它可以让我们更方便的去实现双向绑定。
 1. v-model的使用方法
 ```vue
  <!-- Child.vue -->
  <script setup>
  const model = defineModel()
  
  function update() {
    model.value++
  }
  </script>
  
  <template>
    <div>parent bound v-model is: {{ model }}</div>
  </template>
 ```
 ```vue
  <!-- Parent.vue -->
  <Child v-model="count" />
 ```
 defineModel() 返回的值是一个 ref。它可以像其他 ref 一样被访问以及修改，不过它能起到在父组件和当前变量之间的双向绑定的作用：
 它的 .value 和父组件的 v-model 的值同步；
 当它被子组件变更了，会触发父组件绑定的值一起更新。  
2. v-model接受一个参数
 父组件上的 v-model 也可以接受一个参数：
  ```html
  <UserName
  v-model:first-name="first"
  v-model:last-name="last"/>
  <MyComponent v-model:title="bookTitle" />
  在子组件中，我们可以通过将字符串作为第一个参数传递给 defineModel() 来支持相应的参数：
  ```
  ```vue
  <!-- MyComponent.vue -->
  <script setup>
  const title = defineModel('title')
  </script>
  
  <template>
    <input type="text" v-model="title" />
  </template>
  
  <script setup>
  const firstName = defineModel('firstName')
  const lastName = defineModel('lastName')
  </script>
  
  <template>
    <input type="text" v-model="firstName" />
    <input type="text" v-model="lastName" />
  </template>
  ```
3. v-model修饰符
 1. .lazy
 默认情况下，v-model 会在每次 input 事件后更新数据 (IME 拼字阶段的状态例外)。你可以添加 lazy 修饰符来改为在每次 change 事件后更新数据：
 ```vue
  <!-- 在 "change" 事件后同步更新而不是 "input" -->
  <input v-model.lazy="msg" />
 ```
 2. .number
 如果你想让用户输入自动转换为数字，你可以在 v-model 后添加 .number 修饰符来管理输入：
 ```vue
 <input v-model.number="age" />
 ```
 如果该值无法被 parseFloat() 处理，那么将返回原始值。 number 修饰符会在输入框有 type="number" 时自动启用。
 3. .trim
    如果你想自动过滤用户输入的首尾空白字符，可以添加 trim 修饰符到 v-model 上：
    ```vue
    <input v-model.trim="msg" />
    ```



### 2.5 透传 Attributes
 1. attribute继承
     透传attribute是指将父组件的attribute传递给子组件。如果这个属性没有被声明为**props和emits**，那么这个属性会被传递给子组件。
     ```vue
      <Child id="foo" class="bar" />
     ```
     最常见的例子就是 class、style 和 id。  当一个组件以单个元素为根作渲染时，透传的 attribute 会自动被添加到根元素上。举例来说，假如我们有一个 <MyButton> 组件，它的模板长这样：
    
     ```vue
      <!-- <MyButton> 的模板 -->
      <button>click me</button>
      一个父组件使用了这个组件，并且传入了 class：
      
      <MyButton class="large" />
      最后渲染出的 DOM 结果是：
      
      <button class="large">click me</button>
     ```
     简单而言就是如果你在组件外添加的属性，既不是props也不是emits，这个属性会自动加载给组件里的最外层数据。  
     一般可以用来class和style的合并，就是你外边写了class，那里面也会合并过来。
 2. v-on监听器基础，就是说你可以在组件上添加事件监听器，然后在组件内部去触发这个事件。
     ```vue
      <Child v-on:custom-event="handleCustomEvent" />
     ```
     click 监听器会被添加到 `<Child>`的根元素，即那个原生的 `<button>` 元素之上。当原生的 `<button>` 被点击，会触发父组件的 onClick 方法。  
     同样的，如果原生`button`元素自身也通过 v-on 绑定了一个事件监听器，则这个监听器和从父组件继承的监听器都会被触发。  
     所以，这个监听其实可以打通子组件和父组件之间的联系。  
 3. 透传具有连续性  
     就是可以一个透传一个，A传B，B传C可以连续传。


