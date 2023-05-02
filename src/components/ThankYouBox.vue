<template>
    <div class="thank-you-box">
        <h1>Thank You!</h1>
        <p>Thank you for playing the quiz. Hope to see you again!</p>
        <button @click="$emit('replayEvent', 0)">Replay Quiz</button>
    </div>
</template>


<script>
    export default {
        name: "ThankYouBox",
    }
</script>



<style>

    .thank-you-box {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
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

   .thank-you-box p {
        text-align: center;
    }

    .thank-you-box button {
        padding: 10px 20px;
        background-color: palevioletred;
        color: white;
        border: none;
        border-radius: 10px;
        cursor: pointer;
    }

    .thank-you-box button:hover {
        background-color: white;
        color: black;
        box-shadow: 2px 2px  2px grey;
        transition: all 0.2s ease-in;
    }
</style>