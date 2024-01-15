<script>
	import '../app.css';
	import Footer from '../lib/components/Footer.svelte';
	import Navbar from '../lib/components/Navbar.svelte';
</script>

<Navbar />

<main class="min-h-screen">
	<slot />
</main>

<Footer />

<style lang="postcss">
	:global(html) {
		font-family: 'Cuprum', sans-serif;
		color: theme('colors.white');
		background-color: theme('colors.gray.800');
	}
</style>
