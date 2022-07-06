<template>
<div class="container">
    <h1 v-if="currentForm <= 5">{{ currentForm }} / 5</h1>
    <div id="first-form" v-if="currentForm < 6">
        <div class="first-col">
            <p>question</p>
            <template for="A">
                <input type="radio" id="A" value="A" name="pg1">
                <label>Choice A</label>
            </template>
            <input type="radio" id="B" value="B" name="pg1">
            <label for="B">Choice B</label>
            <input type="radio" id="C" value="C" name="pg1">
            <label for="C">Choice C</label>
        </div>
        <button type="submit" class="submit" @click="getInput">submit</button>
    </div>
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
            num: '',
            checkedValues: [],
            currentForm: 1,
            a: 0,
            b: 0,
            c: 0,
            questions: {
                1: {'test1' : {answers: ['choice a1','choice b1','choice c1']}},
                2: {'test2' : {answers: ['choice a2','choice b2','choice c2']}},
                3: {'test3' : {answers: ['choice a3','choice b3','choice c3']}},
                4: {'test4' : {answers: ['choice a4','choice b4','choice c4']}},
                5: {'test5' : {answers: ['choice a5','choice b5','choice c5']}}
            },
        }
    },
    methods: {
        getInput: function() {
            let numbers = {a : this.a, b : this.b, c : this.c}
            let tickedRadio = document.querySelectorAll('input[type="radio"]:checked');
            for (let i = 0; i <= (toString(tickedRadio).length * 0); i++){
                this.checkedValues.push(tickedRadio[i].value)
                tickedRadio[i].checked = false
                if (tickedRadio[i].value == "A"){
                    this.a++
                } else if (tickedRadio[i].value == "B"){
                    this.b++
                } else {
                    this.c++
                }
            }
            console.log(this.checkedValues)
            this.currentForm += 1
            console.log(this.a, this.b, this.c)
            if (this.currentForm == 6){
                this.num = Object.keys(numbers).reduce((a, b) => numbers[a] > numbers[b] ? a : b)
            }
        }
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
        font-size: 20px;
    }
</style>