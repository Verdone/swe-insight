<script>
	import ThirdPartyResource from './ThirdPartyResource.svelte';
	import { websiteName } from '$lib/stores';

	const resources = [
		{
			name: 'Flaticon - Wissawa Khamsriwath',
			url: 'https://www.flaticon.com/authors/wissawa-khamsriwath',
			licenseUrl: 'https://www.flaticon.com/authors/wissawa-khamsriwath',
			licenseText: 'Wissawa Khamsriwath is the creator of the favicon used on this website.',
			fullLicenseName: 'Flaticon Basic License'
		},
		{
			name: 'Flowbite',
			url: 'https://flowbite.com/docs/',
			licenseUrl: 'https://flowbite.com/docs/getting-started/license/',
			licenseText: 'Flowbite is a free and open-source HTML, Tailwind CSS and vanilla JS UI kit.',
			fullLicenseName: 'MIT License'
		},
		{
			name: 'Heroicons',
			url: 'https://heroicons.com/',
			licenseUrl: 'https://github.com/tailwindlabs/heroicons/blob/master/LICENSE',
			licenseText:
				'Heroicons is a set of free MIT-licensed high-quality SVG icons for you to use in your web projects.',
			fullLicenseName: 'MIT License'
		},
		{
			name: 'p5-svelte',
			url: 'https://github.com/tonyketcham/p5-svelte',
			licenseUrl: 'https://github.com/tonyketcham/p5-svelte/blob/main/LICENSE',
			licenseText:
				'p5-svelte is a Svelte component for using the p5.js library. It allows you to easily create interactive sketches on your website.',
			fullLicenseName: 'MIT License'
		},
		{
			name: 'SvelteKit',
			url: 'https://kit.svelte.dev/',
			licenseUrl: 'https://github.com/sveltejs/kit/blob/main/LICENSE',
			licenseText:
				'SvelteKit simplifies the process of creating full-stack web applications with the Svelte JavaScript framework.',
			fullLicenseName: 'MIT License'
		},
		{
			name: 'SvHighlight',
			url: 'https://github.com/bennymi/svhighlight',
			licenseUrl: 'https://github.com/bennymi/svhighlight/blob/main/LICENSE',
			licenseText:
				'SvHighlight is a syntax highlighting library for Svelte built on top of hightlight.js.',
			fullLicenseName: 'MIT License'
		},
		{
			name: 'TailwindCSS',
			url: 'https://tailwindcss.com/',
			licenseUrl: 'https://github.com/tailwindlabs/tailwindcss/blob/master/LICENSE',
			licenseText:
				"Tailwind CSS is a utility-first CSS framework that's great for prototyping because it promotes rapid development and easily customizable styles.",
			fullLicenseName: 'MIT License'
		},
		{
			name: 'Undraw',
			url: 'https://undraw.co/',
			licenseUrl: 'https://undraw.co/license',
			licenseText: 'Undraw has a collection of PNG/SVG images available for free use.',
			fullLicenseName: 'MIT License'
		},
		{
			name: 'Unsplash',
			url: 'https://unsplash.com/',
			licenseUrl: 'https://unsplash.com/license',
			licenseText: 'Unsplash is a website dedicated to sharing stock photography.',
			fullLicenseName: 'Unsplash License'
		},
		{
			name: 'Vercel',
			url: 'https://vercel.com/',
			licenseUrl: 'https://github.com/vercel/vercel/blob/main/LICENSE',
			licenseText:
				'Vercel is a cloud platform for frontend development and serverless functions. It allows anyone to deploy and host their own websites/applications.',
			fullLicenseName: 'Apache License 2.0'
		}
	];
</script>

<svelte:head>
	<title>Home - {websiteName}</title>
</svelte:head>

<section class="bg-white dark:bg-gray-800">
	<div class="py-8 px-4 mx-auto max-w-screen-xl lg:py-16 lg:px-6">
		<div class="max-w-screen-lg text-gray-300 sm:text-lg">
			<h2 class="mb-4 text-4xl tracking-tight font-bold text-gray-900 dark:text-white">
				Copywright
			</h2>
			<p class="mb-8 font-light">
				The following third-party resources were used in the creation of this website:
			</p>

			<ul>
				{#each resources as resource (resource.name)}
					<ThirdPartyResource {...resource} />
				{/each}
			</ul>
		</div>
	</div>
</section>
