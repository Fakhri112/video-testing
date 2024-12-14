<script setup lang="ts">
import { defineProps, defineEmits, ref } from "vue";
import { onClickOutside } from "@vueuse/core";

defineProps({
	isOpen: Boolean,
	mediaInfoData: String,
});

const emit = defineEmits(["modal-close"]);

const target = ref(null);
onClickOutside(target, () => emit("modal-close"));
</script>

<template>
	<div v-if="isOpen" class="modal-mask grid place-items-center">
		<div class="modal-wrapper w-[66%] rounded-md h-[86%] bg-white p-3">
			<div class="modal-container h-full flex flex-col" ref="target">
				<p class="font-bold mb-2">Mediainfo</p>
				<textarea
					readonly
					name=""
					id=""
					class="mediainfo-area appearance-none rounded-md resize-none border border-slate-600 p-2 text-sm w-full h-full"
					>{{ mediaInfoData }}</textarea
				>
			</div>
		</div>
	</div>
</template>

<style scoped>
.modal-mask {
	position: fixed;
	z-index: 9998;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	background-color: rgba(0, 0, 0, 0.5);
}

.mediainfo-area {
	font-family: Consolas, Monaco, Lucida Console, Liberation Mono,
		DejaVu Sans Mono, Bitstream Vera Sans Mono, Courier New, monospace;
}
</style>
