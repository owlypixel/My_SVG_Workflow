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
At this point everything is ready to transform my drawing into SVG image. Adobe Illustrator natively supports saving vector images to fully editable SVG format, so it's not some kind of temporary export option. But I prefer to simply copy generated SVG code into my text editor and work with it there. To do this I go to File/SaveAs and in the format dropdown at the bottom select SVG. 
In the nice dialog stuffed with tons of options that pops up I generally keep everything by default, cause I really don't know what all those options mean, but here's a couple moments to keep an eye on: 
SVG Profile: SVG 1.1
Tick off the checkbox Preserve Illustrator editing capabilities
Next, I click the button SVG Code... to see the actual code, and copy it into my editor Sublime Text. 
### Fix _1_ and id's in the SVG code
You probably noticed Illustrator's excellent naming convention for the generated SVG code.
```
<g id="Stars">
	<path id="StarSmall3_1_" class="st8" d="M12,12.3c0,0-0.1,4.2-3.9,4.6c3.8,0.3,3.9,4.3,3.9,4.3s0-4,4.4-4.4
		C12.6,16.4,12,12.3,12,12.3z"/>
	<path id="StarSmall2_1_" class="st8" d="M68.9,26.7c0,0-0.1,4.2-3.9,4.6c3.8,0.3,3.9,4.3,3.9,4.3s0-4,4.4-4.4
		C69.5,30.8,68.9,26.7,68.9,26.7z"/>
</g>
```

Yeah, those annoying underscores are a pain in the butt :) But I fix that using replace in Sublime (Ctrl + H) and replace _1_ to nothing. In the same way I prefer to replace all id's in the SVG to classes. However, one thing to note here: you can't reference gradients and other dynamic fills with classes. So, I'll manually go and change those to ids.  
### Remove hidden layers with raster images
Sometimes in Illustrator I use raster image as a background for outlining. And it's no big deal, when I'm done with the drawing I simply make it a hidden layer and forget about it. But those images still show up in the generated SVG code, so I remove them manually. They're usually not that hard to notice because of their distinct BLOB-like view in the document. 

## Putting SVG image into an HTML file
Ok, at this point I usually have pretty cleaned-up SVG file which now needs to be embedded in some kind of web page. The simplest way here would be of course to dump it into CodePen's Html box and start playing around with JavaScript and CSS right away. However, due to the lack of stable Internet connection I'm forced to do everything locally. 
I've created a blank project which I just copy, rename the folder and it's basically ready for the next steps.
And the next step is to inline SVG code into html page. Of course there's multiple variants of including your SVGs in the page, but I chose inline variant because:
- it's more performant
- it saves you another HTTP-request
- gives you the ability to control everything with JavaScript and CSS
- you can attach event handlers to everything

### Put SVGs inside a container
I always try to put my SVGs inside of a containing element, in that way it can be easily centered, resized, and overall it's much easier to work with it.
