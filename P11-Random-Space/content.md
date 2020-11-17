---
title: "Display a Random Space"
slug: display-a-random-space
---

## Show a random public space

What if people wanted to find new spaces or just see something random? You could make a button to do this. 

To generate a random number with JavaScript you can use `Math.random()`. This method returns a random number between 0.0 and 1.0. It doesn't take any parameters or provide any other options. Typical output might look like this:  

- 0.18688631567790337
- 0.2833598281388573
- 0.07430992503059852
- 0.3424389185783543
- 0.780044321714769
- 0.10202516555210439

I generated these numbers with `Math.random()`. If you need numbers that look different from this you'll need to do some work. 

First you can multiply the value by the range of numbers you need. For example: `Math.random() * 10` might output: 

- 3.9817693263500997
- 1.9900180705556125
- 6.624325586714287
- 6.776353541892094
- 9.51050569288244
- 9.292188988843789

Now you need to round the numbers off. JS supplies three choices for rounding: 

- `Math.floor()` - rounds down `Math.floor(3.9817693263500997) // 3`
- `Math.ceil()` - rounds up `Math.floor(9.292188988843789) // 10`
- `Math.round()` - rounds up/down 
	- `Math.floor(9.51050569288244) // 10`
	- `Math.floor(9.292188988843789) // 9`

The situation we are in provides us with an array of spaces and we need to select a random space from the array. The number of spaces in the array is provided by the length: 

```JS
data.length
```

The index of elements in an array start at 0 and end at length - 1. So `Math.floor()` might be our best choice! Here is some sample code: 

```JS
const index = Math.floor(Math.random() * data.length)
```

Or we could break that up across several lines to make it easier to read: 

```JS
const length = data.length
const randomNumber = Math.random() * length
const index = Math.floor(randomNumber)
// get a random space with: data[index]
```

Since we're using react Router and have a route to show a detail page with an index if we generate a route with that index we can show the page. For example: `http://localhost:3000/?#/details/2` if the 2 were a random number it would display a random page. 

```JS
const length = data.length
const randomNumber = Math.random() * length
const id = Math.floor(randomNumber)
// Router could work with this:
// /details/:id
```

A quick aside, I'm regretting naming the the compoennt Title, when that component became the Header or PageHeader. This would a good place to rename these! For this dicussion I'm going to stick with the original name: Title. 

### React Router History

Displaying a new random page requires we use React Router. Remember React Router manages the "Pages" in our Single Page Site. 

The method I chose was `history`. Using history will allow random searches to be tracked by the history and users will be able to use the back button in the browser to go back to the previous space they viewed. 

Now we need a button or link to initiate the action. I added a button to the `Title` (😑) component. You could put this button anywhere. So our strategy will be to make a component that is just the button that loads a random space and then we can import that button where ever we might want to use it. 

> [info]
> 
> Make a new folder: `components/RandomSpace/`
> 
> Next make a new file: `RandomSpace/RandomSpace.js`
>
> Now add the following to `RandomSpace.js`: 
>
```JS
import React from 'react'
import { useHistory } from 'react-router-dom'
import './RandomSpace.css';
import data from '../../sfpopos-data.json'
>
function RandomSpace() {
	const history = useHistory()
  return (
		<button onClick={(e) => {
			const id = Math.floor(Math.random() * data.length)
			history.push(`/details/${id}`)
		}}>Show me a random space</button>
  )
}
>
export default RandomSpace
```
>

This creates a component that outputs a single button. 

I imported `useHistory`. `useHistory` is a 'hook' that we can use with React Router to navigate to a new page. You'll call this method in your component function to get the history object.

I also imported `sfpopos-data.json` as `data` since I'll need to know the length of the list. 

The code here handles a click on the button with `onClick`. Without all of the extra code the button might look like: 

```JS
<button onClick={() => {
	// run some code here when the clicked
}}>Show me a random Space</button>
```

The code above uses an arrow function. These are similar to regular functions: 

```JS
// Old school function
function(a,b,c) {

}

// Arrow function
(a,b,c) => {

}
```

Inside the onClick function the code gets a random number from 0 to the length - 1 as id. Then uses `history.push()` to navigate to the details page with the random id.  

```JS
const id = Math.floor(Math.random() * data.length)
history.push(`/details/${id}`)
```

### Use the new RandomSpace component

Use the new component like any other component. 

- Import 
- then put it in your JSX

Lets add a RandomSpace button to the Title (😑). 

> [info] 
> 
> Edit `Title.js`. Add the following at the top and adjust the path to fit your arrangement of files. 
> 
```JS
import RandomSpace from '../RandomSpace/RandomSpace'
```
> 
> Inside the function that defines the component find a place to add the new button component: 
> 
```JS
function Title() {
  return (
    <div className="Title">
      <header>
        ...
        <div>
          ...
          <RandomSpace />
        </div>
      </header>
    </div>
  )
}
```
>

I put the random space button after the list of NavLinks. You could put it anywhere. 

### Style the RandomSpace button 

Add a style sheet and style the RandomSpace button. 
