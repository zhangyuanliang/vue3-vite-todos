<script setup>
const props = defineProps({
  todo: Object,
  default: () => {},
});

const emit = defineEmits(['destoryTodo']);

const toggleFinish = (todo) => {
  props.todo.finished = !props.todo.finish;
};
const toDestory = () => {
  emit('destoryTodo', props.todo.id);
};

</script>

<template>
  <div :class="['todo-item', { finished: todo.finished }]">
    <input type="checkbox" class="toggle" v-model="todo.finished" @click="toggleFinish" />
    <label for="">{{ todo.title }}</label>
    <button class="destory" @click="toDestory"></button>
  </div>
</template>

<style lang="less" scoped>
.todo-item {
  position: relative;
  margin-top: 3px;
  font-size: 24px;
  border-bottom: 1px dashed #a2a1a2;
  border-top: 1px solid #cccacd;
}
.todo-item label {
  display: block;
  margin-left: 45px;
  padding: 15px 60px 15px 15px;
  line-height: 1.2;
  color: #34373b;
  -webkit-font-smoothing: antialiased;
  font-weight: 400;
}
.todo-item:hover .destory:after {
  content: 'x';
}
.todo-item.finished label {
  color: #b5b1b1;
  text-decoration: line-through;
}
.toggle {
  position: absolute;
  top: 0;
  bottom: 0;
  margin: auto 0;
  width: 40px;
  height: 40px;
  line-height: 40px;
  appearance: none;
  outline: none;
  cursor: pointer;
}
.toggle:after {
  content: url('https://photo.qihaikj.com/round.svg');
}
.toggle:checked:after {
  content: url('https://photo.qihaikj.com/done.svg');
}

.destory {
  position: absolute;
  top: 0;
  right: 10px;
  bottom: 0;
  margin: auto 0;
  width: 40px;
  height: 40px;
  background-color: transparent;
  border: none;
  outline: none;
  color: #da7274;
  font-size: 25px;
  cursor: pointer;
}
</style>
