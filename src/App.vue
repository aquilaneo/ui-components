<template>
	<SplitView
		:initialWidths="['10rem','10rem', '10rem']"
		:minWidths="['2rem','2rem','2rem']"
		:maxWidths="['20rem','20rem','20rem']">
		<template #split1>あああ</template>
		<template #split2>いいい</template>
		<template #split3>ううう</template>
	</SplitView>
</template>

<style scoped>

</style>

<script setup lang="ts">
import SplitView from "@/components/SplitView.vue";
</script>
