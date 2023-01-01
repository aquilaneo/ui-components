<template>
	<TabView>
		<TabContent label="タブ1" formName="tab-a">
			<h1>タブ1の中身</h1>
			<div>中身</div>
		</TabContent>

		<TabContent label="タブ2" formName="tab-a">
			<h1>タブ2の中身</h1>
			<div>中身</div>
		</TabContent>
	</TabView>
</template>

<style scoped>

</style>

<script setup lang="ts">
import TabView from "@/components/TabView.vue";
import TabContent from "@/components/TabContent.vue";
</script>
