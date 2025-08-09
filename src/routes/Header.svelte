<script>
	import { page } from '$app/stores';
	import { ChevronDown, Search, User, Menu } from 'lucide-svelte';

	let searchQuery = '';
	let isMenuOpen = false;
</script>

<header class="sticky top-0 z-50 bg-[#18191d] shadow-lg">
	<div class="mx-auto w-full px-4 sm:px-6 lg:px-8">
		<div class="flex h-16 items-center justify-between">
			<!-- Left Side: Logo and Navigation Menu -->
			<div class="flex items-center gap-8">
				<!-- Logo -->
				<a href="/" class="flex items-center">
					<div class="rounded bg-red-600 px-4 py-2 text-xl font-bold text-white">Vidio</div>
				</a>

				<!-- Navigation Menu - Only visible on md and up -->
				<nav class="hidden space-x-6 text-sm font-medium md:flex">
					<a href="/" class="py-2 text-white transition-colors hover:text-red-400">Home</a>
					<button class="py-2 text-white transition-colors hover:text-red-400">Live</button>
					<button class="py-2 text-white transition-colors hover:text-red-400">Sports</button>
					<button class="py-2 text-white transition-colors hover:text-red-400">Series</button>
					<button class="py-2 text-white transition-colors hover:text-red-400">Movies</button>
					<button class="py-2 text-white transition-colors hover:text-red-400">TV Show</button>
					<button
						class="flex items-center gap-1 py-2 text-white transition-colors hover:text-red-400"
						>Lainnya <ChevronDown size={14} />
					</button>
				</nav>
			</div>

			<!-- Right Side: Search Bar, Subscribe Button, User Menu -->
			<div class="flex items-center space-x-4">
				<!-- Search Bar - Only visible on md and up -->
				<div class="hidden md:block">
					<div class="relative">
						<input
							bind:value={searchQuery}
							type="text"
							placeholder="Nonton apa hari ini?"
							class="w-80 rounded-lg bg-[#26292e] px-4 py-2.5 pr-10 text-sm text-white placeholder-gray-400 focus:ring-2 focus:ring-red-500 focus:outline-none lg:w-96"
						/>
						<button
							class="absolute top-1/2 right-3 -translate-y-1/2 text-gray-400 transition-colors hover:text-white"
							aria-label="Search"
						>
							<Search size={18} />
						</button>
					</div>
				</div>

				<!-- Subscribe Button -->
				<button
					class="hidden rounded-lg border border-orange-500 px-4 py-2 text-sm font-semibold text-orange-500 transition-all hover:bg-orange-500 hover:text-white md:block"
				>
					LANGGANAN
				</button>

				<!-- User Menu -->
				<div class="relative">
					<button
						class="flex items-center space-x-2 text-white transition-colors hover:text-red-400"
					>
						<div class="flex h-8 w-8 items-center justify-center rounded-full bg-gray-600">
							<User size={18} />
						</div>
						<span class="hidden md:block">Masuk</span>
						<ChevronDown size={14} class="hidden md:block" />
					</button>
				</div>

				<!-- Mobile menu button -->
				<button
					on:click={() => (isMenuOpen = !isMenuOpen)}
					class="p-2 text-white hover:text-red-400 focus:outline-none md:hidden"
					aria-label="Toggle mobile menu"
				>
					<Menu size={20} />
				</button>
			</div>
		</div>
	</div>

	<!-- Mobile menu -->
	{#if isMenuOpen}
		<div class="mobile-menu-enter border-t border-gray-600 bg-[#18191d] md:hidden">
			<!-- Mobile Search -->
			<div class="px-4 py-3">
				<div class="relative">
					<input
						bind:value={searchQuery}
						type="text"
						placeholder="Nonton apa hari ini?"
						class="w-full rounded-lg bg-[#26292e] px-4 py-2.5 pr-10 text-sm text-white placeholder-gray-400 focus:ring-2 focus:ring-red-500 focus:outline-none"
					/>
					<button
						class="absolute top-1/2 right-3 -translate-y-1/2 text-gray-400 transition-colors hover:text-white"
						aria-label="Search"
					>
						<Search size={18} />
					</button>
				</div>
			</div>

			<!-- Mobile Navigation -->
			<nav class="space-y-1 px-4 pb-4">
				<a
					href="/"
					class="block border-b border-gray-700 py-3 text-white transition-colors hover:text-red-400"
					>Home</a
				>
				<button
					class="block w-full border-b border-gray-700 py-3 text-left text-white transition-colors hover:text-red-400"
					>Live</button
				>
				<button
					class="block w-full border-b border-gray-700 py-3 text-left text-white transition-colors hover:text-red-400"
					>Sports</button
				>
				<button
					class="block w-full border-b border-gray-700 py-3 text-left text-white transition-colors hover:text-red-400"
					>Series</button
				>
				<button
					class="block w-full border-b border-gray-700 py-3 text-left text-white transition-colors hover:text-red-400"
					>Movies</button
				>
				<button
					class="block w-full border-b border-gray-700 py-3 text-left text-white transition-colors hover:text-red-400"
					>TV Show</button
				>
				<button
					class="block w-full border-b border-gray-700 py-3 text-left text-white transition-colors hover:text-red-400"
					>Lainnya</button
				>

				<!-- Mobile Subscribe Button -->
				<div class="pt-4">
					<button
						class="w-full rounded-lg border border-orange-500 px-4 py-3 text-sm font-semibold text-orange-500 transition-all hover:bg-orange-500 hover:text-white"
					>
						LANGGANAN
					</button>
				</div>
			</nav>
		</div>
	{/if}
</header>
