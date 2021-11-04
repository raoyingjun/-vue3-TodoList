<template>
  <p>
    <input type="text" v-model="text" placeholder="添加待办事项" @keyup.enter="handleSubmit">
    <button @click="handleSubmit">
      <slot>提交</slot>
    </button>
    <Confirm
      is-alert
      v-model="alertVisible"
      title="提示"
      content="输入不能为空"
      confirm-text="我知道了"/>
  </p>
</template>

<script lang="ts">
import { defineAsyncComponent, defineComponent, ref } from 'vue'

export default defineComponent({
  components: {
    Confirm: defineAsyncComponent(() => import('./Confirm.vue'))
  },
  emits: ['add'],
  setup (props, { emit }) {
    const text = ref('')
    const alertVisible = ref(false)
    const handleSubmit = () => {
      if (!text.value) {
        alertVisible.value = true
        return
      }
      emit('add', text.value)
    }
    return {
      text,
      handleSubmit,
      alertVisible
    }
  }
})
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
</style>
