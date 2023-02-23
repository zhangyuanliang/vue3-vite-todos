<script setup>
import { ref, computed } from 'vue';

const props = defineProps({
  filter: {
    type: String,
    require: true,
  },
  todos: {
    type: Array,
    require: true,
  },
});

const emit = defineEmits(['changeFilter', 'toClearAllCompleted']);

const states = ref(['all', 'active', 'completed']);

const todosLeft = computed(() => {
  return props.todos.filter((todo) => !todo.finished).length;
});

const changeStates = function (state) {
  emit('changeFilter', state);
};
const clearAllCompleted = function () {
  emit('toClearAllCompleted');
};
</script>

<template>
  <div class="helper">
    <span class="left">{{ todosLeft }} items left</span>
    <span class="tabs">
      <span
        v-for="state in states"
        :class="[state, filter == state ? 'actived' : '']"
        v-on:click="changeStates(state)"
        >{{ state }}</span
      >
    </span>
    <span class="clear" v-on:click="clearAllCompleted">clear completed</span>
  </div>
</template>

<style lang="less" scoped>
.helper {
  font-size: 16px;
  line-height: 1.5em;
  padding: 5px 8px;
  color: #fff;
  display: flex;
  justify-content: space-between;
  -webkit-font-smoothing: antialiased;
  font-weight: 200;
}
.tabs {
  display: flex;
  justify-content: space-around;
  width: 230px;
}
.tabs span {
  display: inline-block;
  padding: 0 10px;
  cursor: pointer;
}
.tabs span.actived {
  border: 1px solid #48e436;
  border-radius: 5px;
  color: #48e436;
}
.clear {
  cursor: pointer;
}
</style>
