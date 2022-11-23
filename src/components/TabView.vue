<template>
	<!-- タブ切り替え用のラジオボタンとラベル -->
	<div v-for="(tabContent, index) in tabContents">
		<input type="radio" :id="getId(index)" :name="uuid" :checked="tabContent.checked">
		<label :for="index">{{ tabContent.label }}</label>
	</div>

	<!-- タブの中身 -->
	<slot/>
</template>

<style scoped>

</style>

<script setup lang="ts">
import {computed, useSlots} from "vue";
import {v4 as uuidv4} from "uuid";

// inputのname属性に与えるuuid
const uuid = uuidv4 ();

// 子のTabContentたちを取得
const tabContents = computed ((): { label: String, checked: Boolean }[] => {
	// TabViewの子となる要素一覧を取得
	const slots = useSlots ().default?. ();
	if (!slots) {
		return [];
	}

	// タブのラベル名を取得
	const tabs = [];
	for (const slot of slots) {
		if (slot.props) {
			tabs.push ({label: slot.props.label, checked: slot.props.checked === true});
		} else {
			tabs.push ({label: "[ERROR]", checked: false});
		}
	}

	return tabs;
});

// inputタグにつけるidを取得
const getId = (index: number) => {
	return `tab-${uuid}-${index}`;
};
</script>
