<template>
  <div id="app">
    <template v-for="(exercise, index) in exercises">
      <div>Q.{{ index + 1 }} {{ exercise.question }}</div>
      <ul>
        <li v-for="num in exercise.cases.length">
          <input
            :name="'exercise' + index"
            type="radio"
            :value="num"
            v-if="exercise.answer.length == 1"
          />
          <input
            :name="'exercise' + index"
            type="checkbox"
            :value="num"
            v-else
          />

          {{ exercise.cases[num - 1] }}
        </li>
      </ul>
      <div>Answer: {{ exercise.answer }}</div>
    </template>
    {{ total }}, {{ randomNum }}
  </div>
</template>

<script>
import Exercises from "./assets/exercise.json";

export default {
  name: "app",
  data() {
    return {
      exercises: null,
      total: Exercises.length,
      randomNum: 0
    };
  },
  created() {
    this.createRandomNum();
    this.exercises = Exercises.filter(v => v.number == this.randomNum);
  },
  methods: {
    createRandomNum() {
      this.randomNum = Math.floor(Math.random() * this.total) + 1;
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
