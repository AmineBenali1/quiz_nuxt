<template>
    <h1>Available quizzes</h1>
    <NuxtLink to="/add" style="text-decoration: none; font-weight: bolder; color: black; border: solid 2px black; padding: 10px;">Add quiz</NuxtLink><br><br>
    <div class="filter">
        Filter by Title : <input type="text" v-model="titleFilter"><br>
        Filter by Difficulty : <select v-model="diffFilter">
            <option> all </option>
            <option> easy </option>
            <option> mid </option>
            <option> hard </option>
        </select>
    </div>
    <div class="quizzes">
        <quizCard v-for="quiz in filteredQuizzes" :quiz="quiz" @delete = "removeQuiz"></quizCard>
    </div>
</template>

<script setup>
import {computed} from 'vue'

const {data : quizzes, refresh} = await useFetch('http://localhost:3001/quizzes')
const titleFilter = ref('')
const diffFilter=ref('all')
const removeQuiz = async (id) =>{
    await $fetch(`http://localhost:3001/quizzes/${id}`,{
        method: 'DELETE'
    })
    quizzes.value = quizzes.value.filter(q => q.id !== id)  // delete 
}

const filteredQuizzes = computed(() =>{
    const arr = []
    for(let i=0; i< quizzes.value.length ; i++){
        const q = quizzes.value[i]
        if(q.title.toLowerCase().includes(titleFilter.value.toLowerCase()) &&
        ( diffFilter.value == 'all' || q.difficulty == diffFilter.value ) ){
            arr.push(q)
        }
    }
    return arr;
})

</script>

<style scoped>
.quizzes{
    display: grid;
    grid-template-columns: repeat(4,24%);
    justify-content: space-between;
    row-gap: 10px;
}

</style>