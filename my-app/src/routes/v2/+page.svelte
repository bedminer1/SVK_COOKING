<script lang="ts">
    import { swipe } from 'svelte-gestures';
    import image1 from "$lib/images/1.jpeg"
	import image2 from "$lib/images/2.jpeg"
	import image3 from "$lib/images/3.jpeg"

	const images: string[] = [image1, image2, image3]
    let liked = new Set<string>()
    let disliked = new Set<string>()
    let direction: string;
    let index: number = 0
    
    function handler(event: CustomEvent) { 
        direction = event.detail.direction;
        
        // INVALID SWIPES, IMAGE QUEUE EMPTY
        if (index === images.length
            || direction === "top"
            || direction === "bottom")
                 return

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
    
    <div class="w-full h-screen flex items-center justify-center">
        <div use:swipe={{ timeframe: 300, minSwipeDistance: 60 }} on:swipe={handler}>
            direction: {direction}
            {#if index == images.length}
                <p>OUT OF SWIPES</p>
            {:else}
                <img src={images[index]} 
                alt="" 
                class="w-full h-[40vh] pointer-events-none select-none"
                >
            {/if}
        </div>
    </div>