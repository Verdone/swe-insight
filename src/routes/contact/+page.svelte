<script>
	import undraw_relax from '$lib/assets/images/undraw_relax.svg';
	import { websiteName } from '$lib/stores';
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

<svelte:head>
	<title>Home - {websiteName}</title>
</svelte:head>

<section class="bg-white dark:bg-gray-800">
	<div class="py-8 px-4 mx-auto max-w-screen-xl lg:py-16 lg:px-6">
		<div class="max-w-screen-lg text-gray-400 sm:text-lg mb-10">
			<h2 class="mb-4 text-4xl tracking-tight font-bold text-gray-900 dark:text-white">
				Social Networks
			</h2>
			<p class="mb-4 font-light">
				You can send me a message on <a
					href="
                    https://www.linkedin.com/in/giuliano-verdone"
					target="_blank"
					class="text-blue-500 hover:text-blue-300">LinkedIn</a
				>, or check out my GitHub profile
				<a
					href="https://github.com/Verdone"
					target="_blank"
					class="text-blue-500 hover:text-blue-300">here</a
				>.
			</p>
			<p class="mb-4 font-light">
				If you'd like to submit an issue or feature request for this website, you can do so via this
				<a
					href="https://github.com/Verdone/swe-insight/issues"
					target="_blank"
					class="text-blue-500 hover:text-blue-300">GitHub repository</a
				>.
			</p>
		</div>

		<div class="max-w-screen-lg text-gray-400 sm:text-lg">
			<h2 class="mb-4 text-4xl tracking-tight font-bold text-gray-900 dark:text-white">Email</h2>
			<p class="mb-4 font-light">
				Feel free to send an email to
				<a
					href="mailto:
					giulianoverdone@gmail.com"
					target="_blank"
					class="text-blue-500 hover:text-blue-300"
					>giulianoverdone@gmail.com
				</a>
				if you want to get in touch.
			</p>
		</div>
		{#if showError}
			<!-- Show error message or alternative content if the image fails to load -->
			<div class="text-red-500">Error loading image</div>
		{:else if imageLoaded}
			<!-- Show the SVG if it's loaded -->
			<img src={undraw_relax} alt="Undraw - Relaxed" class="w-80 h-80 mx-auto mt-10" />
		{:else}
			<!-- Show a Tailwind CSS loader while the image is still loading -->
			<div
				class="animate-spin rounded-full border-t-4 border-blue-500 border-opacity-25 h-16 w-16"
			></div>
		{/if}
	</div>
</section>
