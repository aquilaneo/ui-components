<template>
	<div v-for="(tabContent, index) in tabContents">
		<input type="radio" :id="index" :name="uuid">
		<label :for="index">AAA</label>
	</div>
</template>

<style scoped>

</style>

<script setup lang="ts">
import {computed, ref, useSlots} from "vue";
import {v4 as uuidv4} from "uuid";

const uuid = ref (uuidv4 ());

// TabContentたちを取得
const tabContents = computed ((): string[] => {
	// TabViewの子となる要素一覧を取得
	const slots = useSlots ().default?. ();
	if (!slots) {
		return [];
	}

	const tabs = new Array<string> ();
	for (const slot of slots) {
		tabs.push ("AAA");
	}

	return tabs;
});
</script>
