<template>
	<input type="radio" :name="formName" :id="inputId" v-model="model"/>
	<label :for="inputId">{{ props.label }}</label>
</template>

<style scoped>
</style>

<script setup lang="ts">
import { computed, ref } from "vue";
const props = defineProps ({
	label: String,
	formName: String,
});

const model = ref<string>("");

const inputId = computed(() => {
	return `${props.formName}-${props.label}`;
});

</script>
