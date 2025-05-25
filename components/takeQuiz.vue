<template>
    <h3>Welcome to '{{ quiz.title }}' quiz</h3>
    <div class="question">
        Question {{ qstIndex + 1 }}: <br>
        {{ questions[qstIndex].question }}<br>
        <div v-for="(answer,idx) in questions[qstIndex].answers">
            <input type="radio" v-model="userAnswer" :name="'question'+qstIndex" :value="answer"> {{ answer }} <br>
        </div>
        <button @click="nextQuestion">{{ qstIndex + 1 < total ? '-> Next' : 'Finish' }}</button>
        <div v-if="finished">
            Your final score is : {{ correct }}/{{ total }}
        </div>

    </div>
</template>

<script setup>

const {quiz} = defineProps(['quiz'])
const questions = ref(quiz.questions)
const qstIndex = ref(0)
const userAnswer = ref("")
const total = ref(questions.value.length)
const correct = ref(0)
const finished = ref(false)

const nextQuestion = () => {
    if (finished.value) return;
    if (userAnswer.value === questions.value[qstIndex.value].correct_answer) {
        correct.value++;
    }
    if (qstIndex.value + 1 === total.value) {
        finished.value = true;
    } else {
        qstIndex.value++;
        userAnswer.value = ""; // reset answer for next question
    }
}

</script>

<style scoped>
body{
    text-align: left;
}
</style>