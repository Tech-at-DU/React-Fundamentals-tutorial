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
```