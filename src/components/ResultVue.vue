<template>
    <div class="result">
        <div class="title">{{ results[resultIndex].title }}</div>
        <div class="desc">
            {{ results[resultIndex].desc }}
        </div>
    </div>
</template>

<script>
export default {
    name: 'ResultVue',
    props: ['results', 'totalCorrect'],
    computed: {
        resultIndex() {
            let index = 0;

            let pos = 0;
            for (let result of this.results) {
                console.log(result.min, "<=", this.totalCorrect, result.max, ">=", this.totalCorrect)
                if (result.min <= this.totalCorrect && result.max >= this.totalCorrect) {
                    index = pos;
                }
                pos++;
            }

            return index;
        }
    }
};
</script>