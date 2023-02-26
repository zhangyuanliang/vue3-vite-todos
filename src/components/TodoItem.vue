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
@coolGray: #e5e7eb;
.todo-item {
  position: relative;
  margin-top: 3px;
  font-size: 24px;
  border-bottom: 1px dashed @coolGray;
  border-top: 1px solid @coolGray;
  label {
    display: block;
    margin-left: 45px;
    padding: 15px 44px 15px 15px;
    line-height: 1.2;
    color: #34373b;
    -webkit-font-smoothing: antialiased;
    font-weight: 400;
    max-width: 554px;
    overflow: hidden;
    text-overflow: ellipsis;
  }
  &.finished label {
    color: @coolGray;
    text-decoration: line-through;
  }
  &:hover .destory:after {
    content: 'x';
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
    color: #FCA5A5;
    font-size: 25px;
    cursor: pointer;
  }
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
  &:after {
    content: url('@/assets/images/round.svg');
  }
  &:checked:after {
    content: url('@/assets/images/done.svg');
  }
}
</style>
