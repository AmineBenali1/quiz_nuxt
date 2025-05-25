<template>
    <div class="quiz">
    <div style="font-weight: bolder; text-align: center;">{{ quiz.title }}</div><br>
    Difficulty : <b>{{quiz.difficulty}}</b><br><br>
    <NuxtLink :to="`/quiz/${quiz.id}`" style="text-decoration: none; color: black;"><b>Take quiz</b></NuxtLink><br>
    <NuxtLink :to="`/modify/${quiz.id}`" style="text-decoration: none; color: green;">Modify quiz</NuxtLink><br>
    <span style="color: red; cursor: pointer;" @click="$emit('delete',quiz.id)">Delete quiz</span>
    </div>
</template>

<script setup>
const {quiz} = defineProps(['quiz'])

// If i dont want to use emit just reload the page
const DeleteQuiz = async () =>{
    await $fetch(`http://localhost:3001/quizzes/${quiz.id}`,{
        method: 'DELETE'
    })
    window.location.reload()  // reload the page
}

</script>

<style scoped>
.quiz{
    border: black 1px solid;
    border-radius: 3px;
}
</style>