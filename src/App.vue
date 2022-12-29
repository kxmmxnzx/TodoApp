<template>
  <div class="header">
    <h1>TODO LIST</h1>
  </div>
  <div class="add_todo">
    <input
      class="input_todo"
      type="text"
      v-model="todoInput"
      @keyup.enter="addTodo"
    />
  </div>
  <ul class="list">
    <li class="todo" v-for="(todo, index) in todos" :key="index">
      <div>
        <input
          class="todo_checkbox"
          type="checkbox"
          :id="index"
          @change="todoCheck"
        />
        <label :for="index" class="checkIcon">{{ check }}</label>
        <span>{{ todo }} </span>
        <div
          class="more"
          @mouseover="menu_on = true"
          @mouseout="menu_on = false"
        >
          <span>...</span>
          <div v-show="menu_on" class="menu">
            <ul>
              <li><button>수정</button></li>
              <li><button>삭제</button></li>
            </ul>
          </div>
        </div>
      </div>
    </li>
  </ul>
</template>




<script>
import { reactive, toRefs } from "@vue/reactivity";
export default {
  setup() {
    const state = reactive({
      todoInput: "",
      todos: [],
      check: "☆",
      menu_on: false,
    });

    let addTodo = () => {
      if (state.todoInput != "") {
        state.todos.push(state.todoInput);
        state.todoInput = "";
        console.log(state.todos);
      }
    };

    let todoCheck = () => {
      if (state.check == "☆") {
        state.check = "★";
      } else {
        state.check = "☆";
      }
    };

    return {
      ...toRefs(state),
      todoCheck,
      addTodo,
    };
  },
};
</script>

<style>
/* html,
body {
  margin: 0;
  padding: 0;
}

ul {
  list-style: none;
}

.todo_checkbox {
  display: none;
}

.header {
  margin-left: auto;
  margin-right: auto;
  text-align: center;
  max-width: 600px;
  height: 50px;
  background: #ffcac8;
  border-radius: 10px;
}

.checkIcon {
  float: left;
  margin-right: 20px;
}

.more {
  float: right;
  margin-right: 60px;
}

.menu {
  position: absolute;
  right: 20px;
}

.add_todo {
  border: none;
  width: 600px;
  margin-left: auto;
  margin-right: auto;
  height: 50px;
  border-radius: 10px;
  background: #f8f988;
}

.input_todo {
  height: 50px;
} */
</style>
