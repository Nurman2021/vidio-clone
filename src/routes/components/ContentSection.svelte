<script>
	import { onMount, createEventDispatcher } from 'svelte';
	import Glide from '@glidejs/glide';
	import { ChevronLeft, Play, ChevronRight } from 'lucide-svelte';

	export let title = '';
	export let content = [];
	export let type = 'grid'; // 'grid', 'ranked', 'continue'

	const dispatch = createEventDispatcher();
	let glideElement;
	let glideInstance;

	onMount(() => {
		if (glideElement && content.length > 0) {
			glideInstance = new Glide(glideElement, {
				type: 'carousel',
				perView: type === 'ranked' ? 6 : 5,
				gap: 20,
				bound: true,
				breakpoints: {
					1200: { perView: type === 'ranked' ? 4 : 3 },
					768: { perView: type === 'ranked' ? 3 : 2 },
					480: { perView: 1 }
				}
			});

			glideInstance.mount();
		}

		return () => {
			if (glideInstance) {
				glideInstance.destroy();
			}
		};
	});

	function playContent(item) {
		dispatch('playVideo', item);
	}
</script>

<div class="py-8">
	<div class="mb-6 flex items-center justify-between">
		<h2 class="text-2xl font-bold text-white">{title}</h2>
		{#if content.length > 5}
			<button class="flex items-center space-x-1 text-red-400 hover:text-red-300">
				<span>Lihat Semua</span>
				<ChevronRight size={16} />
			</button>
		{/if}
	</div>

	<div bind:this={glideElement} class="glide">
		<div class="glide__track" data-glide-el="track">
			<ul class="glide__slides">
				{#each content as item, index}
					<li class="glide__slide">
						<button class="w-full cursor-pointer text-left" on:click={() => playContent(item)}>
							<div class="hover-container relative overflow-hidden rounded-lg">
								{#if type === 'ranked'}
									<div class="absolute top-2 left-2 z-10">
										<div class="rounded bg-red-600 px-3 py-1 text-3xl font-bold text-white">
											{item.rank}
										</div>
									</div>
								{/if}

								<img
									src={item.image}
									alt={item.title}
									class="w-full {type === 'ranked'
										? 'aspect-[3/4]'
										: type === 'continue'
											? 'aspect-video'
											: 'aspect-video'} object-cover transition-transform duration-300 hover:scale-105"
									loading="lazy"
								/>

								{#if type === 'continue'}
									<div
										class="absolute right-0 bottom-0 left-0 bg-gradient-to-t from-black to-transparent p-4"
									>
										<div class="mb-2 h-1 rounded-full bg-gray-300">
											<div
												class="h-full rounded-full bg-red-600"
												style="width: {Math.random() * 70 + 10}%"
											></div>
										</div>
										<p class="text-sm text-white">
											{Math.floor(Math.random() * 40 + 10)} menit tersisa
										</p>
									</div>
								{/if}

								<div
									class="hover-overlay absolute inset-0 flex items-center justify-center transition-all duration-300 hover:bg-black/0"
								>
									<div
										class="hover-play-button opacity-0 transition-opacity duration-300 hover:opacity-100"
									>
										<div class="bg-opacity-20 rounded-full bg-white p-3 text-black">
											<Play size={32} fill="currentColor" />
										</div>
									</div>
								</div>
							</div>

							<div class="mt-3">
								<h3 class="text-lg font-semibold text-white transition-colors hover:text-red-400">
									{item.title}
								</h3>
								{#if item.genre}
									<p class="mt-1 text-sm text-gray-400">{item.genre}</p>
								{/if}
								{#if item.year}
									<p class="text-sm text-gray-400">{item.year}</p>
								{/if}
							</div>
						</button>
					</li>
				{/each}
			</ul>
		</div>

		{#if content.length > 5}
			<div class="glide__arrows mt-4" data-glide-el="controls">
				<button
					class="glide__arrow glide__arrow--left absolute top-1/2 -left-12 -translate-y-1/2 transform rounded-full bg-gray-700 p-2 text-white transition-colors hover:bg-gray-600"
					data-glide-dir="<"
					aria-label="Previous slide"
				>
					<ChevronLeft size={20} />
				</button>
				<button
					class="glide__arrow glide__arrow--right absolute top-1/2 -right-12 -translate-y-1/2 transform rounded-full bg-gray-700 p-2 text-white transition-colors hover:bg-gray-600"
					data-glide-dir=">"
					aria-label="Next slide"
				>
					<ChevronRight size={20} />
				</button>
			</div>
		{/if}
	</div>
</div>
