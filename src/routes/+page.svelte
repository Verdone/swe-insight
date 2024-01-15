<script>
	import { websiteName } from '$lib/stores';

	let activeAccordion = null;

	function toggleAccordion(id) {
		if (activeAccordion === id) {
			activeAccordion = null;
		} else {
			activeAccordion = id;
		}
	}

	$: isAccordionExpanded = activeAccordion === 'accordion-collapse-body';
	$: chevronRotation = isAccordionExpanded ? 'rotate-180' : '';
</script>

<svelte:head>
	<title>Home - {websiteName}</title>
</svelte:head>

<div class="min-h-screen flex flex-col">
	<div class="flex flex-col">
		<!-- Section 1 (Hero) -->
		<section class="bg-gray-800">
			<div
				class="gap-16 items-center py-8 px-4 mx-auto max-w-screen-xl lg:grid lg:grid-cols-2 lg:py-16 lg:px-6 mb-10"
			>
				<div class="font-light sm:text-lg text-gray-300">
					<h2 class="mb-4 text-6xl tracking-tight font-extrabold text-white animate-pulse">
						Elevate Your SWE Journey.
					</h2>
					<p class="mb-4">
						SWE (Software Engineer) Insight guides you from the fundamentals to advanced concepts in
						your software engineering journey.
					</p>
					<p class="mb-4">
						Access resources for all levels in software engineering. Whether you're refining skills
						or aiming for advancement, SWE Insight simplifies coding and software concepts for a
						successful learning journey.
					</p>

					<div class="flex items-center mt-6">
						<svg
							class="w-3 h-3 text-yellow-300 ms-1"
							aria-hidden="true"
							xmlns="http://www.w3.org/2000/svg"
							fill="currentColor"
							viewBox="0 0 22 20"
						>
							<path
								d="M20.924 7.625a1.523 1.523 0 0 0-1.238-1.044l-5.051-.734-2.259-4.577a1.534 1.534 0 0 0-2.752 0L7.365 5.847l-5.051.734A1.535 1.535 0 0 0 1.463 9.2l3.656 3.563-.863 5.031a1.532 1.532 0 0 0 2.226 1.616L11 17.033l4.518 2.375a1.534 1.534 0 0 0 2.226-1.617l-.863-5.03L20.537 9.2a1.523 1.523 0 0 0 .387-1.575Z"
							/>
						</svg>
						<svg
							class="w-3 h-3 text-yellow-300 ms-1"
							aria-hidden="true"
							xmlns="http://www.w3.org/2000/svg"
							fill="currentColor"
							viewBox="0 0 22 20"
						>
							<path
								d="M20.924 7.625a1.523 1.523 0 0 0-1.238-1.044l-5.051-.734-2.259-4.577a1.534 1.534 0 0 0-2.752 0L7.365 5.847l-5.051.734A1.535 1.535 0 0 0 1.463 9.2l3.656 3.563-.863 5.031a1.532 1.532 0 0 0 2.226 1.616L11 17.033l4.518 2.375a1.534 1.534 0 0 0 2.226-1.617l-.863-5.03L20.537 9.2a1.523 1.523 0 0 0 .387-1.575Z"
							/>
						</svg>
						<svg
							class="w-3 h-3 text-yellow-300 ms-1"
							aria-hidden="true"
							xmlns="http://www.w3.org/2000/svg"
							fill="currentColor"
							viewBox="0 0 22 20"
						>
							<path
								d="M20.924 7.625a1.523 1.523 0 0 0-1.238-1.044l-5.051-.734-2.259-4.577a1.534 1.534 0 0 0-2.752 0L7.365 5.847l-5.051.734A1.535 1.535 0 0 0 1.463 9.2l3.656 3.563-.863 5.031a1.532 1.532 0 0 0 2.226 1.616L11 17.033l4.518 2.375a1.534 1.534 0 0 0 2.226-1.617l-.863-5.03L20.537 9.2a1.523 1.523 0 0 0 .387-1.575Z"
							/>
						</svg>
						<svg
							class="w-3 h-3 text-yellow-300 ms-1"
							aria-hidden="true"
							xmlns="http://www.w3.org/2000/svg"
							fill="currentColor"
							viewBox="0 0 22 20"
						>
							<path
								d="M20.924 7.625a1.523 1.523 0 0 0-1.238-1.044l-5.051-.734-2.259-4.577a1.534 1.534 0 0 0-2.752 0L7.365 5.847l-5.051.734A1.535 1.535 0 0 0 1.463 9.2l3.656 3.563-.863 5.031a1.532 1.532 0 0 0 2.226 1.616L11 17.033l4.518 2.375a1.534 1.534 0 0 0 2.226-1.617l-.863-5.03L20.537 9.2a1.523 1.523 0 0 0 .387-1.575Z"
							/>
						</svg>
						<svg
							class="w-3 h-3 text-yellow-300 ms-1"
							aria-hidden="true"
							xmlns="http://www.w3.org/2000/svg"
							fill="currentColor"
							viewBox="0 0 22 20"
						>
							<path
								d="M20.924 7.625a1.523 1.523 0 0 0-1.238-1.044l-5.051-.734-2.259-4.577a1.534 1.534 0 0 0-2.752 0L7.365 5.847l-5.051.734A1.535 1.535 0 0 0 1.463 9.2l3.656 3.563-.863 5.031a1.532 1.532 0 0 0 2.226 1.616L11 17.033l4.518 2.375a1.534 1.534 0 0 0 2.226-1.617l-.863-5.03L20.537 9.2a1.523 1.523 0 0 0 .387-1.575Z"
							/>
						</svg>
						<p class="pl-5 text-sm sm:text-xs">
							<span>
								<span class="text-white">5</span>
								<span class="text-gray-400">/5</span>
							</span>
							<span class="ml-2 text-gray-300 italic"
								>"Wow.. this is nuts." ~ An A.I-Generated testimonial</span
							>
						</p>
					</div>
					<div class="flex items-center">
						<svg
							class="w-3 h-3 text-yellow-300 ms-1"
							aria-hidden="true"
							xmlns="http://www.w3.org/2000/svg"
							fill="currentColor"
							viewBox="0 0 22 20"
						>
							<path
								d="M20.924 7.625a1.523 1.523 0 0 0-1.238-1.044l-5.051-.734-2.259-4.577a1.534 1.534 0 0 0-2.752 0L7.365 5.847l-5.051.734A1.535 1.535 0 0 0 1.463 9.2l3.656 3.563-.863 5.031a1.532 1.532 0 0 0 2.226 1.616L11 17.033l4.518 2.375a1.534 1.534 0 0 0 2.226-1.617l-.863-5.03L20.537 9.2a1.523 1.523 0 0 0 .387-1.575Z"
							/>
						</svg>
						<svg
							class="w-3 h-3 text-yellow-300 ms-1"
							aria-hidden="true"
							xmlns="http://www.w3.org/2000/svg"
							fill="currentColor"
							viewBox="0 0 22 20"
						>
							<path
								d="M20.924 7.625a1.523 1.523 0 0 0-1.238-1.044l-5.051-.734-2.259-4.577a1.534 1.534 0 0 0-2.752 0L7.365 5.847l-5.051.734A1.535 1.535 0 0 0 1.463 9.2l3.656 3.563-.863 5.031a1.532 1.532 0 0 0 2.226 1.616L11 17.033l4.518 2.375a1.534 1.534 0 0 0 2.226-1.617l-.863-5.03L20.537 9.2a1.523 1.523 0 0 0 .387-1.575Z"
							/>
						</svg>
						<svg
							class="w-3 h-3 text-yellow-300 ms-1"
							aria-hidden="true"
							xmlns="http://www.w3.org/2000/svg"
							fill="currentColor"
							viewBox="0 0 22 20"
						>
							<path
								d="M20.924 7.625a1.523 1.523 0 0 0-1.238-1.044l-5.051-.734-2.259-4.577a1.534 1.534 0 0 0-2.752 0L7.365 5.847l-5.051.734A1.535 1.535 0 0 0 1.463 9.2l3.656 3.563-.863 5.031a1.532 1.532 0 0 0 2.226 1.616L11 17.033l4.518 2.375a1.534 1.534 0 0 0 2.226-1.617l-.863-5.03L20.537 9.2a1.523 1.523 0 0 0 .387-1.575Z"
							/>
						</svg>
						<svg
							class="w-3 h-3 text-yellow-300 ms-1"
							aria-hidden="true"
							xmlns="http://www.w3.org/2000/svg"
							fill="currentColor"
							viewBox="0 0 22 20"
						>
							<path
								d="M20.924 7.625a1.523 1.523 0 0 0-1.238-1.044l-5.051-.734-2.259-4.577a1.534 1.534 0 0 0-2.752 0L7.365 5.847l-5.051.734A1.535 1.535 0 0 0 1.463 9.2l3.656 3.563-.863 5.031a1.532 1.532 0 0 0 2.226 1.616L11 17.033l4.518 2.375a1.534 1.534 0 0 0 2.226-1.617l-.863-5.03L20.537 9.2a1.523 1.523 0 0 0 .387-1.575Z"
							/>
						</svg>
						<svg
							class="w-3 h-3 text-yellow-300 ms-1"
							aria-hidden="true"
							xmlns="http://www.w3.org/2000/svg"
							fill="currentColor"
							viewBox="0 0 22 20"
						>
							<path
								d="M20.924 7.625a1.523 1.523 0 0 0-1.238-1.044l-5.051-.734-2.259-4.577a1.534 1.534 0 0 0-2.752 0L7.365 5.847l-5.051.734A1.535 1.535 0 0 0 1.463 9.2l3.656 3.563-.863 5.031a1.532 1.532 0 0 0 2.226 1.616L11 17.033l4.518 2.375a1.534 1.534 0 0 0 2.226-1.617l-.863-5.03L20.537 9.2a1.523 1.523 0 0 0 .387-1.575Z"
							/>
						</svg>
						<p class="pl-5 text-sm sm:text-xs">
							<span>
								<span class="text-white">5</span>
								<span class="text-gray-400">/5</span>
							</span>
							<span class="ml-2 text-gray-300 italic">
								"YEAHHH!!!!!" ~ Another A.I-Generated testimonial
							</span>
						</p>
					</div>

					<div class="container">
						<a
							href="/algorithms"
							class="inline-flex items-center justify-center px-5 py-3 mt-8 border border-transparent text-base font-bold rounded-md text-white bg-primary-600 hover:bg-primary-700 shadow-2xl"
						>
							<svg
								xmlns="http://www.w3.org/2000/svg"
								fill="none"
								viewBox="0 0 24 24"
								stroke-width="1.5"
								stroke="currentColor"
								class="mr-2 w-6 h-6"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									d="M4.26 10.147a60.438 60.438 0 0 0-.491 6.347A48.62 48.62 0 0 1 12 20.904a48.62 48.62 0 0 1 8.232-4.41 60.46 60.46 0 0 0-.491-6.347m-15.482 0a50.636 50.636 0 0 0-2.658-.813A59.906 59.906 0 0 1 12 3.493a59.903 59.903 0 0 1 10.399 5.84c-.896.248-1.783.52-2.658.814m-15.482 0A50.717 50.717 0 0 1 12 13.489a50.702 50.702 0 0 1 7.74-3.342M6.75 15a.75.75 0 1 0 0-1.5.75.75 0 0 0 0 1.5Zm0 0v-3.675A55.378 55.378 0 0 1 12 8.443m-7.007 11.55A5.981 5.981 0 0 0 6.75 15.75v-1.5"
								/>
							</svg>
							Get started with Algorithms
						</a>
					</div>
				</div>
				<div class="grid grid-cols-2 gap-4 mt-8">
					<img
						class="w-full rounded-lg shadow-2xl"
						src="https://images.unsplash.com/photo-1631624215749-b10b3dd7bca7?w=400&auto=format&fit=crop&q=60&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxzZWFyY2h8MTB8fHNvZnR3YXJlJTIwZGV2ZWxvcG1lbnR8ZW58MHx8MHx8fDA%3D"
						alt="Unsplash software development content 1"
					/>
					<img
						class="mt-4 w-full lg:mt-10 rounded-lg shadow-2xl"
						src="https://images.unsplash.com/photo-1664574654700-75f1c1fad74e?q=80&w=987&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
						alt="Unsplash software development content 2"
					/>
				</div>
			</div>
		</section>
		<!-- End of Section 1 -->

		<!-- Section 2 (Software Domains) -->
		<section class="bg-gray-900 py-24 sm:py-32">
			<div class="mx-auto max-w-7xl px-6 lg:px-8">
				<div class="mx-auto max-w-2xl lg:text-center">
					<h2 class="text-base font-semibold leading-7 text-blue-400">Learn faster</h2>
					<p class="mt-2 text-3xl font-bold tracking-tight text-white sm:text-4xl">
						Master one of many concentrations
					</p>
					<p class="mt-6 text-lg leading-8 text-gray-400">
						Software engineering is a vast field; it's easy to get lost in the sea of information
						available online. You'll be able to learn faster and more efficiently by focusing on
						what matters most for your personal roadmap.
					</p>
				</div>
				<div class="mx-auto mt-16 max-w-2xl sm:mt-20 lg:mt-24 lg:max-w-4xl">
					<dl
						class="grid max-w-xl grid-cols-1 gap-x-8 gap-y-10 lg:max-w-none lg:grid-cols-2 lg:gap-y-16"
					>
						<div class="relative pl-16">
							<dt class="text-base font-semibold leading-7 text-gray-300">
								<div
									class="absolute left-0 top-0 flex h-10 w-10 items-center justify-center rounded-lg bg-blue-400 hover:animate-bounce"
								>
									<svg
										xmlns="http://www.w3.org/2000/svg"
										fill="none"
										viewBox="0 0 24 24"
										stroke-width="1.5"
										stroke="currentColor"
										class="w-6 h-6 text-black"
									>
										<path
											stroke-linecap="round"
											stroke-linejoin="round"
											d="M19.5 14.25v-2.625a3.375 3.375 0 0 0-3.375-3.375h-1.5A1.125 1.125 0 0 1 13.5 7.125v-1.5a3.375 3.375 0 0 0-3.375-3.375H8.25M9 16.5v.75m3-3v3M15 12v5.25m-4.5-15H5.625c-.621 0-1.125.504-1.125 1.125v17.25c0 .621.504 1.125 1.125 1.125h12.75c.621 0 1.125-.504 1.125-1.125V11.25a9 9 0 0 0-9-9Z"
										/>
									</svg>
								</div>
								Data Engineering
							</dt>
							<dd class="mt-2 text-base leading-7 text-gray-400">
								Big data has become a big deal. Learn how to build data pipelines and work with
								datasets of all sizes in programming languages tailored for data science.
							</dd>
						</div>
						<div class="relative pl-16">
							<dt class="text-base font-semibold leading-7 text-gray-300">
								<div
									class="absolute left-0 top-0 flex h-10 w-10 items-center justify-center rounded-lg bg-blue-400 hover:animate-bounce"
								>
									<svg
										xmlns="http://www.w3.org/2000/svg"
										fill="none"
										viewBox="0 0 24 24"
										stroke-width="1.5"
										stroke="currentColor"
										class="w-6 h-6 text-black"
									>
										<path
											stroke-linecap="round"
											stroke-linejoin="round"
											d="M14.25 6.087c0-.355.186-.676.401-.959.221-.29.349-.634.349-1.003 0-1.036-1.007-1.875-2.25-1.875s-2.25.84-2.25 1.875c0 .369.128.713.349 1.003.215.283.401.604.401.959v0a.64.64 0 0 1-.657.643 48.39 48.39 0 0 1-4.163-.3c.186 1.613.293 3.25.315 4.907a.656.656 0 0 1-.658.663v0c-.355 0-.676-.186-.959-.401a1.647 1.647 0 0 0-1.003-.349c-1.036 0-1.875 1.007-1.875 2.25s.84 2.25 1.875 2.25c.369 0 .713-.128 1.003-.349.283-.215.604-.401.959-.401v0c.31 0 .555.26.532.57a48.039 48.039 0 0 1-.642 5.056c1.518.19 3.058.309 4.616.354a.64.64 0 0 0 .657-.643v0c0-.355-.186-.676-.401-.959a1.647 1.647 0 0 1-.349-1.003c0-1.035 1.008-1.875 2.25-1.875 1.243 0 2.25.84 2.25 1.875 0 .369-.128.713-.349 1.003-.215.283-.4.604-.4.959v0c0 .333.277.599.61.58a48.1 48.1 0 0 0 5.427-.63 48.05 48.05 0 0 0 .582-4.717.532.532 0 0 0-.533-.57v0c-.355 0-.676.186-.959.401-.29.221-.634.349-1.003.349-1.035 0-1.875-1.007-1.875-2.25s.84-2.25 1.875-2.25c.37 0 .713.128 1.003.349.283.215.604.401.96.401v0a.656.656 0 0 0 .658-.663 48.422 48.422 0 0 0-.37-5.36c-1.886.342-3.81.574-5.766.689a.578.578 0 0 1-.61-.58v0Z"
										/>
									</svg>
								</div>
								Game Development
							</dt>
							<dd class="mt-2 text-base leading-7 text-gray-400">
								The gaming industry thrives thanks to hard-working and creative minds. Learn how to
								build games for PC, mobile, and console.
							</dd>
						</div>
						<div class="relative pl-16">
							<dt class="text-base font-semibold leading-7 text-gray-300">
								<div
									class="absolute left-0 top-0 flex h-10 w-10 items-center justify-center rounded-lg bg-blue-400 hover:animate-bounce"
								>
									<svg
										class="h-6 w-6 text-black"
										fill="none"
										viewBox="0 0 24 24"
										stroke-width="1.5"
										stroke="currentColor"
										aria-hidden="true"
									>
										<path
											stroke-linecap="round"
											stroke-linejoin="round"
											d="M16.5 10.5V6.75a4.5 4.5 0 10-9 0v3.75m-.75 11.25h10.5a2.25 2.25 0 002.25-2.25v-6.75a2.25 2.25 0 00-2.25-2.25H6.75a2.25 2.25 0 00-2.25 2.25v6.75a2.25 2.25 0 002.25 2.25z"
										/>
									</svg>
								</div>
								Cybersecurity
							</dt>
							<dd class="mt-2 text-base leading-7 text-gray-400">
								In today's world, cybersecurity is more important than ever. Learn how to protect
								yourself and others from cyber attacks.
							</dd>
						</div>
						<div class="relative pl-16">
							<dt class="text-base font-semibold leading-7 text-gray-300">
								<div
									class="absolute left-0 top-0 flex h-10 w-10 items-center justify-center rounded-lg bg-blue-400 hover:animate-bounce"
								>
									<svg
										xmlns="http://www.w3.org/2000/svg"
										class="h-6 w-6 text-black"
										fill="none"
										viewBox="0 0 24 24"
										stroke-width="1.5"
										stroke="currentColor"
									>
										<path
											stroke-linecap="round"
											stroke-linejoin="round"
											d="M6 12 3.269 3.125A59.769 59.769 0 0 1 21.485 12 59.768 59.768 0 0 1 3.27 20.875L5.999 12Zm0 0h7.5"
										/>
									</svg>
								</div>
								Embedded &#38; Avionics Software
							</dt>
							<dd class="mt-2 text-base leading-7 text-gray-400">
								Real-time systems are everywhere. Learn how to build software for embedded systems
								and avionics applications.
							</dd>
						</div>
					</dl>
				</div>
			</div>
		</section>
		<!-- End of Section 2 -->

		<!-- Section 3 (Card Showcase) -->
		<section class="pt-20 pb-10 lg:pt-[120px] lg:pb-20">
			<div class="container mx-auto">
				<div class="flex flex-wrap -mx-4">
					<div class="w-full px-4 md:w-1/2 xl:w-1/3">
						<div
							class="mb-10 overflow-hidden duration-300 bg-gray-900 rounded-lg shadow-1 hover:shadow-3 shadow-2xl"
						>
							<img
								src="https://images.unsplash.com/photo-1594729095022-e2f6d2eece9c?q=80&w=2671&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
								alt="Unsplash software development content 5"
								class="w-full"
							/>
							<div class="p-8 text-center sm:p-9 md:p-7 xl:p-9">
								<h3
									class="tracking-tight text-gray-100 hover:text-primary mb-4 block text-xl font-semibold sm:text-[22px] md:text-xl lg:text-[22px] xl:text-xl 2xl:text-[22px]"
								>
									Learn Popular Data Structures and Algorithms
								</h3>
								<p class="text-gray-200 leading-relaxed text-body-color mb-7">
									Demystify data structures and algorithms that are commonplace in the world of
									software.
								</p>
								<div class="container flex-inline justify-center space-x-2">
									<a
										href="/data-structures"
										class="inline-flex items-center justify-center px-5 py-2 mt-2 mx-auto border border-transparent text-base font-bold rounded-md text-white bg-primary-600 hover:bg-primary-700 shadow-2xl"
									>
										Data Structures
									</a>
									<a
										href="/algorithms"
										class="inline-flex items-center justify-center px-5 py-2 mt-2 mx-auto border border-transparent text-base font-bold rounded-md text-white bg-primary-600 hover:bg-primary-700 shadow-2xl"
									>
										Algorithms
									</a>
								</div>
							</div>
						</div>
					</div>
					<div class="w-full px-4 md:w-1/2 xl:w-1/3">
						<div
							class="mb-10 overflow-hidden duration-300 bg-gray-900 rounded-lg shadow-1 hover:shadow-3 shadow-2xl"
						>
							<img
								src="https://images.unsplash.com/photo-1532622785990-d2c36a76f5a6?q=80&w=2670&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
								alt="Unsplash software development content 5"
								class="w-full"
							/>
							<div class="p-8 text-center sm:p-9 md:p-7 xl:p-9">
								<h3
									class=" tracking-tight text-gray-100 hover:text-primary mb-4 block text-xl font-semibold sm:text-[22px] md:text-xl lg:text-[22px] xl:text-xl 2xl:text-[22px]"
								>
									Understand the Fundamentals of Software Engineering
								</h3>
								<p class="text-gray-200 leading-relaxed text-body-color mb-7">
									Gain a solid understanding of software processes for creating efficient digital
									systems.
								</p>
								<div class="container flex-inline justify-center space-x-2">
									<a
										href="/design"
										class="inline-flex items-center justify-center px-5 py-2 mt-2 mx-auto border border-transparent text-base font-bold rounded-md text-white bg-primary-600 hover:bg-primary-700 shadow-2xl"
									>
										Software Development Life Cycle
									</a>
								</div>
							</div>
						</div>
					</div>
					<div class="w-full px-4 md:w-1/2 xl:w-1/3">
						<div
							class="mb-10 overflow-hidden duration-300 bg-gray-900 rounded-lg shadow-1 hover:shadow-3 shadow-2xl"
						>
							<img
								src="https://images.unsplash.com/photo-1528901166007-3784c7dd3653?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
								alt="Unsplash software development content 5"
								class="w-full"
							/>
							<div class="p-8 text-center sm:p-9 md:p-7 xl:p-9">
								<h3
									class=" tracking-tight text-gray-100 hover:text-primary mb-4 block text-xl font-semibold sm:text-[22px] md:text-xl lg:text-[22px] xl:text-xl 2xl:text-[22px]"
								>
									Build Unique Projects to Apply Your Knowledge
								</h3>
								<p class="text-gray-200 leading-relaxed text-body-color mb-7">
									Through hands-on solo/group projects, refine your skills and unleash creativity.
								</p>
								<div class="container">
									<a
										href="/projects"
										class="inline-flex items-center justify-center px-5 py-2 mt-2 mx-auto border border-transparent text-base font-bold rounded-md text-white bg-primary-600 hover:bg-primary-700 shadow-2xl"
									>
										Coding Challenges &#38; Project Ideas
									</a>
								</div>
							</div>
						</div>
					</div>
				</div>
			</div>
		</section>
		<!-- End of Section 3-->

		<!-- Section 4 (Release Notes) -->
		<section class="bg-gray-900 text-white">
			<div
				class="py-28 px-4 max-w-screen-xl mx-auto lg:py-16 lg:px-6 flex justify-center items-center"
			>
				<div class="max-w-screen-lg sm:text-lg text-gray-400">
					<h2 class="mb-10 text-5xl tracking-tight font-bold text-white text-center">
						Release Notes
					</h2>
					<div id="accordion-collapse" data-accordion="collapse">
						<!-- Non-Accordion Item -->
						<div>
							<div class="p-5 border border-b-0 border-gray-700 bg-gray-900">
								<p class="text-white font-bold mb-4">Jan. 13, 2024 (Version 1.0 🎉):</p>

								<ul class="list-disc list-inside">
									<li class="mb-2">
										<span class="text-white">
											<a href="/data-structures">Data Structures</a>:
										</span>
										<span class="text-gray-400">
											Added <a href="/data-structures/linear/stack">Stack</a> and
											<a href="/data-structures/linear/queue">Queue</a> sections.
										</span>
									</li>
									<li class="mb-2">
										<span class="text-white">
											<a href="/algorithms">Algorithms</a>:
										</span>
										<span class="text-gray-400">
											Added <a href="/algorithms/sorting/bubble-sort">Bubble sort</a>,
											<a href="/algorithms/sorting/selection-sort">Selection sort</a>, and
											<a href="/algorithms#pathfinding-algorithms">more</a>.
										</span>
									</li>
								</ul>
							</div>
						</div>

						<!-- First Accordion Item -->
						<h2 id="accordion-collapse-heading">
							<button
								type="button"
								class="flex items-center justify-between w-full p-5 font-medium rtl:text-right border focus:ring-4 focus:ring-gray-800 border-gray-700 text-gray-400 hover:bg-gray-800 gap-3"
								data-accordion-target="#accordion-collapse-body"
								aria-expanded={isAccordionExpanded}
								aria-controls="accordion-collapse-body"
								on:click={() => toggleAccordion('accordion-collapse-body')}
							>
								<span>See previous release notes</span>
								<svg
									data-accordion-icon
									class="w-3 h-3 shrink-0 transform {chevronRotation} transition-transform duration-150 ease-in-out"
									aria-hidden="true"
									xmlns="http://www.w3.org/2000/svg"
									fill="none"
									viewBox="0 0 10 6"
								>
									<path
										stroke="currentColor"
										stroke-linecap="round"
										stroke-linejoin="round"
										stroke-width="2"
										d="M9 5 5 1 1 5"
									/>
								</svg>
							</button>
						</h2>
						<div
							id="accordion-collapse-body"
							class={isAccordionExpanded ? '' : 'hidden'}
							aria-labelledby="accordion-collapse-heading"
						>
							<div class="p-5 border border-t-0 border-gray-700">
								<p class="mb-2 text-gray-400 text-sm">Looks like there's nothing here yet.</p>
							</div>
						</div>
					</div>
				</div>
			</div>
		</section>
		<!-- End of Section 4 -->

		<!-- Section 5 (Upcoming Features) -->
		<div class="bg-gray-800 flex flex-col items-center justify-center py-28">
			<h1 class="text-5xl text-white font-bold mb-8 animate-bounce">More Content is on the way</h1>
			<p class="text-white text-lg mb-4">
				Completed sections for this website (plus internalization and accessibility support,) will
				be coming soon!
			</p>
			<p class="text-white text-lg">Check back soon for more updates. 🚀</p>
		</div>
		<!-- End of Section 5 -->
	</div>
</div>
