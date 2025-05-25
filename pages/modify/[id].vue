<template>
    <modifyForm v-if="quiz" :quiz="quiz" />
</template>

<script setup>
import {useRoute} from 'vue-router'
const route = useRoute()
const id = route.params.id

const {data: quiz} = await useFetch(`http://localhost:3001/quizzes/${id}`)

</script>