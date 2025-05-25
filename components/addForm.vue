<template>
    <h1>Add quiz Form</h1>
    Title : <input type="text" v-model="newTitle"><br>
    Difficulty : <select v-model="newDifficulty">
        <option>easy</option>
        <option>mid</option>
        <option>hard</option>
    </select><br>
    <fieldset>
        <legend>Questions</legend>
        Question : <input type="text" v-model="qst"><br>
        Answer1 : <input type="text" v-model="answers[0]"><br>
        Answer2 : <input type="text" v-model="answers[1]"><br>
        Answer3 : <input type="text" v-model="answers[2]"><br>
        Answer4 : <input type="text" v-model="answers[3]"><br>
        Correct Answer: <input type="text" v-model="correct"><br>
        <button @click="addQuestion">Add question</button>
    </fieldset>
    <button @click="AddQuiz">Sumbit</button>
</template>

<script setup>
import {useRouter} from 'vue-router'
const router = useRouter()

const {data : quizzes} = await useFetch('http://localhost:3001/quizzes')
console.log(quizzes)
const newID = String(Number(quizzes.value[quizzes.value.length - 1].id) + 1)
const newQuestions = ref([]) 
const newTitle = ref('')
const newDifficulty = ref('easy')
const qst = ref('')
const answers = ref(["","","",""])
const correct = ref('')
const addQuestion = () =>{
    newQuestions.value.push(
        {
            question : qst.value,
            answers : answers.value,
            correct_answer : correct.value
        }
    )
    console.log(newQuestions.value[0].question)
    qst.value = ""
    answers.value = ["","","",""]
    correct.value = ""
}

const AddQuiz = async () =>{
    await $fetch('http://localhost:3001/quizzes',{
        method : "POST",
        headers : {'Content-Type' : 'application/json'},
        body: JSON.stringify({
            id : newID,
            title : newTitle.value,
            difficulty : newDifficulty.value,
            questions : newQuestions.value
        })
    })
    router.push('/')
}
</script>