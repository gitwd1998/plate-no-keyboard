<template>
  <transition
    @before-enter="onBeforeEnter"
    @after-enter="onAfterEnter"
    @before-leave="onBeforeLeave"
    @after-leave="onAfterLeave"
  >
    <div v-if="visible" ref="plateNoKeyboardRef" class="plate-no-keyboard">
      <button class="value-btn" v-for="(value, index) in keyboard" :key="index" :disabled="modelValue.length >= maxlength" @touchstart="onPrint(value)">{{ value }}</button>
      <button class="switch-btn" @touchstart="toggle = !toggle">
        <svg t="1743437048443" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="10258" width="26" height="26"><path d="M512 76.53333333C266.66666667 76.53333333 70.4 272.8 70.4 518.13333333S266.66666667 959.73333333 512 959.73333333s441.6-196.26666667 441.6-441.6C953.6 278.93333333 757.33333333 76.53333333 512 76.53333333zM377.06666667 150.13333333c-24.53333333 24.53333333-42.93333333 61.33333333-61.33333334 98.13333334-18.4-6.13333333-36.8-18.4-49.06666666-30.66666667 30.66666667-30.66666667 67.46666667-49.06666667 110.4-67.46666667zM229.86666667 248.26666667c18.4 18.4 42.93333333 36.8 67.46666666 49.06666666-18.4 61.33333333-30.66666667 128.8-30.66666666 196.26666667H119.46666667c6.13333333-92 49.06666667-177.86666667 110.4-245.33333333zM119.46666667 542.66666667H266.66666667c0 73.6 12.26666667 134.93333333 30.66666666 196.26666666-24.53333333 12.26666667-49.06666667 30.66666667-73.6 49.06666667-55.2-61.33333333-98.13333333-147.2-104.26666666-245.33333333zM266.66666667 824.8c12.26666667-12.26666667 36.8-24.53333333 55.2-36.8 18.4 36.8 36.8 73.6 61.33333333 98.13333333-49.06666667-12.26666667-85.86666667-36.8-116.53333333-61.33333333z m220.8 79.73333333c-49.06666667-12.26666667-98.13333333-67.46666667-128.8-141.06666666 36.8-12.26666667 79.73333333-24.53333333 128.8-24.53333334v165.6z m0-214.66666666c-49.06666667 0-98.13333333 12.26666667-141.06666667 30.66666666-18.4-49.06666667-24.53333333-110.4-30.66666667-177.86666666h171.73333334v147.2z m0-196.26666667H315.73333333c0-61.33333333 12.26666667-122.66666667 24.53333334-177.86666667 49.06666667 18.4 92 30.66666667 147.2 30.66666667v147.2z m0-196.26666667c-49.06666667 0-85.86666667-12.26666667-128.8-24.53333333C389.33333333 199.2 438.4 144 487.46666667 131.73333333v165.6zM757.33333333 217.6c-12.26666667 12.26666667-36.8 24.53333333-55.2 36.8-18.4-36.8-36.8-73.6-61.33333333-98.13333333 49.06666667 12.26666667 85.86666667 30.66666667 116.53333333 61.33333333zM536.53333333 131.73333333c49.06666667 12.26666667 98.13333333 67.46666667 128.8 141.06666667-42.93333333 18.4-79.73333333 24.53333333-128.8 24.53333333V131.73333333z m0 214.66666667c49.06666667 0 98.13333333-12.26666667 141.06666667-30.66666667 12.26666667 49.06666667 24.53333333 110.4 24.53333333 177.86666667H536.53333333V346.4z m0 196.26666667h171.73333334c0 61.33333333-12.26666667 122.66666667-24.53333334 177.86666666-49.06666667-18.4-92-24.53333333-147.2-30.66666666V542.66666667z m0 361.86666666v-165.6c49.06666667 0 85.86666667 12.26666667 128.8 24.53333334-30.66666667 79.73333333-79.73333333 128.8-128.8 141.06666666z m110.4-18.4c24.53333333-24.53333333 42.93333333-61.33333333 61.33333334-98.13333333l55.2 36.8c-36.8 24.53333333-73.6 49.06666667-116.53333334 61.33333333z m147.2-98.13333333c-18.4-18.4-42.93333333-36.8-73.6-49.06666667 18.4-61.33333333 30.66666667-122.66666667 30.66666667-196.26666666h147.2c0 98.13333333-42.93333333 184-104.26666667 245.33333333zM757.33333333 493.6c0-73.6-12.26666667-134.93333333-30.66666666-196.26666667 24.53333333-12.26666667 49.06666667-30.66666667 73.6-49.06666666 61.33333333 61.33333333 104.26666667 147.2 110.4 245.33333333H757.33333333z" fill="#000000" p-id="10259"></path></svg>
      </button>
      <button class="delete-btn" :disabled="!modelValue" @touchstart="onDelete">
        <svg t="1743260041599" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="4757" width="26" height="26"><path d="M856.2 890.5H402.4c-55.3-0.1-108-23.4-145.4-64.2L23 571c-30.7-33.4-30.7-84.8 0-118.2l233.9-255.1c37.3-40.8 90.1-64.1 145.4-64.2h453.8c92.7 0.2 167.8 75.4 167.8 168.1v420.7c0.1 92.8-75 168-167.7 168.2zM402.6 184.9c-41 0-80 17.2-107.8 47.4L60.9 487.6c-12.8 13.7-12.8 34.9 0 48.6l233.7 255.3c27.7 30.2 66.8 47.4 107.8 47.4h454c64.4-0.1 116.5-52.4 116.5-116.8V301.6c0-64.4-52.2-116.6-116.5-116.8H402.6z m323.7 471c-6.8 0-13.4-2.7-18.2-7.5l-100-100.2L508 648.4c-9.9 10.1-26.1 10.2-36.2 0.3-10.1-9.9-10.2-26.1-0.3-36.2l0.4-0.4 100-100.2-100-100.2c-10.1-9.9-10.3-26.1-0.4-36.2 9.9-10.1 26.1-10.3 36.2-0.4l0.4 0.4 100 100.2 100-100.2c10-10 26.2-10 36.2 0 10 10 10 26.2 0 36.2l-100 100.2 100.2 100.2c10 10 10 26.3-0.1 36.3-4.8 4.8-11.3 7.5-18.1 7.5z" p-id="4758" fill="#000000"></path></svg>
      </button>
    </div>
  </transition>
</template>

<script setup>
import { ref, defineExpose, defineProps, defineEmits, computed, nextTick } from 'vue'

const emits = defineEmits(['update:modelValue', 'change', 'print', 'delete', 'open', 'opened', 'close', 'closed'])

const props = defineProps({
  maxlength: {
    type: [Number, String],
    default: 8
  },
  modelValue: {
    type: String,
    default: ''
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

const printValue = ref(props.modelValue)

const plateNoKeyboardRef = ref(null)

const visible = ref(false)

const toggle = ref(Boolean(props.modelValue))

const keyboard = computed(() => {
  return toggle.value
    ? [
        '1', '2', '3', '4', '5', '6', '7', '8', '9', '0',
        'Q', 'W', 'E', 'R', 'T', 'Y', 'U', 'O', 'P', '学',
        'A', 'S', 'D', 'F', 'G', 'H', 'J', 'K', 'L', '临',
        'Z', 'X', 'C', 'V', 'B', 'N', 'M', '挂'
      ]
    : [
        '京', '津', '晋', '冀', '蒙', '辽', '吉', '黑', '沪', '苏',
        '浙', '皖', '闽', '赣', '鲁', '豫', '湘', '鄂', '粤', '桂',
        '琼', '渝', '川', '云', '贵', '藏', '陕', '甘', '青', '宁',
        '新', '台', '港', '澳', '使', '领', '警', '军'
      ]
})

function onPrint (value) {
  if (printValue.value.length >= props.maxlength) return
  printValue.value += value
  toggle.value = Boolean(printValue.value)
  emits('print', value)
  emits('update:modelValue', printValue.value)
  emits('change', printValue.value)
}
function onDelete () {
  if (!printValue.value.length) return
  printValue.value = printValue.value.slice(0, -1)
  toggle.value = Boolean(printValue.value)
  emits('delete')
  emits('update:modelValue', printValue.value)
  emits('change', printValue.value)
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
.plate-no-keyboard button.switch-btn {
  grid-column: 1 / 2;
  grid-row-start: 4;
}
.plate-no-keyboard button.delete-btn {
  grid-column: -2 / -1;
}
.v-enter-from, .v-leave-to {
  transform: translateY(100%);
}
.v-enter-to, .v-leave-from {
  transform: translateY(0);
}
</style>
