<template>
    <div class="welcome-box">
        <h1>Country Quiz!</h1>
        <p>Hi Player! Welcome to the Country Quiz, where we quiz you about the capital of every country in the world.</p>
        <p>Are you ready?</p>
        <button @click="$emit('welcomeEvent', 1)">Let's Begin!</button>
    </div>
</template>



<script>
    export default {
        name: "WelcomeBox",
    }
</script>



<style>

    .welcome-box {
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

   .welcome-box p {
        text-align: center;
    }

    .welcome-box button {
        padding: 10px 20px;
        background-color: palevioletred;
        color: white;
        border: none;
        border-radius: 10px;
        cursor: pointer;
    }

    .welcome-box button:hover {
        background-color: white;
        color: black;
        box-shadow: 2px 2px  2px grey;
        transition: all 0.2s ease-in;
    }
</style>