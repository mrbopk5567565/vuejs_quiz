<template>
  <div class="question-box-container">
    <b-jumbotron>
      <template v-slot:lead>{{ currentQuestion.question }}</template>

      <hr class="my-4" />

      <!-- <p v-for="(answer, idx) in answers" :key="idx">
        {{ answer }}
      </p>-->

      <b-list-group>
        <b-list-group-item 
          v-for="(answer, idx) in answers" 
          :key="idx"
          @click="selectAnswer(idx, answer)"
          :class="[ selectedIndex === idx ? 'selected' : '']"
        >
          {{ answer }}
        </b-list-group-item>
      </b-list-group>

      <b-button
        variant="primary" 
        href="#"
        @click="submitAnswer"
      >
        Submit
      </b-button>
      <b-button @click="next" variant="success" href="#">Next</b-button>
    </b-jumbotron>
  </div>
</template>

<script>
import _ from 'lodash';
export default {
  data() {
    return {
      selectedIndex: null,
      shuffleAnswers: []
    }
  },
  props: {
    currentQuestion: Object,
    next: Function,
    increment: Function,
  },
  computed: {
    answers() {
      let answers = [...this.currentQuestion.incorrect_answers];
      answers.push(this.currentQuestion.correct_answer);
      return answers;
    }
  },
  watch: {
    currentQuestion: {
      immediate: true,
      handler() {
        this.selectedIndex = null;
        this.shuffleAnswersFunc();
      }
    }
  },
  methods: {
    selectAnswer(idx) {
      this.selectedIndex = idx;
    },
    shuffleAnswersFunc() {
      let answers = [ ...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer ]
      this.shuffleAnswers = _.shuffle(answers)
    },
    submitAnswer() {
      let isCorrect = false;
      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true
      }
      this.increment(isCorrect)
    }
  },
  // mounted() {
  //   this.shuffleAnswersFunc();
  // }
};
</script>

<style>
.list-group-item {
  cursor: pointer;
}
.list-group-item:hover {
  background: gray;
}
.btn {
  margin: 0 5px;
}
.list-group .selected {
  background-color: skyblue;
}
.list-group .correct {
  background: greenyellow;
}
.list-group .incorrect {
  background: red;
}
.list-group {
  margin-bottom: 15px;
}
</style>