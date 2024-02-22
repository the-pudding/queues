<script>
	import Scrolly from "$components/helpers/Scrolly.svelte";
	import { onMount } from "svelte";
	import { Rive } from "@rive-app/canvas";
	import { fixed } from "$stores/misc.js";

	export let steps;

	let canvasEl;
	let scrollValue;
	let riveStep;
	let leftSelect;
	let rightSelect;

	$: top = $fixed ? 653 : 0; // 70vh - just mobile

	const onClick = [() => leftSelect.fire(), () => rightSelect.fire()];

	onMount(() => {
		const r = new Rive({
			src: "https://ucarecdn.com/f4639c73-2ad7-4b0e-918d-40d6ec439eed/240215_QueuesExperiment",
			canvas: canvasEl,
			autoplay: true,
			stateMachines: "StateMachine",
			onLoad: () => {
				const inputs = r.stateMachineInputs("StateMachine");
				riveStep = inputs.find((i) => i.name === "rive-step");
				leftSelect = inputs.find((i) => i.name === "Left-select");
				rightSelect = inputs.find((i) => i.name === "Right-Select");
				riveStep.value = 1;
			}
		});
	});
</script>

<div class="scene-wrapper" class:fixed={$fixed}>
	<div class="canvas">
		<canvas bind:this={canvasEl} height={500}></canvas>
	</div>

	<div class="text">
		<Scrolly bind:value={scrollValue} {top}>
			{#each steps as { text, prompt, options }, i}
				{@const active = scrollValue === i}
				<p class="step" class:active>
					{@html text}

					{#if prompt && options}
						<p class="prompt">{@html prompt}</p>
						{#each options as { label, value }, i}
							<button on:click={onClick[i]}>{label}</button>
						{/each}
					{/if}
				</p>
			{/each}
		</Scrolly>
		<div style:height="500px"></div>
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
		margin: 8em 0;
		padding: 1rem;
		opacity: 0.4;
	}
	.step:first-of-type {
		margin-top: 0;
	}
	.step.active {
		opacity: 1;
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
