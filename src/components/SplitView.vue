<template>
	<div class="splitview">
		<!-- SplitView本体 -->
		<template v-for="i of panelCount">
			<div :style="getStyle(i - 1)" class="splitview-content">
				<slot :name="`split${i}`"/>
			</div>
			<div class="splitview-splitter" v-if="i < panelCount"
				 @mousedown="(e) => {startDragging(i - 1, e.pageX, e.pageY)}"
			/>
		</template>

		<!-- mousemove、mouseup検出用ダミー要素 -->
		<div class="splitview-dummy" v-if="draggingIndex !== -1"
			 @mousemove="(e) => {updateDragging(e.pageX, e.pageY)}"
			 @mouseleave="endDragging" @mouseup="endDragging"/>
	</div>
</template>

<script setup lang="ts">
import {ref, useSlots} from "vue";

const props = defineProps ({
	// 幅の初期値
	initialWidths: {
		type: Array,
		required: true
	},

	// maxWidth
	maxWidths: {
		type: Array,
		required: true
	},

	// minWidth
	minWidths: {
		type: Array,
		required: true
	}
});

// Data
const panelCount = Object.keys (useSlots ()).length; // 子パネルの個数
const widthDeltas = ref<number[]> (new Array (panelCount).fill (0)); // 幅の差分px

// minWidthやmaxWidthを反映したスタイル文字列を取得する
const getStyle = (index: number) => {
	const width = `width: calc(${props.initialWidths[index]} + ${widthDeltas.value[index]}px);\n`;
	const maxWidth = props.maxWidths[index] ? `max-width: ${props.maxWidths[index]};\n` : "\n";
	const minWidth = props.minWidths[index] ? `min-width: ${props.minWidths[index]};\n` : "\n";
	return width + maxWidth + minWidth;
};

// パネルの幅を更新
const updateWidth = (index: number, deltaX: number, deltaY: number) => {
	widthDeltas.value[index] += deltaX;     // 左側のパネルは加算
	widthDeltas.value[index + 1] -= deltaX; // 同じ分だけ右側のパネルから減算
};

// ドラッグに必要なイベントたち
const draggingIndex = ref (-1); // ドラッグ中のindex(ドラッグ中じゃないときは-1)
const oldCursorPosition = {x: 0, y: 0}; // 1サイクル前のカーソル位置
const startDragging = (index: number, cursorX: number, cursorY: number) => {
	// console.log ("start");
	draggingIndex.value = index;
	oldCursorPosition.x = cursorX;
	oldCursorPosition.y = cursorY;
};
const updateDragging = (cursorX: number, cursorY: number) => {
	// console.log ("update");
	// カーソル移動量
	const deltaX = cursorX - oldCursorPosition.x;
	const deltaY = cursorY - oldCursorPosition.y;
	// 1サイクル前の値として現在の座標を記録
	oldCursorPosition.x = cursorX;
	oldCursorPosition.y = cursorY;

	updateWidth (draggingIndex.value, deltaX, deltaY);
};
const endDragging = () => {
	// console.log ("end");
	draggingIndex.value = -1;
};
</script>

<style scoped>
.splitview {
	display: flex;
	width: 100%;
	height: 100%;
}

.splitview-content {
	height: 100%;
}

.splitview-splitter {
	width: 0.4rem;
	cursor: col-resize;
}

.splitview-dummy {
	position: absolute;
	top: 0;
	right: 0;
	bottom: 0;
	left: 0;
	cursor: col-resize;
}
</style>
