<template>
  <section class="container">
    <div class="heading">
      <h2>Lista todo</h2>
      <p>Wykonane: {{ finishedTotal }}</p>
    </div>

    <ul class="todo-list">
      <li v-for="todo in todoList" :key="todo.id" class="todo-item" @click="removeTodo(todo.id)">
        <div class="circle" :class="{ 'circle--finished': todo.finished }" @click.stop="setFinished(todo.id)"></div>
        <p @click="removeTodo(todo.id)">{{ todo.description }}</p>
      </li>
    </ul>
    <span><input class="todo-input" type="text" placeholder="+ Dodaj nowy element checklisty" v-model="todoInput"
        v-on:keyup.enter="addTodo"></span>
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
  margin-bottom: 28px;
  color: var(--color-heading)
}

.heading h2,
.heading p {
  font-weight: 600;
  font-size: 1.2em;
}

.todo-list {
  padding: 0;
}

.todo-item {
  display: flex;
  padding: 10px;
  border-bottom: 1px solid var(--color-border);
  cursor: pointer;
}

.todo-item:hover {
  border-bottom: 1px solid var(--color-active);
}

.circle {
  margin-right: 8px;
  width: 18px;
  height: 18px;
  border-radius: 50%;
  border: 1px solid var(--color-border);
}

.circle--finished {
  background-color: var(--color-active)
}

.todo-input {
  width: 100%;
  padding: 12px 15px;
  font-size: 1em;
  border: none;
  border-bottom: 1px solid var(--color-border);
}

.todo-input:focus,
.todo-input:hover {
  outline: none;
  border-bottom: 1px solid var(--color-active);
}

.todo-input:before {
  display: inline-block;
  color: red;
  content: 'Pseudo Element Text ';
}
</style>

