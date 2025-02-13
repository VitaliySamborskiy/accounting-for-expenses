<script setup lang="ts">
import formItem from "../src/components/inputs-block/form-adding-costs.vue";
import listItem from "../src/components/list-block/list-block.vue";
import totalCostsBlock from "../src/components/total-costs-block/total-costs-block.vue";
import { onMounted, ref, watch } from "vue";
import { Notify } from "notiflix";

let items = ref<string[][]>([]);

function handleData(newItem: string[]) {
	items.value = [...items.value, newItem];
}

function deleteItem(index: number) {
	items.value.splice(index, 1);
	Notify.info("Витрата успішно видалена");
}

function setDataStorage(itemsArray: string[][]): void {
	localStorage.setItem("items", JSON.stringify(itemsArray));
}

function getDataStorage(): string[][] {
	const storage = localStorage.getItem("items");
	if (!storage) return [];
	return JSON.parse(storage);
}

onMounted(() => (items.value = getDataStorage()));

watch(
	() => items.value,
	itemsArr => {
		setTimeout(() => setDataStorage(itemsArr), 0);
	},
	{ immediate: true, deep: true }
);
</script>

<template>
	<main>
		<form-item @form-submitted="handleData" />
		<list-item
			:items-arr="items"
			@delete-item="deleteItem" />
		<total-costs-block :items-arr-sum="items" />
	</main>
</template>

<style scoped lang="scss"></style>
