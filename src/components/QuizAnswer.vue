
<template>
    <div :class="answerClasses" @click="markAnswered" ><span>{{ text }}</span></div>
</template>

<script>
export default {
    methods: {
        markAnswered() {
            this.$emit('question-answered', { 'questionId': this.questionId, 'selectedAnswer': this.text, 'isCorrect': this.isCorrect });
        }
    },
    computed: {
        answerClasses() {
            return {
                answer: true,
                'answer-not-selected': this.selectedAnswerInQuestion !== this.text,
                'answer-selected': this.selectedAnswerInQuestion === this.text
            }
        }
    },
    props: {
        selectedAnswerInQuestion: {
            required: false,
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

.answer-correct {
    background-color: green;
}

.answer-incorrect {
    background-color: red;
}

.answer-selected:not(.answer-correct, .answer-incorrect) {
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