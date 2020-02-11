---
title: "Adding React Router"
slug: adding-react-router
---

Now you have a single page that shows a list of projects. What you wanted your single page website to display multiple pages. For example imagine you want to click on a project and show a page dedicated to that project.

Simple web sites use different files loaded for each page of content. Single pages are just a single and are never reloaded. 

If this is the case how does a single page site show multiple pages? With React this is done by creating components for each page and showing only the component for the currently visible page. 

React Router is a powerful tool that manages components to make your React projects act like mulitpage web sites. You should use it for your project!

The first step is to import `React Router`. 

In terminal run the command:
```cmd
npm install react-router-dom --save
```

Now go to `app.js` and import it at the top of the page

```js
import { BrowserRouter as Router, Route } from 'react-router-dom'
 ```

For `React Router` to work, you need to **wrap the entire app in `Router`**. You are going to alter the return in your `app.js` component to look like:

```jsx
return(
  <Router>
    <div className="App">
    ...
    </div>
  </Router>
 )
```
Now you are all set up to use `React Router`.

Start by learning to change the URL. 

The `<a>` refreshes loads a new page. This is an issue because you don't want the page to reload it would break your single page application.

React Router gives us a solution. 

React Router gives us the `<Link>` component. This component acts just like an `<a>` tag, except without refreshing the page! `Link` only chnages the URL without refreshing the page.

Set the `to` attribute rather than an `href` attribute when using `Link`.

```xml
<Link to="/images/kitten-0.jpeg">
```

Update our `Project.js` file.

At the top, import `Link`:

```js
import { Link } from 'react-router-dom'
```

Add a Link that will act as navigation. This link will navigate to a "Page" by showing a new component. 

```xml
<div className='project'>
  ...
  <Link to={props.link}>Link to project</Link>
</div>
```

Go back to the `PageContent.js` file, and change the `link` attribute on the `Project` components to be something like `/home` and `/signup`. These can be whatever you want as long as they start with a backslash.

When you test the page and click the links, you see it updates the URL, but nothing on the page changes. To 'navigate to another "page" you need to create some `Routes`. You'll do that in an upcoming step. Before that you will make a few changes to the existing code. 

Ntice in the `PageContent.js` file has repeated a similar line of code many times. Better to make a loop here. 

Download the images we will be using:

[images](https://drive.google.com/drive/folders/1x7vuBrK7riYPJaKCotfG9kF91vCcSlxv?usp=sharing)

They should all be in a folder called `images`, which is inside the `public` folder.

Now create a new file in the `src` folder called `data.js`.

This will be the data that descibes all of your projects. In future projects you might follow a simialr pattern for building an but this data would be laoded from a server as JSON.

Inside `data.js`, add the following. 

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

Now that your data is defined go back to `PageContent.js` file. 

First, import your data at the top of the file.

```js
import data from './data'
```

Then remove all of the `<Project>` components. 

You're going to use `array.map` to  transform the arrays of JavaScript objects in the data array into an array of components you can display. 

Inside the `projects` div, map data to an array of components.

```js
...
 <div className="projects">
  {
    // place is the element in the array
    // i is the index of the element
    data.map((place, i) => { // data takes a function as a parameter
      return ( // Return a component
      <Project 
        key={`${i}-${place.image}`} 
        title={place.title} 
        image={place.image} 
        link={`${i}`} 
      />
    )
  })
 }
 </div>
...
```

Let's break down the map method.

Take a look at the first line:

```js
data.map((place, i) => { ... })
```

The map method takes in a function as it's first parameter. It calls this function once for each item in the array (`data`)

The example uses an arrow function. These are similar to the functions you've written before. 

Here is a function:

```js
const name = function(param) {
  ...
}
```

Here is the same function written as an arrow function:

```js
const name = (param) => {

}
```

The sample code for uses this type of function. 

```js
data.map((place, i) => { ... })
```

The function provided as a parameter to map is called once for each item in the array. This function takes two parameters. The first is `place` and will be one of the values from the array, the second parameter `i` i will be the index of that value in the array. 

The function supplied to map needs to return a values. Each value returned is added to a new array which returned by `map()`. In this way `Array.map()` transform an array of one type into an array of another type.  

Take a look at the JSX returned inside the mapping function. 

```xml
<Project 
  key={`${i}-${place.image}`} 
  title={place.title} 
  image={place.image} 
  link={`${i}`} 
/>
```

Here you are defining a new component using JSX and defing four attributes. The values for these attributes are taken from the places object. 

Take a look at the data array in data.js. You'll see all of the properties taken from place exist on each object in the array.

Go to the `app.js` file. Now it's time to create some routes.

`<Route>` is a component that is rendered by React Router when the URL matches the path of the route. 

**Note: don't confuse Router and Route!** Router is a component that manages Routes. 

Set the path of a route with the path attribute: 

```xml
<Route path='/home' component={home} />
```

In `app.js` alter the `<PageContent>` component to be rendered by a path.

```xml
...
<Route exact path='/' component={PageContent} />
...
```

Now the `PageContent` component will be rendered only when the url is exactly `/`. 

At the top of the page import data:

```js
import data from './data'
```

Make a new Component to show a selected project. Clicking on a project will display the selected project and show details about that project. 

Creat a new file: `SelectedProject.js`. Define a new component in this file:
```jsx
import React from 'react'
import {Link} from 'react-router-dom'

function SelectedProject(props) {


  return (
    <div className='project'>
      <img alt="" src={place.image} width="600" height="400" />
      <h3>{place.title}</h3>
      <p>{place.desc}</p>
      <Link to='/'>Back to Home</Link>
    </div>
  )
}

export default SelectedProject
```

Notice the Link will take up back to the homepage, since it sets the url to `/`.

Import the new component in `app.js`. 

```JS
import SelectedProject from './SelectedProject.js'
```

Add a Route to display a selected project.

```xml
...
<Route exact path='/' component={PageContent} />
<Route path='/:index' component={SelectedProject} />
...
```

Adding a colon in the path makes it a URL parameter, you can access this value in `SelectedProject.js`. Go to that file now. 

Import our data, as well as add `useParams()`:

```js
import data from './data'
import { Link, useParams } from 'react-router-dom'
```

`useParams` allows you to grab all of the URL parameters in a route, in this case it will give you the value of `index`.

Before the return statement get the value of index with `useParams()`. Then get the data object from the data array with `index`.

```jsx
function SelectedProject(props) {
  const { index } = useParams()
  const place = data[index]
  
  return (
    ...
```

Earlier you used `place` in this block now it is defined! 

```xml
<div className='project'>
  <img alt="" src={place.image} width="600" height="400" />
  <h3>{place.title}</h3>
  <p>{place.desc}</p>
  <Link to='/'>Back to Home</Link>
</div>
```

And congratulations you should now be able to navigate to and from different locations!

