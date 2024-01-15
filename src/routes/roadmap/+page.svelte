<script>
	import ComingSoon from '$lib/components/ComingSoon.svelte';
	import { websiteName } from '$lib/stores';
</script>

<svelte:head>
	<title>Roadmaps - {websiteName}</title>
</svelte:head>

<ComingSoon />
<!-- Include an actual roadmap page here, and references to good resources for learning Svelte. e.g.
Leetcode for websites, or a book for learning a language/topic. Then get specific with things like
Leetcode blind 75 -->
