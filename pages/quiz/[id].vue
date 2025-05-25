<template>
    <takeQuiz v-if="quiz" :quiz="quiz" />
</template>

<script setup>
import {useRoute} from "vue-router";

const router = useRoute()
const id = router.params.id

const {data: quiz} = useFetch(`http://localhost:3001/quizzes/${id}`) 
</script>