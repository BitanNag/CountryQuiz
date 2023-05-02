<template>
	<div class="country-quiz-app">
		<div class="box-container" :style="{ backgroundImage: image }">
			<welcome-box v-if="display[0]" @welcomeEvent="switchDisplay"></welcome-box>
			<question-box v-else-if="display[1]" :countryName="countryName" @submitEvent="checkAnswer"></question-box>
			<success-box v-else-if="display[2]" :message="message" @successEvent="checkChoice"></success-box>
			<failure-box v-else-if="display[3]" :message="message" @failureEvent="checkChoice"></failure-box>
			<thank-you-box v-else-if="display[4]" @replayEvent="switchDisplay"></thank-you-box>
		</div>
	</div>
</template>



<script>
	import { WelcomeBox, QuestionBox, SuccessBox, FailureBox, ThankYouBox } from "./components";
	import axios from "axios";

	export default {
		name: 'CountryQuiz',


		components: {
			WelcomeBox,
			QuestionBox,
			SuccessBox,
			FailureBox,
			ThankYouBox
		},


		data() {
			return {
				display: [true, false, false, false, false],
				backgroundImageList: [
					`url(${ require('./assets/background-img-1.jpg') })`,
					`url(${ require('./assets/background-img-2.jpg') })`,
					`url(${ require('./assets/background-img-3.jpg') })`,
					`url(${ require('./assets/background-img-4.jpg') })`,
					`url(${ require('./assets/background-img-5.jpg') })`
				],
				countriesList: [],
				countryName: "",
				countryCapital: "",
				message: "",
				image: ''
			}
		},


		created() {
			this.image = this.backgroundImageList[0]
			this.getCountryData()
		},


		methods: {
			switchDisplay(displayNumber) {
				if(displayNumber == 1) this.buildQuestion();
				this.display.fill(false);
				this.image = this.backgroundImageList[displayNumber];
				this.display[displayNumber] = true;
			},

			async getCountryData() {
				try {
					let result = await axios.get('https://countriesnow.space/api/v0.1/countries/capital');
					if(result.status == 200) this.countriesList = [...result.data.data];
					else throw "An error was encountered!";
				} catch(error) {
					console.log(error)
				}
			},

			buildQuestion() {
				let randomNumber = Math.floor(Math.random() * this.countriesList.length);
				this.countryName = this.countriesList[randomNumber].name;
				this.countryCapital = this.countriesList[randomNumber].capital;
				if(this.countryCapital.length == 0) this.buildQuestion();
			},

			checkAnswer(capital) {
				if(capital.toLowerCase() == this.countryCapital.toLowerCase()) {
					this.message = `You're correct! The capital of ${ this.countryName } is ${ this.countryCapital }.`;
					this.switchDisplay(2)
				} else {
					this.message = `Oops, you got it wrong! The capital of ${ this.countryName } is ${ this.countryCapital }.`;
					this.switchDisplay(3)
				}
			},

			checkChoice(choice) {
				if(choice == "Next Question") this.switchDisplay(1)
				else this.switchDisplay(4)
			}
		}

	}
</script>



<style>
	@import url('https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');;
	*, *::before, *::after {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
		font-family: 'Poppins', sans-serif;
	}

	.country-quiz-app {
		height: 100vh;
		width: 100vw;
		padding: 50px;
		background-color: lightblue;
	}

	.country-quiz-app .box-container {
		width: 100%;
		height: 100%;
		position: relative;
		border: 1px solid grey;
		border-radius: 20px;
		display: flex;
		justify-content: center;
		align-items: center;
		background-size: cover;
		transition: all 0.5s ease-in-out;
	}
</style>
