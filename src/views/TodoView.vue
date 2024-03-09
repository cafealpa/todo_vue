<script setup>
import {reactive, ref} from "vue";
import TodoList from "@/components/TodoList.vue";

const dataObj = reactive({
  todo: [
    {id: 'todo-1', title: '항목1', isCompleted: true, isDeleted: false, createdAt: '2024-01-01', completedAt: null, deletedAt: null},
    {id: 'todo-2', title: '항목2', isCompleted: true, isDeleted: false, createdAt: '2024-02-01', completedAt: null, deletedAt: null},
    {id: 'todo-3', title: '항목3', isCompleted: false, isDeleted: false, createdAt: '2024-03-01', completedAt: null, deletedAt: null},
    {id: 'todo-4', title: '항목4', isCompleted: false, isDeleted: false, createdAt: '2024-01-02', completedAt: null, deletedAt: null},
    {id: 'todo-5', title: '항목5', isCompleted: false, isDeleted: false, createdAt: '2024-01-03', completedAt: null, deletedAt: null},
    {id: 'todo-6', title: '항목6', isCompleted: false, isDeleted: false, createdAt: '2024-02-05', completedAt: null, deletedAt: null},
    {id: 'todo-7', title: '항목7', isCompleted: false, isDeleted: false, createdAt: '2024-03-07', completedAt: null, deletedAt: null},
    {id: 'todo-8', title: '항목8', isCompleted: false, isDeleted: false, createdAt: '2024-03-08', completedAt: null, deletedAt: null},
  ],
  tabType: 'all'
});

const selectedTodos = reactive({});

const updateSelected = (selected) => {
  console.log('selected', selected);
  Object.assign(selectedTodos, selected);
  console.log('selectedTodos', selectedTodos);
}

const selectTodoType = (type) => {
  dataObj.tabType = type;
}

const complete = () => {
  console.log('complete');
  for(let key in selectedTodos) {
    const index = dataObj.todo.findIndex(todo => todo.id === key);
    console.log('index', index);
    dataObj.todo[index].isCompleted = true;
  }
}

</script>

<template>

  <section class="vh-100 gradient-custom">
    <div class="container py-5 h-100">
      <div class="row d-flex justify-content-center align-items-center h-100">
        <div class="col col-xl-10">

          <div class="card">
            <div class="card-body p-5">
              <form class="d-flex justify-content-center align-items-center mb-4">
                <div class="form-outline flex-fill">
                  <input type="text" id="form2" class="form-control" placeholder="New task..."/>
                </div>
                <button type="submit" class="btn btn-info ms-2">Add</button>
              </form>

              <!-- Tabs navs -->
              <ul class="nav nav-tabs mb-4 pb-2" id="ex1" role="tablist">
                <li class="nav-item" role="presentation">
                  <a class="nav-link" :class="{ 'active': dataObj.tabType === 'all' }" id="ex1-tab-1" data-mdb-toggle="tab" role="tab" @click="selectTodoType('all')">All</a>
                </li>
                <li class="nav-item" role="presentation">
                  <a class="nav-link" :class="{ 'active': dataObj.tabType === 'active' }"  id="ex1-tab-2" data-mdb-toggle="tab" role="tab" @click="selectTodoType('active')">Active</a>
                </li>
                <li class="nav-item" role="presentation">
                  <a class="nav-link" :class="{ 'active': dataObj.tabType === 'completed' }" id="ex1-tab-3" data-mdb-toggle="tab" role="tab" @click="selectTodoType('completed')">Completed</a>
                </li>
              </ul>
              <!-- Tabs navs -->

              <!-- Tabs content -->
              <TodoList :data="dataObj" @updateSelected="updateSelected"/>
              <!-- Tabs content -->

              <form class="d-flex justify-content-center align-items-center mb-4">
                <button type="button" class="btn btn-success w-30 ms-2" @click="complete()">Completed</button>
                <button type="button" class="btn btn-danger w-30 ms-2">Delete</button>
              </form>

            </div>
          </div>

        </div>
      </div>
    </div>
  </section>

</template>

<style scoped>
.gradient-custom {
  background: radial-gradient(50% 123.47% at 50% 50%, #00ff94 0%, #720059 100%),
  linear-gradient(121.28deg, #669600 0%, #ff0000 100%),
  linear-gradient(360deg, #0029ff 0%, #8fff00 100%),
  radial-gradient(100% 164.72% at 100% 100%, #6100ff 0%, #00ff57 100%),
  radial-gradient(100% 148.07% at 0% 0%, #fff500 0%, #51d500 100%);
  background-blend-mode: screen, color-dodge, overlay, difference, normal;
}
.w-30 {
  width: 30%;
}
</style>