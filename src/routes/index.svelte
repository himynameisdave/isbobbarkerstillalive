
<script>
	import { tweened } from 'svelte/motion';
	import { cubicOut } from 'svelte/easing';
	const backgroundImage = 'price-is-right.jpg'

	const REFRESH_RATE = 16;
	const loadAnim = tweened(100, {
		duration: 700,
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
		align-items: flex-start;
		display: flex;
		justify-content: center;
		padding-top: 3rem
	}

	h1 {
		color: #f1f1f1;
		text-align: center;
		font-weight: 900;
		font-size: 6rem;
		text-shadow: 0 0 1rem #333;
		width: 90%;
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
</section>