<template>
  <div>
    <form v-on:submit.prevent="addNewTodo">
      <label for="new-todo">Eine Person hinzufügen</label>
      <input
        type="text"
        v-model="newTodoText"
        id="new-todo"
        placeholder="Max Mustermann"
      />
      <button>Hinzufügen</button>
    </form>
    <ul>
      <list
        v-for="(todo, index) in persons"
        :key="todo.id"
        :title="todo.title"
        @remove="todos.splice(index, 1)"
      ></list>
    </ul>
    <CalculateWinners
    @calculate="calculateWinners"/>
  </div>
</template>

<script>
import CalculateWinners from "./components/CalculateWinners.vue";
import List from "./components/List.vue";
import calculateWinners from "@/components/CalculateWinners.vue";
export default {
  name: "App",
  components: {
    List: List,
    CalculateWinners: CalculateWinners,
  },
  data() {
    return {
      newTodoText: "",
      persons: [
      ],
      nextTodoId: 1,
    };
  },
  methods: {
    calculateWinners() {
      alert('test')
    },
    addNewTodo() {
      this.persons.push({
        id: this.nextTodoId++,
        title: this.newTodoText,
      });
      this.newTodoText = "";
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: black;
  margin-top: 60px;

}
button {
  background-color: #42b983;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 4px;
  cursor: pointer;
}
input {
  padding: 10px;
  margin: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  width: 200px;
}
body {
  background-color:white;
}
ul {
  list-style-type: none;
  padding: 20px 0;
}
li {
  padding: 10px;
  border-bottom: 1px solid #ccc;
}
</style>
