<template>
  <div class="ctr">
    <questions-vue :questions="questions"
      :questionsAnswered="questionsAnswered"
      @question-answered="questionAnswered"
      v-if="questionsAnswered < questions.length"
      >
    </questions-vue>
    <result-vue v-else
      :results="results"
      :totalCorrect="totalCorrect"></result-vue>
    <button type="button" 
      class="reset-btn"
      @click.prevent="reset"
      v-show="questionsAnswered === questions.length">Reset</button>
  </div>
</template>

<script>
import QuestionsVue from './components/QuestionsVue.vue';
import ResultVue from './components/ResultVue.vue';

export default {
  name: 'App',
  methods: {
    questionAnswered(isCorrect) {
      this.totalCorrect += isCorrect ? 1 : 0;
      this.questionsAnswered++;
    },
    reset() {
      this.totalCorrect = 0;
      this.questionsAnswered = 0;
    }
  },
  data() {
    return {
      questionsAnswered: 0,
      totalCorrect: 0,
      questions: [
        {
          q: 'What is 2 + 2?',
          answers: [
            {
              text: '4',
              is_correct: true
            },
            {
              text: '3',
              is_correct: false
            },
            {
              text: 'Fish',
              is_correct: false
            },
            {
              text: '5',
              is_correct: false
            }
          ]
        },
        {
          q: 'How many letters are in the word "Banana"?',
          answers: [
            {
              text: '5',
              is_correct: false
            },
            {
              text: '7',
              is_correct: false
            },
            {
              text: '6',
              is_correct: true
            },
            {
              text: '12',
              is_correct: false
            }
          ]
        },
        {
          q: 'Find the missing letter: C_ke',
          answers: [
            {
              text: 'e',
              is_correct: false
            },
            {
              text: 'a',
              is_correct: true
            },
            {
              text: 'i',
              is_correct: false
            }
          ]
        },
      ],
      results: [
        {
          min: 0,
          max: 2,
          title: "Try again!",
          desc: "Do a little more studying and you may succeed!"
        },
        {
          min: 3,
          max: 3,
          title: "Wow, you're a genius!",
          desc: "Studying has definitely paid off for you!"
        }
      ]
    }
  },
  components: {
    QuestionsVue,
    ResultVue
  },
}
</script>./components/ResultVue.vue./components/QuestionsVie.vue