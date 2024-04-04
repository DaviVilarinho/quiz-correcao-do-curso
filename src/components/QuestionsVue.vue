<template>
  <div class="questions-ctr">
    <div class="progress">
      <div class="bar" :style="{ width: `${questionsAnswered / questions.length * 100}%` }">
      </div>
      <div class="status">{{ questionsAnswered }} out of {{ questions.length }} questions answered</div>
    </div>
    <TransitionGroup name="fade">
      <div class="single-question" v-for="(question, index) in questions" :key="question.q"
        v-show="index === questionsAnswered">
        <div class="question">{{ question.q }}</div>
        <div class="answers">
          <div class="answer" v-for="answer in question.answers" :key="answer.text"
            @click.prevent="selectAnswer(answer.is_correct)">{{ answer.text }}</div>
        </div>
      </div>
    </TransitionGroup>
  </div>
</template>

<script>
export default {
  name: 'QuestionsVue',
  emits: ['question-answered'],
  methods: {
    selectAnswer(isCorrect) {
      this.$emit('question-answered', isCorrect);
    }
  },
  props: ['questions', 'questionsAnswered']
};
</script>