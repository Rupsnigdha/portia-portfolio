<script lang="ts">
	import { fade, scale } from 'svelte/transition';
	import { onMount } from 'svelte';
	import Img1 from '$lib/assets/1.jpeg';
	import Img2 from '$lib/assets/2.png';
	import Img3 from '$lib/assets/3.png';
	import Img4 from '$lib/assets/4.jpeg';
	import Img5 from '$lib/assets/5.jpeg';
	import Img6 from '$lib/assets/6.jpeg';
	import Img7 from '$lib/assets/7.png';
	import Img8 from '$lib/assets/8.jpeg';
	import Img9 from '$lib/assets/9.jpeg';
	import Img10 from '$lib/assets/10.jpeg';
	import Img11 from '$lib/assets/11.jpeg';
	import Img12 from '$lib/assets/12.jpeg';

	const categories = [
		'All',
		'Social Media',
		'Logos and Tattoos',
		'Posters',
		'Photoshop',
		'UI',
		'Typography'
	];

	let activeCategory = $state('All');
	let showOverlay = $state(false);
	let selectedImage = $state('');

	// Add this for controlling body scroll
	onMount(() => {
		return () => {
			// Ensure scroll is re-enabled when component is destroyed
			document.body.classList.remove('no-scroll');
		}
	});

	function openImageOverlay(image: string) {
		selectedImage = image;
		showOverlay = true;
		// Disable scroll
		document.body.classList.add('no-scroll');
	}

	function closeImageOverlay() {
		showOverlay = false;
		// Re-enable scroll
		document.body.classList.remove('no-scroll');
	}

	interface Design {
		img: string;
		category: string[];
	}
	const designs: Design[] = [
		{
			img: Img1,
			category: ['Social Media']
		},
		{
			img: Img2,
			category: ['Social Media']
		},
		{
			img: Img3,
			category: ['Social Media']
		},
		{
			img: Img4,
			category: ['Social Media']
		},
		{
			img: Img5,
			category: ['Logos and Tattoos']
		},
		{
			img: Img6,
			category: ['Logos and Tattoos']
		},
		{
			img: Img7,
			category: ['Posters']
		},
		{
			img: Img8,
			category: ['Posters']
		},
		{
			img: Img9,
			category: ['Photoshop']
		},
		{
			img: Img10,
			category: ['Photoshop']
		},
		{
			img: Img11,
			category: ['UI']
		},
		{
			img: Img12,
			category: ['Typography']
		}
	];
</script>

<!-- Image Overlay -->
{#if showOverlay}
<div 
	class="fixed inset-0 bg-black/80 z-50 flex justify-center p-4 md:p-8 cursor-pointer" 
	onclick={closeImageOverlay}
	transition:fade={{ duration: 200 }}
>
		<img 
            src={selectedImage} 
            alt="Selected work" 
            onclick={(e) => {e.preventDefault()}}
            class="max-w-full max-h-full object-contain cursor-default" 
        />
	</div>
{/if}

<section class="container mx-auto flex h-screen items-center px-4 text-[#A75F37]">
	<div class="flex flex-col">
		<p class="">Hey, I'm</p>
		<h2 class="font-lora mb-4 text-4xl">Portia</h2>
		<p class="max-w-sm text-[#CA8E82]">
			Lorem ipsum, dolor sit amet consectetur adipisicing elit. Fuga asperiores, optio in illo
			dolorum modi quam excepturi fugit ipsa vero dolor debitis incidunt recusandae, nisi
			consectetur dolorem, nostrum dicta. Facilis.
		</p>
		<a
			href="#showcase"
			class="font-lora relative mt-4 block self-start bg-[#A75F37] px-8 py-2 text-[#f2e7dd] transition-all hover:bg-[#8d441d]"
			>View my works!
			<div class="absolute top-1 -right-1 -z-10 h-full w-full bg-[#CA8E82]"></div>
		</a>
	</div>
</section>

<section id="showcase" class="container mx-auto px-4 py-20">
	<h2 class="font-lora mb-4 text-4xl text-[#A75F37]">Portfolio</h2>
	<div class="mt-4 flex gap-4 flex-wrap" >
		{#each categories as category}
			<button
				class="font-lora relative block cursor-pointer bg-[#A75F37] px-4 py-1 text-[#f2e7dd] transition-colors hover:bg-[#8d441d]"
				class:chip-highlight={activeCategory === category}
				onclick={() => {
					activeCategory = category;
				}}
				>{category}
				<div class="absolute top-1 -right-1 -z-10 h-full w-full bg-[#CA8E82]"></div>
			</button>
		{/each}
	</div>
	<div class="mt-8 grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
		{#each designs.filter(design => activeCategory === 'All' || design.category.includes(activeCategory)) as design (design.img)}
				<div 
					class="w-full h-auto aspect-square overflow-hidden border border-[#A75F37] hover:bg-[#CA8E82] cursor-pointer transition-all p-8 md:p-4 xl:p-6 2xl:p-8"
					onclick={() => openImageOverlay(design.img)}
				>
					<div class="w-full h-full relative">
						<div class="absolute w-full h-0.25 top-0 z-10 bg-[#A75F37] transform scale-x-105 origin-center"></div>
						<div class="absolute w-full h-0.25 bottom-0 z-10 bg-[#A75F37] transform scale-x-105 origin-center"></div>
						<div class="absolute h-full w-0.25 left-0 z-10 bg-[#A75F37] transform scale-y-105 origin-center"></div>
						<div class="absolute h-full w-0.25 right-0 z-10 bg-[#A75F37] transform scale-y-105 origin-center"></div>
						<img src={design.img} alt="" class="object-cover w-full h-full" />
					</div>
				</div>
		{/each}
	</div>
</section>

<style>
	.chip-highlight {
		background-color: #8d441d;
	}
	
	:global(body.no-scroll) {
		overflow: hidden;
	}
</style>
