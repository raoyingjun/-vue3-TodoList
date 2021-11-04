<template>
  <p>
    {{ `（${index + 1}）${completed ? '已完成' : '未完成'}` }}：{{ text }}
  </p>
  <p>
    <button @click="changeStatus">
      <slot name="status">修改状态</slot>
    </button>
    <button @click="handleRemove">
      <slot name="remove">移除该项</slot>
    </button>
  </p>
</template>

<script lang="ts">

import { defineComponent, toRefs } from 'vue'

export default defineComponent({
  props: {
    completed: {
      type: Boolean,
      required: true
    },
    index: {
      type: Number,
      required: true
    },
    text: {
      type: String,
      required: true
    }
  },
  emits: ['remove', 'update:completed'],
  setup (props, { emit }) {
    const { index, completed } = toRefs(props)
    const handleRemove = () => {
      emit('remove', index.value)
    }
    const changeStatus = () => {
      emit('update:completed', !completed.value)
    }
    return {
      handleRemove,
      changeStatus
    }
  }
})
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
</style>
