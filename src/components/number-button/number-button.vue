<script setup>
const props = defineProps({
	btnValue: null,
	type: 0,
});
const emits = defineEmits(['button-selected']);

const buttonSelected = () => {
	emits('button-selected', {
		value: props.btnValue,
		type: props.type,
	});
};
</script>
<template>
	<button :value="btnValue" @click="buttonSelected">
		{{ btnValue }}
	</button>
</template>
<style scoped></style>
