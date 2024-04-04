
<template>
    <div :class="answerClasses" @click="markAnswered" ><span>{{ text }}</span></div>
</template>

<script>
export default {
    methods: {
        markAnswered() {
            if (!this.isSubmitted) {
                this.$emit('question-answered', { 'questionId': this.questionId, 'selectedAnswer': this.text, 'isCorrect': this.isCorrect });
            }
        }
    },
    computed: {
        answerClasses() {
            return {
                answer: true,
                'answer-not-selected': this.selectedAnswerInQuestion !== this.text && !this.isSubmitted,
                'answer-selected': this.selectedAnswerInQuestion === this.text && !this.isSubmitted,
                'incorrect-answer': this.selectedAnswerInQuestion === this.text && this.isSubmitted && !this.isCorrect,
                'correct-answer': this.isSubmitted && this.isCorrect,
            }
        }
    },
    props: {
        selectedAnswerInQuestion: {
            required: false,
        },
        isSubmitted: {
            required: true,
            type: Boolean
        },
        text: {
            required: true,
            type: String
        },
        questionId: {
            required: true,
            type: String
        },
        isCorrect: {
            required: true,
            type: Boolean
        }
    },
    emits: ['question-answered']
}
</script>

<style>
.answer {
  border: 1px solid #8e959f;
  padding: 20px;
  font-size: 18px;
  width: 100%;
  transition: 0.2s linear all;
}

.answer-not-selected {
    background-color: #fff;
}

.correct-answer {
    background-color: green;
}

.incorrect-answer {
    background-color: red;
}

.answer-selected:not(.correct-answer, .incorrect-answer) {
    background-color: #ddd;
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