<script setup lang="ts">
import { ref, nextTick } from 'vue';
import EqualButton from '../buttons/equal-button.vue';
import NumberButton from '../buttons/number-button.vue';
import Display from '../display/display.vue';

const currentValue = ref('');
const previousValue = ref('');
const operator = ref('');

const triggerAnimation = ref(false);

const valuesArray: (number | string)[] = [9, 8, 7, 6, 5, 4, 3, 2, 1, 0, '.'];
const operatorsArray: string[] = ['+', '-', '/', '*'];

const selectedOperator = (oper: string): void => {
    if (!currentValue.value) return;
    if (previousValue.value === '') {
        previousValue.value = currentValue.value;
        currentValue.value = '';
        operator.value = oper;
    } else {
        solveOperation(false);
        currentValue.value = '';
        operator.value = oper;
    }
    triggerAnimation.value = false;
    nextTick(() => {
        triggerAnimation.value = true;
        setTimeout(() => {
            triggerAnimation.value = false;
        }, 250);
    });
};
const addValue = (number: number | string): void => {
    if (number === '.' && currentValue.value.includes('.')) return;
    currentValue.value += number;
};

const removeNumber = (): void => {
    currentValue.value = currentValue.value.slice(0, -1);
};

const solveOperation = (isEqual = true): void => {
    if (!currentValue.value || !previousValue.value) return;
    const solve = previousValue.value + operator.value + currentValue.value;
    const result = parseFloat(eval(solve).toFixed(4));

    if (isEqual) {
        currentValue.value = String(result);
        previousValue.value = '';
    } else {
        previousValue.value = String(result);
    }
};
</script>

<template>
    <Display
        :current-value="currentValue"
        :previous-value="previousValue"
        :operator="operator"
        :trigger-animation="triggerAnimation"
    ></Display>
    <div class="calculator-container">
        <div class="numbers-container">
            <NumberButton
                v-for="val in valuesArray"
                :btn-value="val"
                :class="{ zero: val === 0 }"
                @click="addValue(val)"
            ></NumberButton>
        </div>
        <div class="operators-container">
            <div>
                <button class="remove-btn" @click="removeNumber">CE</button>
            </div>
            <div class="operators-buttons">
                <NumberButton
                    v-for="operator in operatorsArray"
                    :btn-value="operator"
                    @click="selectedOperator(operator)"
                ></NumberButton>
            </div>
            <div>
                <EqualButton @click="solveOperation"></EqualButton>
            </div>
        </div>
    </div>
</template>

<style scoped>
.calculator-container {
    padding: 15px 5px 5px 5px;
    border-radius: 0 0 10px 10px;
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
.zero {
    grid-column: 2;
}
.remove-btn {
    width: 100%;
    background-color: #ad69568a;
    border: none;
    border-radius: 10px;
    height: 50px;
    font-size: 17px;
    font-weight: 500;
}
.remove-btn:hover {
    background-color: #c751318a;
    cursor: pointer;
}
.operators-container {
    width: 30%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}
.operators-buttons {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 5px;
}
</style>
