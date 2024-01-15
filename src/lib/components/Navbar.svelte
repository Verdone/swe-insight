<script>
	import { onMount } from 'svelte';

	let btn;
	let menu;

	onMount(() => {
		btn = document.querySelector('.mobile-menu-button');
		menu = document.querySelector('.mobile-menu');

		btn.addEventListener('click', () => {
			menu.classList.toggle('hidden');
		});
	});
</script>

<nav class="bg-gray-900 shadow-2xl z-10 sticky top-0">
	<div class="px-8 mx-auto">
		<div class="flex justify-between">
			<div class="flex space-x-4">
				<!-- logo -->
				<div>
					<a href={'/'} class="flex items-center py-5 px-2 text-gray-100">
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

						<span class="font-bold">SWE Insight</span>
					</a>
				</div>

				<!-- primary nav -->
				<div class="hidden md:flex items-center space-x-1">
					<a
						href={'/roadmap'}
						class="nav-link py-5 px-3 text-gray-100 hover:text-gray-300 tracking-tight font-medium"
						>Roadmap</a
					>
				</div>
			</div>

			<!-- secondary nav -->
			<div class="hidden md:flex items-center space-x-1">
				<a
					href={'/algorithms'}
					class="nav-link py-5 px-3 text-gray-100 hover:text-gray-300 tracking-tight font-medium"
					>Algorithms</a
				>
				<a
					href={'/data-structures'}
					class="nav-link py-5 px-3 text-gray-100 hover:text-gray-300 tracking-tight font-medium"
					>Data Structures</a
				>
			</div>

			<!-- mobile hamburger menu button -->
			<div class="md:hidden flex items-center">
				<button class="mobile-menu-button">
					<svg
						class="w-6 h-6 text-gray-100 hover:text-gray-300 transition duration-300"
						xmlns="http://www.w3.org/2000/svg"
						fill="none"
						viewBox="0 0 24 24"
						stroke="currentColor"
					>
						<!-- Menu open: "hidden", Menu closed: "block" -->
						<path
							class="inline-flex"
							stroke-linecap="round"
							stroke-linejoin="round"
							stroke-width="2"
							d="M4 6h16M4 12h16M4 18h16"
						></path>
						<!-- Menu open: "block", Menu closed: "hidden" -->
						<path class="hidden" d="M6 18L18 6M6 6l12 12"></path>
					</svg>
				</button>
			</div>
		</div>

		<!-- mobile menu -->
		<div class="mobile-menu hidden md:hidden">
			<a href={'/roadmap'} class="nav-link block py-2 px-4 text-sm hover:bg-gray-950">Roadmap</a>
			<a href={'/algorithms'} class="nav-link block py-2 px-4 text-sm hover:bg-gray-950"
				>Algorithms</a
			>
			<a href={'/data-structures'} class="nav-link block py-2 px-4 text-sm hover:bg-gray-950"
				>Data Structures</a
			>
		</div>
	</div>
</nav>

<style>
	/* Style for the line under the nav items */
	.nav-link {
		position: relative;
	}

	.nav-link::before {
		content: '';
		position: absolute;
		bottom: -2px; /* Adjust the thickness of the line */
		left: 50%; /* Start at the center */
		width: 0%;
		height: 2px; /* Adjust the thickness of the line */
		background-color: #fff;
		transition:
			width 0.3s ease-out,
			left 0.3s ease-out; /* Transition properties */
	}

	.nav-link:hover::before {
		width: 100%; /* Expand to the edges */
		left: 0; /* Start from the left */
	}
</style>
