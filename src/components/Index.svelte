<script>
	import Scene from "$components/Scene.svelte";
	import copy from "$data/copy.json";
</script>

<article>
	<section id="title">
		<h1>{@html copy.hed} <span>(insert header illustration here)</span></h1>
		<p>{@html copy.byline}</p>
		<p>{@html copy.byline2}</p>
		<p>{@html copy.byline3}</p>
	</section>

	<section id="intro">
		{#each copy.intro as { value }}
			<p>{@html value}</p>
		{/each}
	</section>

	<section id="scenes">
		{#each [1, 2, 3] as i}
			<Scene />
		{/each}
	</section>
</article>

<style>
	article {
		max-width: 600px;
		margin: auto;
		font-family: var(--sans);
	}
	section {
		margin: 3rem 0;
	}
	section:first-child {
		margin-top: 0;
	}
	#intro {
		font-size: 1.25rem;
	}
	#title p {
		text-align: center;
	}
	#title p:nth-of-type(1) {
		font-size: 1.5rem;
	}
	#title p:nth-of-type(2) {
		font-size: 1.25rem;
	}
	#title p:nth-of-type(3) {
		font-size: 1rem;
	}
	h1 {
		width: 100%;
		border: 1px dashed var(--color-fg);
		padding: 4rem;
	}
	h1 span {
		font-size: 1rem;
	}
</style>
