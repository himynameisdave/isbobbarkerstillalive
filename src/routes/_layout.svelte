<script>
	// import Nav from '../components/Nav.svelte';

	export let segment;
</script>

<style>
	footer {
		position: fixed;
		font-family: monospace;
		font-size: 0.5rem;
		text-align: center;
		bottom: 0;
		width: 100%;
		padding: 1rem;
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
		Made by Dave in 2019 ✌️
	</div>
	<div>
		<a class='{segment === "about" ? "selected" : ""}' href='about'>
			About
		</a>
		<a href='https://github.com/himynameisdave/isbobbarkerstillalive'>
			Source
		</a>
	</div>
</footer>