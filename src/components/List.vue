<script>
  export default {
    props: {
      todos: {
        type: Array,
        default: []
      }
    },
    setup(props, { emit }) {
      const deleteTodo = (index) => {
        emit('deleteTodo', index);
      }
      
      const doneTodo = (index) => {
        emit('doneTodo', index);
      }

      return {
        deleteTodo,
        doneTodo
      }
    }
  }

  // export default {
  //   props: {
  //     todos: {
  //       type: Array,
  //       default: []
  //     }
  //   },
  //   methods: {
  //     deleteTodo(index) {
  //       this.$emit('deleteTodo', index);
  //     },
  //     doneTodo(index) {
  //       this.$emit('doneTodo', index);
  //     }
  //   }
  // }
</script>

<template>
  <div class="row">
    <div class="col">
      <ul class="list-group">
        <li class="list-group-item" v-for="(todo, index) in todos" :key="todo">
          <div class="row">
            <div class="col">
              <span v-if="todo.isDone">
                <del>{{ todo.activity }}</del>
              </span>
              <span v-else>{{ todo.activity }}</span>
            </div>
            <div class="col-auto">
              <div class="row gx-2">
                <div class="col">
                  <button @click="doneTodo(index)" class="btn btn-info">done</button>
                </div>
                <div class="col">
                  <button @click="deleteTodo(index)" class="btn btn-danger">x</button>
                </div>
              </div>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>