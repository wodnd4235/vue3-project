<template>
  <div class="container">
    <h2>To-Do List</h2>
    <form @submit.prevent="onSubmit" class="d-flex">
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
    </form>
    {{ todos }}
  </div>
</template>

<script>
// v-model input에 입력된 값으로 value 해줌
// v-bind: = :
// v-on: =@
// 스크립트로 변수 변경하기 위해 필요(string,obejct,array)
// obj, array 사용시 name.value.id 이렇게 value 붙여야함
import { ref } from "vue";

// 객체 로 사용 후 변수 값 변경하기 위해 사용 (obejct,array만 가능)
// import { reactive } from "vue";

export default {
  setup() {
    const todo = ref("choi");
    const todos = ref([]);

    const onSubmit = () => {
      todos.value.push({
        id: Date.now(),
        subject: todo.value,
      });
    };

    return {
      todo,
      todos,
      onSubmit,
    };
  },
};
</script>

<style>
.name {
  color: red;
}
</style>
