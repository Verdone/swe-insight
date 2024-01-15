<script>
	import { websiteName } from '$lib/stores';
</script>

<svelte:head>
	<title>Data Structures - {websiteName}</title>
</svelte:head>

<section class="bg-gray-800 flex flex-col items-center justify-center py-20 my-10">
	<h1 class="text-5xl text-white font-bold mb-8">Data Structures</h1>
	<p class="text-gray-200 text-lg">
		A data structure is a way of organizing data so that it can be used effectively.
	</p>
</section>

<section class="pt-10 pb-10 lg:pt-[120px] lg:pb-20">
	<div class="container mx-auto">
		<div class="sm:text-lg text-gray-400" id="sorting-algorithms">
			<h2 class="mb-10 text-4xl tracking-tight font-bold text-white">Linear Data Structures</h2>
			<p class="mb-4 font-medium">
				Linear data structures are data structures that store data in a linear fashion. They are
				used to store data in a way that is easy to access and manipulate. There are many different
				types of linear data structures, such as arrays, linked lists, stacks, queues, and trees.
			</p>
			<p class="mb-10 font-medium">
				Each type of linear data structure has its own advantages and disadvantages. For example,
				arrays are good for storing data that is accessed sequentially, but they are not good for
				storing data that is accessed randomly. Linked lists are good for storing data that is
				accessed randomly, but they are not good for storing data that is accessed sequentially.
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
							Stack
						</h3>
						<div class="container flex-inline justify-center space-x-2">
							<a
								href="/data-structures/linear/stack"
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
							Queue
						</h3>
						<div class="container flex-inline justify-center space-x-2">
							<a
								href="/data-structures/linear/queue"
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
