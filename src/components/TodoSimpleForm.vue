<template>
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
      <!-- <button @click="fnError">에러문구 노출</button> -->
    </div>
  </form>
</template>

<script>
import { ref } from "vue";

export default {
  emits: ["add-todo"],
  // 부모에서 사용하기 위해 파라미터 추가
  setup(props, { emit }) {
    const todo = ref("");
    const hasError = ref(false);

    const onSubmit = () => {
      if (todo.value === "") {
        hasError.value = true;
      } else {
        // 부모 컴포넌트에서 add-todo를 사용
        emit("add-todo", {
          id: Date.now(),
          subject: todo.value,
          completed: false,
        });

        hasError.value = false;
        todo.value = "";
      }
    };

    return {
      todo,
      hasError,
      onSubmit,
    };
  },
};
</script>

<style></style>
