<script setup lang="ts">
const props = defineProps({
    previousValue: String,
    currentValue: String,
    operator: String,

    triggerAnimation: Boolean,
});
</script>

<template>
    <div class="display">
        <div class="values-container" :class="{ animate: triggerAnimation }">
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
    padding: 5px;
    min-height: 50px;
    font-weight: 600;
    letter-spacing: 2px;
    text-align: end;
    display: grid;
    overflow: hidden;
}

.values-container {
    padding: 5px 10px 0 0;
    display: flex;
    flex-direction: column;
    gap: 5px;
}
.previous-value {
    height: 50%;
    color: #534e4e;
    font-size: 17px;
}
.current-value {
    height: 50%;
    font-size: 18px;
}

.previous-value,
.current-value {
    transition: transform 0.25s cubic-bezier(0.4, 0, 0.2, 1);
}

.values-container.animate .current-value {
    transform: translateY(-10px);
    opacity: 0.6;
}

.values-container.animate .previous-value {
    transform: translateY(-10px);
}
</style>
