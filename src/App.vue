<template>
  <div id="app">
    <div class="qustion">Q. {{ exercises.question }}</div>
    <div>{{ answerCheck }}</div>
    <ul>
      <li :key="ind" v-for="(num, ind) in exercises.cases.length">
        {{ alphabet[num - 1] }}
        <input
          type="radio"
          :value="alphabet[num - 1]"
          v-if="exercises.answer.length == 1"
          v-model="answerCheck"
        />
        <input
          type="checkbox"
          :value="alphabet[num - 1]"
          v-model="answerCheck"
          v-else
        />

        {{ exercises.cases[num - 1] }}
      </li>
    </ul>
    <div v-if="fetch.solve">
      <div>Answer: {{ exercises.answer }}</div>
      <div>explanation: {{ exercises.explanation }}</div>
      <div>reference: {{ exercises.reference }}</div>
    </div>
    // {{ exercises.answer }} //
    <div>
      {{ total }}, {{ randomNum }}<br /><input
        type="button"
        name="confirm"
        value="확인"
        @click="confirm()"
      />
    </div>
  </div>
</template>

<script>
import Exercises from "./assets/exercise.json";

export default {
  name: "app",
  data() {
    return {
      fetch: {
        solve: false
      },
      answerCheck: [],
      exercises: null,
      total: Exercises.length,
      randomNum: 0,
      alphabet: ["A", "B", "C", "D", "E", "F", "G"]
    };
  },
  created() {
    this.createRandomNum();
    //this.exercises = Exercises.filter(v => v.number == this.randomNum);
    this.exercises = Exercises[this.randomNum];
    console.log(this.exercises);
  },
  methods: {
    createRandomNum() {
      this.randomNum = Math.floor(Math.random() * this.total) + 1;
    },
    confirm() {
      console.log(this.exercises.answer);
      console.log(this.answerCheck);
      let correctYn = true;

      if (this.answerCheck.length > 1) {
        this.answerCheck.forEach(answer => {
          if (this.exercises.answer.indexOf(answer) <= -1) {
            correctYn = false;
          }
        });
      } else {
        correctYn = this.exercises.answer == this.answerCheck ? true : false;
      }

      if (correctYn) {
        alert("맞다!");
      } else {
        alert("틀리다.");
      }
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1,
h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
