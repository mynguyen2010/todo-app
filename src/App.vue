// Component A
<template>
  <div class="container">
    <input
      type="text"
      class="todo-input"
      placeholder="enter text"
      v-model="newTodo"
      @keyup.enter="addTodo"
    />
    <div v-for="(todo, index) in todos" :key="todo.id" class="todo-item">
      <div class="todo-item-left">
        <input type="checkbox" class="check" v-model="todo.completed" />
        <div
          v-if="!todo.editing"
          @dblclick="editTodo(todo)"
          :class="{ completed: todo.completed }"
        >
          {{ todo.title }}
        </div>
        <input
          v-else
          class="todo-item-edit"
          type="text"
          v-model="todo.title"
          @blur="donedit(todo)"
          @keyup.enter="donedit(todo)"
          @keyup.esc="cancelEdit(todo)"
        />
      </div>
      <!-- hello dsd-->
      <div class="remove-item" @click="removeTodo(index)">&times;</div>
    </div>
    <div class="footer">
      <div>
        <label for=""
          ><input
            type="checkbox"
            :checked="!anyRemainming"
            @change="checkAllTodo"
          />Check All</label
        >
      </div>
      <div>{{ remainming }}item left</div>
    </div>
    <!-- <div class="btn-footer">
      <div class="btn">
        <button :class="{ active: filter == 'all' }" @click="filter = 'all'">
          All {{filter}}
        </button>
        <button
          :class="{ active: filter == 'active' }"
          @click="filter = 'active'"
        >
          Active {{filter}}
        </button>
        <button
          :class="{ active: filter == 'complete' }"
          @click="filter = 'complete'"
        >
          Completed {{filter}}
        </button>
      </div>
      <div>Clear Completed</div>
    </div> -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: "",
      idForTodo: 3,
      beforeEdit: "",
      todos: [
        {
          id: 1,
          title: "title1",
          completed: false,
          editing: false,
        },
        {
          id: 2,
          title: "title2",
          completed: false,
          editing: false,
        },
      ],
    };
  },
  directives: {
    focus: {
      // directive definition
      inserted: function (el) {
        el.focus();
      },
    },
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim().length == 0) {
        return;
      }
      this.todos.push({
        id: this.idForTodo,
        title: this.newTodo,
        completed: false,
      });
      (this.newTodo = ""), this.idForTodo++;
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    editTodo(todo) {
      this.beforeEdit = todo.title;
      todo.editing = true;
    },
    donedit(todo) {
      if (todo.title.trim() == "") {
        todo.title = this.beforeEdit;
      }
      todo.editing = false;
    },
    cancelEdit(todo) {
      todo.title = this.beforeEdit;
      todo.editing = false;
    },
    checkAllTodo(e) {
      this.todos.forEach((todo) => {
        todo.completed = e.target.checked;
      });
    },

  },
  computed: {
    remainming() {
      return this.todos.filter((todo) => !todo.completed).length;
    },
    anyRemainming() {
      return this.remainming;
    },
  //   todosFilter(){
  //     if(this.filter == 'all'){
  //       console.log("hh");
  //       return this.todos
  //     }
  //     else if(this.filter == 'active'){
  //       return this.todos.filter(todo =>{
  //       console.log("aa");

  //         !todo.completed
  //       })
  //     }
  //     else if(this.filter == 'complete'){
  //       return this.todos.filter(todo =>{
  //         todo.completed
  //       })
  //   }
  //   return this.todos
  // },
}
}
</script>

<style>
.container {
  max-width: 600px;
  margin: 0 auto;
}
.todo-item-left {
  display: flex;
}
.todo-item {
  display: flex;
  justify-content: space-between;
}
.check {
  margin-right: 7px;
}
.completed {
  text-decoration: line-through;
  color: #bbbb;
}
.footer {
  display: flex;
  justify-content: space-between;
}
.btn-footer {
  display: flex;
  justify-content: space-between;
}
</style>
