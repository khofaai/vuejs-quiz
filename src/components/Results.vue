<template>
  <div class="result">
    <div class="title">{{ result.title }}</div>
    <div class="desc">
      {{ result.desc }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    selectedAnswers: {
      default: () => ([]),
      type: Array,
    },

    totalQuestions: {
      default: 0,
      type: Number,
    },
  },

  data() {
    return {
      results: [
        {
          title: 'Try again!',
          desc: 'Do a little more studying and you may succeed!'
        },
        {
          title: "Wow, you're a genius!",
          desc: 'Studying has definitely paid off for you!'
        }
      ],
    }
  },

  computed: {
    result() {
      const correctAnswers = this.selectedAnswers.filter(({ is_correct }) => is_correct);
      return correctAnswers.length === this.totalQuestions ? this.results[1] : this.results[0];
    },
  }
}
</script>

<style scoped>
.result {
  width: 50%;
}
.title {
  width: 100%;
  padding: 20px;
  font-size: 32px;
  font-weight: bold;
  text-align: center;
  background-color: #12cbc4;
  color: #fff;
  box-sizing: border-box;
}
.desc {
  border: 1px solid #8e959f;
  padding: 20px;
  font-size: 18px;
  width: 100%;
  background-color: #fff;
  transition: 0.4s linear all;
  text-align: center;
}
</style>
