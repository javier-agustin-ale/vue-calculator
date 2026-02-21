<script setup lang="ts">
const props = defineProps({
    previousValue: String,
    currentValue: String,
    operator: String,
});
</script>

<template>
    <div class="display">
        <div class="values-container">
            <div class="previous-value">
                {{ previousValue }}
                {{ operator && previousValue ? operator : '' }}
            </div>
            <div class="current-value">
                {{ currentValue }}
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
    min-height: 50px;
    font-weight: 600;
    font-size: 17px;
    letter-spacing: 2px;
    margin: auto;
    text-align: end;
    display: grid;
}
.values-container {
    padding: 5px 10px 0 0;
    display: flex;
    flex-direction: column;
    gap: 5px;
}
.previous-value {
    height: 50%;
    color: gray;
}
.current-value {
    height: 50%;
}
</style>
