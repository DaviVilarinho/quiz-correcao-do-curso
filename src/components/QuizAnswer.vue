
<template>
    <div :class="['answer']" @click="markAnswered" >{{ text }}</div>
</template>

<script>
export default {
    methods: {
        markAnswered() {
            this.isSelected = true;
            this.$emit('question-answered', { 'questionId': this.questionId, 'isCorrect': this.isCorrect });
        }
    },
    data () {
        return {
            isSelected: false 
        };
    },
    props: {
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
  background-color: #fff;
  transition: 0.2s linear all;
}

.answer-selected {
    background-color: #8e959f;
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