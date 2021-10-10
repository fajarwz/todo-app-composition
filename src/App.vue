<template>
  <div class="container" style="margin-top: 20px">
    <div class="card">
      <div class="card-header">
        <h5 class="card-title">Simple Todo App</h5>
      </div>
      <div class="card-body">
        <div class="row mb-2">
          <div class="col-10">
            <input v-model="todo" @keyup.enter="add" type="text" name="" id="" class="form-control">
          </div>
          <div class="col-2">
            <button @click="add" class="btn btn-success">Add</button>
          </div>
        </div>
        <list :todos="list" @doneTodo="doneTodo" @deleteTodo="deleteTodo"/>
        <small>Total Todo: {{ totalTodo }}</small>
      </div>
    </div>
  </div>
</template>

<script>
  import { ref, reactive, onMounted, computed, toRefs } from 'vue'
  import List from './components/List.vue'

  export default {
    components: { List },
    setup() {
      const todo  = ref('')
      const todos = reactive({
        list: []
      })

      onMounted(() => {
        if(localStorage.getItem('todos') !== null)
          todos.list = JSON.parse(localStorage.getItem('todos'))
      }) 

      const totalTodo = computed(() => {
        if(todos != null)
          return todos.list.length;
      })

      const add = () => {
        todos.list.unshift({
          activity: todo.value,
          isDone: false
        });
        todo.value = '';
        saveToLocalStorage();
      }

      const deleteTodo = (todoIndex) => {
        todos.list = todos.list.filter((item, index) => {
          if (index != todoIndex) {
            return item
          }
        });
        saveToLocalStorage();
      }

      const doneTodo = (todoIndex) => {
        todos.list = todos.list.filter((item, index) => {
          if (index == todoIndex) {
            return item.isDone = true
          }

          return item
        });
        saveToLocalStorage();
      }

      const saveToLocalStorage = () => {
        localStorage.setItem('todos', JSON.stringify(todos.list))
      }

      return {
        todo,
        ...toRefs(todos),
        totalTodo,
        add,
        deleteTodo,
        doneTodo,
        saveToLocalStorage
      }
    }
  }
</script>

<style>

</style>