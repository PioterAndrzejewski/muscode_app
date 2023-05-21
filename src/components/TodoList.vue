<template>
  <section class="container">
    <div class="heading">
      <h2>Lista todo</h2>
      <p>Wykonane: <span>{{ finishedTotal }}</span></p>
    </div>

    <ul class="todo-list">
      <li v-for="todo in todoList" :key="todo.id" class="todo-item">
        <div class="circle" :class="{ 'circle--finished': todo.finished }" @click="setFinished(todo.id)"></div>
        <p @click="removeTodo(todo.id)">{{ todo.description }}</p>
      </li>
    </ul>
    <input type="text" placeholder="Dodaj nowy element checklisty" v-model="todoInput" v-on:keyup.enter="addTodo">
  </section>
</template>

<script>
export default {
  data() {
    return {
      todoList: [
        {
          id: 0,
          description: 'Lorem ipsum dolor ist amet',
          finished: false,
        },
        {
          id: 1,
          description: 'Sed do eiusmod tempor incud',
          finished: false,
        },
        {
          id: 2,
          description: 'Labore et dolore magna aluqia',
          finished: false,
        },
        {
          id: 3,
          description: 'Sed ut persipiciatis uinde omnis iste natus',
          finished: false,
        },
        {
          id: 4,
          description: 'Minima veniam, quis nostrum exercitationem',
          finished: false,
        },
      ],
      todoInput: "",
    }
  },
  methods: {
    setFinished(id) {
      const index = this.todoList.findIndex(todo => todo.id === id);
      this.todoList[index].finished = !this.todoList[index].finished;
    },
    removeTodo(id) {
      this.todoList = this.todoList.filter(todo => todo.id !== id)
    },
    addTodo() {
      if (this.todoInput !== "") {
        this.todoList.push({
          id: new Date().getTime(),
          description: this.todoInput,
          finished: false,
        });
        this.todoInput = "";
      }
    },
  },
  computed: {
    finishedTotal() {
      return this.todoList.reduce((acc, curr) => curr.finished ? acc + 1 : acc, 0)
    }
  }
}
</script>

<style scoped>
.heading {
  display: flex;
  justify-content: space-between;
}

.todo-list {
  padding: 0;
}

.todo-item {
  display: flex;
}

.circle {
  width: 15px;
  height: 15px;
  border-radius: 50%;
  border: 1px solid var(--color-border);
}

.circle--finished {
  background-color: var(--color-active)
}
</style>

