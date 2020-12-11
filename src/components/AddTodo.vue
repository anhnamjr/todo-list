<template>
  <div>
      <h3>Add todo</h3>
      <div class="addTodo" @submit="onSubmit">
          <form>
              <input type="text" v-model="title" placeholder="Add Todo...">
              <input type="submit" value="Submit">
          </form>
      </div>
  </div>
</template>

<script>
import { mapActions } from 'vuex'

export default {
    name: 'AddTodo',
    data(){
        return {
            title: '',
            id: 200
        }
    },
    methods: {
        ...mapActions(["addTodo"]),
        onSubmit(e){
            e.preventDefault();
            this.addTodo(this.title)
            this.title = ''
            this.id++;
        }
    }
}
</script>

<style scoped>
.addTodo form{
    display: flex;
}

input[type="text"]{
    flex: 10;
    border: 1px solid #ccc;
    outline: none;
    padding: 1rem;
}

input[type="submit"]{
    flex: 2;
    background: #41b883;
    border: 1px solid #41b883;
    cursor: pointer;
}
</style>