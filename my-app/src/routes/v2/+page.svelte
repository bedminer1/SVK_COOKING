<script lang="ts">
    import { swipe } from 'svelte-gestures';
    import image1 from "$lib/images/1.jpeg"
	import image2 from "$lib/images/2.jpeg"
	import image3 from "$lib/images/3.jpeg"

	const images: string[] = [image1, image2, image3]
    let liked = new Set<string>()
    let disliked = new Set<string>()
    let direction: string;
    let target: string;
    let index: number = 0
    
    function handler(event: CustomEvent) {
        direction = event.detail.direction;
        if (direction === "left") {
            liked.add(images[index].split('.')[0].substring(16))
        } else {
            disliked.add(images[index].split('.')[0].substring(16))
        }

        console.log("Liked: ", liked,)
        console.log("Disliked: ", disliked)
        index = (index + 1) % images.length
    }
    </script>
    
    <div use:swipe={{ timeframe: 300, minSwipeDistance: 60 }} on:swipe={handler} class="w-full h-screen flex items-center justify-center">
        <div>
            direction: {direction}
            <img src={images[index]} alt="" class="w-full h-[40vh]">
        </div>
    </div>