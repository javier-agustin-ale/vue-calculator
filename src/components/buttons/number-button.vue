<script setup>
const props = defineProps({ btnValue: null });
</script>
<template>
    <button class="number-btn" :value="btnValue">
        {{ btnValue }}
    </button>
</template>

<style scoped>
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
    cursor: pointer;
}
</style>
