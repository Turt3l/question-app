<template>
<div class="container" >
    <div class="starting-screen" v-if="currentForm == 0">
        <h1>Epic form</h1>
        <button id="startButton" class="startButton" @click="startForm">start here</button>
    </div>
    <h1 v-if="currentForm <= 5 && currentForm > 0">{{ currentForm }} / 5</h1>
    <form id="first-form" v-if="currentForm < 6 && currentForm > 0">
        <div class="first-col">
            <div v-for="question, id in questions" id="for-block" v-show="id == currentForm">
                <p id="question">{{question.name}}</p>
                <template id="possible-answers" v-for="answer, key in question.answers">
                    <input ref="radiod" type="radio" :value="key" v-model="pickedA">
                    <label id="answer">{{answer}}</label>
                    <a>{{pickedA}}</a>
                </template>
            </div>
        </div>
        <button type="button" class="submit" id="submit" @click="getInput">submit</button>
    </form>
    <div class="screen" v-if="currentForm > 5">
        <h1>Most pressed answer</h1>
        <p id="mostPressed">{{ num }}</p>
    </div>
</div>
</template>

<script>

export default {
    data() {
        return{
            checkedValues: [],
            currentForm: 0,
            checked: false,
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
            console.log(this.pickedA)
            //seto checked uz false, lai tas nepaliek true
            this.checked = false
            // ja nav neviens chekots, tad tas iziet no funkcijas
            if (this.pickedA == "") return false;
            // for loops prieks atbilzu skaitisanas
            this.checkedValues.push(this.$refs.radiod.pickedA)
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
            console.log(this.checkedValues)
            console.log(this.a, this.b, this.c)
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
    #mostPressed{
        text-transform: uppercase;
        font-size: 50px;
    }
    .container{
        width: 70vw;
        height: 600px;
        background-color: white;
        text-align: center;
        border-radius: 25px;
        padding-top: 100px;
    }
    body{
        font-family: "Haas Grot Text R Web", "Helvetica Neue", Helvetica, Arial, sans-serif;
        background-image: radial-gradient(at left top, rgb(143, 148, 251), rgb(239, 59, 54));
        height: 100vh;
        width: 100%;
        display: flex;
        align-items: center;
        overflow: hidden;
        font-weight: bold;
        color: black;
        justify-content: center;
    }
    h1{
        font-size: 50px;
    }
    button{
        position: relative;
        top: 20vh;
        width: 200px;
        height: 50px;
        color: white;
        border-radius: 70px;
        box-shadow: 0 3px 6px #00000029;
        text-transform: uppercase;
        font-size: 1.5rem;
        letter-spacing: 1px;
        transition: .4s ease;
        border: none;
        background: black;
    }
    label {
        font-size: 30px;
    }
    p {
        font-size: 40px;
    }
</style>