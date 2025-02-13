<script setup lang="ts">
import inputItem from "./input.vue";
import { onMounted, defineEmits } from "vue";
import JustValidate, { FieldRuleInterface, Rules } from "just-validate";
import { Notify } from "notiflix";

type ValidateFields = {
	inputName: string;
	rules: FieldRuleInterface[];
};

const rulesValidate: ValidateFields[] = [
	{
		inputName: "#name",
		rules: [
			{
				rule: Rules.Required,
				errorMessage: "Ви не ввели назву витрати",
			},
		],
	},
	{
		inputName: "#category",
		rules: [
			{
				rule: Rules.Required,
				errorMessage: "Ви не ввели категорію витрати",
			},
		],
	},
	{
		inputName: "#amount",
		rules: [
			{
				rule: Rules.Required,
				errorMessage: "Ви не ввели витрату",
			},
		],
	},
	{
		inputName: "#date",
		rules: [
			{
				rule: Rules.Required,
				errorMessage: "Ви не ввели дату",
			},
		],
	},
];

const inputs = [
	{
		name: "name",
		id: "name",
		label: "назва",
	},
	{
		name: "category",
		id: "category",
		label: "категорія",
	},
	{
		name: "amount",
		id: "amount",
		label: "сума",
		type: "number",
	},
	{
		name: "date",
		id: "date",
		label: "дата",
		type: "date",
	},
];

const emit = defineEmits();

function validateInput(fields: ValidateFields[]) {
	const validator = new JustValidate(document.getElementById("addCostsForm") as HTMLElement, {
		errorFieldCssClass: "text-danger border-danger",
		errorLabelCssClass: "text-danger fs-6 position-absolute",
	});

	fields.forEach(field => {
		validator.addField(field.inputName, field.rules);
	});

	validator
		.onSuccess(() => {
			Notify.success("Витрату створенно успішно");
			const itemsData = getFormData(document.getElementById("addCostsForm") as HTMLFormElement);
			emit("form-submitted", itemsData);
			console.log(itemsData);
		})
		.onFail(() => {
			Notify.warning("Дані не коректні, перевірте їх будь ласка");
		});
}

function getFormData(form: HTMLFormElement): string[] {
	const data = new FormData(form);
	return Array.from(data.values()).map(value => value.toString());
}

onMounted(() => {
	validateInput(rulesValidate);
});
</script>

<template>
	<form
		class="p-3 border rounded bd-example mt-4"
		id="addCostsForm">
		<fieldset class="d-flex justify-content-between align-items-center gap-2">
			<input-item
				v-for="(item, index) in inputs"
				:key="index"
				:name="item.name"
				:id="item.id"
				:label="item.label"
				:type="item.type"></input-item>
		</fieldset>
		<button
			type="submit"
			class="btn btn-success w-100 mt-5">
			додати витрату +
		</button>
	</form>
</template>

<style scoped lang="scss"></style>
