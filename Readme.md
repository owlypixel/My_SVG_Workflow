# My SVG Animation Workflow
If you've ever worked with SVG you probably noticed the fact that the tools you have to use in the process are relatively unstable and can give you unpredictable results. There are a lot of small pitfalls which can cause you to do the same work over and over again, until you get desired results. 
After I noticed that I spend more and more time doing the things that easily could have been avoided, I decided to document the process highlighting the key points to keep in mind while working with SVG. So, this post therefore serves as a reference for me, and possibly, can be of use for somebody else.

## Creating the artwork in Adobe Illustrator
It all starts in Adobe Illustrator, where I create the artwork. For me this process is completely intuitive, starting just from a small idea (a face, a weird animal, an owl) and gradually adding more elements, shapes, colors and other things as I draw. 
### Fit to artwork bounds
As soon as the illustration is complete, the first problem shows up - artboard size issues. 
Countless times I've put SVG image on a page, gave it specific width and height and then found out that it was being displayed at a size smaller or bigger than what I specified. It is caused by an amount of white space inside the SVG viewport. 
Now, because I'm not a professional illustrator, my drawings are usually pretty simple, so in order to deal with this issue I simply go to Object/Artboards and select an option Fit to artwork bounds.
### Name and group each layer
Fairly often, I get carried away by the illustration and absolutely forget about the project structure. So, second small tip here would be to name your layers, because the layer names are going to be converted into id's and class names for the generated SVG. It doesn't have to be a complex system with lots of naming rules, just simple names to tell elements and groups apart from each other. 


## Saving the artwork in SVG format

### Fix _1_ and id's

<g id="Stars">
	<path id="StarSmall3_1_" class="st8" d="M12,12.3c0,0-0.1,4.2-3.9,4.6c3.8,0.3,3.9,4.3,3.9,4.3s0-4,4.4-4.4
		C12.6,16.4,12,12.3,12,12.3z"/>
	<path id="StarSmall2_1_" class="st8" d="M68.9,26.7c0,0-0.1,4.2-3.9,4.6c3.8,0.3,3.9,4.3,3.9,4.3s0-4,4.4-4.4
		C69.5,30.8,68.9,26.7,68.9,26.7z"/>
	<path id="StarSmall_1_" class="st8" d="M155.8,22.1c0,0-0.1,4.2-3.9,4.6c3.8,0.3,3.9,4.3,3.9,4.3s0-4,4.4-4.4
		C156.4,26.3,155.8,22.1,155.8,22.1z"/>
</g>