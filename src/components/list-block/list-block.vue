<script setup lang="ts">
import ListItem from "./list-item.vue";
import { defineProps } from "vue";

const props = defineProps<{
	itemsArr: string[][];
}>();
const emit = defineEmits<{
	"delete-item": [index: number];
}>();
const title: string[] = ["назва", "категорія", "сума", "дата"];

function handleDelete(index: number) {
	emit("delete-item", index);
}
</script>

<template>
	<section class="p-3 border rounded bd-example mt-4">
		<div class="d-flex justify-content-between align-items-center gap-2">
			<p
				class="w-100 mb-3 fw-bold text-center"
				v-for="(item, index) in title"
				:key="index">
				{{ item }}
			</p>
		</div>
		<div class="">
			<ListItem
				v-for="(items, index) in props.itemsArr"
				:key="index"
				:item="items"
				@delete="() => handleDelete(index)" />
		</div>
	</section>
</template>

<style scoped lang="scss"></style>
