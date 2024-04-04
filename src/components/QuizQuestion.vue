<template>
    <slot name="question"></slot>
    <slot name="answers"></slot>
</template>

<script>
export default {
}
</script>

<style>
.ctr {
  margin: 0 auto;
  max-width: 600px;
  width: 100%;
  box-sizing: border-box;
  position: relative;
}

.questions-ctr {
  position: relative;
  width: 100%;
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
</style>