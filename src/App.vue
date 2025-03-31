<template>
  <input class="text-input" type="text" readonly v-model="value" @click="$refs.PlateNoKeyboardRef.open()">

  <plate-no-keyboard
    ref="PlateNoKeyboardRef"
    v-model="value"
    @change="onChange"
    @delete="onDelete"
    @print="onPrint"
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
      value: ''
    }
  },
  methods: {
    onChange (v) {
      console.log('onChange', v)
    },
    onDelete (v) {
      console.log('onDelete', v)
    },
    onPrint (v) {
      console.log('onPrint', v)
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
