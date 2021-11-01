# Styling Spaces

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

Create a new file named: `POPOSSpace.css`. This should be in the same folder as the `POPOSSPace.js` file.

Import the CSS and add the class name:

Add the following at the top of `POPOSSpace.js`:

```JS
import './POPOSSpace.css'
```

Now add the class to the root element:

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

Now you'll add some styles to style the elements here.

It would be nice if the images were flexible. The columns of the grid change size as the page changes sizes.

Add the following to: `POPOSSpace.css`:

```CSS
.POPOSSpace img {
	width: 100%;
	height: auto;
}
```

You might have to refresh to make sure the changes to CSS show up when testing.

With this change the images in POPOSSpace should have a width of 100% of the available space.

## Have some fun with the title

Let's move the title to the upper left corner of the picture. To do this you'll use relative and absolute position.

The structure of the POPOSpace is:

- div.POPOSSpace
	- Link
		- img
	- Link
		- h1 (title)
	- div (address)
	- div (hours)

By making the parent component `div.POPOSSpace` position relative it will become the positioning context for any children that use absolute position. When an element uses absolute position you can position it by it's left and top edges. To figure where the top and left are the element looks up the DOM tree for an element that has `position: relative`.

Give it a try!

Edit `POPOSSpace.css `, set the position property of the parent element to relative.

```CSS
.POPOSSpace {
	position: relative;
}
```

Now add a new classname to the title element. This is in a Link component, you'll need to assign this a className.

In `POPOSSpace.js` find the name in it's Link tag and add a new class name.

```JS
function POPOSSpace(props) {
  ...
  return (
    ...
			<Link
				className="POPOSSpace-title" // add a class name!
				to={`/details/${id}`}>
				<h1>{name}</h1>
			</Link>
			...
  )
}
```

Next style the new class.

In `POPOSSpace.css` add some new style rules:

```CSS
.POPOSSpace .POPOSSpace-title {
	display: block;
	position: absolute;
	left: 0;
	top: 0;
}

.POPOSSpace h1 {
	margin: 0;
	font-weight: lighter;
	background-color: rgba(255, 255, 255, 0.9);
	padding: 0.5rem;
	text-align: left;
}
```

This should move the title to the upper left corner and give it some font styles.

Now move the address and hours to the lower right corner. It will ne easier if these elements share a common parent.

Edit `POPOSSpace.js`:

```JS
...
function POPOSSpace(props) {
  ...
  return (
    <div className="POPOSSpace">
			...
			<div className="POPOSSpace-info">
				<div >{address}</div>
				<div>{hours}</div>
			</div>
    </div>
  )
}
```

Now with a a parent element and a class name we can apply styles to the parent and it's children.

Edit `POPOSSpace.css` and add thw following.

```CSS
.POPOSSpace .POPOSSpace-info {
	position: absolute;
	right: 0;
	bottom: 0;
	text-align: right;
}

.POPOSSpace .POPOSSpace-info div {
	display: inline-block;
	padding: 0.25em 0.5em;
	background-color: rgba(255, 255, 255, 0.9);
}
```

Here the container `.POPOSSpace-info` is declared position absolute This way we can place it where we want. In this case I put it at right 0 and bottom 0 which make it hug the lower right corner. I also aligned the text to the right.

The `.POPOSSpace .POPOSSpace-info div` selector applies to the two child divs. Here I added some padding and a background color.

# Next

Click [here](../P09-Style-the-details-page/content.md) to move onto the next section about styling the details page.
