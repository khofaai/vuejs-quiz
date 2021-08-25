<template>
  <div class="questions-ctr">
    <div class="progress">
      <div class="bar" :style="{ width: `${questionsAnswered / questions.length * 100}%`}" />
      <div class="status">{{ questionsAnswered }} out of {{ questions.length }} questions answered</div>
    </div>
    <div>
      <div
        v-for="(question, index) in questions"
        :key="question.q"
        class="single-question"
      >
        <div v-show="questionsAnswered === index">
          <div class="question">{{ question.q }}</div>
          <div
            v-for="answer in question.answers"
            :key="answer.text"
            class="answer"
            @click.prevent="selectAnswer(answer)"
          >
            {{ answer.text }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    questions: {
      default: () => ([]),
      type: Array,
    },

    questionsAnswered: {
      default: 0,
      type: Number,
    }
  },

  emits: ['question-answered'],

  methods: {
    selectAnswer(answer) {
      this.$emit('question-answered', answer)
    },
  }
}
</script>

<style scoped>
.questions-ctr {
  position: relative;
  width: 50%;
}
.progress {
  height: 50px;
  margin-top: 10px;
  background-color: #ddd;
  position: relative;
}
.bar {
  height: 50px;
  background-color: #ff6372;
  transition: all 0.3s linear;
}
.status {
  position: absolute;
  top: 15px;
  left: 0;
  text-align: center;
  color: #fff;
  width: 100%;
}
.ctr {
  margin: 0 auto;
  max-width: 600px;
  width: 100%;
  box-sizing: border-box;
  position: relative;
}
.question {
  width: 100%;
  padding: 20px;
  font-size: 32px;
  font-weight: bold;
  text-align: center;
  background-color: #00ca8c;
  color: #fff;
  box-sizing: border-box;
}
.single-question {
  position: relative;
  width: 100%;
}
.answer {
  border: 1px solid #8e959f;
  padding: 20px;
  font-size: 18px;
  width: 100%;
  background-color: #fff;
  transition: 0.2s linear all;
}
.answer span {
  display: inline-block;
  margin-left: 5px;
  font-size: 0.75em;
  font-style: italic;
}
.answer:not(.is-answered) {
  cursor: pointer;
}
.answer:not(.is-answered):hover {
  background-color: #8ce200;
  border-color: #8ce200;
  color: #fff;
}
</style>
