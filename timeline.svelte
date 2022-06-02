<script>
	import { onMount } from 'svelte';

	let timelineList = [
		{ year: '2018', desc: 'Lorem1 ipsum dolor sit amet consectetuer adipiscing' },
		{ year: '2019', desc: 'Lorem2 ipsum dolor sit amet consectetuer adipiscing' },
		{ year: '2020', desc: 'Lorem3 ipsum dolor sit amet consectetuer adipiscing' },
		{ year: '2021', desc: 'Lorem4 ipsum dolor sit amet consectetuer adipiscing' },
		{ year: '2022', desc: 'Lorem5 ipsum dolor sit amet consectetuer adipiscing' },
		{ year: '2023', desc: 'Lorem6 ipsum dolor sit amet consectetuer adipiscing' },
		{ year: '2024', desc: 'Lorem7 ipsum dolor sit amet consectetuer adipiscing' },
		{ year: '2025', desc: 'Lorem8 ipsum dolor sit amet consectetuer adipiscing' },
		{ year: '2026', desc: 'Lorem9 ipsum dolor sit amet consectetuer adipiscing' },
		{ year: '2027', desc: 'Lorem10 ipsum dolor sit amet consectetuer adipiscing' },
		{ year: '2028', desc: 'Lorem11 ipsum dolor sit amet consectetuer adipiscing' },
		{ year: '2029', desc: 'Lorem12 ipsum dolor sit amet consectetuer adipiscing' },
		{ year: '2030', desc: 'Lorem ipsum dolor sit amet consectetuer adipiscing' }
	];
	var currentPage = 0;
	var largeScreen;
	var itemsPerPage;
	var totalPage;
	function nextPage(n) {
		currentPage += n;
		var slides = document.getElementsByClassName('slides');
		for (let i = 0; i < slides.length; i++) {
			slides[i].style.display = 'none';
		}
		slides[currentPage].style.display = 'inline-flex';
		if(slides[currentPage].classList.contains('animate-left')){
			slides[currentPage].classList.remove('animate-left');
		}
		if(slides[currentPage].classList.contains('animate-right')){
			slides[currentPage].classList.remove('animate-right');
		}
		if(n == -1){
			slides[currentPage].classList.add('animate-left');
		}
		else{
			slides[currentPage].classList.add('animate-right');
		}
		
	}
	onMount(() => {
		const screenSize = window.innerWidth > 0 ? window.innerWidth : window.screen.width;
		largeScreen = screenSize > 1024 ? 4 : 2;
		itemsPerPage = largeScreen;
		totalPage = Math.ceil(timelineList.length / largeScreen);
	});
</script>

<!-- --slider-- -->

<div>
	<div class=" flex justify-between">
		<h1 class="text-xl text-custom-dark lg:text-3xl font-bold text-center">Our Timeline</h1>
		<div class=" inline-flex gap-5">
			{#if currentPage > 0}
				<div class="rounded-full control p-4" on:click={() => nextPage(-1)}>
					<img src="./left.png" alt="" />
				</div>
			{/if}
			{#if currentPage < totalPage - 1}
				<div class="rounded-full control p-4" on:click={() => nextPage(1)}>
					<img class="rotate-180" src="./left.png" alt="" />
				</div>
			{/if}
		</div>
	</div>
	<div class="overflow-hidden">
		{#each Array(totalPage) as _, t}
			<div class={`slides mt-10 grid-cols-2 lg:grid-cols-4 grid ${t == 0 ? 'animate-left' : 'hidden'}`}>
				{#each Array(itemsPerPage) as _, i}
					{#if timelineList[currentPage * largeScreen + i]}
						<div class={`bottom-green pb-12 relative mb-5`}>
							<div class=" text-xl text-custom-linegreen font-semibold">
								{timelineList[currentPage * largeScreen + i].year}
							</div>
							<div class=" mt-3 text-xl text-custom-dark opacity-70 subHeading w-3/4">
								{timelineList[currentPage * i].desc}
							</div>
							<div class="absolute bottom-[-10px]">
								<div class=" bg-custom-linegreen rounded-full  h-5 w-5" />
							</div>
						</div>
					{/if}
				{/each}
			</div>
		{/each}
	</div>
</div>

<style>
	.control {
		background-color: theme('colors.custom.midgreen3');
		cursor: pointer;
	}
	.control:hover {
		background-color: theme('colors.custom.midgreen');
	}
	.control:hover img {
		filter: brightness(0) invert(1);
	}
	.rotate-180 {
		-webkit-transform: rotate(180deg);
		-moz-transform: rotate(180deg);
		-ms-transform: rotate(180deg);
		-o-transform: rotate(180deg);
		transform: rotate(180deg);
	}
	.bottom-green {
		border-bottom: 1px solid #52b43b;
	}
	.animate-left {
		position: relative;
		animation: animateleft 1s;
	}
	@keyframes animateleft {
		from {
			left: -100px;
			opacity: 0;
		}
		to {
			left: 0;
			opacity: 1;
		}
	}
	.animate-right {
		position: relative;
		animation: animateright 1s;
	}
	@keyframes animateright {
		from {
			right: -100px;
			opacity: 0;
		}
		to {
			right: 0;
			opacity: 1;
		}
	}
</style>
