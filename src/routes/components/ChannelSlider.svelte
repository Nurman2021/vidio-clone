<script>
	import { onMount } from 'svelte';
	import Glide from '@glidejs/glide';
	import { Calendar, Tv, Radio, Camera } from 'lucide-svelte';

	let glideElement;
	let glideInstance;

	const channels = [
		{ name: 'Lihat Jadwal', icon: 'calendar', bgColor: 'bg-orange-500' },
		{ name: 'Daftar Channel', icon: 'tv', bgColor: 'bg-purple-600' },
		{ name: 'SCTV', icon: 'SCTV', bgColor: 'bg-blue-500' },
		{ name: 'Indosiar', icon: 'IND', bgColor: 'bg-yellow-500' },
		{ name: 'Moji', icon: 'MOJI', bgColor: 'bg-blue-400' },
		{ name: 'ANTV', icon: 'ANTV', bgColor: 'bg-pink-500' },
		{ name: 'TRANS TV', icon: 'TTV', bgColor: 'bg-cyan-500' },
		{ name: 'TVOne', icon: 'TV1', bgColor: 'bg-red-600' },
		{ name: 'Trans7', icon: 'T7', bgColor: 'bg-blue-700' },
		{ name: 'Metro TV', icon: 'MTV', bgColor: 'bg-gray-500' }
	];

	onMount(() => {
		if (glideElement) {
			glideInstance = new Glide(glideElement, {
				type: 'carousel',
				perView: 8,
				gap: 20,
				autoplay: 3000,
				hoverpause: true,
				breakpoints: {
					1200: { perView: 6 },
					768: { perView: 4 },
					480: { perView: 2 }
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
</script>

<div class="bg-gray-800 py-8">
	<div class="mx-auto max-w-7xl px-4">
		<div bind:this={glideElement} class="glide">
			<div class="glide__track" data-glide-el="track">
				<ul class="glide__slides">
					{#each channels as channel}
						<li class="glide__slide">
							<div class="flex cursor-pointer flex-col items-center">
								<div
									class="h-16 w-16 {channel.bgColor} my-4 mb-2 flex items-center justify-center rounded-full transition-transform hover:scale-110"
								>
									{#if channel.icon === 'calendar'}
										<Calendar size={24} color="white" />
									{:else if channel.icon === 'tv'}
										<Tv size={24} color="white" />
									{:else if channel.icon.length > 2}
										<span class="text-xs font-bold text-white">{channel.icon}</span>
									{:else}
										<span class="text-2xl">{channel.icon}</span>
									{/if}
								</div>
								<span class="text-center text-sm text-white">{channel.name}</span>
							</div>
						</li>
					{/each}
				</ul>
			</div>
		</div>
	</div>
</div>
