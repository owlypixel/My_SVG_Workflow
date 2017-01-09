# My SVG Animation Workflow
If you've ever worked with SVG you probably noticed the fact that the tools you have to use in the process are relatively unstable and can give you unpredictable results. There are a lot of small pitfalls which can cause you to do the same work over and over again, until you get desired results. 
After I noticed that I spend more and more time doing the things that easily could have been avoided, I decided to document the process highlighting the key points to keep in mind while working with SVG. So, this post therefore serves as a reference for me, and possibly, can be of use for somebody else.

## Creating the Artwork in Adobe Illustrator
It all starts in Adobe Illustrator, where I create the artwork. For me this process is completely intuitive, starting just from a small idea (a face, a weird animal, an owl) and gradually adding more elements, shapes, colors and other things as I draw. 
### Tip1. Fit to Artwork Bounds
As soon as the illustration is complete, the first problem shows up: **artboard size issues**. 
Countless times I've put SVG image on a page, gave it specific width and height and then found out that it was being displayed at a size smaller or bigger than what I specified. It is caused by an amount of white space inside the SVG viewport. 
Now, because I'm not a professional illustrator, my drawings are usually pretty simple, so in order to deal with this issue I simply go to `Object → Artboards` and select an option <nobr>`Fit to Artwork Bounds`</nobr>. That makes my artboard just big enough to fit the drawing inside of it.
### Tip2. Name and Group Each Layer
Fairly often I get carried away by the illustration and absolutely forget about the project structure. So, second small tip here would be to name your layers, because the layer names are going to be converted into id's and class names for the generated SVG. It doesn't have to be a complex system with lots of naming rules, just simple names to tell elements and groups apart from each other. 


## Saving the Artwork in SVG Format
At this point everything is ready to transform my drawing into SVG document. Adobe Illustrator natively supports saving vector images to fully editable SVG format, so it's not some kind of temporary export option. But I prefer to simply copy generated SVG code into my text editor and work with it there. To do this I go to `File → SaveAs` and in the `format` dropdown at the bottom select `SVG`. 
Next, in the dialog stuffed with tons of options that pops up, I generally keep everything by default, because I really don't know what all those options mean, but here's a couple moments to keep an eye on: 

1. SVG Profile: `SVG 1.1`
2. Tick off the checkbox `Preserve Illustrator Editing Capabilities`

Finally, I click the button `SVG Code...` to see the actual code, and copy it into my editor. 
### Tip3. Fix \_1_ and Id's in the SVG Code
You probably noticed Illustrator's excellent naming convention for the generated SVG code.
```html
<g id="Stars">
	<path id="StarSmall3_1_" class="st8" d="M12,12.3c0,0-0.1,4.2-3.9,4.6c3.8,0.3,3.9,4.3,3.9,4.3s0-4,4.4-4.4
		C12.6,16.4,12,12.3,12,12.3z"/>
	<path id="StarSmall2_1_" class="st8" d="M68.9,26.7c0,0-0.1,4.2-3.9,4.6c3.8,0.3,3.9,4.3,3.9,4.3s0-4,4.4-4.4
		C69.5,30.8,68.9,26.7,68.9,26.7z"/>
</g>
```

Yeah, those annoying underscores are a pain in the butt :disappointed:. But I fix that using find in Sublime **(Ctrl + H)** and replace **\_1_** to nothing. In the same way I prefer to replace all id's in the SVG to classes. However, one thing to remember here: 

**Note:** _you can't reference gradients and other dynamic fills with classes._

So, I manually go and change those to ids.  
### Tip4. Remove Hidden Layers with Raster Images
Sometimes in Illustrator I use raster image as a background for outlining. And it's no big deal, when I'm done with the drawing I simply make it a hidden layer and forget about it. But those images still show up in the generated SVG code, so I remove them manually. They're usually not that hard to notice because of their distinct BLOB-like view in the document. 

## Putting SVG Image into HTML File
Ok, at this point I usually have pretty cleaned-up SVG file which now needs to be embedded in some kind of web page. The simplest way here would be of course to dump it into CodePen's Html box and start playing around with JavaScript and CSS right away. However, due to the lack of stable Internet connection I'm forced to do everything locally. 
I've created a blank project which I just copy, rename the folder and it's basically ready for the next steps.
And the next step is to inline SVG code into html page. Of course there's multiple variants of including your SVGs in the page, but I chose inline variant because:

+ It's more performant
+ It saves you another HTTP-request
+ Gives you the ability to control everything with JavaScript and CSS
+ You can attach event handlers to everything

### Tip5. Put SVGs Inside a Container
I always try to put my SVGs inside of a containing element, in that way it can be easily centered, resized, and overall it's much easier to work with it.

## Animating SVG Parts
Now that I have everything in place, I can actually start applying animations to individual parts of SVG image. For now, I'm not very familiar with the animation frameworks and libraries like [GreenSock](https://greensock.com/) or [SnapSVG](http://snapsvg.io/), so all my animations boil down to simply adding or removing classes from the elements with JavaScript or JQuery. All animations are mostly based on CSS transforms like `translate`, `rotate`, `scale` and others.
### Small Example
Let's look at the example of simple animation using one of my recent pens: [Owlymug](http://codepen.io/owlypixel/pen/rjVqMG).
In this pen I animate the wings of an owl with the help of simple CSS transform: `rotate`.
Firstly, I identify the part of the image that needs to be animated. In our case it's the groups with the classes `RightWing` and `LeftWing`. 
```html
<g class="RightWing">
	<path class="st7" d="M137.8,145.5c0,0,14.3,28.3,22.1,25.4c1.3-3.1,2.3-6,3-8.8c5.2-18.7,0.4-31.4-4.1-38.5
		c-2.9-4.5-5.6-6.7-5.6-6.7s-13.6-7-19.6,1.8C127.7,127.5,137.8,145.5,137.8,145.5z"/>
	<path class="st7" d="M144.5,123.4c4.5-2.6,14.3,0.2,14.3,0.2"/>
	<path class="st7" d="M150.3,131.8c4.8-2.4,13.1,1.7,13.1,1.7"/>
	<path class="st7" d="M153.4,140.9c4.8-2.7,11.6,1.3,11.6,1.3"/>
	<path class="st7" d="M157.6,159.2c2.3-1.1,5.7,1.8,5.7,1.8"/>
	<path class="st7" d="M165,150.9c0,0-4.6-2.9-9.4-0.7"/>
</g>
<g class="LeftWing">
	<path class="st7" d="M68.7,144.4c0,0-18.3,24.3-25.2,20.3c-0.7-3.1-1.2-6-1.5-8.8c-1.9-18.4,4.7-29.6,10.2-35.6
		c3.5-3.8,6.4-5.4,6.4-5.4s14.1-4.3,18.3,5S68.7,144.4,68.7,144.4z"/>
	<path class="st7" d="M65.9,122.6c-3.9-3.2-13.7-2.2-13.7-2.2"/>
	<path class="st7" d="M59,129.5c-4.2-3.1-12.7-0.6-12.7-0.6"/>
	<path class="st7" d="M54.5,137.6c-4.1-3.3-11.2-0.7-11.2-0.7"/>
	<path class="st7" d="M47.6,154.1c-2-1.4-5.7,0.8-5.7,0.8"/>
	<path class="st7" d="M41.9,145.1c0,0,4.8-2,9.1,1"/>
</g>
```
As this is a very simple animation, I can jump right into the browser and apply <nobr>`transform: rotate(90deg)`</nobr> right there, and check out the results of transformation. Usually by default it's going to rotate itself by exact middle of the element, and in most cases this is what I need, but in this case I need to **transform the origin** of the rotation.
With a bit of tweaking and experimenting, I see that for the left wing `transform-origin` should be `68% 22%`, and for the right wing `34% 22%`.
Ok, now I simply add the animation rule to the elements, name the animations `shake-left-wing` and `shake-right-wing` respectively, set the animation duration to `2s` and specify that it's going to be repeating `infinitely`.

```css
.LeftWing {
	animation: shake-left-wing 2s infinite;
	transform-origin: 68% 22%;
}
.RightWing {
	animation: shake-right-wing 2s infinite;
	transform-origin: 34% 22%;
}
```
After that, I only need to create `@keyframes` rule for each animation, specifying the rotation degrees.

```
@keyframes shake-left-wing {
	0% {
		transform: rotate(0deg);
	}
	50% {
		transform: rotate(90deg);
	}
	100% {
		transform: rotate(0deg);
	}
}
@keyframes shake-right-wing {
	0% {
		transform: rotate(0deg);
	}
	50% {
		transform: rotate(-100deg);
	}
	100% {
		transform: rotate(0deg);
	}
}
```
That's it! Our happy owl animation is now complete.

Hopefully, this post can save somebody, who is an absolute beginner in animations, some time in the future. Additionally, I now have a reference in case I forget something after not working with animations for a while. Of course, I might have missed a few tips that can make the process even simpler, so If you know any, please feel free to share them in the comments below.
Cheers!

