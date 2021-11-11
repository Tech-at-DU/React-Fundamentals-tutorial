# Adding React Router

The project you have built is described as a **single page application** but most web pages we use daily are built as, or at least act as, multi-page applications.

A single page application is just that: a single html page. Single page applications control the DOM by updating, adding, or removing elements. In this way they can function as multi-page applications.

A single page application built with React can display different content through components. Components can represent whole pages of content in a React app.

You can use the React Router library to make your React apps function like multi-page apps. You'll add a sub-page for each public space location. These sub-pages will show detailed information about each location.

# React Router

**React Router** is a library that can create a multipage experience in React. It does this by selectively rendering components. You'll define components that render at routes. A **route** is an address that appears in the address bar of the browser and is tied to a component. When the route in the address bar changes React Router renders a component to the page. 

To work with React Router it helps to understand some terminology.

- **Router** - Is the top level component that manages all routes and navigation
- **Routes** - A parent component that manages Routes
- **Route** - A component that displays another component

Think of the Router as the manager, you only need one of these. The Router checks the URL in the address bar and passes this information to its descendant Routes.

Imagine a website with three pages built with React using React Router. The Router and Route components might be arranged like this:

- Router
  - Routes
    - Route - Home Page
    - Route - About Page
    - Route - Map Page

A Route is responsible for displaying components. Routes have a path property: when the path matches the URL in the address, the Route displays the appropriate component, otherwise not.

In code this might look like:

```js
<Router>
  <Routes>
    <Route path="/" element={<App />}>
      <Route path="list" element={<POPOSList />} />
      <Route path="about" element={<About />} />
    </Route>
  </Routes>
</Router>
```

**Important!** The names: `Router`, `Routes` and `Route` are different by only a single character, but they are very different in function and must be used correctly. Watch your spelling!

# Getting started

The first step to using React Router is to import it.

Got to the terminal and run:

`npm install react-router-dom`

This should import the React Router libraries as a dependency to your project.

Coming up, you'll import `HashRouter` into `App.js`. This is a component that manages routes.

> Quick note! `HashRouter` and `BrowserRouter` are two options. They act the same in our app and only differ in how they handle the URL/Path.
>
> HashRouter includes a # in the URL, while BrowserRouter does not include the #.  
>
> For example a HashRouter URL might look like this:
>
> `http://localhost:3000/#/about`
>
> The same URL in BrowserRouter would look like this:
>
> `http://localhost:3000/about`
>
> Why use one or the other? In most cases they are interchangeable. Since we plan to publish the completed site to GitHub pages in the future, we're using HashRouter because GitHub pages doesn't work with BrowserRouter!

## Make an About page

Your site could use an About page. Let's create a new component! Adding this new page will give our site something to navigate to. 

Make a new file `src/About.js` with the following code:

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

This component will display a heading and a paragraph of text. You can add some styles later, and maybe a picture and more info like a map. For now we are concerned with Routes.

## Setting up the Router

In `index.js` you'll set up your `Router` and `Routes`. 

```JS
...
import App from './App';
import { HashRouter as Router, Routes, Route } from 'react-router-dom'
import About from './About'
import POPOSList from './POPOSList'

ReactDOM.render(
  <Router>
    <Routes>
      <Route path="/" element={<App />}>
        <Route path="/" element={<POPOSList />} />
        <Route path="about" element={<About />} />
      </Route>
    </Routes>
  </Router>,
  document.getElementById('root')
);
...
```

Notice that all `Route` components appear inside the `Routes` component. 

Also, notice that the `<Route path="/" element={<App />}>` contains the other routes! App contains the title/navbar and will appear on all pages. To make this work you're making the other routes children of this route. Notice the path is `/`. With this arrangement `POPOSList` and `About` components will appear inside `App`.

Look at the `element="..."` prop. This is the component that will be displayed by this route. 

Look at the `path="..."` prop for each route. This will determine what the address needs to be to display this component. Notice that both `App` and `POPOSList` are displayed at the `/` "root" route. 

### Nesting Routes

Above you nested the `POPOSList` and `About` inside the `/` route that displays the `App` component. To display those nested routes you need to add an outlet. 

```js
import { Outlet } from 'react-router-dom'

import './App.css';
import Title from './Title';

function App() {
  return (
    <div>
      <Title />
      <Outlet />
    </div>
  );
}

export default App;

```

Test your routes. We haven't added any navigation yet so at this point we need to test the routes manually by entering the routes in the address bar of the browser. 

Try these addresses in your browser: 

http://localhost:3000/#/

http://localhost:3001/#/about

The first should show the root page, and the second should show the about page. 

# Linking to Routes

This is working but we can't ask people to navigate to pages by typing the URL, people need something to click!

React Router provides a `NavLink` component. The `NavLink` sets the address to navigate to in our browser's URL bar, and navigates the user to that address. It's like the `<a>` tag but specific to React Router.

Add two links to the `Title` Component. Open `Title.js`. Add this to the top of the page:

```js
import { NavLink } from 'react-router-dom'
```

here you've imported `NavLink` from React Router DOM.

Now add two links to your `Title` in `src/Title.js`. Note below we also have the subtitle from an earlier stretch challenge:

```js
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

Notice that each `NavLink` has a `to` prop. This sets what the path in the address bar will become when you click this link.

Try it out in your browser!

The `NavLink`s need some style. `NavLink` translates to a regular anchor `<a>` tag in the DOM. You can treat these like any other tag/component:

In `src/Title.js`, give the NavLinks a class name:

```html
<NavLink to="/">List</NavLink>
<NavLink to="/about">About</NavLink>
```

Then, open `src/Title.css` and add some styles.

```CSS
.Title a {
  display: inline-block;
  padding: 0.5em 1em;
  color: rgba(255, 255, 255, 0.835);
  font-weight: bold;
  text-decoration: none;
}
```

This looks better, but you could do more! Currently the active link (the link that represents the current "page") doesn't stand out from the other links. It should, as this would help users understand where they are what they can do, thereby improving the UX (User eXperience).

We can run a function to determine what class name should be applied to any link. React Router will pass an `isActive` prop. This is a Boolean. True when the link is active and False when not. 

*Edit* your `NavLink`s in `src/Title.js` to be the following:

```js
<NavLink 
	className={({ isActive }) => isActive ? "nav-link-active" : "nav-link" }
	to="/">List</NavLink>
<NavLink 
	className={({ isActive }) => isActive ? "nav-link-active" : "nav-link" }
	to="/about">About</NavLink>
```

With these options, the selected `NavLink` will have the class: `nav-link-active`. You should add a style for this!

Add the following to `src/Title.css`:

```CSS
.Title .nav-link-active {
  color: #fff;
  border-bottom: 2px solid;
}
```

# Details page Route Parameters

Things are looking pretty good. Now let's tackle the details page. The details page will be a page that is dedicated to a single location. It will show all of the information for that location. Right now we show all locations on the List Page but the information is minimal. The details page will be a page dedicated to just one location.

Currently there are only a small number of spaces in our data list, but there are a lot more spaces that might be added in the future. We don't want to make a component for each space. Instead you will make a single component and pass props to it containing the information that needs to display.

When you made the list of `POPOSSpace` components, you passed all of the values the component displays into the component via props. You also made all of those components in the list with `map()`.

This time you'll take a different approach. In this situation you want to make a single component and you'll be displaying it with React Router as a Route. Router allows you to pass values to a Route through the URL/path. This is good for this use because the URL/path can be bookmarked, Which will allow visitors to bookmark a detail page or return to it directly by entering its URL.

### Making the Details Component

This component will be a lot like the `POPOSSpace` component but will show more details. Let's call it `POPOSDetails`.

Where the `POPOSpace` component showed the image, title, and address.  The `POPOSDetails` component will show all of the images (remember images in the data is an _array_), title, address, description, hours, and features of a single space.

Remember how all of the data is in the `sfpopos-data.json` file? Any of your components can import this file. As long as a component knows the index of the item in the data, it can display it.

The goal then is to pass the index to the `POPOSDetails` component, and `POPOSDetails` will get the information it needs from the data.

Make a new file named: `src/POPOSDetails.js`, and add the following code to it:

```js
// src/POPOSDetails.js

import React from 'react'
import { useParams } from 'react-router'
import data from './sfpopos-data.json'

function POPOSDetails(props) {
  const params = useParams()
  const { id } = params // Location index
  const { images, title, desc, hours, features, geo } = data[id]

  return (
    <div>
      <div>
        <img src={`${process.env.PUBLIC_URL}images/${images[0]}`} alt={title} />
      </div>

      <div>
        <h1>{ title }</h1>
        <p>{ desc }</p>
        <p>{ hours }</p>
        <p>{ features }</p>
        <p>{ geo.lat } { geo.lon }</p>
      </div>

    </div>
  )
}

export default POPOSDetails
```

The code above is just like the other components you've made. One small change is at the top you've imported `sfpopos-data.js`.

Here you imported the `useParams` hook from `react-router-dom`. You'll use this method to access any params that are part of a route. A param is part of the url that isn't used in the path. Later we are going to add the id of public space to the url. It might look like this: 

```
http://localhost:3000/#/details/32
```

Imagine number `32` is the id of the public space we want to see on the details page. 

On the next line you're using the `id` to get the data for the location at the index. Using deconstruction we can break object at that index down into: `images`, `title`, `desc`, `hours`, `features`, and `geo` coordinates.

The rest of the component is similar to the other components you wrote previously. Feel free to modify this and add styles. Notice that `images` is an array to display images. For example, you're using `images[0]` to get the first image in this array.

### Details Route

Add a new Route to `index.js`. This new route will be displayed as a child of the `App` component so it will need to be nested in that route! 

Open `App.js`, and add an import for `POPOSDetails.js` at the top:

```js
import POPOSDetails from './POPOSDetails'
```

Now add a new Route nested inside the `App` route:

```js
<Route path="/" element={<App />}>
  <Route path="/" element={<POPOSList />} />
  <Route path="about" element={<About />} />
  <Route path="/details/:id" element={<POPOSDetails />} />
</Route>
```

Notice the path in the new Route: `path="/details/:id"`. Here `id` defines a variable that will get it's value from the url: 

`http://localhost:3000/#/details/0` - `id` would be 0

or

`http://localhost:3000/#/details/42` - `id` would be 42

You can test your work by trying these addresses in your browser:

`http://localhost:3000/#/details/0`
`http://localhost:3000/#/details/1`
`http://localhost:3000/#/details/2`

What's important here is your app can find a details page by entering a URL. A user now could go directly to a page by entering that address, they could also bookmark a page.

The next step is to add some links that navigate to these routes. 

### Passing the id

To be able to link to something with an id we need to have that id. Here in this step you'll pass the id to a `POPOSSpace` from `POPOSList`.

Open `POPOSList.js`. Find the line where you mapped data to the `POPOSSpace` via the `spaces` const, and edit it to be the below code. **Notice the small changes with `i` in map() and the added `id` attribute**:

```JS
const spaces = data.map(({ title, address, images, hours }, i) => {
  return (
    <POPOSSpace
      id={i}
      key={title}
      name={title}
      address={address}
      image={images[0]}
      hours={hours}
    />
  )
})
```

On the first line there is a second parameter to:

`map(obj, i)`, or

`map({ ... }, i)`. Here is the whole line as it is shown above:

`const spaces = data.map(({ title, address, images, hours }, i) => {`

The second change is the added prop `id={i}` in the `POPOSSpace` component.

```html
<POPOSSpace
  id={i} // added new prop id here!
  ...
/>
```

When using `map()` this method provides the index of the element as a second parameter. This is useful in many cases, you're using it here as the index of the data from our JSON data.

# Linking to Details

With the last piece in place you can get to the details Route. This is good but you really want visitors to be able to click a location in the list and show its details.

For a page to link to its details, it needs to know the index in the array where its data is stored. This will happen in `POPOSList`.

You can also do this by using a `<Link>` component. `<Link>` is a component provided by React Router for linking/navigating to different Routes.

`Link` is different from `NavLink` in that `NavLink` is used for top level navigation that would be visible on all pages. `Link` on the other hand is for general navigation that might appear anywhere else. The big difference is `NavLink` offers the extra feature of `activeClassName` and `Link` doesn't have this.

Let's make some links in the `POPOSSpace`. It's probably best if people can click both the title and image to link to the detail page.

In `src/POPOSpace.js`, import the Link component at the top.

```js
import { Link } from 'react-router-dom'
```

Since id should now be passed as a prop you can access it with:

`props.id`

or deconstruct it with:

`const { id } = props`

Or if you're already deconstructing props just add it to the list:

`const { name, image, address, hours, id } = props`

In `src/POPOSpace.js`, first add `id` to your props. Then wrap the `img` in a `Link`. You should have something like this:

```js
const { name, image, address, hours, id } = props

...

<Link to={`/details/${id}`}>
  <img src={`${process.env.PUBLIC_URL}images/${image}`} width="300" height="300" alt="Hello" />
</Link>
```

Notice the `to` path! Remember the path will look for a param following the `/`. Here the param will be the id!

In `src/POPOSpace.js`, do the same with the title:

```js
<h1>
  <Link to={`/details/${id}`}>
    {name}
  </Link>
</h1>
```

Check your work! Clicking a link should take you to the detail page for that location.

# Feedback and Review - 2 minutes

If you found any technical issues or spelling errors, or just think of a good suggestions to improve the code shown in the tutorial post an issue to the GitHub repo: https://github.com/MakeSchool-Tutorials/React-Fundamentals

Give us general feedback on the tutorial, **we promise this won't take longer than 2 minutes!**

Please take a moment to rate your understanding of the learning outcomes from this tutorial, and how we can improve it via our [tutorial feedback form](https://forms.gle/2yApCdKchE5WkNKD6)

This allows us to get feedback on how well the students are grasping the learning outcomes and tells us where we can improve the tutorial experience.

# Note on remaining chapters

The remaining chapters are optional, and meant for those who want some extra practice with React. At this point you're ready to take on the rest of your course, but if you want some more practice, keep going!

# Next

Click [here](../P06-Organizing-Files/) to move onto the next (optional) section about organizing files.
