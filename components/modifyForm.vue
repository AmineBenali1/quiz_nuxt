<template>
    <h1>Quiz Modification Form</h1>
    Title : <input type="text" v-model="quiz.title"><br>
    Difficulty : <select v-model="quiz.difficulty">
        <option>easy</option>
        <option>mid</option>
        <option>hard</option>
    </select><br>
    <fieldset>
        <legend>Questions</legend>
        <div v-for="q in quiz.questions">
            Question : <input type="text" v-model="q.question">
            <div v-for="(ans,idx) in q.answers">
                Answer {{ idx +1 }} : <input type="text" v-model="q.answers[idx]">
            </div>
            Correct Answer: <input type="text" v-model="q.correct_answer">
            <hr>
        </div>
    </fieldset>
    <button @click="ModifyQuiz">Sumbit</button>
</template>

<script setup>
import {useRouter} from 'vue-router'
const router = useRouter()
const {quiz} = defineProps(['quiz'])

const ModifyQuiz = async() =>{
    await $fetch(`http://localhost:3001/quizzes/${quiz.id}`,{
        method: 'PATCH',
        headers:{'Content-Type':'application/json'},
        body:JSON.stringify({
            title : quiz.title,
            difficulty : quiz.difficulty,
            questions : quiz.questions
        })
        
    })
    router.push('/')
}
</script>