---
title: "Styling the List"
slug: styling-the-list
---

## The list could use some styles

The POPOSList component displays a list of POPOSSpace components. The list is only responsible for arranging the spaces. To get things to look great you'll need to style both and get those styles to work together. 

This step will only cover styling the list. There may be a few issues with the way the spaces display which will be covered in another section. 

Create a CSS file. 

> [info] 
> 
> If you haven't already create a new file: `POPOSList.css` it should be in the same folder as the `POPOSList.js` file. 
> 

Now import the CSS. 

> [info]
> 
> Next import the the new CSS file into the `POPOSList.js` add the following at the top.
> 
> `import './POPOSList.css'`
>
> Now, in the `POPOSList` component add a class name: 
> 
```JS
function POPOSList() {
  ...
  return (
    <div className="POPOSList">
			...
    </div>
  )
}
```
>

Arranging the elements in a grid would be a good idea. Luckily CSS provides a `display: grid` property. This is similar to `display: flex`. Where flex is a one dimmensional arrangement grid is two dimmendsional. With flex everything would be arranged in a row or a column, with grid things are arranged in both rows and columns. 

> [info]
>
> Add the following to `POPOSList.css`
> 
```CSS
.POPOSList {
	display: grid;
	grid-template-columns: 1fr 1fr 1fr;
}
```
>

The code above declare the parent element as display grid and defines three equal sized columns. The `1fr` is 1 fraction. the `fr` unit that is a fraction of the availble space. So `1fr 1fr 1fr` could considered the same as `33.333% 33.333% 33.333%` but it reads better and is more accurate. 

Test this out and resize the page. There are a couple things missing. 

- The grid columns and rows need some space between them
- When the page is really wide the columns are too far apart
- When the page is too narrow the columns are too close together

> [info]
> 
> Add the following to the `.POPSList` rule in `POPOSList.css`
> 
```CSS
.POPOSList {
	display: grid;
	grid-template-columns: 1fr 1fr 1fr;
	grid-gap: 2em;
	max-width: 1200px;
	margin: auto;
	padding: 2em;
} 
> 

- `grid-gap: 2em` adds a 2em space between rows and columns in the grid
- `max-width: 1200px` sets a maximum width for the element
- `margin: auto` makes the margins equal on the left and right this has the effect of centering the grid container on the page. 
- `padding: 2em` adds some space on the left and right so the pictures don't hit the edges of the page when the window is narrow. 

This looks better but there are some problems when the page is narrow. Add some media queries to take care of these. 

A media query is a rule that is only applied some times or under certain circumstances. You'll use media queries here to make adjustments for smaller screens, like tablets, and mobile devices. 

> [info]
> 
> Add the following to `POPOSList.css`
> 
```CSS
/* Smaller screens and tablets */
@media only screen and (max-width: 960px) {
	.POPOSList {
		grid-template-columns: 1fr 1fr;
	}
}
```
>

Here the number of columns is changed to two equal columns when the screen is 960px or smaller. 

Test your work. resizing the page should change the display to two columns when the screen gets down to 960px and show 3 columns when the screen is wider. 

Let's do that again. 

> [info]
> 
> Add the following to `POPOSList.css`
> 
```CSS
/* Small screens mobile */
@media only screen and (max-width: 700px) {
	.POPOSList {
		grid-template-columns: 1fr;
	}
} 
```
>

Here the the layout switched to a single column when the screen is smaller than 700px. 

test your work. The screen shoould switch between 3, 2, and 1 column as the screen narrows. 

Think of other things you might want to change as the screen changes size? 

Important! In the POPOSList stylesheet you're only concerned with the list of spaces. If the changes you want to make concern the Spaces (thats' the image and text) it should be applied to the POPOSSpace.css. See the section on styling these! 


