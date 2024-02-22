<script>
	import Scrolly from "$components/helpers/Scrolly.svelte";
	import { onMount } from "svelte";
	import { Rive } from "@rive-app/canvas";
	import { fixed } from "$stores/misc.js";

	export let steps;

	let canvasEl;
	let riveStep;
	let scrollyValue;

	$: scrollyTop = $fixed ? 653 : 0; // 70vh

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

<div class="scene-wrapper" class:fixed={$fixed}>
	<div class="canvas">
		<canvas bind:this={canvasEl}></canvas>
	</div>

	<div class="text">
		<Scrolly bind:value={scrollyValue} top={scrollyTop}>
			{#each steps as { text, prompt, options }, i}
				{@const active = scrollyValue === i}
				<p class="step" class:active>
					{@html text}

					{#if prompt && options}
						<p class="prompt">{@html prompt}</p>
						{#each options as { label, value }}
							<button>{label}</button>
						{/each}
					{/if}
				</p>
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
	.text {
		width: 40%;
	}
	.canvas {
		position: sticky;
		top: 0;
		height: 100vh;
		width: 60%;
		display: flex;
		flex-direction: column;
		justify-content: center;
	}
	canvas {
		width: 100%;
	}
	.step {
		margin: 5em 0;
		padding: 1rem;
	}
	.step:first-of-type {
		margin-top: 0;
	}
	.step.active {
		/* background: lightyellow; */
	}
	.prompt {
		font-weight: bold;
	}
	button {
		background: none;
		border: 1px solid var(--color-gray-300);
		margin-right: 0.5rem;
	}
	button:hover {
		background: var(--color-gray-100);
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
