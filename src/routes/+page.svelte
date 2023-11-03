<script lang="ts">
	import hello from '$lib/hello.json';
	import { onMount } from 'svelte';
	import { fade, fly } from 'svelte/transition';

	let current = 0;

	onMount(() => {
		setInterval(() => {
			current = current + 1;
			if (current >= hello.length - 1) current = 0;
		}, 1500);
	});
</script>

<svelte:head>
	<link rel="stylesheet" href="/styles.css" />
</svelte:head>

<div class="container">
	{#key current}
		<h1
			in:fly={{ y: -100, delay: 200, duration: 200 }}
			out:fly={{ y: 200, duration: 200 }}
			class="hello"
		>
			{hello[current].hello}
		</h1>
	{/key}
</div>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@600&display=swap');

	.hello {
		font-size: min(60px, 13vw);
		font-family: Montserrat, sans-serif;
		font-weight: 600;
		text-align: center;
		margin: 0;
		background: linear-gradient(-45deg, #fdba74, #86efac, #67e8f9, #a5b4fc, #fda4af);
		background-size: 500% 500%;
		animation: gradient 10s ease infinite;
		-webkit-background-clip: text;
		-webkit-text-fill-color: transparent;
	}

    .container {
        height: 73.6px;
    }

	@keyframes gradient {
		0% {
			background-position: 0% 50%;
		}
		50% {
			background-position: 100% 50%;
		}
		100% {
			background-position: 0% 50%;
		}
	}
</style>
