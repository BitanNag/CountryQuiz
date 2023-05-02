<template>
    <div class="question-box">
        <h1>Question Time!</h1>
        <p>What is the capital of {{ countryName }}?</p>
        <small v-if="emptyAnswer"><i>{{ errorMessage }}</i></small>
        <input type="text" v-model="answer">
        <button @click="checkAnswer">Submit</button>
    </div>
</template>



<script>
    export default {
        name: "QuestionBox",


        props: {
            countryName: String
        },


        data() {
            return {
                emptyAnswer: false,
                errorMessage: "",
                answer: ""
            }
        },


        methods: {
            checkAnswer() {
                if(this.answer.length == 0) {
                    this.emptyAnswer = true;
                    this.errorMessage = "Answer cannot be empty! Please enter a name."
                } else {
                    this.emptyAnswer = false;
                    this.$emit('submitEvent', this.answer);
                }
            }
        }
    }
</script>


<style>
    .question-box {
        height: 350px;
        width: 600px;
        border: 2px solid goldenrod;
        border-radius: 20px;
        background-color: bisque;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: center;
        padding: 40px;
        animation: fadeIn 1s;
    }

    @keyframes fadeIn {
        0% { 
            opacity:  0; 
            translate: 0 -30px;
        }
        100% { 
            opacity: 1; 
            translate: 0 0
        }
    }

    .question-box p {
        text-align: center;
    }

    .question-box small {
        color: red;
        text-decoration: italic;
    }

    .question-box button {
        padding: 10px 20px;
        background-color: palevioletred;
        color: white;
        border: none;
        border-radius: 10px;
        cursor: pointer;
    }

    .question-box button:hover {
        background-color: white;
        color: black;
        box-shadow: 2px 2px  2px grey;
        transition: all 0.2s ease-in;
    }
</style>