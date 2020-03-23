---
title: "Adding React Router"
slug: adding-react-router
---

The project you have built is described as a single page application but most web web pages we use daily are built as, or at least, act as multi-page applications. 

A single page applicatio is just that: a single html page. Single page applications control the DOM by updating, adding, or removing elements. In this way they can function as multi-page applicqtions. 

A single page application built with React can display different content through components. Components can represent whole pages of content in a React app. Conveniently someone has a made a library just for this purpose! 

You will use that library in this step to add a sub-page for each of the locations. These sub-pages will show detailed information about each location. 

## React Router 

React Router is a library the purpose of which is to create a multipage experience in React. It does this by rendering and not rendering components. You'll define components that render at routes. A route is an address that appears in the address bar of the browser. 

To work with React Router it helps to understand the terminology. 

- **Router** - A parent component that manages Routes
- **Route** - A component that displays another component

Think of Router as the manager, you only need one of these. The Router checks the URL in the address bar and passes this information to it's descendant Routes. 

A Route id responsible for displaying component. Routes each have a path property. When the path matches the URL in the address the Route displays their component, otherwise not. 

Imortant! The two names: Router and Route are different by only a single character but they are very different in fucntion and must be used correctly. Watch your spelling! 

### Getting started 

The first step to using React Router is to import. Got to the terminal and run: 

`npm install react-router-dom`

This should import the React Router libraries as a dependency to your project. 

In App.js you'll import `HashsRouter`. This a component that manages routes. 

Quick note! `HashRouter` and `BrowserRouter` are two options. They act the same in our app and only differ in how they handle the URL. 

HashRouter inlcudes a # in the URL, while BrowserRouter does not include the #.  

For example a HashRouter URL might look like this: 

`http://localhost:3000/#/about`

The same URL in BrowserRouter would look like this: 

`http://localhost:3000/about`

Why use one or the other? In most cases they are interchangeable. Since I have this plan for you to publish your site to GitHub pages in future I chose HashRouter. GitHub pages doesn't work with BrowserRouter! 

## Setting up the Router

Router manages routes. It should be a top level component. For this reason you'll define your Router in App.js. 

Open App.js. Import `HashRouter` and `Route` at the top. 

`import { HashRouter as Router, Route } from 'react-router-dom'`

Why `HashRouter as Route`? This is an alias. You're importing HashRouter but using it under the name Router instead. 

Next, Wrap your entire App in the `<Router>` component. 

```JSX
function App() {
  return (
    <Router>

      <div className="App">
        <Title />
        <POPOSList />
      </div>

    </Router>
  );
}
```

Notice how Router surrounds everything. 

### Adding Routes

A route displays a component at a path. You want the POPOSList to display at the `/` path. 

```JSX
function App() {
  return (
    <Router>
      <div className="App">
        <Title />
        <Route path="/" component={POPOSList}/>
      </div>
    </Router>
  );
}
```

Notice when you created the Route you used two props: path and component. Path defines the URL that will makes component display. 

The `/` route is the root route. So the list should display now. In your browser add something to the end of the path in the address bar. Try this: 

`http://localhost:3000/#/about`

The list should still display. This is because the `/` is contained in the route above. 

`http://localhost:3000/# / about`

You can make the route an exact route. In the case the list would only display when the route matches exactly. 

Make this change: 

`<Route exact path="/" component={POPOSList}/>`

Now try these paths in the address bar of the browser. 

This should display the list:

`http://localhost:3000/#/` 

Using this address should not display the list, It's not an exact match.

`http://localhost:3000/#/about`

Notice the Title Component is displayed every time. It's not managed by a Route so it's always displayed. 

### Adding another route

Your site could use an About page. Create a new component. Make a new File: 

`About.js`

Add the following code here: 

```JS
import React from 'react'

function About() {
  return (
    <div>
      <h1>About SFPOPOS</h1>
      <p>POPOS are publicly accessible spaces in 
        forms of plazas, terraces, atriums, small 
        parks, and even snippets which are provided 
        and maintained by private developers. In San 
        Francisco, POPOS mostly appear in the Downtown 
        office district area.</p>
    </div>
  )
}

export default About
```

This is simple component that will display a heading and a paragraph of text. You can add some styles later, and maybe a picture and more info, or a map. For now we are concerned with Routes. 

Back in `App.js` import the `About` Component at the top. 

`import About from './About'`

Inside the Router add a new Route. 

```JSX
...
<Router>
  <div className="App">

    <Title />

    <Route exact path="/" component={POPOSList}/>
    <Route path="/about" component={About} />

  </div>
</Router>
...
```

Notice the new route as a path of `/about` and renders the `About` component. 

Save your work and try it in the browser. Try these two paths in the address bar: 

Should display teh list

`http://localhost:3000/#/` 

Should display the about page

`http://localhost:3000/#/about`

### Linking to Routes

This is all working but we can't ask people to navigate to pages by typing the URL, people need something to click!

React Router provdes a `NavLink` component. The NavLink sets the address in bar. It's like the `<a>` tag but specific to React Router. 

Add two links to the Title Component. Open `Title.js`. Add this to the top of the page: 

`import { NavLink } from 'react-router-dom'`

here you imported `NavLink` from React Router Dom. 

Now add two links 

```JSX
function Title() {
  return (
    <div className="Title">
      <header>
        <h1>SFPOPOS</h1>
        <div className="Title-Subtitle">San Francisco Privately Owned Public Open Spaces</div>

        <div>
          <NavLink to="/">List</NavLink>
          <NavLink to="/about">About</NavLink>
        </div>

      </header>
    </div>
  )
}
```

Notice each NavLink has a `to` prop. This sets what path in the address bar will become when you click this link. 

Try it out. 

The navlinks need some style. NavLink translates to a regular anchor `<a>` tag in the DOM. You can treat these like any other tag/component. 

Give the NavLinks a class name:

```JSX
<NavLink className="nav-link" to="/">List</NavLink>
<NavLink className="nav-link" to="/about">About</NavLink>
```

Open `Title.css` and add some styles. 

```CSS
.nav-link {
  display: inline-block;
  padding: 0.5em 1em;
  color: #fff;
  text-decoration: none;
}
```

This look better but you could do more! Currently the active link (the link that represents the current "page") is doesn't stand out from the other link. It should, this would help users understand where they are what they can do and improve the UX (User eXperience). 

Luckily NavLink has a prop for this! Add the `activeClassName` prop/attribute to each of the NavLinks. This prop defines a class name that will be added to the element when that link is the currently link. 















Now you have a single page that shows a list of projects. What you wanted your single page website to display multiple pages. For example imagine you want to click on a project and show a page dedicated to that project.

Simple web sites use different files loaded for each page of content. Single pages are just a single and are never reloaded.

If this is the case how does a single page site show multiple pages? With React this is done by creating components for each page and showing only the component for the currently visible page.

React Router is a powerful tool that manages components to make your React projects act like mulitpage web sites. You should use it for your project!

The first step is to import `React Router`.

> [action]
>
> In terminal run the command:
>
```bash
npm install react-router-dom --save
```
>
> Now go to `src/App.js` and import it at the top of the page
>
```js
import { BrowserRouter as Router, Route } from 'react-router-dom';
```

For `React Router` to work, you need to **wrap the entire app in `Router`**.

> [action]
>
> Alter the return in your `src/App.js` component to look like the following:

```js
// src/App.js
>
...
>
function App() {
  return (
    <Router>
        <div className="App">
          <Title />
          <PageContent />
        </div>
    </Router>
  );
}
```
Now you are all set up to use `React Router`!

Let's start by learning to change the URL.

The `<a>` loads a new page. This is an issue because you don't want the page to reload it would break your single page application.

React Router gives us a solution.

React Router gives us the `<Link>` component. This component acts just like an `<a>` tag, except without refreshing the page! `Link` only changes the URL without refreshing the page.

**Make sure to set the `to` attribute rather than an `href` attribute when using `Link`:**

```xml
<Link to="/images/kitten-0.jpeg">
```

> [action]
>
> At the top of `src/Project.js`, import `Link`:
>
```js
import { Link } from 'react-router-dom'
```
>
> Update the `Project` function to add a Link that will act as navigation. This link will navigate to a "Page" by showing a new component.
>
```js
function Project(props) {
    // Note the added className as well
    return (
        <div className='project'>
            <img src={props.image} width="300" height="200" />
            <h3>{props.title}</h3>
            <Link to={props.link}>Link to project</Link>
        </div>
    )
}
```

Now we need to add proper `link` attributes to the projects.


> [action]
>
> In `src/PageContent.js`, change the `link` attributes on the `Project` components to be something like `/home` and `/signup`. These can be whatever you want as long as they start with a backslash.

When you test the page and click the links, you see it updates the URL, but nothing on the page changes. To 'navigate to another "page" you need to create some `Routes`. You'll do that in an upcoming step. Before that you will make a few changes to the existing code.

Notice in `src/PageContent.js` we repeat a similar line of code many times. It would be better to make a loop here.

> [action]
>
> Download the images we will be using:
> [images](https://drive.google.com/drive/folders/1x7vuBrK7riYPJaKCotfG9kF91vCcSlxv?usp=sharing)
>
> Transfer the images to your `public/images` folder.

Now we need to add some data. This data will that describe all of your `Projects`. In future projects, you might follow a similar pattern, but the data would be loaded from a server as JSON.


> [action]
>
> Now create a new file in the `src` folder called `data.js`. Inside `src/data.js`, add the following:
>
```js
// src/data.js
>
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

Now that your data is defined, let's use it in `PageContent`

> [action]
>
> In `src/PageContent.js`, import your data at the top of the file:
>
```js
// src/PageContent.js
>
import data from './data';
```
>
> Then remove all of the `<Project>` components in the `return` function

You're going to use `array.map` to  transform the arrays of JavaScript objects in the data array into an array of components you can display.

> [action]
>
> In `src/PageContent.js`, update the `PageContent` function to be the following:
>
```js
// src/PageContent.js
>
...
>
function PageContent() {
   return (
       <div className="PageContent">
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
   )
}
>
...
```

Your project should now look like the following:

![city-images](./assets/city-images.png)

# Breaking Down the Map method

There was a lot going on in that map method. Let's break it down:

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

The function provided as a parameter to map is called once for each item in the array. This function takes two parameters. The first is `place` and will be one of the values from the array, the second parameter `i` will be the index of that value in the array.

The function supplied to map needs to return values. Each value returned is added to a new array which is returned by `map()`. In this way `Array.map()` transforms an array of one type into an array of another type.  

Take a look at the JSX returned inside the mapping function.

```xml
<Project
  key={`${i}-${place.image}`}
  title={place.title}
  image={place.image}
  link={`${i}`}
/>
```

Here you are defining a new component using JSX and defining four attributes. The values for these attributes are taken from the places object.

Take a look at the data array in `src/data.js`. You'll see all of the properties taken from `place` exist on each object in the array.

Now it's time to create some routes!

# Routes

`<Route>` is a component that is rendered by React Router when the URL matches the path of the route.

**Note: don't confuse Router and Route!** Router is a component that manages Routes.

We can set the path of a route with the path attribute:

```xml
<Route path='/home' component={home} />
```

> [action]
>
> In `src/App.js`, alter the `<PageContent>` component to be rendered by a path:
>
```js
// src/App.js
>
...
>
function App() {
  return (
    <Router>
        <div className="App">
          <Title />
          <Route exact path='/' component={PageContent} />
        </div>
    </Router>
  );
}
...
```

Now the `PageContent` component will be rendered only when the url is exactly `/`.

# Selected Project

Let's make a new Component to show a selected project. Clicking on a project will display the selected project and show details about that project.

> [action]
>
> At the top of `src/App.js`, import our data:
>
```js
// src/App.js
>
import data from './data'
```

Now let's create a new component: `SelectedProject`

> [action]
>
> Create a new file: `src/SelectedProject.js`. Define a new component in this file:
>
```js
// src/SelectedProject.js
>
import React from 'react'
import {Link} from 'react-router-dom'
import data from './data'
import { Link, useParams } from 'react-router-dom'
>
function SelectedProject(props) {
  const { index } = useParams()
  const place = data[index]
>
  return (
    <div className='project'>
      <img alt="" src={place.image} width="600" height="400" />
      <h3>{place.title}</h3>
      <p>{place.desc}</p>
      <Link to='/'>Back to Home</Link>
    </div>
  )
}
>
export default SelectedProject
```

<!-- -->

> [info]
>
> `useParams` allows you to grab all of the URL parameters in a route, in this case it will give you the value of `index`.

Notice the `Link` will take us back to the homepage, since it sets the url to `/`.

> [action]
>
> Import the new component in `app.js`.
>
```JS
// src/App.js
>
import SelectedProject from './SelectedProject';
>
...
```
>
> Next let's Add a `Route` to display a selected project. Place it underneath the `Route` for `PageContent`
>
```xml
...
<Route exact path='/' component={PageContent} />
<Route path='/:index' component={SelectedProject} />
...
```

Adding a colon in the path makes it a URL parameter.

Earlier you used `place` in this block now it is defined!

```xml
<div className='project'>
  <img alt="" src={place.image} width="600" height="400" />
  <h3>{place.title}</h3>
  <p>{place.desc}</p>
  <Link to='/'>Back to Home</Link>
</div>
```

Clicking on a project link should take you to a page that looks like the following:

![selected-project](./assets/selected-project.png)

**Congratulations you should now be able to navigate to and from different locations!**

# Feedback and Review - 2 minutes

**We promise this won't take longer than 2 minutes!**

Please take a moment to rate your understanding of the learning outcomes from this tutorial, and how we can improve it via our [tutorial feedback form](https://forms.gle/2yApCdKchE5WkNKD6)

This allows us to get feedback on how well the students are grasping the learning outcomes and tells us where we can improve the tutorial experience.
