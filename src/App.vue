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

<script>
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
</script>

<style>
body, html {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
}
#app {
  width: 100%;
  height: 100%;
  background-image: url('~@/assets/bg.png');
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
}
.text-input {
  width: 100%;
  font-size: 24px;
  line-height: 30px;
  padding: 10px;
  box-sizing: border-box;
}
</style>
