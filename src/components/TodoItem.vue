<template>
  <p>
    {{ `（${index + 1}）${data.completed ? '已完成' : '未完成'}` }}：{{ data.text }}
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

import { defineAsyncComponent, defineComponent, PropType } from 'vue'
import { TodoItemType } from '@/assets/ts/interfaces'

export default defineComponent({
  props: {
    data: {
      type: Object as PropType<TodoItemType>,
      required: true
    },
    index: {
      type: Number,
      required: true
    }
  },
  emits: ['remove', 'statusChange'],
  methods: {
    handleRemove () {
      this.$emit('remove', this.index)
    },
    changeStatus () {
      this.$emit('statusChange', this.index, !this.data.completed)
    }
  }
})
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
</style>
