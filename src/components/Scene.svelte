<script>
	import Scrolly from "$components/helpers/Scrolly.svelte";
	import { onMount } from "svelte";
	import { Rive } from "@rive-app/canvas";

	export let fixed;

	let canvasEl;
	let riveStep;
	let scrollyValue;

	onMount(() => {
		// const r = new Rive({
		// 	src: "https://ucarecdn.com/f4639c73-2ad7-4b0e-918d-40d6ec439eed/240215_QueuesExperiment",
		// 	canvas: canvasEl,
		// 	autoplay: true,
		// 	stateMachines: "StateMachine",
		// 	onLoad: () => {
		// 		const inputs = r.stateMachineInputs("StateMachine");
		// 		riveStep = inputs.find((i) => i.name === "rive-step");
		// 		riveStep.value = 1;
		// 	}
		// });
	});
</script>

<div class="scene-wrapper" class:fixed>
	<div class="canvas">
		sticky active step = {scrollyValue}
		<!-- <canvas bind:this={canvasEl}></canvas> -->
	</div>

	<div class="text">
		<Scrolly bind:value={scrollyValue} top={fixed ? 653 : 0}>
			<!-- 70vh -->
			{#each [0, 1, 2, 3, 4] as text, i}
				{@const active = scrollyValue === i}
				<p class="step" class:active>{text}</p>
			{/each}
		</Scrolly>
	</div>
</div>

<style>
	.scene-wrapper {
		display: flex;
		position: relative;
		width: 100%;
	}
	.text,
	.canvas {
		width: 50%;
	}
	.canvas {
		background: lightpink;
		position: sticky;
		top: 0;
		height: 100vh;
	}
	.step {
		background: lightgrey;
		margin: 16em 0;
		padding: 1rem;
	}
	.step:first-of-type {
		margin-top: 0;
	}
	.step.active {
		background: gold;
	}

	@media (max-width: 600px) {
		.scene-wrapper {
			flex-direction: column;
		}
		.canvas {
			height: 70vh;
			width: 100%;
			margin-bottom: 1rem;
		}
		.text {
			width: 100%;
		}
		.fixed .text {
			padding-top: calc(70vh + 1rem);
		}
		.fixed .canvas {
			position: fixed;
			top: 0;
			left: 0;
			z-index: 1;
		}
	}
</style>
