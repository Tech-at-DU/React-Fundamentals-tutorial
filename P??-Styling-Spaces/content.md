---
title: "Styling Spaces"
slug: styling-spaces
---

## Styling Spaces

The POPOSSpace component displays a a single Public space in the list of public spaces on the home page. Each of these displays an image, the name of the space, it's address, and hours. 

## Using ancestor selector

Styles have been divided between several style sheets. To keep these styles from conflicting you'll use the strategy of assigning the root element in a component class name that matches the component name. The Component names should be unique like class names. You should also use this class name as the ancestor for other styles applied within the component. For example: 

```CSS 
.POPOSSpace {
	/* Styles for the root element */
}

.POPOSSpace img {
	/* Styles for img inside this component */
}
```

The second style above styles img tags but only if they are descendants of an element with the class name: POPOSSpace. This way the styles here don't affect img tags elsewhere on the page. 

## Styling POPOSSpace

Create a new stylesheet if you having. This should be a in the same folder as the `POPOSSpace.js` file. 

> [info]
> 
> Create a new file named: `POPOSSpace.css`. This should be in the same folder as the `POPOSSPace.js` file. 
> 

Import the CSS and add the class name: 

> [info]
> 
> Add the following at the top of `POPOSSpace.js`:
> 
```JS
import './POPOSSpace.css'
```
> 
> Now add the class to the root element: 
> 
```JS
function POPOSSpace(props) {
  ...
  return (
    <div className="POPOSSpace">
			...
    </div>
  )
}
```
>

Now you'll add some styles to style the elements here. 

It would be nice if the images were flexible. The columns of the grid change size as the page changes sizes. 

> [info]
> 
> Add the following to: `POPOSSpace.css`:
> 
```CSS
.POPOSSpace img {
	width: 100%;
	height: auto;
}
```
>

You might have to refresh to make sure the changes to CSS show up when testing. 

With this change the images in POPOSSpace should have a width of 100% of the available space. 




- Editing POPOSSpace
	- add className POPOSSpace
	- import styles 
	- images 100% width
	- Style the content 
		- Title
		- address
		- hours

