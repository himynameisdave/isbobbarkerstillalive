<script>
	export let status;
	export let error;

	const dev = process.env.NODE_ENV === 'development';
</script>

<style>
	h1, h2, a {
		color: lime;
		margin: 0 auto;
		text-align: center;
	}

	h1 {
		font-size: 2.8em;
		font-weight: 700;
		margin: 0 0 0.5em 0;
	}

	div {
		background-repeat: repeat;
		height: 100%;
		width: 100%;
	}

	a {
		display: block;
		color: #00aacc;
		text-decoration: none;
	}
	a:hover {
		color: lime;
	}
</style>

<svelte:head>
	<title>Ruh Roe | Is Bob Barker Still Alive?</title>
</svelte:head>

<div style="background-image: url('img/bob-404.gif')">
	<h1>The price is wrong</h1>
	<h2>{status} {error.message}</h2>
	<a href="/">👈 Back to reality...</a>
	{#if dev && error.stack}
		<pre>{error.stack}</pre>
	{/if}
</div>
