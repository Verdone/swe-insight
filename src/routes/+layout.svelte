<script>
	import '../app.css';
	import Navbar from '../lib/components/Navbar.svelte';
</script>

<Navbar />

<main>
	<slot />
</main>

<style lang="postcss">
	:global(html) {
		font-family: 'Inter', sans-serif;
		color: theme('colors.white');
		background-color: theme('colors.gray.800');
	}
</style>
