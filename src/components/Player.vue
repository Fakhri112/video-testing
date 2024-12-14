<script setup lang="ts">
// import mediaInfoFactory from "mediainfo.js";
// import Modal from "./Modal.vue";
import Plyr from "plyr";
import { ref, watch } from "vue";
import { checkURL } from "../utils/function";
const src = ref("");
const urlInput = ref("");
const isLoading = ref(false);
//const isModalOpened = ref(false);
// const mediainfodata = ref("");
// const openModal = () => (isModalOpened.value = true);
// const closeModal = () => (isModalOpened.value = false);

watch(src, () => {
	setTimeout(() => {
		new Plyr("#player");
	}, 300);
});

const handleonload = () => {
	isLoading.value = false;
};

const playvideo = () => {
	// mediainfodata.value = "";
	if (isLoading.value) return;
	src.value = "";
	if (!urlInput.value) return;
	if (!checkURL(urlInput.value)) return;
	isLoading.value = true;
	setTimeout(() => {
		src.value = urlInput.value;
	}, 800);
	setTimeout(() => {
		if (!isLoading.value) return;
		isLoading.value = false;
		src.value = "";
	}, 9000);
	// fetch(urlInput.value)
	// 	.then(function (response) {
	// 		console.log(response);
	// 		return response.blob();
	// 	})
	// 	.then(function (blob) {
	// 		const file = new File([blob], "video", { type: blob.type });
	// 		const readChunk = async (chunkSize: number, offset: number) =>
	// 			new Uint8Array(
	// 				await file.slice(offset, offset + chunkSize).arrayBuffer(),
	// 			);

	// 		mediaInfoFactory({ format: "text" }, (mediainfo) => {
	// 			mediainfo
	// 				.analyzeData(file.size, readChunk)
	// 				.then((result) => {
	// 					isLoading.value = false;
	// 					if (result.length < 80) return (src.value = "");
	// 					src.value = urlInput.value;
	// 					mediainfodata.value = result;
	// 				})
	// 				.catch((error) => {
	// 					isLoading.value = false;
	// 					console.log("error");
	// 				});
	// 		});
	// 	})
	// 	.catch((error) => {
	// 		console.log(error);

	// 		isLoading.value = false;
	// 		//return (src.value = "");
	// 	});
};
</script>

<template>
	<div class="mb-3 flex justify-between">
		<div class="flex gap-x-3">
			<p class="font-bold text-white">Video Testing</p>
			<svg
				:class="[!isLoading && 'hidden']"
				class="w-6 animate-spin fill-slate-100"
				xmlns="http://www.w3.org/2000/svg"
				viewBox="0 0 512 512">
				<path
					d="M222.7 32.1c5 16.9-4.6 34.8-21.5 39.8C121.8 95.6 64 169.1 64 256c0 106 86 192 192 192s192-86 192-192c0-86.9-57.8-160.4-137.1-184.1c-16.9-5-26.6-22.9-21.5-39.8s22.9-26.6 39.8-21.5C434.9 42.1 512 140 512 256c0 141.4-114.6 256-256 256S0 397.4 0 256C0 140 77.1 42.1 182.9 10.6c16.9-5 34.8 4.6 39.8 21.5z" />
			</svg>
		</div>

		<!-- <button
			@click="openModal"
			:disabled="mediainfodata.length == 0"
			:class="[mediainfodata.length == 0 ? 'btn-disabled' : 'btn-primary']">
			Open Mediainfo
		</button> -->
	</div>
	<div class="flex mb-4">
		<input
			required
			type="text"
			placeholder="Enter the video link"
			class="h-12 w-full px-4"
			:value="urlInput"
			@input="(event: any) => (urlInput = event.target.value)" />

		<button
			@click="playvideo()"
			class="font-semibold bg-blue-400 px-4 hover:bg-blue-500">
			Play
		</button>
	</div>
	<!-- 
	<Modal
		:media-info-data="mediainfodata"
		:isOpen="isModalOpened"
		@modal-close="closeModal"
		name="first-modal">
		<template #content>{{ mediainfodata }}</template>
	</Modal> -->
	<div v-if="src" class="lg:h-[100%] bg-black flex justify-center">
		<video
			autoplay
			controls
			name="media"
			class="h-full w-full"
			id="player"
			@loadeddata="handleonload()">
			<source :src="src" type="video/mp4" />
		</video>
	</div>
	<div v-else class="w-full bg-black h-80"></div>
</template>
