<template>
  <div id="app">
    <h1>ToDoList</h1>
    <input type="radio" id="all" v-model="options" value="すべて" name="options" />
    <label for="all">すべて</label>
    <input type="radio" id="do" v-model="options" value="作業中" name="options" />
    <label for="do">作業中</label>
    <input type="radio" id="done" v-model="options" value="完了" name="options" />
    <label for="done">完了</label>
    <table>
      <thead>
        <tr>
          <th class="id">ID</th>
          <th class="comment">コメント</th>
          <th class="state">状態</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(todo, index) in filterList" :key="todo.name">
          <td>{{index}}</td>
          <td>{{todo.name}}</td>
          <td class="state">
            <button class="stateButton" v-on:click="doChangeState(index)">{{todo.progressButton}}</button>
          </td>
          <td class="button">
            <button v-on:click="onDelete(index)">削除</button>
          </td>
        </tr>
      </tbody>
    </table>
    <h2>新規タスクの追加</h2>
    <input v-model="inputText" type="text" />
    <button @click="onAdd">追加</button>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      todos: [],
      options: "すべて",
      inputText: ""
    };
  },
  methods: {
    onAdd() {
      if (this.inputText) {
        this.todos.push({
          name: this.inputText,
          progressButton: "作業中"
        });
        this.inputText = "";
      }
    },
    onDelete(index) {
      this.todos.splice(index, 1);
    },
    doChangeState: function(i) {
      if (this.todos[i].progressButton === "作業中") {
        this.todos[i].progressButton = "完了";
      } else if (this.todos[i].progressButton === "完了") {
        this.todos[i].progressButton = "作業中";
      }
    }
  },
  computed: {
    filterList: function() {
      return this.todos.filter(item => {
        if (this.options === "すべて") {
          return item;
        } else {
          return this.options === item.progressButton;
        }
      });
    }
  }
};
</script>












