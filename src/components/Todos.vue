<template>
  <div>
      <h2>Todos:</h2>
      <div class="legend">
          <span>Double click to mark as complete</span>
          <span>
              <span class="incomplete-box"></span> = Incomplete
          </span>
          <span>
              <span class="complete-box"></span> = Complete
          </span>
      </div>

      <div class="todos">
          <div v-for="todo in allTodos" :key="todo.id" class="todo" @dblclick="todo.completed = !todo.completed" 
          :class="todo.completed ? 'complete-todo' : ''">
              {{ todo.title }}
              <i @click="deleteTodo(todo.id)" class="fas fa-trash-alt"></i>
          </div>
      </div>
  </div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex'

export default {
    name: "Todos",
    methods: {
        ...mapActions(["fetchTodos", "deleteTodo"])
    },
    computed: mapGetters(['allTodos']),
    created(){
        this.fetchTodos()
    }
}
</script>

<style scoped>
.todos{
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 1rem;
}

.todo{
    border: 1px solid #ccc;
    background: #41b883;
    padding: 1rem;
    border-radius: 5px;
    cursor: pointer;
    text-align:center;
    position: relative;
}

i{
    position: absolute;
    right: 5px;
    bottom: 5px;
    color: #fff;
    cursor: pointer;
}

.legend{
    display: flex;
    justify-content: space-between;
    margin-bottom: 1rem;
}

.incomplete-box, .complete-box{
    display: inline-block;
    width: 10px;
    height: 10px;
}

.incomplete-box{
    background-color: #41b883;
}

.complete-box{
    background-color: #35495e;
}

.complete-todo{
    background-color: #35495e;
}


@media (max-width: 564px){
    .todos{
        grid-template-columns: 1fr;
    }

    .legend{
        flex-direction: column;
    }
}
</style>