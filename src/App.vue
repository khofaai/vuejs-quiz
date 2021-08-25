<template>
  <div class="ctr">
    <Questions
      v-if="questionsAnswered < questions.length"
      :questions="questions"
      :questions-answered="questionsAnswered"
      @question-answered="questionAnswered"
    />
    <Results
      v-else
      :total-questions="questions.length"
      :selected-answers="selectedAnswers"
    />
    <button
      v-if="questionsAnswered === questions.length"
      type="button"
      class="reset-btn"
      @click.prevent="reset"
    >
      Reset
    </button>
  </div>
</template>

<script>
import questions from '@/questions';
import Questions from '@/components/Questions'
import Results from '@/components/Results'

export default {
  name: 'App',

  components: {
    Questions,
    Results,
  },

  data() {
    return {
      selectedAnswers: [],
      questions,
    }
  },

  computed: {
    questionsAnswered() {
      return this.selectedAnswers.length;
    },
  },

  methods: {
    questionAnswered(answer) {
      this.selectedAnswers.push(answer)
    },

    reset() {
      this.selectedAnswers = []
    }
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}
body {
  font-size: 20px;
  font-family: sans-serif;
  padding-top: 20px;
  background: #e6ecf1;
}
.fade-enter-from {
  opacity: 0;
}
.fade-enter-active {
  transition: all 0.3s linear;
}
.fade-leave-active {
  transition: all 0.3s linear;
  opacity: 0;
  position: absolute;
}
.reset-btn:active, .reset-btn:focus, .reset-btn:hover{
  border: 0;
  outline: 0;
}
.reset-btn {
  background-color: #ff6372;
  border: 0;
  font-size: 22px;
  color: #fff;
  padding: 10px 25px;
  margin: 10px auto;
}
</style>
