<template>
    <div class="success-box">
        <h1>Correct Answer!</h1>
        <p>{{ message }}</p>
        <p>Do you wish to continue with the quiz?</p>
        <div class="selection">
            <button @click="$emit('successEvent', 'Next Question')">Yes</button>
            <button @click="$emit('successEvent', 'End Quiz')">No</button>
        </div>
    </div>
</template>



<script>
    export default {
        name: "SuccessBox",


        props: {
            message: String
        },

    }

</script>



<style>
    .success-box {
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

    .success-box p {
        text-align: center;
    }

    .success-box .selection {
        display: flex;
        justify-content: space-evenly;
        align-items: center;
        width: 100%;
    }

    .success-box .selection button {
        width: 100px;
        padding: 10px 20px;
        background-color: palevioletred;
        color: white;
        border: none;
        border-radius: 10px;
        cursor: pointer;
    }

    .success-box .selection button:hover {
        background-color: white;
        color: black;
        box-shadow: 2px 2px  2px grey;
        transition: all 0.2s ease-in;
    }
</style>