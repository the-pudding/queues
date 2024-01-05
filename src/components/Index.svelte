<script>
	import { onMount } from "svelte";
	import { Rive } from "@rive-app/canvas";
	import Scrolly from "$components/helpers/Scrolly.svelte";

	let canvasEl;
	let value;

	onMount(() => {
		const r = new Rive({
			src: "https://cdn.rive.app/animations/vehicles.riv",
			canvas: canvasEl,
			autoplay: true,
			stateMachines: "bumpy",
			onLoad: () => {
				r.resizeDrawingSurfaceToCanvas();
			}
		});
	});
</script>

<section id="scrolly">
	<div class="sticky">
		<h2>step <span>{value}</span></h2>
		<canvas bind:this={canvasEl} width="500" height="500"></canvas>
	</div>
	<div class="spacer" />
	<Scrolly bind:value>
		{#each [0, 1, 2, 3, 4] as text, i}
			{@const active = value === i}
			<div class="step" class:active>
				<p>{text}</p>
			</div>
		{/each}
	</Scrolly>
	<div class="spacer" />
</section>

<style>
	.sticky {
		position: sticky;
		top: 2rem;
		width: 60%;
		height: calc(100vh - 2rem);
	}

	.spacer {
		height: 75vh;
	}

	.step {
		height: 80vh;
		background: var(--color-gray-100);
		text-align: center;
	}

	.step p {
		padding: 1rem;
	}
</style>
