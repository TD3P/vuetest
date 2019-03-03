<template>
<div>
  <form>
    <button v-on:click="addTodo()">ADD TASK</button>
    <button>DELETE FINISHED TASKS</button>
    <p>input: <input type="text" v-model="newTodo" placeholder="edit me"></p>
    <p>task: {{ newTodo }}</p>
  </form>

  <div class="task-list">
    <label class="task-list__item" v-for="todo in todos" v-bind:key="todo.text">
      <input type="checkbox"><button>EDIT</button>{{todo.text}}
    </label>
  </div>
</div>
</template>

<script>
export default {
  data: function () {
    return {
      todos: [{
        text: 'あ',
        done: false
      },
      {
        text: 'い',
        done: false
      },
      {
        text: 'う',
        done: false
      },
      {
        text: 'aホゲホゲ',
        done: true
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
        done: false
      })
      this.newTodo = ''
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
