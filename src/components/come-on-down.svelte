<script>
    import { onMount } from 'svelte';
    import { tweened } from 'svelte/motion';
    import { cubicIn } from 'svelte/easing';

    const CACHE_KEY = '__IS_BOB_BARKER_STILL_ALIVE__CACHE__';
    const FIVE_MINS = 300000;

    let status = 'Checking';

    let cache;

    const animConfig = {
        duration: 750,
        easing: cubicIn,
    };

    let scaleAnim = tweened(0, animConfig);
    let rotateAnim = tweened(-180, animConfig);

    const isCacheInvalid = () => {
        const now = Date.now();
        cache = JSON.parse(window.localStorage.getItem(CACHE_KEY));
        if (!cache || (cache.timestamp - now) > FIVE_MINS) {
            return true;
        }
        return false;
    };

    onMount(async () => {
        if (!isCacheInvalid()) {
            status = cache.isAlive ? 'Alive' : 'Dead';
            // status = cache.isAlive ? 'Dead' : 'Alive';
            scaleAnim.set(1);
            rotateAnim.set(730);
            return;
        }

        const res = await fetch('https://c5q496vt22.execute-api.us-east-1.amazonaws.com/dev/isbobbarkerstillalive');
        const { isAlive } = await res.json();
        window.localStorage.setItem(CACHE_KEY, JSON.stringify({
            isAlive,
            timestamp: Date.now(),
        }));

        if (isAlive) {
            status = isAlive ? 'Alive' : 'Dead';
            // status = isAlive ? 'Dead' : 'Alive';
            scaleAnim.set(1);
            rotateAnim.set(730);
        }
        mixpanel.track('Load Page: Main', { isAlive });
	});
</script>

<style>
    h3 {
        color: #f1f1f1;
        font-family: 'Pricedown', Roboto, -apple-system, BlinkMacSystemFont, Segoe UI, Oxygen, Ubuntu, Cantarell, Fira Sans, Droid Sans, Helvetica Neue, sans-serif;
        font-size: 3rem;
        text-shadow: 0 0 1rem #333;
        text-align: center;
        z-index: 2;
    }
    img {
        border-radius: 100%;
        box-shadow: 0 0 2rem 0.5rem #800080;
        transform: translate(-50%, -40%);
        position: absolute;
        top: 50%;
        left: 50%;
        width: 90vw;
        max-width: 600px;
        z-index: 0;
    }
    .dead-link {
        color: #00aacc;
        font-family: 'Pricedown', Roboto, -apple-system, BlinkMacSystemFont, Segoe UI, Oxygen, Ubuntu, Cantarell, Fira Sans, Droid Sans, Helvetica Neue, sans-serif;
        font-size: 2.25rem;
        text-align: center;
        transition: color 0.2s ease-in;
        text-shadow: 0 0 1rem #333;
        z-index: 2;
    }
    .dead-link:hover {
        color: lime;
    }
</style>

<svelte:head>
	<title>He's {status} | Is Bob Barker Still Alive?</title>
</svelte:head>

<h3>
    {#if status === 'Alive'}
        Looks like Bob is still {status}!
    {:else if status === 'Dead'}
        Uh oh, it looks like Bob is {status}!
    {:else}
        Checking if Bob is still with us...
    {/if}
</h3>
{#if status === 'Alive'}
    <img
        src="img/bob-barker.jpg"
        alt="Bob Barker's Beautiful Face"
        style="
            transform: translate(-50%, -40%) scale({$scaleAnim}) scale({$scaleAnim}) rotate({$rotateAnim}deg);
            opacity: {$scaleAnim};
        "
    />
{/if}
{#if status === 'Dead'}
    <a href="https://www.google.com/search?q=is+bob+barker+still+alive%3F&hl=en&tbm=nws" class="dead-link">Wait what...?</a>
{/if}

