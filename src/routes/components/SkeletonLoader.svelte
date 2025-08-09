<script>
	export let type = 'hero'; // 'hero', 'card', 'channel', 'list'
	export let count = 1;
</script>

{#if type === 'hero'}
	<!-- Hero Skeleton -->
	<div class="relative h-screen animate-pulse bg-gray-800">
		<div class="absolute inset-0 bg-gradient-to-r from-gray-800 to-gray-700">
			<div class="flex h-full items-center">
				<div class="mx-auto w-full max-w-7xl px-4">
					<div class="max-w-2xl space-y-4">
						<!-- Title skeleton -->
						<div class="h-12 w-3/4 rounded bg-gray-600"></div>
						<div class="h-12 w-1/2 rounded bg-gray-600"></div>

						<!-- Subtitle skeleton -->
						<div class="h-6 w-2/3 rounded bg-gray-700"></div>

						<!-- Description skeleton -->
						<div class="space-y-2">
							<div class="h-4 w-full rounded bg-gray-700"></div>
							<div class="h-4 w-5/6 rounded bg-gray-700"></div>
							<div class="h-4 w-4/5 rounded bg-gray-700"></div>
						</div>

						<!-- Buttons skeleton -->
						<div class="flex space-x-4 pt-4">
							<div class="h-12 w-32 rounded-lg bg-gray-600"></div>
							<div class="h-12 w-36 rounded-lg bg-gray-700"></div>
						</div>
					</div>
				</div>
			</div>
		</div>

		<!-- Dots indicator skeleton -->
		<div class="absolute bottom-8 left-1/2 flex -translate-x-1/2 transform space-x-2">
			{#each Array(5) as _}
				<div class="h-3 w-3 rounded-full bg-gray-600"></div>
			{/each}
		</div>
	</div>
{:else if type === 'channel'}
	<!-- Channel Slider Skeleton -->
	<div class="bg-gray-800 py-8">
		<div class="mx-auto max-w-7xl px-4">
			<div class="flex space-x-4">
				{#each Array(8) as _}
					<div class="flex animate-pulse flex-col items-center">
						<div class="mb-2 h-16 w-16 rounded-full bg-gray-600"></div>
						<div class="h-3 w-16 rounded bg-gray-700"></div>
					</div>
				{/each}
			</div>
		</div>
	</div>
{:else if type === 'card'}
	<!-- Content Card Skeleton -->
	<div class="grid grid-cols-2 gap-4 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 2xl:grid-cols-6">
		{#each Array(count) as _}
			<div class="group animate-pulse cursor-pointer">
				<!-- Image skeleton -->
				<div class="aspect-video w-full rounded-lg bg-gray-700"></div>

				<!-- Content skeleton -->
				<div class="mt-3 space-y-2">
					<div class="h-4 w-full rounded bg-gray-700"></div>
					<div class="h-3 w-3/4 rounded bg-gray-600"></div>
					<div class="h-3 w-1/2 rounded bg-gray-600"></div>
				</div>
			</div>
		{/each}
	</div>
{:else if type === 'list'}
	<!-- List Item Skeleton -->
	<div class="space-y-4">
		{#each Array(count) as _}
			<div class="flex animate-pulse space-x-4">
				<!-- Thumbnail skeleton -->
				<div class="h-20 w-32 flex-shrink-0 rounded bg-gray-700"></div>

				<!-- Content skeleton -->
				<div class="flex-1 space-y-2">
					<div class="h-4 w-full rounded bg-gray-700"></div>
					<div class="h-3 w-3/4 rounded bg-gray-600"></div>
					<div class="h-3 w-1/2 rounded bg-gray-600"></div>
				</div>
			</div>
		{/each}
	</div>
{:else if type === 'section'}
	<!-- Section with Title and Cards Skeleton -->
	<div class="animate-pulse space-y-6">
		<!-- Section title skeleton -->
		<div class="flex items-center justify-between">
			<div class="h-8 w-48 rounded bg-gray-700"></div>
			<div class="h-6 w-24 rounded bg-gray-600"></div>
		</div>

		<!-- Cards skeleton -->
		<div
			class="grid grid-cols-2 gap-4 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 2xl:grid-cols-6"
		>
			{#each Array(6) as _}
				<div class="group cursor-pointer">
					<div class="aspect-video w-full rounded-lg bg-gray-700"></div>
					<div class="mt-3 space-y-2">
						<div class="h-4 w-full rounded bg-gray-700"></div>
						<div class="h-3 w-3/4 rounded bg-gray-600"></div>
					</div>
				</div>
			{/each}
		</div>
	</div>
{:else if type === 'ranking'}
	<!-- Ranking List Skeleton -->
	<div class="space-y-4">
		{#each Array(count) as _, i}
			<div class="flex animate-pulse items-center space-x-4">
				<!-- Rank number skeleton -->
				<div class="h-8 w-8 rounded bg-gray-600"></div>

				<!-- Thumbnail skeleton -->
				<div class="h-16 w-28 flex-shrink-0 rounded bg-gray-700"></div>

				<!-- Content skeleton -->
				<div class="flex-1 space-y-2">
					<div class="h-4 w-full rounded bg-gray-700"></div>
					<div class="h-3 w-2/3 rounded bg-gray-600"></div>
				</div>
			</div>
		{/each}
	</div>
{:else if type === 'grid'}
	<!-- Grid Layout Skeleton (for movies/shows) -->
	<div class="grid grid-cols-2 gap-4 md:grid-cols-4 lg:grid-cols-6">
		{#each Array(count || 12) as _}
			<div class="animate-pulse">
				<div class="aspect-[3/4] w-full rounded-lg bg-gray-700"></div>
				<div class="mt-2 space-y-2">
					<div class="h-3 w-full rounded bg-gray-700"></div>
					<div class="h-3 w-2/3 rounded bg-gray-600"></div>
				</div>
			</div>
		{/each}
	</div>
{:else if type === 'horizontal'}
	<!-- Horizontal Scroll Skeleton -->
	<div class="flex space-x-4 overflow-hidden">
		{#each Array(count || 8) as _}
			<div class="w-64 flex-shrink-0 animate-pulse">
				<div class="aspect-video w-full rounded-lg bg-gray-700"></div>
				<div class="mt-2 space-y-2">
					<div class="h-4 w-full rounded bg-gray-700"></div>
					<div class="h-3 w-3/4 rounded bg-gray-600"></div>
				</div>
			</div>
		{/each}
	</div>
{/if}

<style>
	@keyframes pulse {
		0%,
		100% {
			opacity: 1;
		}
		50% {
			opacity: 0.5;
		}
	}

	.animate-pulse {
		animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
	}
</style>
