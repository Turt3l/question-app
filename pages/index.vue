<template>
<div class="test-container container-fluid d-flex justify-content-center text-center">
    <div class="starting-screen" v-if="currentForm == 0">
        <h1>Epic form</h1>
        <button id="startButton" class="startButton btn btn-outline-danger" @click="startForm">Start here</button>
    </div>
    <h1 v-if="currentForm <= 5 && currentForm > 0">{{ currentForm }} / 5</h1>
    <form id="first-form" v-if="currentForm < 6 && currentForm > 0">
        <div class="first-col">
            <div v-for="question, id in questions" id="for-block" v-show="id == currentForm">
                <p id="question"><b>{{question.name}}</b></p>
                <template id="possible-answers" v-for="answer, key in question.answers">
                    <input ref="radiod" type="radio" :value="key" v-model="pickedA" style="color: red;">
                    <label id="answer">{{answer}}</label>
                </template>
            </div>
        </div>
        <button type="button" class="submit btn btn-outline-danger" id="submit" @click="getInput">Submit</button>
    </form>
    <div class="screen" v-if="currentForm > 5">
        <h1>Most pressed answer</h1>
        <p id="mostPressed" style="font-size: 20px;"><b>{{ num.toUpperCase() }}</b></p>
    </div>
</div>
</template>

<script>

export default {
    data() {
        return{
            currentForm: 0,
            pickedA: '',
            a: 0,
            b: 0,
            c: 0,
            questions: {
                '1': {
                    name: 'test1',
                    answers: {
                        'A':'choice a1',
                        'B': 'choice b1',
                        'C': 'choice c1'
                    }
                },
                '2': {
                    'name': 'test2',
                    answers: {
                        'A':'choice a2',
                        'B': 'choice b2',
                        'C': 'choice c2'
                    }
                },
                '3': {
                    'name': 'test3',
                    answers: {
                        'A':'choice a3',
                        'B': 'choice b3',
                        'C': 'choice c3'
                    }
                },
                '4': {
                    'name': 'test4',
                    answers: {
                        'A':'choice a4',
                        'B': 'choice b4',
                        'C': 'choice c4'
                    }
                },
                '5': {
                    'name': 'test5',
                    answers: {
                        'A':'choice a5',
                        'B': 'choice b5',
                        'C': 'choice c5'
                    }
                }
            },
        }
    },
    methods: {
        //  metode
        getInput: function() {
            //deklarē mainīgos(numbers priekš daudzuma cik tickoti)
            let numbers = {a : this.a, b : this.b, c : this.c}
            //klausās inputus kuri ir atzīmēti
            //seto checked uz false, lai tas nepaliek true
            // ja nav neviens chekots, tad tas iziet no funkcijas
            if (this.pickedA == "") return false;
            // for loops prieks atbilzu skaitisanas
            this.pickedA == ""
            if (this.pickedA == "A"){
                this.a++
                this.checked = true
            } else if (this.pickedA == "B"){
                this.b++
                this.checked = true
            } else if (this.pickedA == "C"){
                this.c++
                this.checked = true
            }
            // ja checked ir true, tad palaizts nakosais jautajums
            if (this.checked){
                this.currentForm += 1
            }
            // kalkule lielako skaitu atbilzu burtu
            if (this.currentForm == 6){
                this.num = Object.keys(numbers).reduce((a, b) => numbers[a] > numbers[b] ? a : b)
            }
            this.pickedA = "";
        },
        startForm: function(){
            this.currentForm++
        }
    },
    mounted(){
    }
}
</script>

<style>
    body {
        background-color: red;
    }
    .test-container{
        background-color: white;
        width: 30%;
        border-radius: 25px;
        margin-top: 20%;
    }
    .test-container button{
        margin-bottom: 20px;
    }
</style>