<script>
	export let size = 'md'; // 'sm', 'md', 'lg'
	export let color = 'red';

	const sizeClasses = {
		sm: 'w-4 h-4',
		md: 'w-8 h-8',
		lg: 'w-12 h-12'
	};

	const colorClasses = {
		red: 'border-red-500',
		white: 'border-white',
		gray: 'border-gray-500'
	};
</script>

<div class="flex items-center justify-center">
	<div class="animate-spin rounded-full {sizeClasses[size]} border-b-2 {colorClasses[color]}"></div>
</div>
