<script>
	import { onMount, createEventDispatcher } from 'svelte';
	import videojs from 'video.js';

	export let video = null;

	const dispatch = createEventDispatcher();
	let videoElement;
	let player;

	onMount(() => {
		if (video && videoElement) {
			player = videojs(videoElement, {
				controls: true,
				responsive: true,
				fluid: true,
				sources: [
					{
						src: video.videoUrl,
						type: 'video/mp4'
					}
				],
				poster: video.image
			});

			player.ready(() => {
				console.log('Video player ready');
			});
		}

		return () => {
			if (player) {
				player.dispose();
			}
		};
	});

	function closeModal() {
		if (player) {
			player.pause();
		}
		dispatch('close');
	}

	function handleKeydown(event) {
		if (event.key === 'Escape') {
			closeModal();
		}
	}
</script>

<svelte:window on:keydown={handleKeydown} />

{#if video}
	<div class="bg-opacity-90 fixed inset-0 z-50 flex items-center justify-center bg-black p-4">
		<div class="relative w-full max-w-6xl overflow-hidden rounded-lg bg-gray-900">
			<!-- Close button -->
			<button
				on:click={closeModal}
				class="bg-opacity-50 hover:bg-opacity-75 absolute top-4 right-4 z-10 rounded-full bg-black p-2 text-white transition-colors"
				aria-label="Close video modal"
			>
				<svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
					<path
						stroke-linecap="round"
						stroke-linejoin="round"
						stroke-width="2"
						d="M6 18L18 6M6 6l12 12"
					></path>
				</svg>
			</button>

			<!-- Video Player -->
			<div class="relative">
				<video
					bind:this={videoElement}
					class="video-js vjs-default-skin w-full"
					controls
					preload="auto"
					data-setup={'{}'}
				>
					<track kind="captions" />
				</video>
			</div>

			<!-- Video Info -->
			<div class="p-6 text-white">
				<h2 class="mb-2 text-2xl font-bold">{video.title}</h2>
				{#if video.subtitle}
					<p class="mb-3 text-lg text-gray-300">{video.subtitle}</p>
				{/if}
				{#if video.description}
					<p class="leading-relaxed text-gray-400">{video.description}</p>
				{/if}

				<div class="mt-6 flex items-center space-x-4">
					<button
						class="rounded-lg bg-red-600 px-6 py-2 font-semibold text-white transition-colors hover:bg-red-700"
					>
						Subscribe to Watch
					</button>
					<button
						class="rounded-lg bg-gray-700 px-6 py-2 font-semibold text-white transition-colors hover:bg-gray-600"
					>
						Add to Watchlist
					</button>
					<button
						class="rounded-lg bg-gray-700 p-2 text-white transition-colors hover:bg-gray-600"
						aria-label="Like video"
					>
						<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z"
							></path>
						</svg>
					</button>
					<button
						class="rounded-lg bg-gray-700 p-2 text-white transition-colors hover:bg-gray-600"
						aria-label="Share video"
					>
						<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M8.684 13.342C8.886 12.938 9 12.482 9 12c0-.482-.114-.938-.316-1.342m0 2.684a3 3 0 110-2.684m0 2.684l6.632 3.316m-6.632-6l6.632-3.316m0 0a3 3 0 105.367-2.684 3 3 0 00-5.367 2.684zm0 9.316a3 3 0 105.367 2.684 3 3 0 00-5.367-2.684z"
							></path>
						</svg>
					</button>
				</div>
			</div>
		</div>
	</div>
{/if}

<style>
	@import 'video.js/dist/video-js.css';
</style>
