<script>
	import { websiteName } from '$lib/stores';
	import { CodeBlock } from 'svhighlight';
	import { onMount, onDestroy } from 'svelte';

	// ======= Selection Sort Visualization =======

	let n = 20;
	let array = [];
	let audioCtx = null;
	let volume = 0.02;
	let volumeMuted = false;
	const delay = 45;
	let totalSwaps = 0;
	let totalComparisons = 0;
	let totalArrayAccesses = 0;
	let animationPaused = false;
	let movesQueue = [];

	onMount(() => {
		init(); // Initialize array with random values
	});

	onDestroy(() => {
		if (audioCtx !== null) {
			audioCtx.close();
		}
		if (movesQueue.length > 0) {
			movesQueue = [];
		} // Clear moves queue (reset animation)
	});

	function playSound(freq) {
		if (audioCtx == null) {
			audioCtx = new (AudioContext || webkitAudioContext)();
		}

		const duration = 0.1;
		const osc = audioCtx.createOscillator();
		osc.frequency.value = freq;
		osc.type = 'triangle';
		osc.start(0);
		osc.stop(audioCtx.currentTime + duration);
		const node = audioCtx.createGain();
		node.gain.value = volume;
		node.gain.exponentialRampToValueAtTime(0.00001, audioCtx.currentTime + duration);
		osc.connect(node);
		node.connect(audioCtx.destination);
	}

	function selectionSort(array) {
		const moves = [];

		for (let i = 0; i < array.length - 1; i++) {
			let minIndex = i;

			for (let j = i + 1; j < array.length; j++) {
				moves.push({
					indices: [i, j],
					type: 'compare'
				});

				if (array[j] < array[minIndex]) {
					minIndex = j;
				}
			}

			if (minIndex !== i) {
				moves.push({
					indices: [i, minIndex],
					type: 'swap'
				});
				[array[i], array[minIndex]] = [array[minIndex], array[i]];
			}
		}

		return moves;
	}

	function showBars(move) {
		const bars = document.querySelectorAll('.bar');
		bars.forEach((bar, index) => {
			if (move && move.indices.includes(index)) {
				bar.style.backgroundColor = move.type == 'swap' ? '#f08178' : '#b0c4de'; // light red, light blue (low contrast for epileptic users)
			} else {
				bar.style.backgroundColor = 'white';
			}
		});
	}

	function toggleAnimation() {
		const button = document.querySelector('#pauseBtn');
		if (animationPaused) {
			button.textContent = 'Pause ⏸️';
			animationPaused = false;
			continueAnimation();
		} else {
			button.textContent = 'Play ▶️';
			animationPaused = true;
		}
	}

	function play() {
		const playBtn = document.querySelector('#playBtn');
		playBtn.disabled = true;
		playBtn.style.display = 'none';
		const copy = [...array];
		movesQueue = selectionSort(copy); // Changed to selection sort
		continueAnimation();
		const pauseBtn = document.querySelector('#pauseBtn');
		pauseBtn.style.display = 'inline-block';
		pauseBtn.disabled = false;
		pauseBtn.textContent = 'Pause ⏸️';
		animationPaused = false;
	}
	function continueAnimation() {
		if (movesQueue.length > 0 && !animationPaused) {
			const move = movesQueue.shift();
			const [i, j] = move.indices;

			if (move.type === 'swap') {
				[array[i], array[j]] = [array[j], array[i]];
				totalSwaps++;
				totalArrayAccesses += 4;
			} else {
				totalComparisons++;
				totalArrayAccesses += 2;
			}

			if (!volumeMuted) {
				playSound(440 + array[i] * 10);
				playSound(440 + array[j] * 10);
			}

			showBars(move);

			setTimeout(() => {
				continueAnimation();
			}, delay);
		} else {
			showBars(undefined);
		}
	}

	function toggleVolume() {
		const volumeBtn = document.querySelector('#volumeBtn');

		if (volumeMuted) {
			volume = 0.02;
			volumeBtn.textContent = '🔊';
		} else {
			volume = 0;
			volumeBtn.textContent = '🔇';
		}

		volumeMuted = !volumeMuted;
	}

	function init() {
		for (let i = 0; i < n; i++) {
			array.push(Math.floor(Math.random() * 100));
		}
	}

	$: array;
	$: totalSwaps;
	$: totalComparisons;
	$: totalArrayAccesses;

	// ======= End of Selection Sort Visualization =======

	// ======= Code Highlights for Selection Sort =======

	let codeLang = 'Python';

	$: code = `
		${
			codeLang === 'Python'
				? `
def selection_sort(arr):
    for i in range(len(arr)): # Loop through array
        min_idx = i # Set min index to current index
        for j in range(i + 1, len(arr)): # Loop through unsorted part of array
            if arr[min_idx] > arr[j]: # If current element is less than min element
                min_idx = j # Set min index to current index
        arr[i], arr[min_idx] = arr[min_idx], arr[i] # Swap min element with first element of unsorted array

    return arr
                `
				: ''
		}
        ${
					codeLang === 'C++'
						? `
int[] selection_sort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) { // Loop through array
        int min_idx = i; // Set min index to current index
        for (int j = i + 1; j < n; j++) { // Loop through unsorted part of array
            if (arr[j] < arr[min_idx]) { // If current element is less than min element
                min_idx = j; // Set min index to current index
            }
        }
        swap(arr[min_idx], arr[i]); // Swap min element with first element of unsorted array
    }
    return arr;
}
                `
						: ''
				}
        
        ${
					codeLang === 'Java'
						? `
int[] selectionSort(int arr[]) {
    int n = arr.length; // Get length of array
    for (int i = 0; i < n - 1; i++) { // Loop through array
        int min_idx = i; // Set min index to current index
        for (int j = i + 1; j < n; j++) { // Loop through unsorted part of array
            if (arr[j] < arr[min_idx]) { // If current element is less than min element
                min_idx = j; // Set min index to current index
            }
        }
        int temp = arr[min_idx];
        arr[min_idx] = arr[i]; // Swap min element with first element of unsorted array
        arr[i] = temp;  // Swap min element with first element of unsorted array
    }
    return arr;
}
                `
						: ''
				}

        ${
					codeLang === 'Go'
						? `
func selectionSort(arr []int) []int{
    for i := 0; i < len(arr) - 1; i++ { // Loop through array
        min_idx := i // Set min index to current index
        for j := i + 1; j < len(arr); j++ { // Loop through unsorted part of array
            if arr[j] < arr[min_idx] { // If current element is less than min element
                min_idx = j // Set min index to current index
            }
        }
        arr[i], arr[min_idx] = arr[min_idx], arr[i] // Swap min element with first element of unsorted array
    }
    return arr
}
                `
						: ''
				}
    `;
</script>

<svelte:head>
	<title>Selection Sort - {websiteName}</title>
</svelte:head>

<div class="container mx-auto mb-20">
	<!-- Title -->
	<div class="flex justify-center items-center px-20">
		<h1 class="text-6xl font-bold white">Selection Sort</h1>
	</div>
</div>

<div class="container mx-auto">
	<div class="md:flex md:justify-center md:space-x-4">
		<!-- Section for Algorithm Properties -->
		<div
			class="mx-4 p-4 h-64 border border-gray-500 rounded-lg shadow-xl mb-4 md:mb-0 md:mx-0 sm:mb-4 overflow-hidden"
			style="background-color: #141414;"
		>
			<p class="text-base font-semibold text-gray-100 text-center">Performance</p>
			<div class="flex-col justify-between mt-2">
				<div class="mb-1">
					<div class="inline-flex items-center">
						<p class="text-base text-gray-200">Time Complexity:</p>
					</div>
					<p class="text-xl font-bold" style="color: #ff8989;">O(n&#178;)</p>
				</div>
				<div class="mb-1">
					<div class="inline-flex items-center">
						<p class="text-base text-gray-200">Space Complexity:</p>
					</div>
					<p class="text-xl font-bold" style="color: #57ce00;">O(1)</p>
				</div>
				<div class="mb-1">
					<div class="inline-flex items-center">
						<p class="text-base text-gray-200">Stable Sorting?</p>
					</div>
					<p class="text-xl font-bold text-blue-600">❌ No</p>
				</div>
				<div class="mb-1">
					<p class="text-xs text-gray-200 mt-2">
						What's "<a
							href={'/algorithms#algorithm-analysis'}
							class="text-blue-400 hover:text-blue-300">Big-O</a
						>" notation?
					</p>
				</div>
			</div>
		</div>

		<!-- Section for Animation -->
		<div
			class="w-96 h-64 border border-gray-500 rounded-lg shadow-xl overflow-hidden relative mb-4 md:mb-0 md:mr-4 sm:mb-4"
			style="background-color: #141414;"
		>
			<!-- Circular button for volume toggle -->
			<button
				id="volumeBtn"
				on:click={toggleVolume}
				class="z-10 absolute top-4 left-4 w-12 h-12 bg-blue-500 hover:bg-blue-400 text-white font-bold py-2 px-3 rounded-full"
				style="display: inline-block;"
			>
				🔊
			</button>

			<div class="array flex justify-center items-end h-full">
				{#each array as item}
					<div class="bar h-full" style="height: {item * 2}px;"></div>
				{/each}
			</div>
			<div class="absolute top-0 left-0 w-full h-full flex items-center justify-center">
				{#if array.length === 0}
					<p class="text-gray-200 z-10">Press the 'Play Animation' button.</p>
				{/if}
			</div>
		</div>

		<!-- Section for Real-time sorting statistics -->
		<div
			class="mx-4 p-4 h-64 border border-gray-500 rounded-lg shadow-xl mb-4 md:mb-0 md:mr-4 sm:mb-4 overflow-hidden"
			style="background-color: #141414;"
		>
			<p class="text-base font-semibold text-gray-100 text-center">Sorting Statistics</p>
			<div class="flex-col justify-between mt-2">
				<div class="mb-1">
					<div class="inline-flex items-center">
						<span class="w-2 h-2 inline-block rounded-full me-2" style="background-color: #f08178;"
						></span>
						<p class="text-base text-gray-200">Swaps:</p>
					</div>
					<p class="text-xl font-bold text-blue-600">{totalSwaps}</p>
				</div>
				<div class="mb-1">
					<div class="inline-flex items-center">
						<span class="w-2 h-2 inline-block rounded-full me-2" style="background-color: #b0c4de;"
						></span>
						<p class="text-base text-gray-200">Comparisons:</p>
					</div>
					<p class="text-xl font-bold text-blue-600">{totalComparisons}</p>
				</div>
				<div class="mb-1">
					<div class="inline-flex items-center -ml-1">
						<span class="inline-block text-xs mr-1">🔍</span>
						<p class="text-base text-gray-200">Array Accesses:</p>
					</div>
					<p class="text-xl font-bold text-blue-600">{totalArrayAccesses}</p>
				</div>
				<div class="mb-1">
					<p class="text-xs text-gray-200 mt-2">Delay: {delay} ms | Size: {n}</p>
				</div>
			</div>
		</div>
	</div>
</div>

<div class="container py-8 items-center justify-center mx-auto">
	<button
		on:click={toggleAnimation}
		id="pauseBtn"
		disabled
		style="display: none;"
		class="w-48 bg-blue-500 hover:bg-blue-400 text-white font-bold py-2 px-4 border-b-4 border-blue-700 hover:border-blue-500 rounded"
		>Pause ⏸️</button
	>
	<button
		on:click={play}
		id="playBtn"
		class="w-50 bg-blue-500 hover:bg-blue-400 text-white font-bold py-2 px-4 border-b-4 border-blue-700 hover:border-blue-500 rounded"
		>🎬 Play Animation 📊</button
	>

	<div class="py-8">
		<p class="text-xs text-white mt-2 text-center">
			⚠️ <span class="font-bold">Note:</span> this animated visualization is a work-in-progress. If you
			are encountering errors or want to replay the animation, please refresh the page.
		</p>
		<p class="text-xs text-white mt-2 text-center">
			If you would like to report a bug or suggest an improvement, please create an issue on
			<a
				href={'https://github.com/Verdone/swe-insight/issues'}
				target="_blank"
				class="text-blue-500 hover:text-blue-300">GitHub</a
			>.
		</p>
	</div>
</div>

<!-- Section 1: Explanation of the Algorithm -->
<section class="bg-gray-900">
	<div class="py-8 px-4 mx-auto max-w-screen-xl lg:py-16 lg:px-6">
		<div class="max-w-screen-lg sm:text-lg text-gray-400">
			<h2 class="mb-10 text-4xl tracking-tight font-bold text-white">
				Understanding Selection Sort
			</h2>
			<p class="mb-4 font-light">
				Selection Sort is a simple sorting algorithm that works by repeatedly finding the minimum
				element from the unsorted part of the array and placing it at the beginning of the array.
				The algorithm maintains two subarrays in a given array:
			</p>
			<ul class="list-disc pl-6 mb-4">
				<li>The subarray which is already sorted.</li>
				<li>Remaining subarray which is unsorted.</li>
			</ul>

			<p class="mb-4 font-medium">During the sorting process there are the following operations:</p>

			<ul class="list-disc pl-6 mb-4">
				<li>Find the minimum element in the unsorted subarray.</li>
				<li>Swap the found minimum element with the first element of the unsorted subarray.</li>
			</ul>
		</div>
	</div>
</section>

<!-- Section 2: Complexity Analysis -->
<section class="bg-gray-800">
	<div class="py-8 px-4 mx-auto max-w-screen-xl lg:py-16 lg:px-6">
		<div class="max-w-screen-lg sm:text-lg text-gray-400">
			<h2 class="mb-10 text-4xl tracking-tight font-bold text-white">Complexity Analysis</h2>
			<p class="mb-4 font-medium">Selection Sort has the following complexities:</p>

			<div class="relative overflow-x-auto mb-4">
				<table class="w-full text-sm text-left rtl:text-right text-gray-400">
					<thead class="text-xs uppercase bg-gray-900 text-gray-400">
						<tr>
							<th scope="col" class="px-6 py-3"> Case </th>
							<th scope="col" class="px-6 py-3"> Time Complexity </th>
							<th scope="col" class="px-6 py-3"> Space Complexity </th>
						</tr>
					</thead>
					<tbody>
						<tr class="border-b bg-gray-950 border-gray-700">
							<th scope="row" class="px-6 py-4 font-medium whitespace-nowrap text-white">
								Best Case
							</th>
							<td class="px-6 py-4 text-gray-200"> Ω(n&sup2;) </td>
							<td class="px-6 py-4 text-gray-200"> Ω(1) </td>
						</tr>
						<tr class="bg-gray-950 border-gray-700">
							<th scope="row" class="px-6 py-4 font-medium whitespace-nowrap text-white">
								Average Case
							</th>
							<td class="px-6 py-4 text-gray-200"> Θ(n&sup2;) </td>
							<td class="px-6 py-4 text-gray-200"> Θ(1) </td>
						</tr>
						<tr class="bg-gray-950">
							<th scope="row" class="px-6 py-4 font-medium whitespace-nowrap text-white">
								Worst Case
							</th>
							<td class="px-6 py-4 text-gray-200"> O(n&sup2;) </td>
							<td class="px-6 py-4 text-gray-200"> O(1) </td>
						</tr>
					</tbody>
				</table>
			</div>

			<p class="mb-4 font-medium">
				It has a quadratic time complexity, meaning that the number of steps required to sort the
				array grows quadratically as the size of the array increases. This is because the algorithm
				has to perform a linear scan of the array for each element in the array. It also has a
				linear space complexity.
			</p>
		</div>
	</div>
</section>

<!-- Section 3: Implementation / Code Snippets -->
<section class="bg-gray-900">
	<div class="py-8 px-4 mx-auto max-w-screen-xl lg:py-16 lg:px-6">
		<div class="max-w-screen-lg sm:text-lg text-gray-400">
			<h2 class="mb-10 text-4xl tracking-tight font-bold text-white">Code Implementation</h2>
			<p class="mb-4 font-medium">
				Selection Sort can be implemented in a variety of languages. Below are some examples of
				implementations in Python, C++, Go, and Java.
			</p>

			<!-- Code block language selection buttons -->
			<div class="flex justify-center items-center space-x-4 mb-4">
				<button
					on:click={() => (codeLang = 'Python')}
					class="w-24 bg-blue-500 hover:bg-blue-400 text-white font-bold py-2 px-4 border-b-4 border-blue-700 hover:border-blue-500 rounded"
				>
					Python
				</button>
				<button
					on:click={() => (codeLang = 'C++')}
					class="w-24 bg-blue-500 hover:bg-blue-400 text-white font-bold py-2 px-4 border-b-4 border-blue-700 hover:border-blue-500 rounded"
				>
					C++
				</button>
				<button
					on:click={() => (codeLang = 'Java')}
					class="w-24 bg-blue-500 hover:bg-blue-400 text-white font-bold py-2 px-4 border-b-4 border-blue-700 hover:border-blue-500 rounded"
				>
					Java
				</button>
				<button
					on:click={() => (codeLang = 'Go')}
					class="w-24 bg-blue-500 hover:bg-blue-400 text-white font-bold py-2 px-4 border-b-4 border-blue-700 hover:border-blue-500 rounded"
				>
					GoLang
				</button>
			</div>

			<div class="shadow-2xl mb-10">
				{#key codeLang}
					<CodeBlock language={codeLang} {code} />
				{/key}
			</div>

			<p class="text-xs text-gray-200 mt-2">
				Note: these implementations are for educational purposes only, such as preparing for a
				technical interview or for learning about sorting algorithms. For production code, please
				use the built-in sorting functions in your programming language's standard library.
			</p>
		</div>
	</div>
</section>

<!-- Section 4: When to Use and When Not to Use -->
<section class="bg-gray-800">
	<div class="py-8 px-4 mx-auto max-w-screen-xl lg:py-16 lg:px-6">
		<div class="max-w-screen-lg sm:text-lg text-gray-400">
			<h2 class="mb-10 text-4xl tracking-tight font-bold text-white">
				When should Selection Sort be used?
			</h2>
			<p class="mb-4 font-light">
				Selection Sort is a simple sorting algorithm that works well for small data sets or when you
				are not concerned about performance. It is also a good choice when memory space is limited,
				as it is an in-place sorting algorithm.
			</p>
			<p class="font-light">
				In the real world, Selection Sort is rarely used because it is very inefficient for large
				data sets. It is also not a stable sorting algorithm, meaning that the relative order of
				equal sort items is not preserved.
			</p>
		</div>
	</div>
</section>

<style>
	.container {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}

	.array {
		display: flex;
		justify-content: center;
		align-items: flex-end;
	}

	.bar {
		width: 5px;
		margin: 0 0.5px;
		background-color: white;
	}
</style>
