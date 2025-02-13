<script setup lang="ts">
import { defineProps } from "vue";

defineProps({
	name: String,
	id: String,
	label: {
		type: String,
		default: "input field",
	},
	type: {
		type: String,
		default: "text",
	},
});
</script>

<template>
	<div class="w-100 mx-auto position-relative">
		<label
			class="form-label"
			:for="id">
			{{ label }}
		</label>
		<input
			:type="type"
			class="form-control"
			:name="name"
			:aria-label="label"
			:id="id" />
	</div>
</template>

<style scoped></style>
