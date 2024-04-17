<script lang="ts">
// @ts-ignore
	import { Swipe, SwipeItem } from "svelte-swipe";
	import image1 from "$lib/images/1.jpeg"
	import image2 from "$lib/images/2.jpeg"
	import image3 from "$lib/images/3.jpeg"

	const images: string[] = [image1, image2, image3]
	const swipeConfig = {
	  autoplay: false,
	  delay: 2000,
	  transitionDuration: 200,
	  defaultIndex: 0,
	  allow_infinite_swipe: true,
	};

	let SwipeComp: Swipe;

	function nextSlide(){
		SwipeComp.nextItem()
	}

	function prevSlide(){
		SwipeComp.prevItem()
	}

	function handleSwipe(event: CustomEvent) {
		console.log(event.detail)
		// logs swipe direction and item index
	}
  </script>
  
  
  <div class="w-full h-screen flex justify-center items-center">
	<div class="w-2/3 h-[50vh] flex flex-col items-center p-3 justify-center">
		<Swipe 
			{...swipeConfig} 
			bind:this={SwipeComp}
			on:change={handleSwipe}
			>
			{#each images as image}
				<SwipeItem>
				<img src={image} alt="" class="w-full h-[40vh]">
				</SwipeItem>
			{/each}
		</Swipe>
		<div class="flex gap-4">
			<button class="btn variant-ghost-primary" on:click={prevSlide}>Prev</button>
			<button class="btn variant-ghost-primary" on:click={nextSlide}>Next</button>
		  </div>
	</div>
  </div>
  