<script>
	import { onMount } from 'svelte';
	import { fade, fly } from 'svelte/transition';

	let currentIndex = 0;
	const emojis = ['🎨', '🎧', '🗄️', '🐤', '✨', '🎬', '💡'];
	let emoji = emojis[0];
	let key = 0;

	onMount(() => {
		const interval = setInterval(() => {
			key += 1;
			currentIndex = (currentIndex + 1) % emojis.length;
			emoji = emojis[currentIndex];
		}, 1000);

		return () => clearInterval(interval);
	});
</script>

<div class="container">
	<h1>
		TC[<span class="emoji-container">
			{#key key}
				<span class="emoji" in:fly={{ y: 50, duration: 300 }} out:fly={{ y: -50, duration: 300 }}
					>{emoji}</span
				>
			{/key}
		</span>]
	</h1>
</div>

<style>
	h1 {
		color: white;
		font-size: calc(100vw / 12);
		line-height: 1em;
		position: relative;
	}

	span {
		display: inline-block;
	}

	.container {
		display: flex;
		justify-content: center;
		align-items: center;
		min-height: 100vh;
	}

	.emoji-container {
		display: inline-block;
		position: relative;
		height: 1em;
		width: 1em;
	}

	.emoji {
		position: absolute;
		left: 0.35em;
		top: 0.35em;
		font-size: 0.6em;
		line-height: calc(100vw / 12);
	}
</style>
