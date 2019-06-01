<script>
	import { onMount } from 'svelte';

	onMount(() => {
		mixpanel.track('Load Page: About');
	});
</script>

<svelte:head>
	<title>About | Is Bob Barker Still Alive?</title>
</svelte:head>

<style>
	section {
		flex-direction: column;
		text-align: center;
		position: relative;
		height: 100vh;
		padding: 2rem 0;
	}
	.close {
		position: fixed;
		top: 2.5vh;
		right: 5vw;
		text-decoration: none;
		font-size: 1.5rem;
	}
	div {
		padding: 4rem 0;
		margin: 0 auto;
		width: 80vw;
	}
	.nerd-stuff {
		padding: 2rem 0 0;
	}
	h1 {
		font-size: 3rem;
	}
	@media screen and (min-width: 480px) {
		div {
			max-width: 420px;
			width: 65vw;
		}
	}
</style>

<section>
	<a class="close" href="/">&#x2716;</a>
	<div>
		<h1>About this site...</h1>
		<p>After I found myself searching "is Bob Barker still alive" more than a few times, I realized I should probably just make a simple site to check for me.</p>
		<p>It will be a very sad day when Bob passes on, but until then it brings me joy to know that Bob is still alive, and I hope it does the same for you.</p>
		<div class="nerd-stuff">
			<pre>&#60;nerd-stuff&#62;</pre>
			<p>I also really wanted to learn about <a href="https://svelte.dev/" target="__blank" onclick="mixpanel.track('Clicked Link: Svelte')">Svelte 3</a>, and the best way to learn something is by using it. It's got some pretty cool stuff in terms of dev ergonomics, plus the lack of a virtual DOM makes it super speedy and reactive.</p>
			<pre>&#60;/nerd-stuff&#62;</pre>
		</div>
	</div>
</section>
