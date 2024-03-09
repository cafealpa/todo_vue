<script setup>

import {computed, reactive} from "vue";

const props = defineProps({
  data: Object
});

const todoItems = computed(() => {
  if (props.data.tabType === 'active') {
    return props.data.todo.filter(todo => todo.isCompleted === false);
  } else if (props.data.tabType === 'completed') {
    return props.data.todo.filter(todo => todo.isCompleted === true);
  } else {
    return props.data.todo;
  }
});

const emits = defineEmits(['updateSelected']);
const selectedTodos = reactive({});

const toggleSelect = (item) => {
  if(selectedTodos[item.id]) {
    delete selectedTodos[item.id];
  } else {
    selectedTodos[item.id] = item;
  }

  emits('updateSelected', selectedTodos);
}





</script>

<template>
  <!-- Todo content list -->
  <div class="tab-content" id="ex1-content">
    <!--    <div v-for="(tab, index) in tabs" :key="index" class="tab-pane fade show" :class="tab.isActive ? 'active' : ''" id="ex1-tabs-1" role="tabpanel">-->
    <ul class="list-group mb-0">
      <li v-for="(item, index) in todoItems" :key="index"
          class="list-group-item d-flex align-items-center border-0 mb-2 rounded"
          :class="item.isCompleted ? 'item-comp-bg-color' : 'item-bg-color'">
        <input class="form-check-input me-2" type="checkbox" @change="toggleSelect(item)" aria-label="..."/>
        <s v-if="item.isCompleted === true">{{ item.title }}</s>
        <span v-else>{{ item.title }}</span>
      </li>
    </ul>
    <!--    </div>-->
  </div>
</template>

<style scoped>
.item-comp-bg-color {
  background-color: #bbbbbb;
}

.item-bg-color {
  background-color: #f4f6f7;
}

</style>