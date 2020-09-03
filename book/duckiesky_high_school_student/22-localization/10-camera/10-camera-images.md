# Comparing Images {#localization-camera-images status=ready}

Image that you're starting to assemble a jigsaw puzzle. You take out the first piece and then you look at the picture on the box to guess where that piece belongs. If the puzzle piece has many differnet colors or distinct lines, then it is easier to find where it belongs in the whole picture. however, if the puzzle piece is a solid color, say a blue part of the sky, it is very difficult to narrow down exactly where the piece belongs. As you find more pieces that fit with your first piece, it becomes easier to determine where those pieces belong in the picture.

This is how localization on the drone works. The drone has a picture of the entire surface that it will fly over stored on it; this is called the _map_. Compare the map to the complete picture on the puzzle box. As the drone is flying, the camera is only able to see part of the map. The drone tries to find where this picture belongs in the map, just like finding where the puzzle piece goes. Once the drone knows approximately where the picture belongs, it can guess how far to the right, and how far up it is flying from the bottom left of the map. And viola, the drone has a position estimate!

Of course, there is a lot math and code behind the picture matching process of the drone; however, the higher level understanding is just as described.
