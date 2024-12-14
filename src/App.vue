<script setup lang="ts">
import Player from "./components/Player.vue";
</script>

<template>
	<div class="bg-blue-900 h-screen grid place-items-center relative">
		<p class="font-bold text-3xl text-white absolute top-4 italic left-5">
			RizFlix21
		</p>
		<div class="lg:w-[65%] w-[80%]">
			<Player />
		</div>
	</div>
</template>
