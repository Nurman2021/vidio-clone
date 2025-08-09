<script>
	import '../app.css';
	import Header from './Header.svelte';
	import SkeletonLoader from './components/SkeletonLoader.svelte';
	import { onMount } from 'svelte';

	let isInitialLoading = true;

	onMount(() => {
		// Quick header load simulation
		setTimeout(() => {
			isInitialLoading = false;
		}, 500);
	});
</script>

<div class="app min-h-screen bg-[#0c0d0f] text-white">
	{#if isInitialLoading}
		<!-- Header Skeleton -->
		<div class="animate-pulse bg-gray-800 px-4 py-4">
			<div class="mx-auto flex max-w-7xl items-center justify-between">
				<div class="h-8 w-24 rounded bg-gray-600"></div>
				<div class="hidden space-x-6 md:flex">
					{#each Array(6) as _}
						<div class="h-6 w-16 rounded bg-gray-700"></div>
					{/each}
				</div>
				<div class="flex items-center space-x-4">
					<div class="h-8 w-32 rounded bg-gray-700"></div>
					<div class="h-8 w-24 rounded bg-gray-600"></div>
					<div class="h-8 w-8 rounded-full bg-gray-600"></div>
				</div>
			</div>
		</div>
	{:else}
		<Header />
	{/if}

	<main class="flex-1">
		<slot />
	</main>

	<footer class="bg-gray-800 px-4 py-8">
		<div class="mx-auto max-w-6xl text-center">
			<p class="text-gray-400">© 2025 Vidio Clone. All rights reserved.</p>
		</div>
	</footer>
</div>
