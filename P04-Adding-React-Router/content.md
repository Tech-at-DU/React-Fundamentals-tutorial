---
title: "Adding React Router"
slug: adding-react-router
---

Now we have a cool looking page, but what if we want to check out one of the cats?

Most websites have different pages you can visit. When you change pages, the page reloads and sends a new request to the server which then loads the page you are looking for. However, when you are building a single page application with something such as React, if you were to reload the window when you wanted to go to a new page, it would defeat the purpose of using react.

So how we get around this is with something called `React Router`. React router allows you to link to new parts of your page without having to refresh the window.

First things first, we need to download import `React Router`. 
 in our terminal we need to run the command:
 ```cmd
npm install react-router-dom --save
 ```
 Now go to `app.js` and import it at the top of the page
 ```js
import { BrowserRouter as Router, Route } from 'react-router-dom'
 ```
 For `React Router` to actually work, we need to wrap the entire app in our `Router`. So we are going to alter the return in our `app.js` to look like:
```jsx
 return(
 <Router>
 <div className="App">
 ...
 </div>
 </Router>
 )
```
Now we are all set up to use `React Router`

Let's start by learning to change our URL. 
 By default the `<a>` actually refreshes the screen before changing the URL. This is an issue because we don't want the page to reload ever.
 
 That's ok though because React Router gives us a solution. 
 React Router gives us a `<Link>` tag that acts just like an `<a>` tag, except without refreshing the page! all you have to do is give it a `to` attribute rather than an `href` attribute and you are good to go.
 ```xml
 <Link to="/images/kitten-0.jpeg">
 ```

 So let's update our `Project.js` file to reflect these changes
 at the top, we have to import our `Link`
 ```js
import { Link } from 'react-router-dom'
 ```

 and then we have to change our `<a>` tag to a `<link>`
 ```xml
 <div className='project'>
 ...
 <Link to={props.link}>Link to project</Link>
</div>
```

Now let's go back over to the `PageContent.js` file, and change the `link` attribute on the `Project` components to be something like `/home` and `/signup` but these can be whatever you want as long as they start with a backslash.

When we go back to look at the page and click the links, we see it updates the URL, but nothing on the page changes.

Before we fix that though, we should dry up or code a little bit. notice in the `PageContent.js` file, we repeat the same line of code many times. So let's get the computer to do that for us.

First things first, here are the images we will be using 
[images](https://drive.google.com/drive/folders/1x7vuBrK7riYPJaKCotfG9kF91vCcSlxv?usp=sharing)
These go in the public folder of the react app, outside of the src folder. 
They should all be in a folder called `images`, which is inside the `public` folder

Now we are going to create a new file in our `src` folder called `data.js` 
this will be where we get the data for our projects. 
inside of this file, we are going to export an array that contains our data.
```js
// Theres a lot here, feel free to copy paste
const data = [
 {
 title: '50 california',
 image: '/images/50-california-st.png',
 desc: 'A small plaza with groomed bushes and trees',
 },
 {
 title: '100 pine',
 image: '/images/100-pine.jpg',
 desc: 'beautiful water fountain',
 },
 {
 title: '101 california',
 image: '/images/101-california.jpg',
 desc: 'nice sitting area with plants',
 },
 {
 title: '343 sansome roof garden',
 image: '/images/343-sansome-roof-garden.jpg',
 desc: 'unique roof garden',
 },
 {
 title: '525 market street plaza',
 image: '/images/525-market-street-plaza.jpg',
 desc: 'large indoor plaza with a fountain',
 },
 {
 title: 'citigroup center',
 image: '/images/citigroup-center.jpg',
 desc: 'neat sitting area with a fountain',
 },
 {
 title: 'empire park',
 image: '/images/empire-park.jpg',
 desc: 'a green shady sitting area',
 },
 {
 title: '150 california garden terrace',
 image: 'images/garden-terrace-at-150-california.jpg',
 desc: 'garden terrace with a sitting area',
 },
 {
 title: 'transamerica redwood park',
 image: '/images/transamerica-redwood-park.jpg',
 desc: 'massive redwood park, with a fountain',
 },
]
export default data
```
So we have our data, now we need to do something with it, lets go back to our `PageContent.js` file. 

First, let's import our data at the top of the file
```js
import data from './data'
```

Then remove all of the `<Project>` components. 
We are going to use an array method known as array.map. This will allow us to make a list, do something to every element, and return a new list.
this is similar to the python `for i in array` but with some differences.

Inside our `projects` div, we are going to add our map function.
```js
...
 <div className="projects">
 { // this is to allow us to write js inside of our HTML
 // place is the element in the array
 // i is the index of the element
 data.map((place, i) => { //data takes a function as a parameter
 return ( //if you return HTML, it will be rendered
 <Project key={`${i}-${place.image}`} title={place.title} image={place.image} link={`${i}`} />
 )

 })
 }
 </div>
...
```

Ok, let's break down the map method a bit more.
let's take a look at just the first line
```js
data.map((place, i) => {})
```
The map method takes in a callback. A callback is a function that doesn't get called right away. So it's saving the function for later.

if you haven't seen a fat arrow function before, it's just another way to write a function in javascript. Rather than
```js
name = function(param) {

}
```
it looks like
```js
name = (param) => {

}
```
So if we look at the map function we are using, we see it gives us 2 parameters, place, and i. 
`place` is the element in the array, which in this case is our SF location 
and i is the index in the array

So now let's look at the HTML

```xml
<Project key={`${i}-${place.image}`} title={place.title} image={place.image} link={`${i}`} />
```
A few things are going on here, first off, if you ever map anything into HTML, you need to give each element a unique "key" so that react knows whats going on. that's what our `key={`${i}-${place.image}`}` attribute is doing. We are setting the key to the index of the element, and then the location of the image.

Then we have `title={place.title}` 
If you look at our `data.js` file, you can see that every item has a few key/value pairs, and one of the keys is the title, this is the same for `image={place.image}`

finally, we have `link={`${i}`}`
What this is doing is setting the `to` attribute of the link to be the index of the element. If you look at our website and click on any of the links now, you'll see it changes the navbar to have a number. This is what we will use to determine where the user wants more info about

Ok, now onto reading the URL, and rendering things off of it.

Let's go to the `app.js` file. 
We are going to be using the `react-router` component called `<Route>`

`<Route>` is what we use to conditionally render things based on the URL.
`<Route>` has a few different attributes, but the one we are worried about is `path`. We use the path to tell react what to render given a URL. We also need a `component` attribute, which is what to render.
```xml
<Route path='/home' component={home} />
```

In `app.js` we are going to alter the `<PageContent>` component to be rendered by a path.
```xml
...
<Route exact path='/' component={PageContent} />
...
```
Now if you go to the website, you may see just the header, if so make sure you are at the `/` route, meaning there shouldn't be any numbers after the slash. This is because of the `exact` attribute. if we left the `exact` out as we did in the example, then any URL that matched would render the component, but because the route is just a slash, every route matches it. So we add the `exact` to make sure it only renders when you are at the index route.

Back to the top of the page, let's import our data again,
```js
import data from './data'
```

We need a new component for our selected location, so let's create a new file in `src` called `SelectedProject.js` and copy almost all of the code from `Project.js` but we are going to change the height and width of the image
```jsx
import React from 'react'
import {Link} from 'react-router-dom'

function SelectedProject(props) {
 return (
 <div className='project'>
 <img alt="" src={props.image} width="600" height="400" />
 <h3>{props.title}</h3>
 <Link to={props.link}>Link to project</Link>
 </div>
 )
}

export default SelectedProject
```
Let's change the link to be back to the home page
```xml
<Link to='/'>Back to Home</Link>
```
And before we link back to home, lets add our description
```xml
<p>{props.desc}</p>
<Link to='/'>Back to Home</Link>
```

Now let's import our new component to `app.js` add some routes for our images 
So instead of making all of the routes ourselves, we are going to use a URL parameter. This will allow us to know what the number is, rather than making a route for every one of the locations.
```xml
import SelectedProject from 'SelectedProject.js'
...
<Route exact path='/' component={PageContent} />
<Route path='/:index' component={SelectedProject} />
...
```
adding a colon makes it a URL parameter, so we can access that back over in the `SelectedProject.js`. We are going to import our data, as well as add `useParams()` where we are importing `react-router`
```js
import data from './data'
import { Link, useParams } from 'react-router-dom'
```
`useParams` will allow us to grab all of the URL parameters in our route, in this case `index`

before the return statement in the function, we are going to create an index variable that will hold our index, and then a variable that will hold all of the data of the location

```jsx
function SelectedProject(props) {
 const { index } = useParams()
 const place = data[index]
 return (
 ...
```

Then we are going to update everything we were using props to gather to use our new place variable instead
```xml
<div className='project'>
 <img alt="" src={place.image} width="600" height="400" />
 <h3>{place.title}</h3>
 <p>{place.desc}</p>
 <Link to='/'>Back to Home</Link>
</div>
```

And congratulations you should now be able to navigate to and from different locations!

# Feedback and Review - 2 minutes

**We promise this won't take longer than 2 minutes!**

Please take a moment to rate your understanding of the learning outcomes from this tutorial, and how we can improve it via our [tutorial feedback form](https://forms.gle/2yApCdKchE5WkNKD6)

This allows us to get feedback on how well the students are grasping the learning outcomes and tells us where we can improve the tutorial experience.

