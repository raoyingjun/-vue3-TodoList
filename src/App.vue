<template>
  <div class="app">
    <TodoList/>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import TodoList from './components/TodoList.vue'

export default defineComponent({
  components: {
    TodoList
  }
})
</script>

<style lang="scss">
ul {
  padding: 0
}
.app {
  text-align: center;
  margin: 100px auto;
}
@media (max-width: 768px) {
  .app {
    width: 100%;
  }
}
</style>
