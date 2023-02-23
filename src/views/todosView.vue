<script setup>
import { ref, reactive, computed, watch } from 'vue';
import TodoItem from '@/components/TodoItem.vue';
import TodoTab from '@/components/TodoTab.vue';

const todos = ref([
  {
    finished: false,
    id: 0,
    title: 'This is a Demo',
  },
]);
const newTodo = ref('');
const filter = ref('all');
const nextTodoId = ref(0);
const scrollbarRef = ref('')

const filterTodos = computed(() => {
  if (filter.value == 'all') {
    return todos.value;
  }
  const finished = filter.value === 'completed';
  return todos.value.filter((todo) => todo.finished === finished);
});

watch(todos, (currTodos, oldTodos) => {
  var ids = currTodos.map((todo) => todo.id);
  nextTodoId.value = Math.max.apply(null, ids) + 1;
});

const addTodo = () => {
  if (!newTodo.value) {
    return false;
  }
  todos.value.unshift({
    id: nextTodoId.value,
    title: newTodo.value,
    finished: false,
  });
  newTodo.value = '';
  scrollbarRef.value.setScrollTop(0)
};
const removeTodo = (todoId) => {
  todos.value.splice(
    todos.value.findIndex((todo) => todo.id === todoId),
    1
  );
};
const updateFilter = (state) => {
  filter.value = state;
};
const clearAllCompleted = () => {
  todos.value = todos.value.filter((todo) => !todo.finished);
};
</script>

<template>
  <div class="main-wrap">
    <header class="main-header">
      <h1>JTodo</h1>
    </header>
    <section class="real-app">
      <input type="text" class="add-input" placeholder="接下来要做什么？" v-model="newTodo" @keyup.enter="addTodo" />
      <el-scrollbar ref="scrollbarRef" height="60vh">
        <TodoItem v-for="todo in filterTodos" @destoryTodo="removeTodo" :todo="todo" :key="todo.id"></TodoItem>
      </el-scrollbar>
      <TodoTab
        :filter="filter"
        :todos="todos"
        @changeFilter="updateFilter"
        @toClearAllCompleted="clearAllCompleted"
      ></TodoTab>
    </section>
  </div>
</template>

<style lang="less" scoped>
.main-wrap {
  width: 100%;
  height: 100vh;
  background: url('https://photo.qihaikj.com/bg-image.jpg');
  background-size: cover;
  background-position: center;
  font: 14px 'microsoft yahei';
  color: #333;
  font-weight: 500;
  .main-header {
    text-align: center;
  }
  .main-header h1 {
    font-size: 50px;
    color: rgba(175, 47, 47, 0.4);
    margin: 20px;
  }
  .real-app {
    width: 600px;
    margin: 0 auto;
    box-shadow: 8px 8px 5px #666;
  }
  .add-input {
    position: relative;
    width: 100%;
    font-size: 24px;
    line-height: 1.4em;
    box-sizing: border-box;
    padding: 16px 16px 16px 36px;
    border: none;
    outline: none;
  }
}
</style>