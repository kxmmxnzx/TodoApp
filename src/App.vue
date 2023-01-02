<template>
  <div id="todolist" style="max-width: 700px">
    <div class="header">
      <h3 class="header_text">TODO LIST</h3>
    </div>
    <div class="input">
      <input
        placeholder="할 일 추가"
        class="input_todo"
        style="width: 100%; height: 100%"
        type="text"
        v-model="todoInput"
        @keyup.enter="addTodo"
      />
    </div>
    <div>
      <ul class="todolist">
        <li
          v-for="(todo, index) in todos"
          :key="todo"
          class="todo_li"
          @click="todoCheck(index)"
        >
          <div class="todoitem">
            <input
              class="checkbox"
              style="display: none"
              type="checkbox"
              :id="index"
              @change="todoCheck(index)"
              v-model="checks[index]"
            />
            <label :for="index" class="todocontent">{{
              checks[index] ? "♥" : "♡"
            }}</label>
            <span
              :style="checks[index] ? 'text-decoration: line-through' : ''"
              >{{ todo }}</span
            >
          </div>
          <span class="button" @click.stop="removeClick(index)">
            <button>X</button>
          </span>
        </li>
      </ul>
    </div>
  </div>
</template>




<script>
import { reactive, toRefs } from "@vue/reactivity";
import { onMounted } from "@vue/runtime-core";
export default {
  setup() {
    const state = reactive({
      todoInput: "",
      todos: [],
      checks: [],
      menu_on: false,
    });

    let addTodo = () => {
      if (state.todoInput != "") {
        state.todos.push(state.todoInput);
        state.checks.push(false);
        let todolist = JSON.stringify(state.todos);
        let checklist = JSON.stringify(state.checks);
        window.localStorage.setItem("todolist", todolist);
        window.localStorage.setItem("checklist", checklist);
        state.todoInput = "";
        console.log(state.todos);
        console.log(state.checks);
      }
    };

    let todoCheck = (index) => {
      if (state.checks[index] == true) {
        state.checks[index] = false;
        let checklist = JSON.stringify(state.checks);
        window.localStorage.setItem("checklist", checklist);
      } else {
        state.checks[index] = true;
        let checklist = JSON.stringify(state.checks);
        window.localStorage.setItem("checklist", checklist);
      }
    };

    let removeClick = (index) => {
      state.todos.splice(index, 1);
      state.checks.splice(index, 1);
      let todolist = JSON.stringify(state.todos);
      let checklist = JSON.stringify(state.checks);
      window.localStorage.setItem("todolist", todolist);
      window.localStorage.setItem("checklist", checklist);
    };

    onMounted(() => {
      let todolist = window.localStorage.getItem("todolist");
      let checklist = window.localStorage.getItem("checklist");
      if (todolist) {
        let list = JSON.parse(todolist);
        console.log(list);
        state.todos = list;
      }
      if (checklist) {
        let list = JSON.parse(checklist);
        state.checks = list;
      }
    });

    return {
      ...toRefs(state),
      addTodo,
      todoCheck,
      removeClick,
    };
  },
};
</script>

<style>
@import url(//spoqa.github.io/spoqa-han-sans/css/SpoqaHanSansNeo.css);

html,
body {
  margin: 0;
  padding: 0;
  background: #cae9f8;
  font-family: "Spoqa Han Sans Neo", "sans-serif";
}
.header {
  background: #fcfcd4;
  border-radius: 15px;
}

.header_text {
  padding: 7px 20px 7px;
  font-weight: 500;
  font-size: 30px;
}

.input_todo {
  padding: 15px 20px;
  font-size: 16px;
  /* border: none; */
}

.input_todo:focus {
  outline: none;
}

.todoitem {
  display: inline-block;
}

.todocontent {
  margin: 0px 15px 0px -3px;
  font-size: 16px;
}

.todo_li {
  padding: 15px;
  border-radius: 15px;
}

.todo_li:hover {
  background: #f3f4f6;
}

.button {
  padding: 5px 12px;
  float: right;
  margin-top: -5px;
  margin-right: 0px;
  border-radius: 10px;
}

.button:hover {
  background: #c7c8c9;
}

li {
  position: relative;
}

.ddddd:hover {
  background: black;
}

#todolist {
  margin-top: 80px;
  margin-right: auto;
  margin-left: auto;
  background: white;
  border-radius: 20px;
  padding: 5px;
}
</style>
