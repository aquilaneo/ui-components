<template>
	<div class="tabview">
		<ul class="tabview-tab_container">
			<li v-for="(tabLabel, index) in props.tabLabels"
				class="tabview-tab" :class="{'tabview-tab_selected': index === selectedTab}">
				<input type="radio" v-model="selectedTab" :name="uid" :value="index" :id="`${uid}-${index}`">
				<label :for="`${uid}-${index}`">{{ tabLabel }}</label>
			</li>
		</ul>

		<div v-for="(tabLabel, index) in props.tabLabels" class="tabview-content">
			<slot :name="`tab${index}`" v-if="index === selectedTab"></slot>
		</div>
	</div>
</template>

<style scoped>
ul {
	padding: 0;
	margin: 0;
	display: flex;
}

li {
	list-style: none;
}

input {
	display: none;
}

label {
	display: inline-block;
	width: 100%;
	height: 100%;
}
</style>

<script setup lang="ts">
import {onMounted, ref} from "vue";
import {v4 as uuidv4} from "uuid";

const props = defineProps ({
	// タブのラベル配列
	tabLabels: {
		type: Array,
		required: true
	},
	// 最初に選択されたタブ
	initialTab: {
		type: Number,
		required: false
	}
});

const selectedTab = ref (0); // 現在選択されているタブ
const uid = ref (""); // inputタグのnameに使う一意なID

onMounted (() => {
	// 初期選択タブを反映する
	if (props.initialTab) {
		selectedTab.value = props.initialTab;
	}

	// 一意なIDを生成
	uid.value = uuidv4 ();
});
</script>
