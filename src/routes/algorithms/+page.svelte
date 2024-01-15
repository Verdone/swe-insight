<script>
	import { websiteName } from '$lib/stores.js';

	let selectedDropdown = null;

	function toggleDropdown(dropdown) {
		if (selectedDropdown === dropdown) {
			selectedDropdown = null;
		} else {
			selectedDropdown = dropdown;
		}
	}
</script>

<svelte:head>
	<title>Algorithms - {websiteName}</title>
</svelte:head>

<section class="bg-gray-800 flex flex-col items-center justify-center py-20 my-10">
	<h1 class="text-5xl text-white font-bold mb-8">Algorithms</h1>
	<p class="text-gray-200 text-lg">
		An algorithm is a finite procedure used for solving a problem or performing a computation.
	</p>
</section>

<section class="pt-10 pb-10 lg:pt-[120px] lg:pb-20 bg-gray-900" id="algorithm-analysis">
	<div class="container mx-auto">
		<div class="sm:text-lg text-gray-400">
			<h2 class="mb-10 text-4xl tracking-tight font-bold text-white">
				Algorithm Analysis - What's "Big O" Notation?
			</h2>
			<p class="mb-4 font-medium">
				Algorithm analysis is an important part of a broader computational complexity theory, which
				provides theoretical estimates for the resources needed by any algorithm which solves a
				given computational problem. These estimates provide an insight into reasonable directions
				of search for efficient algorithms. Maybe you've heard of "Big O" notation before; it's a
				way of describing how the runtime of an algorithm scales with the size of the input in the
				worst case (more on that below).
			</p>
			<p class="mb-10 font-bold">
				This entire section will eventually be its own page, but for now, it will be a part of the
				Algorithms section. In the meantime, a brief overview is provided on algorithm analysis.
			</p>

			<h3 class="mb-10 text-2xl tracking-tight font-bold text-white">
				Time &#38; Space Complexity - Why Growth Rate Matters
			</h3>
			<p class="mb-4 font-medium">
				Time complexity quantifies the runtime of an algorithm by counting elementary operations,
				each taking a fixed time. This measure ensures that the time taken and the number of
				operations differ by at most a constant factor. On the other hand, space complexity gauges
				the working storage an algorithm requires, measured by the number of memory locations used
				to store data, rather than the actual space utilized in those locations.
			</p>
			<p class="mb-10 font-medium">
				Growth rate matters because it determines how well an algorithm scales with the size of the
				input. For example, if an algorithm has a time complexity of O(n<sup>2</sup>), then the
				runtime of the algorithm will increase quadratically as the size of the input increases.
			</p>

			<div class="container mx-auto mb-10">
				<!-- svelte-ignore a11y-no-static-element-interactions -->
				<div class="sm:text-lg text-gray-400">
					<!-- Dropdown for Big O Notation -->
					<!-- svelte-ignore a11y-click-events-have-key-events -->
					<div
						class={`dropdown-header mb-2 text-white ${selectedDropdown === 'bigO' && 'active'}`}
						on:click={() => toggleDropdown('bigO')}
					>
						<span class={`chevron ${selectedDropdown === 'bigO' && 'down'}`}>▼</span>
						<h3 class="mb-10 text-2xl tracking-tight font-bold">Big O Notation</h3>
					</div>
					<div class={`dropdown-content ${selectedDropdown === 'bigO' && 'active'}`}>
						<p class="mb-10 font-medium">
							Big O notation is a mathematical notation that characterizes functions according to
							their worst-case growth rates. Let f(n) and g(n) be two functions defined on some
							subset of the real numbers. One writes f(n) = O(g(n)) if and only if there exist
							positive constants n0 and c such that f(n) ≤ cg(n) for all n ≥ n0.
						</p>
					</div>

					<!-- Dropdown for Big Omega (Ω) Notation -->
					<!-- svelte-ignore a11y-click-events-have-key-events -->
					<div
						class={`dropdown-header mb-2 text-white ${selectedDropdown === 'bigOmega' && 'active'}`}
						on:click={() => toggleDropdown('bigOmega')}
					>
						<span class={`chevron ${selectedDropdown === 'bigOmega' && 'down'}`}>▼</span>
						<h3 class="mb-10 text-2xl tracking-tight font-bold">Big Omega (Ω) Notation</h3>
					</div>
					<div class={`dropdown-content ${selectedDropdown === 'bigOmega' && 'active'}`}>
						<p class="mb-10 font-medium">
							Omega notation is a notation used for describing the best-case runtime of functions.
							It is used primarily for asymptotic lower bounds, that is, to describe the behavior of
							the function when the argument tends towards a particular value or infinity. Let f(n)
							and g(n) be two functions defined on some subset of the real numbers. One writes f(n)
							= Ω(g(n)) if and only if there exist positive constants n0 and c such that f(n) ≥
							cg(n) for all n ≥ n0.
						</p>
					</div>

					<!-- Dropdown for Big Theta (Θ) Notation -->
					<!-- svelte-ignore a11y-click-events-have-key-events -->
					<div
						class={`dropdown-header mb-2 text-white ${selectedDropdown === 'bigTheta' && 'active'}`}
						on:click={() => toggleDropdown('bigTheta')}
					>
						<span class={`chevron ${selectedDropdown === 'bigTheta' && 'down'}`}>▼</span>
						<h3 class="mb-10 text-2xl tracking-tight font-bold">Big Theta (Θ) Notation</h3>
					</div>
					<div class={`dropdown-content ${selectedDropdown === 'bigTheta' && 'active'}`}>
						<p class="mb-10 font-medium">
							Theta notation is a notation used for describing the average-case runtime of
							functions. It is used primarily for asymptotic tight bounds, that is, to describe the
							behavior of the function when the argument tends towards a particular value or
							infinity. Let f(n) and g(n) be two functions defined on some subset of the real
							numbers. One writes f(n) = Θ(g(n)) if and only if there exist positive constants n0,
							c1, and c2 such that c1g(n) ≤ f(n) ≤ c2g(n) for all n ≥ n0.
						</p>
					</div>
				</div>
			</div>

			<h3 class="mb-10 text-2xl tracking-tight font-bold text-white">Nine Important Functions</h3>

			<p class="mb-10 font-medium">
				There are nine functions that are commonly used in algorithm analysis. They are listed
				below:
			</p>

			<div class="grid grid-cols-3 gap-4">
				<ul class="mb-10 font-medium col-span-1">
					<li class="mb-2">
						<span class="text-primary-600 font-bold">Constant</span> - O(1)
					</li>
					<li class="mb-2">
						<span class="text-primary-600 font-bold">Linearithmic</span> - O(n log n)
					</li>
					<li class="mb-2">
						<span class="text-primary-600 font-bold">Exponential</span> - O(2<sup>n</sup>)
					</li>
				</ul>

				<ul class="mb-10 font-medium col-span-1">
					<li class="mb-2">
						<span class="text-primary-600 font-bold">Logarithmic</span> - O(log n)
					</li>
					<li class="mb-2">
						<span class="text-primary-600 font-bold">Quadratic</span> - O(n<sup>2</sup>)
					</li>
					<li class="mb-2">
						<span class="text-primary-600 font-bold">Factorial</span> - O(n!)
					</li>
				</ul>

				<ul class="mb-10 font-medium col-span-1">
					<li class="mb-2">
						<span class="text-primary-600 font-bold">Linear</span> - O(n)
					</li>
					<li class="mb-2">
						<span class="text-primary-600 font-bold">Cubic</span> - O(n<sup>3</sup>)
					</li>
					<li class="mb-2">
						<span class="text-primary-600 font-bold">Polynomial</span> - O(n<sup>k</sup>)
					</li>
				</ul>
			</div>

			<p class="mb-10 font-medium">
				These functions are listed in order of increasing complexity. The constant function is the
				simplest function, and the polynomial function is the most complex function. The constant
				function is the fastest function, and the polynomial function is the slowest function.
			</p>

			<h3 class="mb-10 text-2xl tracking-tight font-bold text-white">Reduction of coefficients</h3>

			<p class="mb-10 font-medium">
				When analyzing the time complexity of an algorithm, the coefficients of the terms are
				ignored. For example, if an algorithm has a time complexity of 5n<sup>2</sup> + 3n + 2, then
				the time complexity is O(n<sup>2</sup>). The coefficients of the terms are ignored because
				they do not affect the growth rate of the function.
			</p>
		</div>
	</div>
</section>

<section class="pt-10 pb-10 lg:pt-[120px] lg:pb-20">
	<div class="container mx-auto">
		<div class="sm:text-lg text-gray-400" id="sorting-algorithms">
			<h2 class="mb-10 text-4xl tracking-tight font-bold text-white">Sorting Algorithms</h2>
			<p class="mb-4 font-medium">
				Sorting is the process of arranging elements in a specific order and it's a fundamental
				concept in computer science and is used in many applications. Some sorting algorithms are
				better on larger data sets and some are better with smaller datasets of only a few thousand
				elements. The time complexity of a sorting algorithm is a measure of how well it scales with
				the size of the data set. The space complexity of a sorting algorithm is a measure of how
				much auxiliary memory it uses.
			</p>
			<p class="mb-10 font-medium">
				Some sorting algorithms sort in place, meaning that they don't use any auxiliary memory.
				Other sorting algorithms are not in place, meaning that they use auxiliary memory. Sorting
				algorithms can also be stable or unstable. A stable sorting algorithm preserves the relative
				order of elements with equal keys. An unstable sorting algorithm does not preserve the
				relative order of elements with equal keys.
			</p>
		</div>

		<div class="flex flex-wrap mb-20">
			<div class="w-full px-4 md:w-1/4 xl:w-1/3">
				<div
					class="mb-10 overflow-hidden duration-300 bg-gray-900 rounded-lg shadow-1 hover:shadow-3 shadow-2xl"
				>
					<div class="p-8 text-center sm:p-9 md:p-7 xl:p-9">
						<h3
							class="tracking-tight text-gray-100 hover:text-primary mb-4 block text-xl font-semibold sm:text-[22px] md:text-xl lg:text-[22px] xl:text-xl 2xl:text-[22px]"
						>
							Bubble
						</h3>
						<div class="container flex-inline justify-center space-x-2">
							<a
								href="/algorithms/sorting/bubble-sort"
								class="inline-flex items-center justify-center px-5 py-2 mt-2 mx-auto border border-transparent text-base font-bold rounded-md text-white bg-primary-600 hover:bg-primary-700 shadow-2xl"
							>
								View
							</a>
							<button
								class="inline-flex items-center justify-center px-5 py-2 mt-2 mx-auto border border-transparent text-base font-bold rounded-md text-white bg-gray-700 hover:bg-gray-800 shadow-2xl"
								on:click={() => {
									alert('Coming soon!');
								}}
							>
								Quick View
							</button>
						</div>
					</div>
				</div>
			</div>

			<div class="w-full px-4 md:w-1/4 xl:w-1/3">
				<div
					class="mb-10 overflow-hidden duration-300 bg-gray-900 rounded-lg shadow-1 hover:shadow-3 shadow-2xl"
				>
					<div class="p-8 text-center sm:p-9 md:p-7 xl:p-9">
						<h3
							class="tracking-tight text-gray-100 hover:text-primary mb-4 block text-xl font-semibold sm:text-[22px] md:text-xl lg:text-[22px] xl:text-xl 2xl:text-[22px]"
						>
							Selection
						</h3>
						<div class="container flex-inline justify-center space-x-2">
							<a
								href="/algorithms/sorting/selection-sort"
								class="inline-flex items-center justify-center px-5 py-2 mt-2 mx-auto border border-transparent text-base font-bold rounded-md text-white bg-primary-600 hover:bg-primary-700 shadow-2xl"
							>
								View
							</a>
							<button
								class="inline-flex items-center justify-center px-5 py-2 mt-2 mx-auto border border-transparent text-base font-bold rounded-md text-white bg-gray-700 hover:bg-gray-800 shadow-2xl"
								on:click={() => {
									alert('Coming soon!');
								}}
							>
								Quick View
							</button>
						</div>
					</div>
				</div>
			</div>
		</div>

		<div class="sm:text-lg text-gray-400" id="pathfinding-algorithms">
			<h2 class="mb-10 text-4xl tracking-tight font-bold text-white">Pathfinding Algorithms</h2>
			<p class="mb-4 font-medium">
				The purpose of a pathfinding algorithm is to find the shortest path between two points. They
				are used in many applications such as GPS navigation, video games, and robotics. There are
				many different pathfinding algorithms, but the most common ones are Dijkstra's algorithm and
				A* star algorithm. Paths can be expressed as a sequence of nodes, edges, or both.
			</p>
			<p class="mb-10 font-medium">
				Pathfinding algorithms make use of search contours, which are the nodes that are currently
				being explored. Some algorithms only require the problem space to be represented as a graph
				and then coded, such as Dijkstra's algorithm. Other algorithms like A* Star require the
				problem space to be represented as a graph and then coded. For example, designing a good
				<a
					href="https://en.wikipedia.org/wiki/Heuristic_(computer_science)"
					class="text-primary-600 font-bold"
					target="_blank">heuristic</a
				>, a key part of A* star algorithm, takes time and effort.
			</p>
		</div>

		<div class="flex flex-wrap mb-10">
			<div class="w-full px-4 md:w-1/4 xl:w-1/3">
				<div
					class="mb-10 overflow-hidden duration-300 bg-gray-900 rounded-lg shadow-1 hover:shadow-3 shadow-2xl"
				>
					<div class="p-8 text-center sm:p-9 md:p-7 xl:p-9">
						<h3
							class="tracking-tight text-gray-100 hover:text-primary mb-4 block text-xl font-semibold sm:text-[22px] md:text-xl lg:text-[22px] xl:text-xl 2xl:text-[22px]"
						>
							A* Star
						</h3>
						<div class="container flex-inline justify-center space-x-2">
							<a
								href="/algorithms/pathfinding/a-star"
								class="inline-flex items-center justify-center px-5 py-2 mt-2 mx-auto border border-transparent text-base font-bold rounded-md text-white bg-primary-600 hover:bg-primary-700 shadow-2xl"
							>
								View
							</a>
							<button
								class="inline-flex items-center justify-center px-5 py-2 mt-2 mx-auto border border-transparent text-base font-bold rounded-md text-white bg-gray-700 hover:bg-gray-800 shadow-2xl"
								on:click={() => {
									alert('Coming soon!');
								}}
							>
								Quick View
							</button>
						</div>
					</div>
				</div>
			</div>

			<div class="w-full px-4 md:w-1/4 xl:w-1/3">
				<div
					class="mb-10 overflow-hidden duration-300 bg-gray-900 rounded-lg shadow-1 hover:shadow-3 shadow-2xl"
				>
					<div class="p-8 text-center sm:p-9 md:p-7 xl:p-9">
						<h3
							class="tracking-tight text-gray-100 hover:text-primary mb-4 block text-xl font-semibold sm:text-[22px] md:text-xl lg:text-[22px] xl:text-xl 2xl:text-[22px]"
						>
							Dijkstra's
						</h3>
						<div class="container flex-inline justify-center space-x-2">
							<a
								href="/algorithms/pathfinding/dijkstras"
								class="inline-flex items-center justify-center px-5 py-2 mt-2 mx-auto border border-transparent text-base font-bold rounded-md text-white bg-primary-600 hover:bg-primary-700 shadow-2xl"
							>
								View
							</a>
							<button
								class="inline-flex items-center justify-center px-5 py-2 mt-2 mx-auto border border-transparent text-base font-bold rounded-md text-white bg-gray-700 hover:bg-gray-800 shadow-2xl"
								on:click={() => {
									alert('Coming soon!');
								}}
							>
								Quick View
							</button>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</section>

<style>
	.dropdown-content {
		display: none;
	}

	.dropdown-content.active {
		display: block;
	}

	.dropdown-header {
		display: flex;
		align-items: center;
		cursor: pointer;
	}

	.chevron {
		transition: transform 0.3s ease-in-out;
		margin-top: -2.4rem;
		margin-right: 5px;
	}

	.chevron.down {
		transform: rotate(180deg);
	}
</style>
