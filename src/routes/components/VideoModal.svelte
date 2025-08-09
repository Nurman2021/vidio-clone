<script>
	import { onMount, createEventDispatcher } from 'svelte';
	import videojs from 'video.js';
	import { X, Heart, Share2, Plus } from 'lucide-svelte';

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
				<X size={24} />
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
						class="flex items-center space-x-2 rounded-lg bg-gray-700 px-6 py-2 font-semibold text-white transition-colors hover:bg-gray-600"
					>
						<Plus size={16} />
						<span>Add to Watchlist</span>
					</button>
					<button
						class="rounded-lg bg-gray-700 p-2 text-white transition-colors hover:bg-gray-600"
						aria-label="Like video"
					>
						<Heart size={20} />
					</button>
					<button
						class="rounded-lg bg-gray-700 p-2 text-white transition-colors hover:bg-gray-600"
						aria-label="Share video"
					>
						<Share2 size={20} />
					</button>
				</div>
			</div>
		</div>
	</div>
{/if}

<style>
	@import 'video.js/dist/video-js.css';
</style>
