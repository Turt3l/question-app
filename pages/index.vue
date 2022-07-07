<template>
<div class="container" >
    <h1 v-if="currentForm <= 5">{{ currentForm }} / 5</h1>
    <form id="first-form" v-if="currentForm < 6">
        <div class="first-col">
            <div v-for="question, id in questions" id="for-block" v-show="id == currentForm">
                <p id="question">{{question.name}}</p>
                <template id="possible-answers" v-for="answer, key in question.answers">
                    <input id="checkbox" type="radio" :id="key" :value="key" name="pg1">
                    <label id="answer">{{answer}}</label>
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
            currentForm: 1,
            checked: false,
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
            let tickedRadio = document.querySelectorAll('input[type="radio"]:checked');
            console.log(tickedRadio)
            //seto checked uz false, lai tas nepaliek true
            this.checked = false
            // ja nav neviens chekots, tad tas iziet no funkcijas
            if (tickedRadio.length <= 0) return false;
            // for loops prieks atbilzu skaitisanas
            for (let i = 0; i <= (toString(tickedRadio).length * 0); i++){
                this.checkedValues.push(tickedRadio[i].value)
                tickedRadio[i].checked = false
                if (tickedRadio[i].value == "A"){
                    this.a++
                    this.checked = true
                } else if (tickedRadio[i].value == "B"){
                    this.b++
                    this.checked = true
                } else if (tickedRadio[i].value == "C"){
                    this.c++
                    this.checked = true
                }
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