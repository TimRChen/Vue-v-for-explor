## Vue 2.0 v-for 响应式key, index及item.id参数对v-bind:key值造成差异研究

> v-for响应式key, index及item.id参数对v-bind:key值造成差异研究

### 实验背景
>   通常情况下，我们渲染一个li列表，采用v-for指令进行渲染，我们需要给渲染的每一项元素绑定一个key值，其实绑定该key值是可选的，但会引起警告。使用v-for参数的过程中，由于v-for提供三个参数，分别是: value, key, index。对其哪一个作为元素绑定key值更能得到我们想要的响应式渲染作出实验。

### 实验目的
>   总结出在采用不同参数作为元素绑定key值时，出现的不同的渲染结果，得出最优渲染方案

### 实验准备
####  我们准备第三个可以作为绑定key值的变量，分别是: 
*   渲染item自带属性id
*   v-for提供的key
*   v-for提供的index

#### 我们制定一个参照表格
***
| `li绑定key值类型` | id | index | key |
| --- | --- | --- | --- |
| 实验一 | 选取 | x | x |
| 实验二 | x | 选取 | x |
| 实验三 | x | x | 选取 |
***
### 实验一
*   li绑定key值为自带属性id
*   分别控制两个变量：改变id值，对li进行排序

##### 实验vue.js代码
```js
// items data
items: [
    {
        id: 2,
    },
    {
        id: 1,
    },
    {
        id: 3,
    },
    {
        id: 4,
    },
]
```
```html
<!-- dom constructor -->
<template>
  <div class="content">
    <ul>
      <li class="animate">对照组</li>
      <li v-for="(item, key, index) in items" class="animate" v-bind:key="item.id">{{item.id}}</li>
      <!-- 当前绑定值为item.id  -->
    </ul>
    </div>
  </div>
</template>
```
首先使用了item.id作为绑定的key值，我们来看下效果：
[渲染效果demo](https://timrchen.github.io/Responsive-study-demo/)

1.  改变第一个元素的id值，第一个li元素重新渲染，其余三个li元素与对照组速度始终保持一致，没有变化，说明li元素**单独**渲染
2.  为了验证1.观点，我们对实验组按照升序进行排列，查看DOM结构，当改变第一个元素位置时，第一个li元素重新渲染，其余三个li元素不重新渲染且与对照组速度始终保持一致，说明第一个li元素单独渲染，验证1.结论


***
### 实验二
*   li绑定key值为 v-for提供的index参数
*   分别控制两个变量：改变id值，对li进行排序

##### 实验vue.js代码
```js
// items data
items: [
    {
        id: 2,
    },
    {
        id: 1,
    },
    {
        id: 3,
    },
    {
        id: 4,
    },
]
```
```html
<!-- dom constructor -->
<template>
  <div class="content">
    <ul>
      <li class="animate">对照组</li>
      <li v-for="(item, key, index) in items" class="animate" v-bind:key="index">{{item.id}}</li>
      <!-- 当前绑定值为index  -->
    </ul>
    </div>
  </div>
</template>
```
在实验二中，使用v-for提供的index参数作为绑定的key值，我们来看下效果：
[渲染效果demo](https://timrchen.github.io/Responsive-study-demo/)

1.  改变第一个元素的id值，第一个li元素与其余三个li元素与对照组速度始终保持一致，没有变化，说明绑定index值并未对li渲染造成影响
2.  为了验证1.观点，我们对实验组按照升序进行排列，查看DOM结构，当改变第一个元素位置时，第一个li元素重新渲染，其余三个li元素也重新渲染均且与对照组速度始终保持一致，说明所有li元素均重新渲染，验证1.结论


***
### 实验三
*   li绑定key值为 v-for提供的key参数
*   分别控制两个变量：改变id值，对li进行排序

##### 实验vue.js代码
```js
// items data
items: [
    {
        id: 2,
    },
    {
        id: 1,
    },
    {
        id: 3,
    },
    {
        id: 4,
    },
]
```
```html
<!-- dom constructor -->
<template>
  <div class="content">
    <ul>
      <li class="animate">对照组</li>
      <li v-for="(item, key, index) in items" class="animate" v-bind:key="key">{{item.id}}</li>
      <!-- 当前绑定值为key  -->
    </ul>
    </div>
  </div>
</template>
```
在实验二中，使用v-for提供的key参数作为绑定的key值，我们来看下效果：
[渲染效果demo](https://timrchen.github.io/Responsive-study-demo/)

1.  改变第一个元素的id值，第一个li元素与其余三个li元素与对照组速度始终保持一致，没有变化，说明绑定key值并未对li渲染造成影响
2.  为了验证1.观点，我们对实验组按照升序进行排列，查看DOM结构，当改变第一个元素位置时，第一个li元素重新渲染，其余三个li元素也重新渲染均且与对照组速度始终保持一致，说明所有li元素均重新渲染，验证1.结论

***
### 实验结论
>   经过三次对照实验（我们的实验采用了控制变量法，对照实验法进行），我们可以得出结论：使用v-for渲染元素时，使用元素自身的id属性去指定渲染元素的key值有利于单个元素的重新渲染，若采用其他如v-for提供的index, key等值，在改变渲染出来的DOM结构时，会触发所有元素的**重新渲染**，当数据过大时，可能会造成性能负担。

### 总结
#### 当我们在使用v-for进行渲染时，尽可能使用渲染元素自身属性的id给渲染的元素绑定一个key值，这样在当前渲染元素的DOM结构发生变化时，能够单独响应该元素而不触发所有元素的渲染。

### 研究成员
[TimRChen](https://github.com/TimRChen)
[libook](https://github.com/libook)
