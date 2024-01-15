<script>
	import undraw_working from '$lib/assets/images/undraw_working.svg';
	import { onMount } from 'svelte';

	let imageLoaded = false;
	let showError = false;

	const handleLoad = () => {
		imageLoaded = true;
	};

	const handleError = () => {
		showError = true;
	};

	onMount(() => {
		handleLoad();
	});
</script>

<div class="min-h-screen bg-gray-800 flex flex-col items-center justify-center">
	<h1 class="text-5xl text-white font-bold mb-8">
		🚧 <span class="animate-pulse">Coming Soon</span> 🚧
	</h1>
	<p class="text-white text-lg mb-8">
		🏗️ We're working hard to bring you something amazing on this page. Stay tuned! 🛠️
	</p>

	{#if showError}
		<!-- Show error message or alternative content if the image fails to load -->
		<div class="text-red-500">Error loading image</div>
	{:else if imageLoaded}
		<!-- Show the SVG if it's loaded -->
		<img src={undraw_working} alt="Undraw - Under Construction" class="w-64 h-64 mx-auto mt-10" />
	{:else}
		<!-- Show a Tailwind CSS loader while the image is still loading -->
		<div
			class="animate-spin rounded-full border-t-4 border-blue-500 border-opacity-25 h-16 w-16"
		></div>
	{/if}
</div>
