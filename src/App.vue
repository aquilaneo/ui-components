<template>
	<TabView :tabLabels="['AAA', 'BBB']">
		<template #tab0>タブ0</template>
		<template #tab1>タブ1</template>
	</TabView>

	<TabView :tabLabels="['CCC', 'DDD']">
		<template #tab0>タブA</template>
		<template #tab1>タブB</template>
	</TabView>
</template>

<style scoped>

</style>

<script setup lang="ts">
import TabView from "@/components/TabView.vue";
</script>
