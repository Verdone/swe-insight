<script>
	export let name;
	export let url;
	export let licenseUrl;
	export let licenseText;
	export let fullLicenseName;
</script>

<li>
	<a href={url} target="_blank" class="text-2xl text-blue-500 hover:text-blue-300">{name}</a>

	<p class="mb-10 font-light">
		{licenseText} It is used under the terms of the
		<a href={licenseUrl} target="_blank" class="text-blue-500 hover:text-blue-300"
			>{fullLicenseName}</a
		>.
	</p>
</li>
