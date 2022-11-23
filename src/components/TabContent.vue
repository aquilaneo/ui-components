<template>
	<div :class="attachedClass">
		<slot/>
	</div>
</template>

<style scoped>
.ui-component-tabview-shown {
	display: block;
}

.ui-component-tabview-hidden {
	display: none;
}
</style>

<script setup lang="ts">

import {computed} from "vue";

const props = defineProps ({
	label: String,
	checked: Boolean,
});

const attachedClass = computed (() => {
	return props.checked ? "ui-component-tabview-shown" : "ui-component-tabview-hidden";
});
</script>
