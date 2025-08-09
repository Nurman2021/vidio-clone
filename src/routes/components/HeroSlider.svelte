<script>
	import { onMount, createEventDispatcher } from 'svelte';
	import Glide from '@glidejs/glide';
	import { Play, Heart, ChevronLeft, ChevronRight } from 'lucide-svelte';

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
												<Play size={20} fill="currentColor" />
												<span>Cek Sekarang</span>
											</button>

											<button
												class="bg-opacity-80 flex items-center space-x-2 rounded-lg bg-gray-700 px-8 py-3 font-semibold text-white transition-colors hover:bg-gray-600"
											>
												<Heart size={20} />
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
			<button
				class="glide__arrow glide__arrow--left bg-opacity-50 hover:bg-opacity-75 pointer-events-auto rounded-full bg-black p-3 text-white transition-all"
				data-glide-dir="<"
			>
				<ChevronLeft size={24} />
			</button>
			<button
				class="glide__arrow glide__arrow--right bg-opacity-50 hover:bg-opacity-75 pointer-events-auto rounded-full bg-black p-3 text-white transition-all"
				data-glide-dir=">"
				aria-label="Next slide"
			>
				<ChevronRight size={24} />
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
