## 基于vue3的TodoList

### 用法
```
cd Vue3-TodoList & npm install
```

### 功能
这是一个使用vue-cli搭建的vue3的TodoList例子，包含：
* 添加事项
* 删除事项
* 弹出式对话框
* 修改事项状态

### 介绍
用到了如下vue3的特性：
* 全部代码使用的是组合式api进行实现
* 新增的内置`<teleport>`标签
* transition组件的class命名`v-enter`修改为`v-enter-from`
* 组件不再必须拥有唯一根节点
* 使用新版的`v-model`用于双向数据绑定，以及带参的`v-model`绑定
* 定义组件方式使用`defineComponent`
* 引入异步组件使用`defineAsyncComponent`
* 新增`emits`对象。指定组件要向父组件发出的事件

### 其他
其它用到了些：
* 该demo基于typescript
* 使用了scss预处理器
* 包含自己手写的Confirm确认框组件，也可以用作Alert提示框组件使用
