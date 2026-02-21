<script setup>
import Calculator from './components/calculator/calculator.vue';
</script>

<template>
    <div class="content">
        <Calculator></Calculator>
    </div>
</template>

<style scoped>
.content {
    height: 100vh;
    max-width: 35%;
    margin: 30px auto;
}
@media (max-width: 650px) {
    .content {
        max-width: 90%;
    }
}
</style>
