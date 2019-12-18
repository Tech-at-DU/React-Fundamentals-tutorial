---
title: "Adding React Router"
slug: adding-react-router
---

# React Router

react Router is a library that adds navigation to your React projects. You would use React Router to make your Single Page Applications built with React act like a multi-page web site. 

Now you have a nice looking single page. What if you wanted to give each cat it's own page? 

Most websites have different pages you can visit. When you change pages, the page reloads and sends a new request to the server which then loads the page you are looking for. However, when you are building a *single page application* with something such as React loading a new page reloads the window and starts your application over again. 

**Single Page Applications** dont't refresh/reload the content of browser. Instead Single Page Applications change the content displayed in the DOM. In other words a Single Page Application changes the HTML displayed in the window without loading a new file. 

In React this happens by controlling which components are displayed. You can think and design your applciations where components are the pages of your web site. 

React router allows you to link to new parts of your page without having to refresh the window.

## Getting started with React Router

You'll need to install React Router then use the components this package provides to create navigation. 

### Install React Router Dom

React Router provides a few different routers. You'll use React Router DOM for this project because it works with the Browser. 

First things first, we need to download import `React Router`. in our terminal we need to run the command:
 
 ```bash
npm install react-router-dom --save
 ```
 
 Now go to `App.js` and import it at the top of the page:
 
 ```js
import { BrowserRouter as Router, Route } from 'react-router-dom'
 ```
 
For `React Router` to work you need to wrap the entire app (all other components) in a `Router`. Alter the return in our `App.js` to look like:

```jsx
 return(
   <Router>
     <div className="App">
       ...
     </div>
   </Router>
  )
```

Now we are all set up to use `React Router` to navigate to different routes. 

Let's start by learning to change our URL. 

By default the `<a>` actually refreshes the screen before changing the URL. This would be an issue because we don't want the page to reload, ever.

React Router gives us a `<Link>` tag that acts just like an `<a>` tag, except without refreshing the page! all you have to do is give it a `to` attribute rather than an `href` attribute and you are good to go.

 ```JSX
 <Link to="/images/kitten-0.jpeg">
 ```

 Update your `Project.js` file to reflect these changes
 at the top, we have to import our `Link`
 
 ```js
import { Link } from 'react-router-dom'
 ```

Next change your `<a>` tag to a `<Link>` (note the case!) and the `href` attribute to `to`:
 
 ```xml
 <div className='project'>
 ...
 <Link to={props.link}>Link to project</Link>
</div>
```

Now go back to the `PageContent.js` file, and change the `Link` attribute on the `Project` components to be something like `/home` and `/signup` but these can be whatever you want as long as they start with a backslash.

View your project in your browser. Click one of the links. The page doesn't change but the url in the address bar does. It should show the value you set as the link. For example: `/home` or `/signup`. This is still not what we want but we're almost there. 

### Improving the code

There is an improvement you can make before continuing. Currently the you've written `<Project ... />` 6 times. This might be better handled with a loop or an Array.

First things first, here are the images we will be using:

[images](https://drive.google.com/drive/folders/1x7vuBrK7riYPJaKCotfG9kF91vCcSlxv?usp=sharing)

These go in the public folder of the react app, outside of the src folder. They should all be in a folder called `images`, which is inside the `public` folder

Create a new file in our `src` folder called `data.js`.

This will hold an array that describes each of the "Projects" and will include the title, image url, and link url for each. 

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

Now that you have data, you need to do something with it, lets go back to your `PageContent.js` file. 

First, let's import our data at the top of the file
```js
import data from './data'
```

Remove all of the `<Project ... />` components. 

Data is an array of objects, you want to turn these into an array Components. 

In the `PageContent` component, inside the function but before `return` add the following: 

```js
...
function PageContent() {
  
  const projects = data.map((place, i) => {
    return <Project key={`${i}-${place.image}`} title={place.title} image={place.image} link={`${i}`} />
  })

  // Replace components with array here:
  return (
    <div className="PageContent">
      {projects}
    </div>
  )
}
...
```

Ok, let's break down the map method a bit more. Take a look at the section before return. 
```js
const projects = data.map((place, i) => {
  return <Project key={`${i}-${place.image}`} title={place.title} image={place.image} link={`${i}`} />
})
```

The map method takes in a callback. A callback is a function that doesn't get called right away. So it's saving the function for later.

if you haven't seen a fat arrow function before, it's just another way to write a function in javascript. Rather than

```js
const myFunction = function(param) {

}
```

An arrow function would look like this:

```js
const myFunction = (param) => {

}
```

In the example the function takes 2 parameters, place, and i. `place` is the element in the array, which in this case is our SF location and `i` this element's index in the array

So now let's look at the HTML

```JSX
<Project key={`${i}-${place.image}`} title={place.title} image={place.image} link={`${i}`} />
```

Now take a look at the changes after `return`

```JSX
return (
  <div className="PageContent">
    {projects}
  </div>
)
```

Here you put the array `projects` where you want all of the Components in the array to be displayed. React is smart, if you try and render an array of components React will automatically loop over the array and display all of the elements. 

(this only applies when the array contains components!)

When you do this React asks one favor in return: it wants each component in the array to have a `key` prop. Take another look at the map function. You'll see that you gave each component a key prop. 

```JSX
<Project key={`${i}-${place.image}`} title={place.title} image={place.image} link={`${i}`} />
```

The value for a key can be anything as long as keys in a collection are unique. 

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

