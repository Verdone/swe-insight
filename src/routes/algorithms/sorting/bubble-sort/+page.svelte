<script>
	import { onMount, onDestroy } from 'svelte';

	let n = 50;
	let array = [];
	let audioCtx = null;
	const delay = 45;
	let totalSwaps = 0;
	let totalComparisons = 0;
	let totalArrayAccesses = 0;
	let animationPaused = false;
	let movesQueue = [];

	onMount(() => {
		init();
	});

	onDestroy(() => {
		if (audioCtx !== null) {
			audioCtx.close();
		}
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
		node.gain.value = 0.02;
		node.gain.exponentialRampToValueAtTime(0.00001, audioCtx.currentTime + duration);
		osc.connect(node);
		node.connect(audioCtx.destination);
	}

	function bubbleSort(array) {
		const moves = [];
		let swapped;
		do {
			swapped = false;
			for (let j = 1; j < array.length; j++) {
				moves.push({
					indices: [j - 1, j],
					type: 'compare'
				});
				if (array[j - 1] > array[j]) {
					moves.push({
						indices: [j - 1, j],
						type: 'swap'
					});
					[array[j - 1], array[j]] = [array[j], array[j - 1]];
					swapped = true;
				}
			}
		} while (swapped);
		return moves;
	}

	function showBars(move) {
		const bars = document.querySelectorAll('.bar');
		bars.forEach((bar, index) => {
			if (move && move.indices.includes(index)) {
				bar.style.backgroundColor = move.type == 'swap' ? '#f08178' : '#b0c4de'; // light red, light blue
			} else {
				bar.style.backgroundColor = 'white';
			}
		});
	}

	function toggleAnimation() {
		const button = document.querySelector('#pauseBtn');
		if (animationPaused) {
			button.textContent = 'Pause';
			animationPaused = false;
			continueAnimation();
		} else {
			button.textContent = 'Resume';
			animationPaused = true;
		}
	}

	function play() {
		const playBtn = document.querySelector('#playBtn');
		playBtn.disabled = true;
		playBtn.style.display = 'none';
		const copy = [...array];
		movesQueue = bubbleSort(copy);
		continueAnimation();
		const pauseBtn = document.querySelector('#pauseBtn');
		pauseBtn.style.display = 'inline-block';
		pauseBtn.disabled = false;
		pauseBtn.textContent = 'Pause';
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

			playSound(440 + array[i] * 10);
			playSound(440 + array[j] * 10);

			showBars(move);

			setTimeout(() => {
				continueAnimation();
			}, delay);
		} else {
			showBars(undefined);
		}
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
</script>

<div class="container flex flex-col items-center justify-center">
	<div class="flex md:flex-row sm:flex-col">
		<div
			class="w-96 h-64 border border-gray-500 rounded-lg overflow-hidden relative mb-4 md:mb-0 md:mr-4 sm:mb-4"
			style="background-color: #141414;"
		>
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

		<div class="mx-4 p-4 h-64 bg-gray-100 rounded-lg shadow-xl mb-4 md:mb-0 md:mr-4 sm:mb-4">
			<p class="text-lg font-semibold text-gray-800">Sorting Statistics</p>
			<div class="flex flex-col justify-between mt-2">
				<div>
					<div class="inline-flex items-center">
						<span class="w-2 h-2 inline-block rounded-full me-2" style="background-color: #f08178;"
						></span>
						<p class="text-base text-gray-700">Swaps:</p>
					</div>
					<p class="text-xl font-bold text-blue-600">{totalSwaps}</p>
				</div>
				<div>
					<div class="inline-flex items-center">
						<span class="w-2 h-2 inline-block rounded-full me-2" style="background-color: #b0c4de;"
						></span>
						<p class="text-base text-gray-700">Comparisons:</p>
					</div>
					<p class="text-xl font-bold text-blue-600">{totalComparisons}</p>
				</div>
				<div>
					<div class="inline-flex items-center -ml-1">
						<span class="inline-block text-xs mr-1">🔍</span>
						<p class="text-base text-gray-700">Array Accesses:</p>
					</div>
					<p class="text-xl font-bold text-blue-600">{totalArrayAccesses}</p>
				</div>
				<div>
					<p class="text-sm text-gray-700 mt-2">Animation Delay: {delay} ms</p>
				</div>
			</div>
		</div>
	</div>

	<div class="py-8">
		<button
			on:click={toggleAnimation}
			id="pauseBtn"
			disabled
			style="display: none;"
			class="w-48 bg-blue-500 hover:bg-blue-400 text-white font-bold py-2 px-4 border-b-4 border-blue-700 hover:border-blue-500 rounded"
			>Pause</button
		>
		<button
			on:click={play}
			id="playBtn"
			class="w-48 bg-blue-500 hover:bg-blue-400 text-white font-bold py-2 px-4 border-b-4 border-blue-700 hover:border-blue-500 rounded"
			>Play animation</button
		>
	</div>

	<div class="py-2">
		<p class="text-xs text-white mt-2 text-center">
			⚠️ Note: this animated visualization is a work-in-progress. If you are encountering any
			bugs/errors or simply wish to replay the animation, please refresh the page.
		</p>
	</div>
</div>

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
