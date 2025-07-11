<template>
    <div>
        <h1>Gewinnerziehung</h1>
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
                v-for="(person, index) in persons"
                :key="person.id"
                :title="person.title"
                @remove="persons.splice(index, 1)"
            ></list>
        </ul>
        <CalculateWinners
            @calculate="calculateWinners"/>

        <div>
            die Gewinner heißen
            <div
                v-for="(winner) in winnerList">
                Gewinner: {{ winner.people.map(p => p.title).join(', ') }}
                Datum: {{ winner.timestamp }}
            </div>
        </div>
    </div>
</template>

<script>
import CalculateWinners from "./components/CalculateWinners.vue";
import List from "./components/List.vue";

export default {
    name: "App",
    components: {
        List: List,
        CalculateWinners: CalculateWinners,
    },
    data() {
        return {
            newTodoText: "",
            persons: [],
            nextTodoId: 1,
            winnerList: []
        };
    },
    methods: {
        getRandomNumber(max) {
            return Math.floor(Math.random() * max);
        },
        selectWinners(users, amountWinners) {
            if (amountWinners > users.length) {
                return null;
            }
            const _users = JSON.parse(JSON.stringify(users));
            const winners = [];

            for (let i = 0; i < amountWinners; i++) {
                let winnerIndex = this.getRandomNumber(_users.length - i);
                let [winner] = _users.splice(winnerIndex, 1);
                winners.push(winner);
            }
            return winners;
        },
        calculateWinners() {
            this.winnerList.push({people:this.selectWinners(this.persons, 2), timestamp:(new Date()).toLocaleString()});
            console.log(this.winnerList);
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
body {
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
    background-color: white;
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
