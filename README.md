# plate-no-keyboard

### 介绍
* plate-no-keyboard是一款基于vue3的车牌号输入控件。

### 使用

* 下载
```
npm install plate-no-keyboard
```

* 在main.js中引入
```js
import PlateNoKeyboard from 'plate-no-keyboard'
import 'plate-no-keyboard/dist/index.css'

createApp(App).use(PlateNoKeyboard).mount('#app')
```

* 在页面中使用
```html
<template>
  <!-- 系统键盘输入 -->
  <input class="text-input" type="text" v-model="value">
  <!-- 插件键盘输入 -->
  <input class="text-input" type="text" readonly v-model="value" @click="visible = !visible">

  <plate-no-keyboard
    v-model="value"
    v-model:visible="visible"
    @update:modelValue="onChange"
    @print="onPrint"
    @delete="onDelete"
    @open="onOpen"
    @opened="onOpened"
    @close="onClose"
    @closed="onClosed"
  />
</template>
```
```js
export default {
  name: 'App',
  data () {
    return {
      visible: false,
      value: ''
    }
  },
  methods: {
    onChange (v) {
      console.log('onChange', v)
    },
    onPrint (v) {
      console.log('onPrint', v)
    },
    onDelete (v) {
      console.log('onDelete', v)
    },
    onOpen (v) {
      console.log('onOpen', v)
    },
    onOpened (v) {
      console.log('onOpened', v)
    },
    onClose (v) {
      console.log('onClose', v)
    },
    onClosed (v) {
      console.log('onClosed', v)
    }
  }
}
```

* 展示效果
<div style="display: flex">
  <img src="./src/assets/IMG_7143.png" alt="展示效果" style="width: 300px;">
  <img src="./src/assets/IMG_7144.png" alt="展示效果" style="width: 300px;">
  <img src="./src/assets/IMG_7145.png" alt="展示效果" style="width: 300px;">
</div>


### Props
名字 | 类型 | 默认值 | 说明
-- | -- | -- | --
v-model | `String` | "" |  默认车牌号
v-model:visible | `Boolean` | false |  键盘是否显示
maxlength | `String` `Number` | 8 |  最大长度

### Events
名字 | 参数 | 说明
-- | -- | --
update:modelValue | value: String | 绑定车牌号变化时触发
print | key: String | 键盘按键按下时触发
delete | - | 删除按键按下时触发
open | - | 打开键盘时触发
opened | height: Number | 打开键盘过渡效果完成时触发
close | - | 关闭键盘时触发
closed | - | 关闭键盘过渡效果完成时触发
