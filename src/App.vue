<template>
  <!-- <div v-if="toggle">true</div>
  <div v-else>false</div>
  <button @click="onToggle">Toggle</button> -->
  <div class="container">
    <h2>To-Do List</h2>
    <!-- 자식의 add-todo 함수값을 사용 -->
    <TodoSimpleForm @add-todo="addTodo" />

    <div v-if="!todos.length">추가된 TODO가 없습니다.</div>
    <!-- props를 사용하여 자식 컴포넌트에서 접근 가능하도록 -->
    <TodoList
      @delete-todo="deleteTodo"
      @toggle-todo="toggleTodo"
      :todos="todos"
    />
  </div>
</template>

<script>
// v-model input에 입력된 값으로 value 해줌
// v-bind: = :
// v-on: =@
// v-show = boolean 값에 따라 보여주는 여부 판단
// 스크립트로 변수 변경하기 위해 필요(string,obejct,array)
// obj, array 사용시 name.value.id 이렇게 value 붙여야함
import { ref } from "vue";
import TodoSimpleForm from "./components/TodoSimpleForm.vue";
import TodoList from "./components/TodoList.vue";

// 객체 로 사용 후 변수 값 변경하기 위해 사용 (obejct,array만 가능)
// import { reactive } from "vue";

export default {
  components: {
    TodoSimpleForm,
    TodoList,
  },

  setup() {
    // const toggle = ref(false);
    const todos = ref([]);

    const todostyle = {
      textDecoration: "line-through",
      color: "gray",
    };

    const addTodo = (todo) => {
      todos.value.push(todo);
    };

    const toggleTodo = (index) => {
      todos.value[index].completed = !todos.value[index].completed;
    };

    const deleteTodo = (index) => {
      todos.value.splice(index, 1);
    };

    return {
      todos,
      addTodo,
      todostyle,
      deleteTodo,
      toggleTodo,
    };
  },
};
</script>

<style>
.todo {
  color: gray;
  text-decoration: line-through;
}
</style>
