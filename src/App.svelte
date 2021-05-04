<script>
	import md5 from 'md5';

	let monokaiExtensionID = "fd330f6f-3f41-421d-9fe5-de742d0c54c0";
	let email;
	let vsKey;
	let sublimeKey;
	
	function formatKey(key) {
		return key.slice(0, 25).match(/.{5}/g).join('-');
	}

	function generateLicense() {
		if (email == "") {
			sublimeKey = undefined;
			vsKey = undefined;
		} else if (email != undefined) {
			// The Sublime Text key is just the first 25 characters of an MD5 hash of the user's email.
			sublimeKey = formatKey(md5(email));
			// The Visual Studio Code key is just the first 25 characters of an MD5 hash of the Monokai Pro VSCode extension ID with the user's email appended.
			vsKey = formatKey(md5(monokaiExtensionID +  email));
		}
	}

</script>

<svelte:head>
	<title>Monogen</title>
</svelte:head>

<main>
	<h1>Monogen</h1>
	<h3>A keygen for <a href="https://monokai.pro">Monokai Pro</a>.</h3>
	Email: 
	<input bind:value={email} placeholder="blackbeard@pirate.ship">
	<button on:click={generateLicense}>Crack it!</button>

	{#if vsKey != undefined && sublimeKey != undefined}
	<p><b>Sublime Text</b>: {sublimeKey}</p>
	<p><b>Visual Studio Code</b>: {vsKey}</p>
	{/if}
</main>

<style>
	main {
		text-align: center;
	}
</style>
