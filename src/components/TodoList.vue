<template>
  <h3>Vue3 Demo 待办事项</h3>
  <TodoForm @add="add">添加事项</TodoForm>
  <ul>
    <li
      @remove="removeAlert"
      v-model:completed="todoItem.completed"
      :index="index"
      :text="todoItem.text"
      v-for="(todoItem, index) in todoList"
      v-is="'TodoItem'"
      :key="index">
      <template #remove>删除该事项</template>
    </li>
  </ul>
  <Confirm
    v-model="alertVisible"
    @confirm="confirmRemove"
    content="确认删除该项吗?"
    confirm-text="确认"/>
</template>

<script lang="ts">
import { defineAsyncComponent, defineComponent, onMounted, ref } from 'vue'
import { TodoItemType } from '@/assets/ts/interfaces.ts'

export default defineComponent({
  setup () {
    const todoList = ref<TodoItemType[]>([])
    const alertVisible = ref(false)
    const currentIndex = ref(0)
    const add = (text: string) => {
      const todoItem: TodoItemType = {
        completed: false,
        text
      }
      todoList.value.push(todoItem)
    }
    const removeAlert = (index: number) => {
      alertVisible.value = true
      currentIndex.value = index
    }
    const confirmRemove = () => {
      todoList.value.splice(currentIndex.value, 1)
    }

    onMounted(() => {
      add('学习一本NodeJs基础书籍')
      add('复习排序算法之八大排序')
    })
    return {
      todoList,
      alertVisible,
      currentIndex,
      add,
      removeAlert,
      confirmRemove
    }
  },
  components: {
    TodoForm: defineAsyncComponent(() => import('./TodoForm.vue')),
    TodoItem: defineAsyncComponent(() => import('./TodoItem.vue')),
    Confirm: defineAsyncComponent(() => import('./Confirm.vue'))
  }
})
</script>

<style lang="scss">
</style>
