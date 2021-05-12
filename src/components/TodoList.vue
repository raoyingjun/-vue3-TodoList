<template>
  <h3>Vue3 Demo 待办事项</h3>
  <TodoForm @add="add">添加事项</TodoForm>
  <ul>
    <li
      @status-change="statusChange"
      @remove="removeAlert"
      :data="todoItem"
      :index="index"
      v-for="(todoItem, index) in todoList"
      v-is="'TodoItem'"
      :key="index">
      <template v-slot:remove>删除该事项</template>
    </li>
  </ul>
  <Alert
    v-model="visible"
    @confirm="confirmRemove"
    content="确认删除该项吗?"
    confirm-text="确认"/>
</template>

<script lang="ts">
import { defineAsyncComponent, defineComponent } from 'vue'
import { TodoItemType } from '@/assets/ts/interfaces.ts'

export default defineComponent({
  data () {
    return {
      todoList: [] as Array<TodoItemType>,
      visible: false,
      currentIndex: 0
    }
  },
  methods: {
    add (text: string) {
      const todoItem: TodoItemType = {
        completed: false,
        text
      }
      this.todoList.push(todoItem)
    },
    removeAlert (index: number) {
      this.visible = true
      this.currentIndex = index
    },
    confirmRemove () {
      this.todoList.splice(this.currentIndex, 1)
    },
    statusChange (index: number, completed: boolean) {
      this.todoList[index].completed = completed
    }
  },
  created () {
    this.add('学习一本NodeJs基础书籍')
    this.add('复习排序算法之八大排序')
  },
  components: {
    TodoForm: defineAsyncComponent(() => import('./TodoForm.vue')),
    TodoItem: defineAsyncComponent(() => import('./TodoItem.vue')),
    Alert: defineAsyncComponent(() => import('./Alert.vue'))
  }
})
</script>

<style lang="scss">
</style>
