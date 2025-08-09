<script>
	import { onMount, createEventDispatcher } from 'svelte';
	import Glide from '@glidejs/glide';

	export let content = [];

	const dispatch = createEventDispatcher();
	let glideElement;
	let glideInstance;

	onMount(() => {
		if (glideElement && content.length > 0) {
			glideInstance = new Glide(glideElement, {
				type: 'carousel',
				autoplay: 5000,
				hoverpause: true,
				perView: 1,
				animationDuration: 800,
				animationTimingFunc: 'ease-in-out'
			});

			glideInstance.mount();
		}

		return () => {
			if (glideInstance) {
				glideInstance.destroy();
			}
		};
	});

	function playVideo(video) {
		dispatch('playVideo', video);
	}
</script>

<div class="relative h-screen overflow-hidden">
	<div bind:this={glideElement} class="glide h-full">
		<div class="glide__track h-full" data-glide-el="track">
			<ul class="glide__slides h-full">
				{#each content as item, index}
					<li class="glide__slide relative h-full">
						<div
							class="absolute inset-0 bg-cover bg-center bg-no-repeat"
							style="background-image: linear-gradient(rgba(0,0,0,0.4), rgba(0,0,0,0.6)), url('{item.image}')"
						>
							<div class="absolute inset-0 flex items-center">
								<div class="mx-auto w-full max-w-7xl px-4">
									<div class="max-w-2xl text-white">
										<h1 class="mb-4 text-5xl font-bold md:text-6xl">{item.title}</h1>
										<p class="mb-2 text-xl text-gray-300 md:text-2xl">{item.subtitle}</p>
										<p class="mb-8 text-lg leading-relaxed text-gray-200">{item.description}</p>

										<div class="flex space-x-4">
											<button
												on:click={() => playVideo(item)}
												class="flex items-center space-x-2 rounded-lg bg-white px-8 py-3 font-semibold text-black transition-colors hover:bg-gray-200"
											>
												<svg class="h-5 w-5" fill="currentColor" viewBox="0 0 20 20">
													<path
														fill-rule="evenodd"
														d="M10 18a8 8 0 100-16 8 8 0 000 16zM9.555 7.168A1 1 0 008 8v4a1 1 0 001.555.832l3-2a1 1 0 000-1.664l-3-2z"
														clip-rule="evenodd"
													></path>
												</svg>
												<span>Cek Sekarang</span>
											</button>

											<button
												class="bg-opacity-80 flex items-center space-x-2 rounded-lg bg-gray-700 px-8 py-3 font-semibold text-white transition-colors hover:bg-gray-600"
											>
												<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
													<path
														stroke-linecap="round"
														stroke-linejoin="round"
														stroke-width="2"
														d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z"
													></path>
												</svg>
												<span>Ingatkan Saya</span>
											</button>
										</div>
									</div>
								</div>
							</div>
						</div>
					</li>
				{/each}
			</ul>
		</div>

		<!-- Navigation arrows -->
		<div
			class="glide__arrows pointer-events-none absolute inset-y-0 right-0 left-0 flex items-center justify-between px-4"
			data-glide-el="controls"
		>
			<!-- svelte-ignore a11y_consider_explicit_label -->
			<button
				class="glide__arrow glide__arrow--left bg-opacity-50 hover:bg-opacity-75 pointer-events-auto rounded-full bg-black p-3 text-white transition-all"
				data-glide-dir="<"
			>
				<svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"
					></path>
				</svg>
			</button>
			<button
				class="glide__arrow glide__arrow--right bg-opacity-50 hover:bg-opacity-75 pointer-events-auto rounded-full bg-black p-3 text-white transition-all"
				data-glide-dir=">"
				aria-label="Next slide"
			>
				<svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"
					></path>
				</svg>
			</button>
		</div>

		<!-- Dots indicator -->
		<div
			class="glide__bullets absolute bottom-8 left-1/2 flex -translate-x-1/2 transform space-x-2"
			data-glide-el="controls[nav]"
		>
			{#each content as _, index}
				<button
					class="glide__bullet bg-opacity-50 hover:bg-opacity-100 h-3 w-3 rounded-full bg-white transition-all"
					data-glide-dir="={index}"
					aria-label="Go to slide {index + 1}"
				></button>
			{/each}
		</div>
	</div>
</div>

<style>
	@import '@glidejs/glide/dist/css/glide.core.min.css';

	:global(.glide__bullet--active) {
		background-color: white !important;
		opacity: 1 !important;
	}
</style>
