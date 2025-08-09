<script>
	import { page } from '$app/stores';

	let searchQuery = '';
	let isMenuOpen = false;
</script>

<header class="sticky top-0 z-50 bg-[#18191d] shadow-lg">
	<div class="mx-auto w-full px-4 sm:px-6 lg:px-8">
		<div class="flex h-14 items-center justify-between">
			<!-- Logo -->
			<div class="flex items-center gap-6">
				<a href="/" class="flex items-center">
					<div class="rounded bg-red-600 px-3 py-1 text-xl font-bold text-white">Vidio</div>
				</a>

				<!-- Navigation Menu -->
				<nav class="hidden space-x-4 text-sm font-semibold md:flex">
					<a href="/" class="text-white transition-colors hover:text-red-400">Home</a>
					<span class="cursor-pointer text-white transition-colors hover:text-red-400">Live</span>
					<span class="cursor-pointer text-white transition-colors hover:text-red-400">Sports</span>
					<span class="cursor-pointer text-white transition-colors hover:text-red-400">Series</span>
					<span class="cursor-pointer text-white transition-colors hover:text-red-400">Movies</span>
					<span class="cursor-pointer text-white transition-colors hover:text-red-400">TV Show</span
					>
					<span
						class="flex cursor-pointer items-center text-white transition-colors hover:text-red-400"
						>Lainnya <svg class="h-4 w-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="m19 9-7 7-7-7"
							></path>
						</svg>
					</span>
				</nav>
			</div>

			<!-- Search Bar -->
			<div class="flex items-center space-x-4">
				<div class="relative">
					<input
						bind:value={searchQuery}
						type="text"
						placeholder="Nonton apa hari ini?"
						class=" w-[25rem] rounded-lg bg-[#26292e] px-4 py-2 text-sm text-white focus:ring-2 focus:ring-red-500 focus:outline-none"
					/>
					<button class="absolute top-2 right-2 text-gray-400 hover:text-white" aria-label="Search">
						<svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="m21 21-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
							></path>
						</svg>
					</button>
				</div>

				<!-- User Actions -->
				<div class="flex items-center space-x-2">
					<button
						class="rounded-lg border border-orange-500 px-2 py-1 text-xs font-semibold text-orange-500 transition-colors hover:bg-orange-600 hover:text-white"
					>
						LANGGANAN
					</button>
					<div class="relative">
						<button class="flex items-center space-x-2 text-white hover:text-red-400">
							<div class="flex h-8 w-8 items-center justify-center rounded-full bg-gray-600">
								<svg class="h-5 w-5" fill="currentColor" viewBox="0 0 20 20">
									<path
										fill-rule="evenodd"
										d="M10 9a3 3 0 100-6 3 3 0 000 6zm-7 9a7 7 0 1114 0H3z"
										clip-rule="evenodd"
									></path>
								</svg>
							</div>
							<span>Masuk</span>
							<svg class="h-4 w-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="m19 9-7 7-7-7"
								></path>
							</svg>
						</button>
					</div>
				</div>
			</div>

			<!-- Mobile menu button -->
			<div class="md:hidden">
				<button
					on:click={() => (isMenuOpen = !isMenuOpen)}
					class="text-white hover:text-red-400 focus:outline-none"
					aria-label="Toggle mobile menu"
				>
					<svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
						<path
							stroke-linecap="round"
							stroke-linejoin="round"
							stroke-width="2"
							d="M4 6h16M4 12h16M4 18h16"
						></path>
					</svg>
				</button>
			</div>
		</div>
	</div>

	<!-- Mobile menu -->
	{#if isMenuOpen}
		<div class="space-y-2 bg-gray-700 px-4 py-2 md:hidden">
			<a href="/" class="block py-2 text-white hover:text-red-400">Home</a>
			<a href="/live" class="block py-2 text-white hover:text-red-400">Live</a>
			<a href="/sports" class="block py-2 text-white hover:text-red-400">Sports</a>
			<a href="/series" class="block py-2 text-white hover:text-red-400">Series</a>
			<a href="/movies" class="block py-2 text-white hover:text-red-400">Movies</a>
			<a href="/tv-show" class="block py-2 text-white hover:text-red-400">TV Show</a>
		</div>
	{/if}
</header>
