<script lang="ts">
    import { swipe } from 'svelte-gestures';
    import image1 from "$lib/images/1.jpeg"
	import image2 from "$lib/images/2.jpeg"
	import image3 from "$lib/images/3.jpeg"
    import { fly } from 'svelte/transition'

	const images: string[] = [image1, image2, image3]
    let liked = new Set<string>()
    let disliked = new Set<string>()
    let direction: string;
    let index: number = 0
    let transitionActive: boolean
    
    function handler(event: CustomEvent) { 
        direction = event.detail.direction;
        
        // INVALID SWIPES, IMAGE QUEUE EMPTY
        if (index === images.length
            || direction === "top"
            || direction === "bottom")
                 return

        // TRANSITION
        transitionActive = true
        setTimeout(() => {
            transitionActive = false
        }, 500)

        // RIGHT FOR LIKE, LEFT FOR DISLIKE
        if (direction === "right") {
            liked.add(images[index].split('.')[0].substring(16))
        } else {
            disliked.add(images[index].split('.')[0].substring(16))
        }

        console.log("Liked: ", liked,)
        console.log("Disliked: ", disliked)
        index++
    }
    </script>
    
    <div class="w-full h-screen flex items-center justify-center"
    >
        <div use:swipe={{ timeframe: 600, minSwipeDistance: 10 }} on:swipe={handler}>
            direction: {direction}
            {#if index == images.length}
                <p>OUT OF SWIPES</p>
            {:else if !transitionActive}
                <img src={images[index]} 
                alt="" 
                out:fly={{duration: 100, x: direction === "right" ? 200 : -200}}
                class="w-full h-[40vh] pointer-events-none select-none"
                >
            {/if}
        </div>
    </div>