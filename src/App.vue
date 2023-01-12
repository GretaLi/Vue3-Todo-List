<script setup>
import { ref, onMounted, watch } from "vue";

// ref() 響應式變量
// 使用 .value 讀寫
const todos = ref([]);
const name = ref("");

const input_content = ref("");

const addTodo = () => {
  if (input_content.value.trim() === "") {
    return;
  }

  todos.value.unshift({
    content: input_content.value,
    done: false,
    id: crypto.randomUUID(),
  });

  input_content.value = "";
};
const removeTodo = (todo) => {
  todos.value = todos.value.filter((t) => t !== todo);
};

// watch() 偵測某個值，當該值有變化時就會執行
watch(
  todos,
  (newVal) => {
    localStorage.setItem("todo", JSON.stringify(newVal));
  },
  { deep: true }
);

watch(name, (newVal) => {
  localStorage.setItem("name", newVal);
});

// onMounted() 在組件掛載完成後執行函數。
onMounted(() => {
  name.value = localStorage.getItem("name") || "";
  todos.value = JSON.parse(localStorage.getItem("todo")) || [];
});
</script>

<template>
  <main class="app">
    <header>
      <section class="greeting">
        <h1>TODO</h1>
        <h2 class="title">
          哈囉! <input type="text" placeholder="請輸入名字" v-model="name" />
        </h2>
      </section>

      <section class="create-todo">
        <form @submit.prevent="addTodo">
          <input
            type="text"
            v-model="input_content"
            placeholder="新增待辦事項"
          />
        </form>
      </section>
    </header>

    <section class="todo-list">
      <div class="list">
        <div
          v-for="todo in todos"
          :key="todo"
          :class="`todo-item ${todo.done && 'done'}`"
        >
          <label>
            <input type="checkbox" v-model="todo.done" />
            <span className="bubble"></span>
          </label>
          <div class="todo-content">
            <input type="text" v-model="todo.content" />
          </div>

          <div class="actions">
            <button class="delete" @click="removeTodo(todo)">
              <i class="fa-solid fa-xmark"></i>
            </button>
          </div>
        </div>
        <div className="empty" v-if="todos.length === 0">尚無待辦事項</div>
      </div>
      <div className="counter" v-if="todos.length">
        {{ todos.filter((t) => !t.done).length }} 件事項未完成
      </div>
    </section>
  </main>
</template>
