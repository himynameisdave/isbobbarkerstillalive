
<script>
	import ComeOnDown from '../components/come-on-down.svelte';
	import { tweened } from 'svelte/motion';
	import { cubicOut } from 'svelte/easing';
	const backgroundImage = 'img/price-is-right.jpg'

	const REFRESH_RATE = 16;
	const loadAnim = tweened(100, {
		duration: 450,
		easing: cubicOut
	});

	const timer = setInterval(() => {
		const gettinLow = $loadAnim - REFRESH_RATE <= 0;
		if ($loadAnim <= 0 || gettinLow) {
			if (gettinLow) {
				$loadAnim = 0;
			}
			return clearInterval(timer);
		}
		$loadAnim -= REFRESH_RATE;
	}, REFRESH_RATE);

	const headerIn = tweened(100, {
		duration: 600,
		easing: cubicOut
	});

</script>

<style>
	.main {
		background-size: cover;
		background-position: 50% 50%;
		height: 100%;
		width: 100%;
		align-items: center;
		display: flex;
		justify-content: flex-start;
		flex-direction: column;
		padding-top: 3rem;
	}

	h1 {
		color: #f1f1f1;
		text-align: center;
		font-weight: 900;
		font-size: 3rem;
		line-height: 1;
		text-shadow: 0 0 1rem #800080;
		width: 90%;
		z-index: 2;
	}
	@media screen and (min-width: 375px) {
		h1 {
			font-size: 4rem;
		}
	}
	@media screen and (min-width: 480px) {
		h1 {
			font-size: 6rem;
		}
	}
</style>

<svelte:head>
	<title>Checking... | Is Bob Barker Still Alive?</title>
</svelte:head>

<section
	class="main"
	style="
		background-image: url({backgroundImage});
		filter: blur({$loadAnim}px) invert({$loadAnim / 100}) brightness({100 - $loadAnim}%);
	"
>
	<h1>Is Bob Barker Still Alive?</h1>
	<ComeOnDown />
</section>