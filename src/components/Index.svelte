<script>
	import Scene from "$components/Scene.svelte";
	import copy from "$data/copy.json";
	import inView from "$actions/inView.js";
	import viewport from "$stores/viewport.js";
	import { fixed } from "$stores/misc.js";

	const onEnter = () => {
		if ($viewport.width < 600) $fixed = false;
	};
	const onExit = () => {
		if ($viewport.width < 600) $fixed = true;
	};
</script>

<article>
	<section id="title">
		<h1>{copy.hed}</h1>
		<h3>{copy.dek}</h3>
		<p>{copy.byline}</p>
		<p>{copy.byline2}</p>
	</section>

	<section id="intro" use:inView on:enter={onEnter} on:exit={onExit}>
		{#each copy.intro as { value }}
			<p>{@html value}</p>
		{/each}
	</section>

	<section id="scene-1">
		<Scene steps={copy.scenes[0].steps} />
	</section>
</article>

<style>
	article {
		max-width: 800px;
		margin: auto;
		font-family: var(--sans);
	}
	#title {
		padding: 0 1rem;
	}
	#intro {
		margin: 0;
		padding: 3rem 1rem;
	}
</style>
