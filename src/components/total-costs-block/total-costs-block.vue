<script setup lang="ts">
import { defineProps, watch, ref } from "vue";
const sum = ref<number>(0);

const props = defineProps<{
	itemsArrSum: string[][];
}>();

function totalCostsSum(arr: string[][]): number {
	return arr.reduce((result, items) => {
		const cost = +items[2];
		return result + cost;
	}, 0);
}

watch(
	() => props.itemsArrSum,
	newArr => {
		sum.value = totalCostsSum(newArr);
	},
	{ immediate: true, deep: true }
);
</script>

<template>
	<section
		class="p-3 border rounded bd-example mt-4 mb-4 d-flex justify-content-between align-items-center">
		<p class="mb-0 text-center">Загальні витрати</p>
		<p class="mb-0 fw-bold text-center">
			{{ sum }}
			<span>гривень</span>
		</p>
	</section>
</template>

<style scoped lang="scss"></style>
