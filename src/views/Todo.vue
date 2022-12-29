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
              <li>수정</li>
              <li>삭제</li>
            </ul>
          </div>
        </div>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  setup() {},
};
</script>
