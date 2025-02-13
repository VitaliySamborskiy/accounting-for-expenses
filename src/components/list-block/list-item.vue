<script setup lang="ts">
import { defineProps, defineEmits } from "vue";

const props = defineProps<{
	item: string[];
}>();

const emit = defineEmits<{
	"delete": [];
}>();
</script>

<template>
	<article
		class="d-flex justify-content-between align-items-center gap-2 border-top pt-2 pb-2 position-relative">
		<p
			class="w-100 mb-0 text-center"
			v-for="(item, index) in props.item"
			:key="index">
			{{ item }}
		</p>
		<button
			@click="emit('delete')"
			class="btn btn-danger fw-bold text-white px-2 py-0 position-absolute end-0">
			X
		</button>
	</article>
</template>

<style scoped lang="scss"></style>
