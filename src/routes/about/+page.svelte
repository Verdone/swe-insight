<script>
	import { websiteName } from '$lib/stores';
</script>

<svelte:head>
	<title>About - {websiteName}</title>
</svelte:head>

<section class="bg-white dark:bg-gray-800">
	<div class="py-8 px-4 mx-auto max-w-screen-xl lg:py-16 lg:px-6">
		<div class="max-w-screen-lg text-gray-500 sm:text-lg dark:text-gray-400">
			<h2 class="mb-4 text-4xl tracking-tight font-bold text-gray-900 dark:text-white">
				About this website
			</h2>
			<p class="mb-4 font-light">
				This website was created with SvelteKit. It uses TailwindCSS for styling and is hosted on
				Vercel. The source code for this website can be found on <a
					href={'https://github.com/Verdone/swe-insight'}
					target="_blank"
					class="text-blue-500 hover:text-blue-300">GitHub</a
				>.
			</p>
			<p class="mb-4 font-light">
				See the <a href="/copywright" class="text-blue-500 hover:text-blue-300"
					>licensing information</a
				> for third-party materials used to create this website.
			</p>
		</div>
	</div>
</section>

<section class="bg-white dark:bg-gray-900">
	<div class="py-8 px-4 mx-auto max-w-screen-xl lg:py-16 lg:px-6">
		<div class="max-w-screen-lg text-gray-500 sm:text-lg dark:text-gray-400">
			<h2 class="mb-4 text-4xl tracking-tight font-bold text-gray-900 dark:text-white">
				Reference list for this website
			</h2>
			<p class="mb-4 font-light">
				(Data Structures and Algorithms in Java, 6th Edition) by Michael T. Goodrich, Roberto
				Tamassia, and Michael H. Goldwasser (2014). Textbook for the course COMP 352 at <a
					href="https://www.concordia.ca/"
					target="_blank"
					class="text-blue-500 hover:text-blue-300">Concordia University</a
				>.
			</p>

			<a
				href={'http://bedford-computing.co.uk/learning/wp-content/uploads/2016/08/Data-Structures-and-Algorithms-in-Java-6th-Edition.pdf'}
				target="_blank"
				class="inline-flex items-center font-medium text-primary-600 hover:text-primary-800 dark:text-primary-500 dark:hover:text-primary-300"
			>
				Link to PDF
				<svg
					class="ml-1 w-6 h-6"
					fill="currentColor"
					viewBox="0 0 20 20"
					xmlns="http://www.w3.org/2000/svg"
					><path
						fill-rule="evenodd"
						d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z"
						clip-rule="evenodd"
					></path></svg
				>
			</a>
		</div>
	</div>
</section>

<section class="bg-white dark:bg-gray-800">
	<div class="py-8 px-4 mx-auto max-w-screen-xl lg:py-16 lg:px-6">
		<div class="max-w-screen-lg text-gray-500 sm:text-lg dark:text-gray-400">
			<h2 class="mb-4 text-4xl tracking-tight font-bold text-gray-900 dark:text-white">About me</h2>
			<p class="mb-4 font-light">
				My name is Giuliano Verdone. I am a second-year student at <a
					href="https://www.concordia.ca/"
					target="_blank"
					class="text-blue-500 hover:text-blue-300">Concordia University</a
				> pursuing a Bachelor's degree in Software Engineering. Right now I'm looking for a Summer 2024
				internship. When I'm not busy, I enjoy creating projects like this website.
			</p>
			<p class="mb-4 font-light">
				If you would like to get in touch with me, please visit the
				<a href="/contact" class="text-blue-500 hover:text-blue-300">contact</a> page.
			</p>
		</div>
	</div>
</section>
