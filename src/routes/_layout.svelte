<script>
	// import Nav from '../components/Nav.svelte';

	export let segment;
</script>

<style>
	footer {
		position: fixed;
		font-family: monospace;
		font-size: 0.55rem;
		text-align: center;
		bottom: 0;
		width: 100%;
		padding: 1rem;
		z-index: 2;
		color: #00aacc;
	}
	div {
		margin-bottom: 0.5rem;
	}
	.bottom a {
		margin: 0 0.5rem;
	}
	a {
		color: #00aacc;
		transition: color 0.3s ease-in;
	}
	a:hover {
		color: lime;
	}
</style>

<slot />

<footer>
	<div>
		Made by <a href="http://himynameisdave.com" target="__blank">Dave</a> in 2019 ✌️
	</div>
	<div class="bottom">
		<a
			class='{segment === "about" ? "selected" : ""}'
			href='about'
			onclick="mixpanel.track('Clicked Link: About')"
		>
			About
		</a>
		<a
			href='https://github.com/himynameisdave/isbobbarkerstillalive'
			onclick="mixpanel.track('Clicked Link: Source')"
		>
			Source
		</a>
	</div>
</footer>