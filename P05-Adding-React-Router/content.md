---
title: "Adding React Router"
slug: adding-react-router
---

The project you have built is described as a **single page application** but most web pages we use daily are built as, or at least act as, multi-page applications.

A single page application is just that: a single html page. Single page applications control the DOM by updating, adding, or removing elements. In this way they can function as multi-page applications.

A single page application built with React can display different content through components. Components can represent whole pages of content in a React app.

You can use the React Router library to make your React apps function like multi-page apps. You'll add a sub-page for each public space location. These sub-pages will show detailed information about each location.

# React Router

**React Router** is a library that can create a multipage experience in React. It does this by selectively rendering components. You'll define components that render at routes. A **route** is an address that appears in the address bar of the browser.

To work with React Router it helps to understand some terminology.

- **Router** - A parent component that manages Routes
- **Route** - A component that displays another component

Think of the Router as the manager, you only need one of these. The Router checks the URL in the address bar and passes this information to its descendant Routes.

Imagine a website with three pages built with React using React Router. The Router and Route components might be arranged like this:

- Router
  - Route - Home Page
  - Route - About Page
  - Route - Map Page

A Route is responsible for displaying components. Routes have a path property: when the path matches the URL in the address, the Route displays the appropriate component, otherwise not.

In code this might look like:

```js
<Router>
  <Route path='/home' ... />
  <Route path='/about' ... />
  <Route path='/home' ... />
</Router>
```

**Important!** The two names: Router and Route are different by only a single character, but they are very different in function and must be used correctly. Watch your spelling!

# Getting started

The first step to using React Router is to import it.

> [action]
>
> Got to the terminal and run:
>
> `npm install react-router-dom`

This should import the React Router libraries as a dependency to your project.

Coming up, you'll import `HashRouter` into `App.js`. This is a component that manages routes.

> [info]
>
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

## Setting up the Router

Router manages routes. It should be a top level component. For this reason you'll define your Router in `App.js`.

> [action]
>
> Open `App.js`. Import `HashRouter` and `Route` at the top.
>
```js
import { HashRouter as Router, Route } from 'react-router-dom'
```

Why `HashRouter as Router`? This is an alias. You're importing HashRouter but using it under the name `Router` instead. This will make it easier to make changes in the future if needed.

> [action]
>
> Next, Wrap your entire App in the `<Router>` component.
>
```JS
function App() {
  return (
    <Router>
>
      <div className="App">
        <Title />
        <POPOSList />
      </div>
>
    </Router>
  );
}
```

Notice how Router surrounds everything. Routes must be children of a Router!

### Adding Routes

A route displays a component as a path. You want the `POPOSList` to display at the `/` path.

> [action]
>
> Update the `App` function in `App.js` to the following:
>
```js
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

Notice when you created the Route you used two props: `path` and `component`. Path defines the URL that will make the component display.

The `/` route is the root route. So the list should display now at `http://localhost:3000/`. In your browser, add something to the end of the path in the address bar, and see what happens when you try to navigate to it. Try this as an example:

`http://localhost:3000/#/about`

The list should still display. This is because the `/` is contained in the route above.

You can make the route an exact route. In this case the list would only display when the route matches exactly.

> [action]
>
> Make this change to the `Route` in `App.js`:
>
```html
<Route exact path="/" component={POPOSList}/>
```

Now try these paths in the address bar of the browser:

This should display the list:

`http://localhost:3000/#/`

Using this address should not display the list, It's not an exact match.

`http://localhost:3000/#/about`

Notice the `Title` Component is displayed every time. It's not managed by a Route so it's always displayed.

## Adding another route

Your site could use an About page. Let's create a new component!

> [action]
>
> Make a new file `src/About.js` with the following code:
>
```JS
import React from 'react'
>
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
>
export default About
```

This component will display a heading and a paragraph of text. You can add some styles later, and maybe a picture and more info like a map. For now we are concerned with Routes.

> [action]
>
> Back in `App.js` import the `About` Component at the top.
>
```js
import About from './About'
```
>
> Inside the `Router`, add a new `Route`:
>
```html
...
<Router>
  <div className="App">
>
    <Title />
>
    <Route exact path="/" component={POPOSList}/>
    <Route path="/about" component={About} />
>
  </div>
</Router>
...
```

Notice the new route has a path of `/about` and renders the `About` component.

Save your work and try it in the browser. Try these two paths in the address bar:

Should display the list

`http://localhost:3000/#/`

Should display the about page

`http://localhost:3000/#/about`

# Linking to Routes

This is working but we can't ask people to navigate to pages by typing the URL, people need something to click!

React Router provides a `NavLink` component. The `NavLink` sets the address to navigate to in our browser's URL bar, and navigates the user to that address. It's like the `<a>` tag but specific to React Router.

> [action]
>
> Add two links to the Title Component. Open `Title.js`. Add this to the top of the page:
>
```js
import { NavLink } from 'react-router-dom'
```

here you've imported `NavLink` from React Router DOM.

> [action]
>
> Now add two links to your `Title` in `src/Title.js`. Note below we also have the subtitle from an earlier stretch challenge:
>
```js
function Title() {
  return (
    <div className="Title">
      <header>
        <h1>SFPOPOS</h1>
        <div className="Title-Subtitle">San Francisco Privately Owned Public Open Spaces</div>
>
        <div>
          <NavLink to="/">List</NavLink>
          <NavLink to="/about">About</NavLink>
        </div>
>
      </header>
    </div>
  )
}
```

Notice that each `NavLink` has a `to` prop. This sets what the path in the address bar will become when you click this link.

Try it out in your browser!

The `NavLink`s need some style. `NavLink` translates to a regular anchor `<a>` tag in the DOM. You can treat these like any other tag/component:

> [action]
>
> In `src/Title.js`, give the NavLinks a class name:
>
```html
<NavLink className="nav-link" to="/">List</NavLink>
<NavLink className="nav-link" to="/about">About</NavLink>
```
>
> Then, open `src/Title.css` and add some styles.
>
```CSS
.Title .nav-link {
  display: inline-block;
  padding: 0.5em 1em;
  color: rgba(255, 255, 255, 0.835);
  font-weight: bold;
  text-decoration: none;
}
```

This looks better, but you could do more! Currently the active link (the link that represents the current "page") doesn't stand out from the other links. It should, as this would help users understand where they are what they can do, thereby improving the UX (User eXperience).

Luckily, `NavLink` has a prop for this! The `activeClassName` prop/attribute defines a class name that will be added to the element when that link is the current link.

**The `activeClassName` is applied by matching the path in the address bar.** It follows the same rules used for Routes. This means that the `/` will match all paths that contain a `/`. Use `exact` to prevent this behavior.


> [action]
>
> *Edit* your `NavLink`s in `src/Title.js` to be the following:
>
```js
<NavLink
  className="nav-link"
  activeClassName="nav-link-active"
  exact
  to="/">List</NavLink>
>
<NavLink
  className="nav-link"
  activeClassName="nav-link-active"
  to="/about">About</NavLink>
```

With these options, the selected `NavLink` will have the class: `nav-link-active`. You should add a style for this!

> [action]
>
> Add the following to `src/Title.css`:
>
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

> [action]
>
> Make a new file named: `src/POPOSDetails.js`, and add the following code to it:
>
```js
// src/POPOSDetails.js
>
import React from 'react'
>
import data from './sfpopos-data.json'
>
function POPOSDetails(props) {
  const { id } = props.match.params // Location index
  const { images, title, desc, hours, features, geo } = data[id]
>
  return (
    <div>
      <div>
        <img src={`${process.env.PUBLIC_URL}images/${images[0]}`} />
      </div>
>
      <div>
        <h1>{ title }</h1>
        <p>{ desc }</p>
        <p>{ hours }</p>
        <p>{ features }</p>
        <p>{ geo.lat } { geo.lon }</p>
      </div>
>
    </div>
  )
}
>
export default POPOSDetails
```

The code above is just like the other components you've made. One small change is at the top you've imported `sfpopos-data.js`.

Inside the function you defined a variable: `id` and set the value to `props.match.params`.

`const { id } = props.match.params // Location index`

On the next line you're using the `id` to get the data for the location at the index. Using deconstruction we can break object at that index down into: `images`, `title`, `desc`, `hours`, `features`, and `geo` coordinates.

The rest of the component is similar to the other components you wrote previously. Feel free to modify this and add styles. Notice that `images` is an array to display images. For example, you're using `images[0]` to get the first image in this array.

### Details Route

Set up a Route to display the details component.

> [action]
>
> Open `App.js`, and add an import for `POPOSDetails.js` at the top:
>
```js
import POPOSDetails from './POPOSDetails'
```
>
> Then in `App.js`, within the return block of the component, make a new Route below the existing Routes:
>
```html
<Route path="/details/:id" component={POPOSDetails} />
```

Notice the path here is different. `path="/:id"` it contains a `:`. This is a parameter. The value following the `/` is now a variable and can be anything. For example:

`http://localhost:3000/#/0` `id` would be 0

or

`http://localhost:3000/#/42` `id` would be 42

You have access to this value inside a Route with: `props.match.params.id`

Take a look back at `src/POPOSDetails.js` somewhere around line 6 you should have:

`const { id } = props.match.params`

Here you get the value of id.

You can test your work by trying these addresses in your browser:

`http://localhost:3000/#/details/0`
`http://localhost:3000/#/details/1`
`http://localhost:3000/#/details/2`

What's important here is your app can find a details page by entering a URL. A user now could go directly to a page by entering that address, they could also bookmark a page.

### Passing the id

To be able to link to something with an id we need to have that id. Here in this step you'll pass the id to a `POPOSSpace` from `POPOSList`.

> [action]
>
> Open `POPOSList.js`. Find the line where you mapped data to the `POPOSSpace` via the `spaces` const, and edit it to be the below code. Notice the small changes with `i` and `id`:
>
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

`map({ ... }, i)`. here is the whole line as it is shown above:

`const spaces = data.map(({ title, address, images, hours }, i) => {`

The second change is the added prop `id={i}` in the `POPOSSpace` component.

```html
<POPOSSpace
  id={i} // added new prop id here!
  ...
/>
```

When using `map()` this method provides the index of the element as a second parameter. This is useful in many cases, you're using it here as the index of the data from our JSON data.

You can now access this index inside an instance of `POPOSSpace` as `props.id`.

# Linking to Details

With the last piece in place you can get to the details Route. This is good but you really want visitors to be able to click a location in the list and show its details.

For a page to link to its details, it needs to know the index in the array where its data is stored. This will happen in `POPOSList`.

You can also do this by using a `<Link>` component. `<Link>` is a component provided by React Router for linking/navigating to different Routes.

`Link` is different from `NavLink` in that `NavLink` is used for top level navigation that would be visible on all pages. `Link` on the other hand is for general navigation that might appear anywhere else. The big difference is `NavLink` offers the extra feature of `activeClassName` and `Link` doesn't have this.

Let's make some links in the `POPOSSpace`. It's probably best if people can click both the title and image to link to the detail page.

> [action]
>
> In `src/POPOSpace.js`, import the Link component at the top.
>
```js
import { Link } from 'react-router-dom'
```

Since id should now be passed as a prop you can access it with:

`props.id`

or deconstruct it with:

`const { id } = props`

Or if you're already deconstructing props just add it to the list:

`const { name, image, address, hours, id } = props`

> [action]
>
> In `src/POPOSpace.js`, first add `id` to your props. Then wrap the `img` in a `Link`. You should have something like this:
>
```js
const { name, image, address, hours, id } = props
>
...
>
<Link to={`/details/${id}`}>
  <img src={`${process.env.PUBLIC_URL}images/${image}`} width="300" height="300" alt="Hello" />
</Link>
```

Notice the `to` path! Remember the path will look for a param following the `/`. Here the param will be the id!

> [action]
>
> In `src/POPOSpace.js`, do the same with the title:
>
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
