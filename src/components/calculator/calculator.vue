<script setup>
import { ref } from 'vue';
import NumberButton from '../number-button/number-button.vue';

// example [+, /]
//const selectedOperators = ref([]);
//example [4,7,10]
// const selectedNumber = ref([]);

// example [+, /]
const selectedOperators = ref([]);

// example '84+4'
const currentOperation = ref('');

const numberArray = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
const operatorsArray = ['+', '-', '/', '*'];

const addSelectedValue = (button) => {
	currentOperation.value = currentOperation.value + String(button.value);
	if (button.type > 0) {
		selectedOperators.value.push(button.value);
	}
};

const solveOperation = () => {
	let splittedNumbers = currentOperation.value.split(/[-+*\/]/);
	console.log(splittedNumbers);
	console.log(selectedOperators.value);
	let result = Number(splittedNumbers[0]);

	for (let i = 1; i < splittedNumbers.length; i++) {
		const oper = selectedOperators.value[i - 1];

		switch (oper) {
			case '+': {
				result = result + Number(splittedNumbers[i]);
				break;
			}
			case '-': {
				result = result - Number(splittedNumbers[i]);
				break;
			}
			case '*': {
				result = result * Number(splittedNumbers[i]);
				break;
			}
			case '/': {
				result = result / Number(splittedNumbers[i]);
				break;
			}
			default:
				break;
		}
		console.log('current Result ' + result);
	}
	console.log('final ', result);
};
</script>

<template>
	<h1>Calculator</h1>
	<div class="display">
		{{ currentOperation }}
	</div>
	<div class="calculator-container">
		<div class="numbers-container">
			<NumberButton
				class="number-btn"
				v-for="num in numberArray"
				:btn-value="num"
				:type="0"
				@button-selected="addSelectedValue"
			></NumberButton>
		</div>
		<div class="ope-container">
			<div class="operators-container">
				<NumberButton
					class="number-btn"
					v-for="operator in operatorsArray"
					:btn-value="operator"
					:type="1"
					@button-selected="addSelectedValue"
				></NumberButton>
			</div>
			<div>
				<button class="equal-btn" @click="solveOperation">=</button>
			</div>
		</div>
	</div>
</template>

<style scoped>
.display {
	background-color: #b8b7b7e6;
	border-radius: 10px 10px 0 0;
	max-width: 30%;
	padding: 5px;
	min-height: 40px;
	font-weight: 600;
	font-size: 16px;
	letter-spacing: 2px;
	margin: auto;
}
.calculator-container {
	padding: 15px 5px 5px 5px;
	margin: auto;
	border-radius: 0 0 10px 10px;
	max-width: 30%;
	display: flex;
	justify-content: space-between;
	gap: 10px;
	background-color: #f2f2f2e6;
}
.numbers-container {
	width: 70%;
	display: grid;
	grid-template-columns: repeat(3, 1fr);
	gap: 5px;
}
.number-btn {
	width: 100%;
	height: 50px;
	border: none;
	border-radius: 10px;
	background-color: #a9a9a95e;
	font-size: 18px;
	font-weight: 500;
}
.number-btn:hover {
	background-color: #a9a9a9b8;
}
.ope-container {
	width: 30%;
	display: flex;
	flex-direction: column;
	justify-content: space-between;
}
.operators-container {
	display: grid;
	grid-template-columns: repeat(2, 1fr);
	gap: 5px;
}
.equal-btn {
	width: 100%;
	background-color: #4a4a768a;
	border: none;
	border-radius: 10px;
	height: 50px;
}
</style>
