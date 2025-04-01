<template>
  <!-- <div v-if="toggle">true</div>
  <div v-else>false</div>
  <button @click="onToggle">Toggle</button> -->
  <div class="container">
    <h2>To-Do List</h2>

    <form @submit.prevent="onSubmit">
      <div class="d-flex">
        <div class="flex-grow-1 mr-2">
          <input
            class="form-control"
            type="text"
            v-model="todo"
            placeholder="Type new to-do"
          />
        </div>
        <div>
          <button class="btn btn-primary" type="submit">add</button>
        </div>
      </div>
      <div v-show="hasError" style="color: red">This filed cannot be empty</div>
      <div>
        <button @click="fnError">에러문구 노출</button>
      </div>
    </form>

    <div v-if="!todos.length">추가된 TODO가 없습니다.</div>
    <div v-for="(todo, index) in todos" :key="todo.id" class="card mt-2">
      <div class="card-body p-2 d-flex align-items-center">
        <div class="form-check flex-grow-1">
          <input
            class="form-check-input"
            type="checkbox"
            v-model="todo.completed"
          />
          <label class="form-check-label" :class="{ todo: todo.completed }">{{
            todo.subject
          }}</label>
        </div>
        <div>
          <button class="btn btn-danger btn-sm" @click="deleteTodo(index)">
            Delete
          </button>
        </div>
      </div>
    </div>
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

// 객체 로 사용 후 변수 값 변경하기 위해 사용 (obejct,array만 가능)
// import { reactive } from "vue";

export default {
  setup() {
    // const toggle = ref(false);
    const todo = ref("");
    const todos = ref([]);
    const hasError = ref(false);
    const todostyle = {
      textDecoration: "line-through",
      color: "gray",
    };

    const onSubmit = () => {
      if (todo.value == "") {
        hasError.value = true;
      } else {
        todos.value.push({
          id: Date.now(),
          subject: todo.value,
          completed: false,
        });
        hasError.value = false;
        todo.value = "";
      }

      //todos.value.push({
      //id: Date.now(),
      //subject: todo.value,
      //});
    };

    const deleteTodo = (index) => {
      todos.value.splice(index, 1);
    };
    // const onToggle = () => {
    //   toggle.value = !toggle.value;
    // };

    return {
      todo,
      todos,
      onSubmit,
      hasError,
      todostyle,
      deleteTodo,
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
