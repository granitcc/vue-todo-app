<template>
  <main>
    <h1>Create Todo</h1>
    <TodoCreatorVue @create-todo="createTodo" />
    <ul class="todo-list" v-if="todoList.length">
      <TodoItem
        v-for="(todo, index) in todoList"
        :todo="todo"
        :index="index"
        :key="todo.id"
        @toggle-complete="toggelTodoComplete"
        @edit-todo="toggleEditTodo"
        @update-todo="updateTodo"
        @delete-todo="deleteTodo"
      />
    </ul>
    <p class="todos-msg" v-else>
      <Icon icon="noto-v1:sad-but-relieved-face" />
      <span>Yo have no todo's to complete! Add one!</span>
    </p>
    <p v-if="todoCompleted && todoList.length > 0" class="todos-msg">
      <span>
        <Icon icon="noto-v1:party-popper" />
        <span> You have completed all your todos!</span>
      </span>
    </p>
  </main>
</template>

<script setup>
import { ref, watch, computed } from "vue";
import { uid } from "uid";
import TodoCreatorVue from "../components/TodoCreator.vue";
import TodoItem from "../components/TodoItem.vue";
import { Icon } from "@iconify/vue";
const todoList = ref([]);

watch(
  todoList,
  () => {
    setTodoListLocalStroage();
  },
  {
    deep: true,
  }
);

const todoCompleted = computed(() => {
  return todoList.value.every((todo) => todo.isCompleted);
});

const setTodoListLocalStroage = () => {
  localStorage.setItem("todoList", JSON.stringify(todoList.value));
};

const fetchTodoList = () => {
  const savedTodoList = JSON.parse(localStorage.getItem("todoList"));
  if (savedTodoList) {
    todoList.value = savedTodoList;
  }
};

fetchTodoList();

const createTodo = (todo) => {
  todoList.value.push({
    id: uid(),
    todo,
    isCompleted: null,
    isEditing: null,
  });
};
const toggelTodoComplete = (index) => {
  todoList.value[index].isCompleted = !todoList.value[index].isCompleted;
};
const toggleEditTodo = (index) => {
  todoList.value[index].isEditing = !todoList.value[index].isEditing;
};
const updateTodo = (todoValue, index) => {
  todoList.value[index].todo = todoValue;
};
const deleteTodo = (id) => {
  todoList.value.forEach((todo, index) => {
    if (todo.id === id) {
      todoList.value.splice(index, 1);
    }
  });
};
</script>

<style scoped lang="scss">
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;
  h1 {
    margin-bottom: 16px;
    text-align: center;
  }
  .todo-list {
    display: flex;
    flex-direction: column;
    list-style: none;
    margin-top: 24px;
    gap: 20px;
  }
  .todos-msg {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 24px;
  }
}
</style>
