# Displaying Features - Details page

Each of the spaces has a list of features. The features describe the location as indoors or outdoors, whether there is coffee, art, or a bathroom available.

We could display these as text but it might be more fun and easier for people to understand if we displayed them with icons or emojis.

We have two choices to work with

- Emoji
- Images

Emojis are built in and require no extra libraries or files. They are also fairly compatible across systems today.

Images represent a lot of things, but using images would require more files, and more work on our part but possible be more compatible. Font Awesome would be a good choice here.

Let's give emoji a try.

## Convert words to emoji

Looking through the base data there are five features:

- outdoors
- coffee
- art
- toilet
- power

We need an emoji for each of these.

- 🌲 - outdoors
- ☕️ - coffee
- 🖼 - art
- 🚽 - toilet
- 🔌 - power

Now we need to convert an array of words to an array of emoji. Array.map is the tool for the job. Map is meant for transforming an array of one type into an array of another type. Here you'd be converting an array of text strings into an array of emoji strings.

Make a component that displays the emoji!

Make a new file: `POPOSFeature.js`.

Define a component:

```JS
import React from 'react'
import './POPOSFeature.css'

function getFeature(str) {
	switch(str) {
		case 'outdoors':
			return '🌲'
		case 'coffee':
			return '☕️'
		case 'art':
			return '🖼'
		case 'toilet':
			return '🚽'
		case 'power':
			return '🔌'
		default:
			return '？'
	}
}

function POPOSFeature(props) {
	const emoji = getFeature(props.name)
	return <div className="POPOSFeature">{emoji}</div>
}

export default POPOSFeature
```

This component will require a prop: name. You might create a instance like this:

```JS
<POPOSFeature name="coffee" />
```

Internally the component translates the word to an emoji using the `getFeature(str)` function.

The `switch` block is like an if else block. The switch tries to match the supplied value agains one of it's cases. If `str` matches the function returns an emoji string.

Add a stylessheet.

Create a new file: `POPOSFeature.css`

Import this new stylesheet at the top `POPOSFeature.js`

```JS
import './POPOSFeature.css'
```

Add the follow code at the top `POPOSFeature.css`:

```CSS
.POPOSFeature {
	font-size: 2em;
	padding: 0.25em;
	margin: 0.125em;
	border-radius: 0.25em;
	background-color: #eee;
}
```

This sets the font size, adds some padding and marging, sets the border radius, and sets a background color.

## Feature list

The SFPOPOS data provides a list of 0 or more strings of features. This means we need to display a list of these `POPOSFeature` components.

Time to make a component! This new component will take an array of strings and return an array of `POPOSFeature` components.

Create a new file: `POPOSFeatureList.js`.

Add the following code here to define the new component.

```JS
import React from 'react'
import POPOSFeature from './POPOSFeature'
import './POPOSFeatureList.css'

function POPOSFeatureList(props) {
	const icons = props.features.map((feature) => {
    return <POPOSFeature key={feature} name={feature} />
  })
	return <div className="POPOSFeatureList">{icons}</div>
}

export default POPOSFeatureList
```

This component imports the `POPOSFeature` component.

This component expects an array of strings named features. We get the array on props as: `props.features`.

The component maps the array of strings into an array `POPOSFeature` components setting the name of each to a feature string from the array.

Add a style sheet.

Add a new file: `POPOSFeatureList.css`.

Import your styles in `POPOSFeatureList.js`:

```JS
import './POPOSFeatureList.css'
```

Then add some styles.

```CSS
.POPOSFeatureList {
	display: flex;
}
```

The only style here is flex which should line up all of the elements in a row.

You could add more styles if you like.

## Use the POPOSFeatureList

Use the feature list and feature components.

To use the `POPOSFeature` component you make an instance and set the name prop, fro example:

```JS
<POPOSFeature name="art" />
```

To use the POPOSFeatureList component you need to include an array of strings as the features prop, for example:

```JS
<POPOSFeatureList features={['coffee', 'art']} />
```

Put this to work in the details page.

Edit `POPOSDetails.js`

```JS
...
import POPOSFeatureList from '../POPOSFeatures/POPOSFeatureList'

function POPOSDetails(props) {
	...
  return (
    <div className="POPOSDetails">
      ...
      <div className="POPOSDetails-info">
        ...
        <POPOSFeatureList features={features}/>
        <p className="POPOSDetails-geo">{ geo.lat } { geo.lon }</p>
      </div>
    </div>
  )
}
```

Be sure to adjust the path to your `POPOSFeatureList` component, it may be in a different location than where I placed mine!

Be sure to remove the previous tag that displayed the features.

What happened here? First we imported the POPOSFeatureList component.

Next, make an instance of `POPOSFeatureList` and set the feature proper to the array of feature strings that came from the data source.

# Next

Click [here](../P13-Publish-to-GitHub-Pages/) to move onto the next section about publishing to GitHub pages.
