<template>
  <transition
    @before-enter="onBeforeEnter"
    @after-enter="onAfterEnter"
    @before-leave="onBeforeLeave"
    @after-leave="onAfterLeave"
  >
    <div v-if="visible" ref="plateNoKeyboardRef" class="plate-no-keyboard">
      <button class="value-btn" v-for="(value, index) in keyboard" :key="index" :disabled="modelValue.length >= maxlength" @touchstart="onPrint(value)">{{ value }}</button>
      <button class="delete-btn" :disabled="!modelValue" @touchstart="onDelete">
        <svg t="1743260041599" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="4757" width="26" height="26"><path d="M856.2 890.5H402.4c-55.3-0.1-108-23.4-145.4-64.2L23 571c-30.7-33.4-30.7-84.8 0-118.2l233.9-255.1c37.3-40.8 90.1-64.1 145.4-64.2h453.8c92.7 0.2 167.8 75.4 167.8 168.1v420.7c0.1 92.8-75 168-167.7 168.2zM402.6 184.9c-41 0-80 17.2-107.8 47.4L60.9 487.6c-12.8 13.7-12.8 34.9 0 48.6l233.7 255.3c27.7 30.2 66.8 47.4 107.8 47.4h454c64.4-0.1 116.5-52.4 116.5-116.8V301.6c0-64.4-52.2-116.6-116.5-116.8H402.6z m323.7 471c-6.8 0-13.4-2.7-18.2-7.5l-100-100.2L508 648.4c-9.9 10.1-26.1 10.2-36.2 0.3-10.1-9.9-10.2-26.1-0.3-36.2l0.4-0.4 100-100.2-100-100.2c-10.1-9.9-10.3-26.1-0.4-36.2 9.9-10.1 26.1-10.3 36.2-0.4l0.4 0.4 100 100.2 100-100.2c10-10 26.2-10 36.2 0 10 10 10 26.2 0 36.2l-100 100.2 100.2 100.2c10 10 10 26.3-0.1 36.3-4.8 4.8-11.3 7.5-18.1 7.5z" p-id="4758" fill="#000000"></path></svg>
      </button>
    </div>
  </transition>
</template>

<script setup>
import { ref, defineModel, defineExpose, defineProps, defineEmits, computed, nextTick } from 'vue'

const emits = defineEmits(['change', 'print', 'delete', 'open', 'opened', 'close', 'closed'])

const props = defineProps({
  maxlength: {
    type: [Number, String],
    default: 8
  },
  firstExtend: {
    type: Array,
    default: () => []
  },
  otherExtend: {
    type: Array,
    default: () => []
  }
})

const modelValue = defineModel()

const plateNoKeyboardRef = ref(null)

const visible = ref(false)

const keyboard = computed(() => {
  return modelValue.value
    ? [
        '1', '2', '3', '4', '5', '6', '7', '8', '9', '0',
        'Q', 'W', 'E', 'R', 'T', 'Y', 'U', 'O', 'P', 'A',
        'S', 'D', 'F', 'G', 'H', 'J', 'K', 'L', 'Z', 'X',
        'C', 'V', 'B', 'N', 'M', ...props.otherExtend
      ]
    : [
        '京', '津', '晋', '冀', '蒙', '辽', '吉', '黑', '沪',
        '苏', '浙', '皖', '闽', '赣', '鲁', '豫', '湘', '鄂',
        '粤', '桂', '琼', '渝', '川', '云', '贵', '藏', '陕',
        '甘', '青', '宁', '新', '港', '澳', '台', ...props.firstExtend
      ]
})

function onPrint (value) {
  if (modelValue.value.length >= props.maxlength) return
  const newValue = modelValue.value + value
  modelValue.value = newValue
  emits('print', value)
  emits('change', newValue)
}
function onDelete () {
  if (!modelValue.value.length) return
  const newValue = modelValue.value.slice(0, -1)
  modelValue.value = newValue
  emits('delete')
  emits('change', newValue)
}
function listenerTouchstart (e) {
  if (plateNoKeyboardRef.value?.contains(e.target)) return
  onClose()
}
function onOpen () {
  if (visible.value) return
  visible.value = true
  nextTick(() => {
    window.addEventListener('touchstart', listenerTouchstart)
  })
}
function onClose () {
  if (!visible.value) return
  visible.value = false
  window.removeEventListener('touchstart', listenerTouchstart)
}

defineExpose({
  open: onOpen,
  close: onClose
})

function onBeforeEnter () {
  emits('open')
}
function onAfterEnter () {
  const { height } = plateNoKeyboardRef.value?.getBoundingClientRect()
  emits('opened', height)
}
function onBeforeLeave () {
  emits('close')
}
function onAfterLeave () {
  emits('closed')
}
</script>

<style scoped>
.plate-no-keyboard {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 10000;
  display: grid;
  padding: 12px 8px 30px;
  column-gap: 8px;
  row-gap: 12px;
  background-color: rgba(230, 230, 230, 0.8);
  backdrop-filter: saturate(100%) blur(4px);
  grid-template-columns: repeat(10, 1fr);
  transition: 0.1s;
}
.plate-no-keyboard button {
  display: inline-flex;
  justify-content: center;
  user-select: none;
  font-size: 18px;
  line-height: 26px;
  border: none;
  border-radius: 4px;
  padding: 8px 0;
  background-color: rgba(255, 255, 255, 0.8);
  backdrop-filter: saturate(100%) blur(4px);
  color: #1f1f1f;
}
.plate-no-keyboard button:active {
  background-color: rgba(0, 0, 0, 0.1);
}
.plate-no-keyboard button[disabled] {
  background-color: rgba(0, 0, 0, 0.05);
}
.plate-no-keyboard button.delete-btn {
  grid-column: -3 / -1;
}
.v-enter-from, .v-leave-to {
  transform: translateY(100%);
}
.v-enter-to, .v-leave-from {
  transform: translateY(0);
}
</style>
