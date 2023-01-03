<template>
	<div style="display: flex;">
		<div :style="styleLeft">
			<slot name="left"/>
		</div>
		<div class="splitview-splitter"></div>
		<div :style="styleRight">
			<slot name="right"/>
		</div>
	</div>
</template>

<script setup lang="ts">
import {computed, onMounted, ref, useSlots} from "vue";

const props = defineProps ({
	// 幅の初期値
	initialWidthLeft: {
		type: String,
		required: true
	},
	initialWidthRight: {
		type: String,
		required: true
	},

	// maxWidth
	maxWidthLeft: {
		type: String,
		required: false
	},
	maxWidthRight: {
		type: String,
		required: false
	},

	// minWidth
	minWidthLeft: {
		type: String,
		required: false
	},
	minWidthRight: {
		type: String,
		required: false
	}
});

// 左パネルのスタイル
const styleLeft = computed (() => {
	const width = `width: calc(${props.initialWidthLeft} + ${widthLeftDelta.value}px);\n`;
	const maxWidth = props.maxWidthLeft ? `max-width: ${props.maxWidthLeft};\n` : "\n";
	const minWidth = props.minWidthLeft ? `min-width: ${props.minWidthLeft};\n` : "\n";
	return width + maxWidth + minWidth;
});

// 右パネルのスタイル
const styleRight = computed (() => {
	const width = `width: calc(${props.initialWidthRight} + ${widthRightDelta.value}px);\n`;
	const maxWidth = props.maxWidthRight ? `max-width: ${props.maxWidthRight};\n` : "\n";
	const minWidth = props.minWidthRight ? `min-width: ${props.minWidthRight};\n` : "\n";
	return width + maxWidth + minWidth;
});

// 各パネルの幅差分
const widthLeftDelta = ref (0);
const widthRightDelta = ref (0);
</script>

<style scoped>
.splitview-splitter {
	width: 0.4rem;
	cursor: col-resize;
}
</style>
