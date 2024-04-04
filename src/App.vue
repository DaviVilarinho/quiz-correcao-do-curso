<template>
  <div>
    <h1 class="title">QUIZ TIME!</h1>
  </div>
  <quiz-question v-for="question in questions" :key="question['q']">
    <template v-slot:question>
      <h2>{{ question['q'] }}</h2>
    </template>

    <template v-slot:answers>
      <quiz-answer v-for="answer in question['answers']" :key="answer['text']" 
        :text="answer['text']"
        :isCorrect="answer['is_correct']"
        :questionId="question['q']"
        :selectedAnswerInQuestion="correctAnswered[question['q']]?.selectedAnswer"
        @question-answered="markAnswered">
      </quiz-answer>
    </template>
  </quiz-question>
  <div>
    <button class="btn reset-btn" @click.prevent="reset">Reset</button>
    <button class="btn submit-btn" @click.prevent="submit">Submit</button>
  </div>
</template>

<script>
import QuizAnswer from './components/QuizAnswer.vue';
import QuizQuestion from './components/QuizQuestion.vue';

export default {
  name: 'App',
  data() {
    return {
      correctAnswered: {},
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
    QuizQuestion,
    QuizAnswer
  },
  methods: {
    markAnswered(answerObject) {
      this.correctAnswered[answerObject['questionId']] = answerObject;
    },
    reset() {
      this.correctAnswered = {}
    },
    submit() {

    }
  },
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

.result {
  width: 100%;
}

.btn {
  border: 1px;
  font-size: 22px;
  color: #fff;
  padding: 10px 25px;
  margin: 10px auto;
  display: block;
}

.reset-btn {
  background-color: #ff6372;
  border-color: #ef6272;
}

.submit-btn {
  background-color: #8ce200;
  border-color: #7ce000;
}


.reset-btn:active,
.reset-btn:focus,
.reset-btn:hover {
  border: 0;
  outline: 0;
}

</style>
