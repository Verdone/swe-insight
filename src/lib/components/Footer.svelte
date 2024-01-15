<script>
	const year = new Date().getFullYear();
	$: year;
</script>

<footer class="shadow bg-gray-900 mx-auto">
	<div class="w-full max-w-screen-xl mx-auto p-4 md:py-8">
		<div class="sm:flex sm:items-center sm:justify-between">
			<a href="/" class="flex items-center mb-4 sm:mb-0 space-x-3 rtl:space-x-reverse">
				<svg
					xmlns="http://www.w3.org/2000/svg"
					fill="none"
					viewBox="0 0 24 24"
					stroke-width="1.5"
					stroke="currentColor"
					class="w-6 h-6 mr-1 text-yellow-400 hover:text-yellow-300 transition-colors"
				>
					<path
						stroke-linecap="round"
						stroke-linejoin="round"
						d="M12 18v-5.25m0 0a6.01 6.01 0 0 0 1.5-.189m-1.5.189a6.01 6.01 0 0 1-1.5-.189m3.75 7.478a12.06 12.06 0 0 1-4.5 0m3.75 2.383a14.406 14.406 0 0 1-3 0M14.25 18v-.192c0-.983.658-1.823 1.508-2.316a7.5 7.5 0 1 0-7.517 0c.85.493 1.509 1.333 1.509 2.316V18"
					/>
				</svg>
				<span class="self-center text-2xl font-semibold whitespace-nowrap text-white"
					>SWE Insight</span
				>
			</a>
			<ul class="flex flex-wrap items-center mb-6 text-sm font-medium sm:mb-0 text-gray-400">
				<li>
					<a href={'/about'} class="hover:underline me-4 md:me-6">About</a>
				</li>
				<li>
					<a href={'/copywright'} class="hover:underline me-4 md:me-6">Copywright</a>
				</li>
				<li>
					<a href={'/contact'} class="hover:underline">Contact</a>
				</li>
			</ul>
		</div>
		<hr class="my-6 sm:mx-auto border-gray-700 lg:my-8" />
		<span class="block text-sm sm:text-center text-gray-400"
			>Copywright © <a href={'https://github.com/Verdone'} target="_blank" class="hover:underline"
				>Giuliano Verdone</a
			>
			2023 - {year}. All rights reserved.</span
		>
	</div>
</footer>
