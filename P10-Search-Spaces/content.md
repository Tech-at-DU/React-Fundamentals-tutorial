---
title: "Searching Spaces"
slug: searching-spaces
---

## Searching Spaces

Imagine you wanted to search spaces by typing the address into a input and showing all spaces in our JSON file that matched. 

To do this you will need to create an input and handle the text entered. React has a special pattern for this called the controlled component pattern. 

The controlled component pattern is built around state. State is a value stored inside of a component that the component tracks. Changes to state cause the component to Render. The idea is that somethings that change need to be reflected in the appearance of a component. 

To make this feature work we need to work with a new React concept: **state**. 

State is a value that is held by a component. When state changes the component will render again. There are two ways to work with state. 

Hooks and Classes

This solution will work with hooks. 

> [info]
> 
> To use state you'll import a special function. Edit `POPOSList.js`. Update the import statement at the top to include `{ useState }`.
> 
```JS
import React, { useState } from 'react'
```
>

Create the input field for the search feature. 

When I did this I had already setup the grid and hadn't thought of the how the form would display with the grid. 

> [info]
>
> Edit the `POPOSList` component in `POPOSList.js`
> 
```JS
function POPOSList() {
	const [ query, setQuery ] = useState('')
	...
  return (
    <div className="POPOSList">
			<form>
				<input 
					value={query}
					placeholder="search"
					onChange={(e) => setQuery(e.target.value)}
				/>
				<button type="submit">Submit</button>
			</form>
			{spaces}
    </div>
  )
}
```
>

If this is working you should be able to type in the field and see the value. 

While it may seem like we are doing extra work here that isn't necessary, in reality it is and best practice. 

Read more about how to handle forms with React here: https://reactjs.org/docs/forms.html

The work above has created a variable `query` that holds the value you entered into the field. In the next step you will use this value to filter the list of spaces displayed. 

To filter the list you'll use `Array.filter()` simialr to `Array.map()` filter takes a callback function as a parameter and returns a new array. 

The callback used with filter receives an item from the array and expected to return true if that it is going to be included in the returned array or false if not. For example: 

```JS
const lessThanThree = [1,2,3,4,5,6].filter((n) => n < 3>)
```

So how to determine if an item should be included? You can use `String.includes()` to ask if a string includes another string. For example: 

```JS
if ('surreptitious'.includes('it')) {
	console.log('I found it')
}
```

Note, case matters: 

```js
'Ithica'.includes('it') // returns false!
```

With this in mind what do we search? The data we have has a couple fields that might contain things people would search for. 

- title - Has the name of the of the location
- address - cotnains the address

the description might be used but it contains a lot of text that might provide false positives and slow our searches. 

> [info]
> 
> Edit `POPOSList.js`.
> 
```JS
function POPOSList() {
	...
	const spaces = data.filter(obj => obj.title.includes(query) || obj.address.includes(query)).map((obj, i) => {
		...
	})
	...
}
```
> 

That's pretty long and probably hard to grok. Let's take it apart. 

Without the callbacks we have: 

```JS
const spaces = data.filter().map()
```

Okay so that's not so bad. We start with `data.filter()` which returns an array and we call map() on that array: `data.filter().map()` and the array returned here is assigned to spaces. 

So what did we do filtered the data, then turned it into `POPOSSpace` components which are rendered later. 

Mapping the data to components was covered in the earlier tutorial so I'll ignore that here. Which leaves the question, what happened in filter? 

Filter takes a callback that reecives an item from data. 

```JS
data.filter(obj => /* return true if obj.title includes query */).map((obj, i) => {
		...
	})
```

That's only half correct, we also need to check the address. 

```JS
data.filter(obj => /* return true if obj.title includes query 
 or if obj.address includes query */).map((obj, i) => {
		...
	})
```

Let's break this function down into a longer form: 


```JS
data.filter((obj) => {
	// true is query is in title
	const inTitle = obj.title.includes(query)
	// true if query is in address
	const inAddress = obj.address.includes(query)
	// return true if either is true
	return inTitle || inAddress
}).map((obj, i) => {
		...
	})
```


