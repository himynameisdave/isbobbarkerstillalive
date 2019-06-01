<script>

    import { onMount } from 'svelte';

    let status = 'Checking';

    onMount(async () => {
        const res = await fetch('https://c5q496vt22.execute-api.us-east-1.amazonaws.com/dev/isbobbarkerstillalive');
        const { isAlive } = await res.json();
        if (isAlive) {
            status = isAlive ? 'Alive' : 'Dead';
        }
	});
</script>

<style>
    h3 {
        color: #f1f1f1;
        font-family: 'Pricedown', Roboto, -apple-system, BlinkMacSystemFont, Segoe UI, Oxygen, Ubuntu, Cantarell, Fira Sans, Droid Sans, Helvetica Neue, sans-serif;
        font-size: 3rem;
        text-shadow: 0 0 1rem #333;
        text-align: center;
    }
</style>

<svelte:head>
	<title>{status} | Is Bob Barker Still Alive?</title>
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
