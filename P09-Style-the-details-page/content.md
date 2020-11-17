---
title: "Style the Details Page"
slug: style-the-details-page
---

## Style the details page

Follow the ideas from the presvious pages. 

> [info] 
> 
> Create a new CSS file: `POPOSDetails.css`
> 
> In `POPOSDetails.js` import your new stylesheet. 
> 
```JS
import './POPOSDetails.css'
```
>

I'm going to place the information on the left and the image on the right and divide the space in 1/3 and 2/3 proportion. 

There are several pieces of information here: 

- Title
- Description
- Hours
- Features
- geo coordinates

It would be nice to give each of these elements their own style. To do that you'll need to add some class names. 

> [info] 
> 
> Edit `POPOSDetails.js`: 
> 
```JS
function POPOSDetails(props) {
  const { id } = props.match.params // Location index
  const { images, title, desc, hours, features, geo } = data[id]
  return (
    <div className="POPOSDetails">
      <div className="POPOSDetails-image">
        <img src={`${process.env.PUBLIC_URL}images/${images[0]}`} />
      </div>
      <div className="POPOSDetails-info">
        <h1 className="POPOSDetails-title">{ title }</h1>
        <p className="POPOSDetails-desc">{ desc }</p>
        <p className="POPOSDetails-hours">{ hours }</p>
        <p className="POPOSDetails-features">{ features }</p>
        <p className="POPOSDetails-geo">{ geo.lat } { geo.lon }</p>
      </div>
    </div>
  )
}
```
>

Now add some styles for these elements. 

> [info]
> 
> Add the following to `POPOSDetails.css`
> 
```css
.POPOSDetails {
	display: flex;
	flex-direction: row-reverse;
	width: 960px;
	margin: auto;
}
>
.POPOSDetails .POPOSDetails-info {
	flex: 1;
	text-align: left;
	padding: 0 1em;
}
>
.POPOSDetails .POPOSDetails-title {
	font-size: 2em;
	margin: 0;
}
>
.POPOSDetails .POPOSDetails-image {
	flex: 2;
}
>
.POPOSDetails .POPOSDetails-image img {
	width: 100%;
}
>
.POPOSDetails .POPOSDetails-hours {
	font-size: 1.5em;
}

```
>

The main container was given row-reverse to move the information to the left and the picture to the right. Since the image came first in the html it would have been on the left otherwise. Margin auto here centers the section by making the margins equal on the left and right side. 

