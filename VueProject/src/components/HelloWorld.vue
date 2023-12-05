<script lang="ts">
import { ref } from "vue";

interface Person {
  name: string;
  age: number;
}

const count = ref(0);
export default {
  data() {
    let persons: Person[] = [
      { name: "Alice", age: 25 },
      { name: "Bob", age: 30 },
      { name: "Charlie", age: 28 },
      { name: "Amiel", age: 37 },
      { name: "Roee", age: 9 },
      { name: "Xor", age: 228 },
    ];
    let goal1: string = "Lean Vue and practice";
    let viteLink = "https://vitejs.dev/guide/";
    let counter = 0;
    let inputMsg = "";
    let submitInput = "";
    let isGood = false;
    let goalInput = "";
    let goals = [];
    let name = "HelloWorld";
    return {
      goal1,
      viteLink,
      counter,
      inputMsg,
      submitInput,
      isGood,
      goalInput,
      goals,
      persons,
      name,
    };
  },
  watch: {
    counter(newValue, oldValue) {
      console.log(
        "Conter changed to " +
          this.counter +
          "(" +
          newValue +
          "," +
          oldValue +
          ")"
      );
    },
  },
  computed: {
    computedCharcter() {
      return this.inputMsg.length;
    },
  },
  methods: {
    GetNumber(): string {
      return "The number is " + this.goal1;
    },
    Add(number) {
      return (this.counter += number);
    },
    Reduce(number) {
      return (this.counter -= number);
    },
    SetInput(event) {
      this.inputMsg = event.target.value;
    },
    SetSubmitInput(event) {
      this.submitInput = event.target.value;
    },
    SendSubmitInput(event) {
      alert("SendSubmitInput" + this.submitInput);
    },
    validateSubmit() {
      alert("validateSubmit");
    },
    addNewGoal() {
      if (this.goalInput.length > 0) {
        this.goals.push(this.goalInput);
        this.goalInput = "";
      }
    },
    clearGoals() {
      this.goals = [];
    },
    removePerson(index) {
      this.persons.splice(index, 1);
    },
    removeGoal(index) {
      this.goals.splice(index, 1);
    },
  },
};
</script>

<template>
  <v-container>
    <v-layout justify-center>
      <div>
        <header>
          <h1>Vue Course Goals</h1>
        </header>
        <section id="user-goals">
          <h2>My course goals ({{ this.goals.length }})</h2>
          <v-text-field
            type="text"
            placeholder="Enter your first goal"
            v-model="goalInput"
          />
          <v-btn @click="addNewGoal">Add Goal</v-btn>
          <v-btn @click="clearGoals">Clear</v-btn>
          <p v-if="this.goals.length === 0">
            No goals have been added yet - please start adding some!
          </p>
          <v-list
            v-else
            @click="removeGoal(index)"
            v-for="(goal, index) in goals"
            :key="index"
          >
            {{ index }} - {{ goal }}
          </v-list>
          <ul>
            <li
              :style="{ color: person.age > 29 ? 'red' : 'green' }"
              v-for="(person, index) in persons"
              :key="index"
              @click="removePerson(index)"
            >
              {{ person.name }} {{ person.age }}
            </li>
          </ul>
        </section>
        <section id="user-goal">
          <h2
            :class="isGood ? 'active' : ''"
            :style="{ color: isGood ? 'red' : 'orange' }"
          >
            My Course Goals :
          </h2>
          <p>{{ goal1 }}</p>
          <p>Learn more about <a v-bind:href="viteLink">Vite</a></p>
          <!-- <button @click="notify">{{GetNumber()}}</button>  -->
          <h2 />
          <v-btn v-on:click="counter++">Add</v-btn>
          <v-btn v-on:click="counter--">Remove</v-btn>
          <v-btn v-on:click="Add(5)">Add Func</v-btn>
          <v-btn v-on:click="Reduce(5)">Remove Func</v-btn>
          <p>Result : {{ counter }}</p>
          <h2 />
          <!-- <input type="text" v-on:input="SetInput" /> -->
          <input type="text" v-model="inputMsg" />
          <p>The input is : {{ inputMsg }} {{ computedCharcter }}</p>
          <h2 />
          <form v-on:submit.prevent="">
            <input
              type="text"
              v-on:input="SetSubmitInput"
              v-on:keyup.enter="validateSubmit"
            />
            <v-btn v-on:click="SendSubmitInput">submit</v-btn>
          </form>
        </section>
      </div>
    </v-layout>
  </v-container>
</template>

<style scoped></style>
