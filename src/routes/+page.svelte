<script>
	import { onMount } from 'svelte';
	import HeroSlider from './components/HeroSlider.svelte';
	import ChannelSlider from './components/ChannelSlider.svelte';
	import ContentSection from './components/ContentSection.svelte';
	import VideoModal from './components/VideoModal.svelte';
	import SkeletonLoader from './components/SkeletonLoader.svelte';

	let showVideoModal = false;
	let currentVideo = null;
	let isLoading = true;

	function openVideoModal(video) {
		currentVideo = video;
		showVideoModal = true;
	}

	function closeVideoModal() {
		showVideoModal = false;
		currentVideo = null;
	}

	// Simulate loading data
	onMount(async () => {
		// Simulate API call delay
		await new Promise((resolve) => setTimeout(resolve, 2000));
		isLoading = false;
	});

	// Sample data with reliable image URLs
	const featuredContent = [
		{
			id: 1,
			title: 'GASPOL',
			subtitle: 'Komedi',
			description: 'Setiap Hari • 07:00 WIB | Seru-seruan bareng Raffi Ahmad dalam program GASPOL!',
			image:
				'https://thumbor.prod.vidiocdn.com/3-1bZnGRJToByAgeWEK-lpfcVL0=/1495x526/filters:quality(75)/vidio-web-prod-headline/uploads/headline/premium_image/32290/liyan-zeff-vs-sabreena-dressler-4af1e1.jpg',
			videoUrl: 'https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny.mp4'
		},
		{
			id: 2,
			title: 'S Line',
			subtitle: 'Thriller • Mystery',
			description:
				'Garis merah misterius muncul di atas kepala orang, menghubungkan mereka yang pernah berhubungan seksual.',
			image:
				'https://thumbor.prod.vidiocdn.com/l04raoRNz0TIyhlqY5NE3MBY7wI=/1495x526/filters:quality(75)/vidio-web-prod-headline/uploads/headline/premium_image/32191/everton-vs-roma-76d7e8.jpg',
			videoUrl:
				'https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ElephantsDream.mp4'
		},
		{
			id: 3,
			title: "Guy Ritchie's The Covenant",
			subtitle: 'Action • War',
			description:
				'Setelah diselamatkan oleh penerjemah lokal Ahmed di Afghanistan, Sergeant Kinley kembali.',
			image:
				'https://thumbor.prod.vidiocdn.com/UeUkfCd4Rj-PtI1YlmwhZRADz3k=/1495x526/filters:quality(75)/vidio-web-prod-film/uploads/film/desktop_headline_image/11487/guy-ritchie-s-the-covenant-9c5f1e.png',
			videoUrl:
				'https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerBlazes.mp4'
		},
		{
			id: 4,
			title: 'Fortuna Sittard vs Go Ahead Eagles',
			subtitle: 'Live • Football • Eredivisie 2025/26',
			description:
				'9 AGU • 01:00 WIB | Menikmati rasa tim di negara sendiri, mamputkah Dean James cs mengalahkan tuan rumah Fortuna Sittard?',
			image:
				'https://thumbor.prod.vidiocdn.com/BTIwhcdynlzhId1UMQ0Pfab71H4=/1495x526/filters:quality(75)/vidio-web-prod-film/uploads/film/desktop_headline_image/9790/kaiju-no-8-77deb3.jpg',
			videoUrl:
				'https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerEscapes.mp4'
		}
	];

	const topWeekContent = [
		{
			id: 1,
			title: 'Cinta Dalam Gulduru',
			rank: 1,
			image:
				'https://thumbor.prod.vidiocdn.com/JamV8bVBDU-gDEJSLXO4snvxnOc=/288x416/filters:quality(70)/vidio-media-production/uploads/image/source/21222/c54bcb.png',
			videoUrl: 'https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny.mp4'
		},
		{
			id: 2,
			title: 'Dilan & Milea',
			rank: 2,
			image:
				'https://thumbor.prod.vidiocdn.com/OYUTSzaJKYgsX-Dy2w9yTbwS4fg=/288x416/filters:quality(70)/vidio-media-production/uploads/image/source/20745/3c3bc3.jpg',
			videoUrl:
				'https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ElephantsDream.mp4'
		},
		{
			id: 3,
			title: 'Fast & Furious',
			rank: 3,
			image:
				'https://thumbor.prod.vidiocdn.com/qdLE_Tzi1rLE0yED08Y1h88_zFg=/288x416/filters:quality(70)/vidio-media-production/uploads/image/source/46143/eaa578.jpg',
			videoUrl:
				'https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerBlazes.mp4'
		},
		{
			id: 4,
			title: 'S Line',
			rank: 4,
			image:
				'https://thumbor.prod.vidiocdn.com/euATbIQT-LBh7rT2nnkxdsdwMs8=/288x416/filters:quality(75)/vidio-media-production/uploads/image/source/43374/dbd42c.png',
			videoUrl:
				'https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerEscapes.mp4'
		},
		{
			id: 5,
			title: 'Alibi.com',
			rank: 5,
			image:
				'https://thumbor.prod.vidiocdn.com/hHFM5pBITaxQthXa6Ux_cVCEFNQ=/288x416/filters:quality(70)/vidio-web-prod-film/uploads/film/image_portrait/11219/no-way-up-a19d7d.jpg',
			videoUrl:
				'https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerJoyrides.mp4'
		},
		{
			id: 6,
			title: 'Cerita Cinta',
			rank: 6,
			image:
				'https://thumbor.prod.vidiocdn.com/SencfupbNa1z83TRo_CAFQLekbA=/288x416/filters:quality(70)/vidio-media-production/uploads/image/source/30928/2a3f44.jpg',
			videoUrl:
				'https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerMeltdowns.mp4'
		}
	];

	const recentlyAdded = [
		{
			id: 1,
			title: 'The Covenant',
			image:
				'https://thumbor.prod.vidiocdn.com/D92C2P-jz8OTGUcTgRDnzr8F-0Q=/640x360/filters:quality(70)/vidio-web-prod-film/uploads/film/image_landscape/11473/the-noisy-mansion-109c9a.jpg',
			videoUrl: 'https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny.mp4'
		},
		{
			id: 2,
			title: 'Dora The Explorer',
			image:
				'https://thumbor.prod.vidiocdn.com/3EwZ5pf7K8kU25qM5CIsBEZb1-k=/640x360/filters:quality(70)/vidio-web-prod-film/uploads/film/image_landscape/11418/ketua-bem-and-his-secret-wife-fe3d5e.png',
			videoUrl:
				'https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ElephantsDream.mp4'
		},
		{
			id: 3,
			title: 'Action Movie',
			image:
				'https://thumbor.prod.vidiocdn.com/ib9sO6Hzen_7e9CD62CRB2iSmpM=/640x360/filters:quality(70)/vidio-web-prod-film/uploads/film/image_landscape/11470/harbin-fe20d8.jpg',
			videoUrl:
				'https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerBlazes.mp4'
		},
		{
			id: 4,
			title: 'Comedy Show',
			image:
				'https://thumbor.prod.vidiocdn.com/QyTB0hisyb_qxFolfF3-9Ct0QUY=/640x360/filters:quality(70)/vidio-web-prod-film/uploads/film/image_landscape/11316/shanghai-affairs-7f033d.png',
			videoUrl:
				'https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerEscapes.mp4'
		},
		{
			id: 5,
			title: 'My Lovely Neighbor',
			image:
				'https://thumbor.prod.vidiocdn.com/s4CwWNyO1_AL5ktqTswCr8IcBOU=/640x360/filters:quality(70)/vidio-media-production/uploads/image/source/47482/9b634f.jpg',
			videoUrl:
				'https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerJoyrides.mp4'
		},
		{
			id: 6,
			title: 'Love Take Two',
			image:
				'https://thumbor.prod.vidiocdn.com/qrZY3c3GPuT1ONBH-uj0IfVbS-U=/640x360/filters:quality(70)/vidio-web-prod-film/uploads/film/image_landscape/11582/mendadak-dangdut-84e8bc.jpg',
			videoUrl:
				'https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerMeltdowns.mp4'
		},
		{
			id: 7,
			title: 'My Lovely Journey',
			image:
				'https://thumbor.prod.vidiocdn.com/lRDajmyyjSpzDQNTaiskW8An_ew=/640x360/filters:quality(70)/vidio-web-prod-film/uploads/film/image_landscape/11456/setengah-hati-08f7ea.jpg',
			videoUrl: 'https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/Sintel.mp4'
		}
	];
</script>

<svelte:head>
	<title>Vidio Clone - Nonton apa hari ini?</title>
	<meta name="description" content="Platform streaming video terbaik di Indonesia" />
</svelte:head>

<div class="min-h-screen bg-gray-900">
	{#if isLoading}
		<!-- Loading Skeleton -->
		<SkeletonLoader type="hero" />
		<SkeletonLoader type="channel" />

		<div class="mx-auto max-w-7xl space-y-8 px-4 py-8">
			<SkeletonLoader type="section" />
			<SkeletonLoader type="section" />

			<!-- Sports Packages Skeleton -->
			<div class="my-8 animate-pulse rounded-lg bg-gray-700 p-6">
				<div class="mb-4 h-8 w-64 rounded bg-gray-600"></div>
				<div class="grid grid-cols-1 gap-4 md:grid-cols-3">
					{#each Array(3) as _}
						<div class="rounded-lg bg-gray-600 p-4">
							<div class="mb-2 h-4 w-32 rounded bg-gray-500"></div>
							<div class="mb-2 h-6 w-48 rounded bg-gray-500"></div>
							<div class="mb-2 h-3 w-24 rounded bg-gray-500"></div>
							<div class="mb-4 h-8 w-20 rounded bg-gray-500"></div>
							<div class="h-10 w-32 rounded bg-gray-500"></div>
						</div>
					{/each}
				</div>
			</div>

			<SkeletonLoader type="section" />
		</div>
	{:else}
		<!-- Hero Slider -->
		<HeroSlider content={featuredContent} on:playVideo={(e) => openVideoModal(e.detail)} />

		<!-- Channel Slider -->
		<ChannelSlider />

		<!-- Content Sections -->
		<div class="mx-auto max-w-6xl space-y-8 px-4 py-8">
			<!-- Top 20 This Week -->
			<ContentSection
				title="Top 20 This Week"
				content={topWeekContent}
				type="ranked"
				on:playVideo={(e) => openVideoModal(e.detail)}
			/>

			<!-- Recently Added -->
			<ContentSection
				title="Recently Added"
				content={recentlyAdded}
				type="grid"
				on:playVideo={(e) => openVideoModal(e.detail)}
			/>

			<!-- Sports Packages -->
			<!-- <div class="my-8 rounded-lg bg-gradient-to-r from-yellow-600 to-red-600 p-6">
				<h2 class="mb-4 text-2xl font-bold">Bebas Pilih Paket Sesukamu</h2>
				<div class="grid grid-cols-1 gap-4 md:grid-cols-3">
					<div class="bg-opacity-30 rounded-lg bg-black p-4">
						<h3 class="font-bold text-yellow-400">Nonton Tayangan</h3>
						<p class="text-2xl font-bold text-yellow-400">5 Match Eksklusif Superstar</p>
						<p class="text-sm">Knockout King of The Ring</p>
						<div class="mt-2 text-3xl font-bold text-yellow-400">29.000</div>
						<button class="mt-2 rounded bg-red-600 px-4 py-2 text-white">Beli Sekarang</button>
					</div>
					<div class="bg-opacity-30 rounded-lg bg-black p-4">
						<h3 class="font-bold text-yellow-400">Nonton Tayangan</h3>
						<p class="text-2xl font-bold text-yellow-400">4 Match Eksklusif</p>
						<p class="text-sm">HW SPORT NIGHT BALI</p>
						<div class="mt-2 text-3xl font-bold text-yellow-400">29.000</div>
						<button class="mt-2 rounded bg-red-600 px-4 py-2 text-white">Beli Sekarang</button>
					</div>
					<div class="bg-opacity-30 rounded-lg bg-black p-4">
						<h3 class="font-bold text-yellow-400">LEBIH DARI 70 SPORTS</h3>
						<p class="text-2xl font-bold text-yellow-400">UNTUK SEMUA PELANGGAN</p>
						<div class="mt-2 text-3xl font-bold text-yellow-400">
							15.1 <span class="text-lg">JT</span>
						</div>
						<button class="mt-2 rounded bg-red-600 px-4 py-2 text-white">Langganan Sekarang</button>
					</div>
				</div>
			</div> -->

			<img
				src="https://thumbor.prod.vidiocdn.com/pRwmOOsvnb5mD2pk73W67AAD0vM=/1200x142/filters:quality(80)/vidio-web-prod-breaking-banner/uploads/breaking_banner/image/6023/b28973.jpg"
				alt="ads"
			/>

			<!-- Continue Watching -->
			<ContentSection
				title="Lanjut Nonton"
				content={recentlyAdded.slice(0, 5)}
				type="continue"
				on:playVideo={(e) => openVideoModal(e.detail)}
			/>
		</div>
	{/if}
</div>

<!-- Video Modal -->
{#if showVideoModal && currentVideo}
	<VideoModal video={currentVideo} on:close={closeVideoModal} />
{/if}
