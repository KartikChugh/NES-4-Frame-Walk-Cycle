# 8-bit devlog – the 4 frame walk cycle
## June 22, 2018
#### by Hawken

We take a look why NES games used a 4 frame walk cycle and muse on how to carry those techniques through to modern games.

As part of a returning series, we’ll be documenting the development process of Pixel Pirate. With Pixel Pirate, the key aesthetic is to mimic NES to the level of something like a “NES+”, a fantasy console that has some of the restriction of the NES (Colours mostly) to help guide it’s look throughout the development process.

All NES games had the luxury of a 128×128 pixel sprite-sheet that was broken down in to tiles. With some fancy memory swapping these 128×128 sheets could be swapped out or even generated on the fly, which is what we are proposing Pixel Pirate is doing in a way, but the earlier games stuck to that one sheet for sprites and the animations had to be tight to fit on the sheet, hence the 3 frame walk cycle.

Lets look at some examples:

### 1. The classic.

Lets start with the most famous of them all, Super Mario Bros. This is a classic walk cycle, that just plays linearly. The trick here is to not provide any shading so the legs interchange with one another making the back leg and front leg use the same frames.

![](/media/mario-1.gif)

One thing to avoid when making walk cycles with a small amount of frames is “persistent pixels” or sticky pixels. This is when a pixel or cluster of pixels of the same colour are unmoving or unchanging through all the frames. Mario only has this on top of his shoulder, which is fine.

### 2. The reused frame or “Ping-Pong”.

So in this example from Super Mario Bros. 3 they have opted for two tile space saving techniques. Firstly they are re-using the Idle pose to add more frames to the loop, and then reusing frame 2 as frame 4 to add even more frames. Technically this walk cycle is only 2 frames but the way the frames are used makes it look like 4. This walk cycle is far more optimised that the classic from Mario 1.

![](/media/mario3.gif)

This one from Castlevania III uses a middle frame, and again is a ping pong cycle, which uses an Idle frame (4th). This animation suffers greatly from “sticky pixels” around the hand area and the middle of the legs. Castlevania split the sprites up so legs and torso could have independent states for attacks so this might be a reason why. The lower frame rate of the walkcycle probably helped mask the Sticky Pixels artefact.

![](/media/castlev3-2.gif)

In the end, this is what most games opted for, two specific frames and one re-usable frame, then ping pong the animation. Games like Mega Man, Ducktales and Metroid all used this technique.

### 3. As many frames as you like.

Later NES games had to concentrate on wowing new customers, from strong competition in the console wars. So they would throw their entire budget on the main sprite, this can be seen in games like Moon Crystal and Batman III.

### So if it’s NES+, how about Ping-Pong-Plus?

In Pixel Pirate we want to keep the NES aesthetic, with a little bit of “Plus”. Previously all walk cycles in the game were a lavish 8 frames. With modern gaming technology we are not limited in any way, the walk cycle could be 20,000 frames and modern hardware wouldn’t miss a beat. However these 8 frames seemed out of place with the overall NES+ feel, so cutting them back helped a lot.

![](/media/pixelpirate-2.gif)
![](/media/pixelpirate-front.gif)

With so few frames it is important to have a lot going on. If one thing is moving left, make another thing move up. If something moves every frame, make another thing move 2 frames. If something is not rigidly tethered, give it gravity after impact and so on. Having areas of irregular unsynchronised motion help create the illusion of more motion.

As the animation for Pete, the character above, is very condensed in to his portly form, animation only needs to be centered around things that move, like his hat, earring, belt etc. A low frame count affords a few benefits:

- Less need for sub-pixel animation (the effect on the brim of the hat moving back and forth).
- More flexibility in key poses.
- More animation can be made in the same time frame which ultimately leads to more variety in the game.

One thing that can’t be done with 4 frame animation is facial expressions like blinking and/or opening of the characters mouth as they walk, as these are usually buried in a higher frame count and the repetition is less noticeable.

Thanks for reading!
