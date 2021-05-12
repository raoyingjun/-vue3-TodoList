<template>
  <p>
    <input type="text" v-model="text" placeholder="添加待办事项" @keyup.enter="handleSubmit">
    <button @click="handleSubmit">
      <slot>提交</slot>
    </button>
  </p>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  data () {
    return {
      text: ''
    }
  },
  emits: ['add'],
  methods: {
    handleSubmit () {
      this.$emit('add', this.text)
    }
  }
})
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
</style>
