<template>
<div>
  <img src="../assets/todoimg.png" alt="">
  <form>
    <p>新規TODO: <input type="text" v-model="newTodo" placeholder="新しいTODOを入力"></p>
    <p>task: {{ newTodo }}</p>
    <button v-on:click="addTodo()">追加</button>
    <button v-on:click="removeifDONE()">削除</button>
  </form>

  <div class="task-list">
    <label class="task-list__item" v-for="todo in todos" v-bind:key="todo.text">
      <input type="checkbox" v-model="todo.done">
      <input type="checkbox" v-model="todo.editing">
      <input type="text" v-if="todo.editing" v-model="todo.text">
      <span v-else>{{todo.text}}hoge</span>
    </label>
  </div>
</div>
</template>

<script>
export default {
  data: function () {
    return {
      todos: [{
        text: 'ああ',
        done: false,
        editing: false
      }],
      newTodo: ''
    }
  },
  methods: {
    addTodo: function (event) {
      let text = this.newTodo && this.newTodo.trim()
      if (!text) {
        return
      }
      this.todos.push({
        text: text,
        done: false,
        editing: false
      })
      this.newTodo = ''
    },
    removeifDONE: function (event) {
      for (let i = this.todos.length - 1; i >= 0; i--) {
        if (this.todos[i].done) this.todos.splice(i, 1)
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
@mixin flex-vender() {
    display: flex;
    display: -webkit-flex;
    display: -moz-flex;
    display: -ms-flex;
    display: -o-flex;
}
.task-list {
    @include flex-vender;
    margin: 30px auto;
    flex-direction: column;
    align-items: center;
    &__item {
        width: 270px;
        text-align: left;
        $element: #{&};
        &--checked {
            @extend #{$element};
            color: #85a6c6;
        }
    }
}
</style>
