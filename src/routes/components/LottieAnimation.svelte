<script>
	import { onMount } from 'svelte';
	import lottie from 'lottie-web';

	export let animationData = null;
	export let width = 200;
	export let height = 200;
	export let autoplay = true;
	export let loop = true;

	let container;
	let animation;

	onMount(() => {
		if (container && animationData) {
			animation = lottie.loadAnimation({
				container: container,
				renderer: 'svg',
				loop: loop,
				autoplay: autoplay,
				animationData: animationData
			});
		}

		return () => {
			if (animation) {
				animation.destroy();
			}
		};
	});

	export function play() {
		if (animation) {
			animation.play();
		}
	}

	export function pause() {
		if (animation) {
			animation.pause();
		}
	}

	export function stop() {
		if (animation) {
			animation.stop();
		}
	}
</script>

<div
	bind:this={container}
	style="width: {width}px; height: {height}px;"
	class="lottie-container"
></div>

<style>
	.lottie-container {
		display: flex;
		align-items: center;
		justify-content: center;
	}
</style>
