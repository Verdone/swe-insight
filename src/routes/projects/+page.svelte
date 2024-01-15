<script>
	import ComingSoon from '$lib/components/ComingSoon.svelte';
	import { websiteName } from '$lib/stores';
</script>

<svelte:head>
	<title>Projects - {websiteName}</title>
</svelte:head>

<ComingSoon />
