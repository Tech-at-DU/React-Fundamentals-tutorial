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
  color: rgba(255, 255, 255, 0.835);
  font-weight: bold;
  text-decoration: none;
}
```

This look better but you could do more! Currently the active link (the link that represents the current "page") is doesn't stand out from the other link. It should, this would help users understand where they are what they can do and improve the UX (User eXperience). 

Luckily NavLink has a prop for this! Add the `activeClassName` prop/attribute to each of the NavLinks. This prop defines a class name that will be added to the element when that link is the currently link.

**The `activeClassName` is applied by matching the path in the address bar.** It follows the same rules used for Routes. This means that the `/` will match all paths that contain a `/`. Use `exact` to prevent this behavior. 

Your NavLinks should look something like this: 

```JSX
<NavLink 
  className="nav-link" 
  activeClassName="nav-link-active" 
  exact 
  to="/">List</NavLink>

<NavLink 
  className="nav-link" 
  activeClassName="nav-link-active" 
  to="/about">About</NavLink>
```

With these options the selected NavLink will have the class: `nav-link-active`. You should add a style for this. Open Title.css. 

```CSS
.nav-link-active {
  color: #fff;
  border-bottom: 2px solid;
}
```

## Details page Route Parameters

Things are looking pretty good. Now let's tackle the detail page. The detail page will be a page that is dedeicated to a single location. It will show all of the information for that location. Right now we show all locations on the List Page but the information is minimal. The details page will be a page dedicated to just one location. 

Currently there 11 spaces in our data list but there are a lot more spaces that might be added in the future. We don't want to make a component for each space. Instead you will make a single component and pass props to it containing the information that needs to display. 

When you made the list of POPOSSpace components you passed all of the values the component displays into the component via props. You also made all of those components in the list with `map()`. 

This time you'll take a different appraoch. In this situation you want to make a single component and you'll be displaying it with React Router as a Route. Router allows you to pass values to a Route through the URL/path. This is good for this use bcause the URL/path can be bookmarked, Which will allow visitors to book mark a detial page or return to it directly by enter it's URL. 

### Making the Details Component

This component will be a lot like the POPOSSpace component but will show more details let's call it POPOSDetails. 

Where the POPOSpace component showed the image, title, and address.  The POPOSDetails component will show all of the images (remember images in the data is an array), title, address, description, hours, and features.

Remember all of the data is in the sfpopos-data.json file. Any of your components can import this file. As long a componen knows the index of the item in the data it can display it. 

The goal then is to pass the index to POPOSDetails component and POPOSDetails will get the information it needs from the data. 

Make a new file named: `POPOSDetails.js`

```JSX
import React from 'react'

import data from './sfpopos-data.json'

function POPOSDetails(props) {
  const { id } = props.match.params // Location index
  const { images, title, desc, hours, features, geo } = data[id]

  return (
    <div>
      <div>
        <img src={`${process.env.PUBLIC_URL}images/${images[0]}`} />
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

Inside the function you defined a variable: `id` and set the value to `props.match.params`. 

`const { id } = props.match.params // Location index`

On the next line you're using the `id` to get the data for the location at the index. Using deconstruction we can break object at that index down int: `images`, `title`, `desc`, `hours`, `features`, and `geo` coordinates. 

The rest of the component is similar to the other components you wrote previously. Feel free to modify this and add styles. Notice that `images` is an array to display the image at the top you're using `images[0]` to get the first image in this array. 

### Details Route

Set up a Route to display the details component. 

Open App.js. 

Import `POPOSDetails.js` at the top: 

`import POPOSDetails from './POPOSDetails'`

Then within the return block of the component make a new Route: 

```JSX 
<Route path="/:id" component={POPOSDetails} />
```

Place this below the existing Routes. 

Notice the path here is different. `path="/:id"` it contains a `:`. This is a parameter. The value following the `/` is now a variable and can be anything. For example: 

`http://localhost:3000/#/0` id would be 0

or 

`http://localhost:3000/#/42` id would be 42

You have access to this value inside a Route with: `props.match.params.id`

Take a look back at `POPOSDetails.js` somewhere around line 6 you have: 

`const { id } = props.match.params` 

Here you get the value of id. 

You can test your work. 

Try these addresses in your browser. 

`http://localhost:3000/#/0`
`http://localhost:3000/#/1`
`http://localhost:3000/#/2`

What's important here is you app can find a details page by entering a URL. A user now could go directly to a page by entering that address, they could also bookmark a page. 

### Passing the id 

To be able to link to something with an id we need to have that id. Here in this step you'll pass the id to a POPOSSpace from POPOSList. 

Open `POPOSSpace.js`. Find the line where you mapped data to the `POPOSSpace`s. It should look like the code below. Notice that there are two small changes:  

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

On the first line there is a second parameter to: `map(obj, i)`, or `map({ ... }, i)`. here is the whole line: 

`const spaces = data.map(({ title, address, images, hours }, i) => {`

The second change is the added prop `id={i}` in the `POPOSSpace` component. 

```JSX
<POPOSSpace 
  id={i}
  ...
/>`
```

When using `map()` this method provides the index of the element as a second parameter. This is useful in many cases. 

You can now access this incde inside an instance of `POPOSSpace` as `props.id`.

### Linking to Details

With the last piece in place you can get to the details Route. This is good but you really want visitors to be able to click a location in the list and show it's details. 

For a page to link to it's details it needs to know the index in the array where it's data is stored. This will happen in POPOSList. 

You can do this also by using a `<Link>` component. `<Link>` is a component provided by React Router for linking/navigating to different Routes. 

`Link` is different from `NavLink` in that `NavLink` is used for top level navigation that would be visible on all pages. `Link` on the other hand is for general navigation that might appear anywhere else. The big difference is `NavLink` offers the extra feature of `activeClassName` and `Link` doesn't have this. 

Make some links in the POPOSSpace. It's probably best if people can click both the title and image to link to the detail page.

Import the Link component at the top. 

`import { Link } from 'react-router-dom'`

Since id should now be passed as a prop you can access it with: 

`props.id` 

or deconstruct it with: 

`const { id } = props`

Or if you're already deconstructing props just add it to the list: 

`const { name, image, address, hours, id } = props`

Now wrap the image in a `Link`. You should have something like: 

```JSX
<img src={`${process.env.PUBLIC_URL}images/${image}`} width="300" height="300" alt="Hello" />
```

Change this to: 

```JSX
<Link to={`/${id}`}>
  <img src={`${process.env.PUBLIC_URL}images/${image}`} width="300" height="300" alt="Hello" />
</Link>
```

Notice the path! `<Link to={`/${id}`}>` remember the path will look for a parm following the `/`. Here the param will be the id! 

Do the same with the title. Yoiu have something like: 

```JSX
<h1>{name}</h1>
```

Change this to something like: 

```JSX
<h1>
  <Link to={`/${id}`}>
    {name}
  </Link>
</h1>
```

Check your work! Clicking a link should take you to the detail page for that location. 

# Feedback and Review - 2 minutes

**We promise this won't take longer than 2 minutes!**

Please take a moment to rate your understanding of the learning outcomes from this tutorial, and how we can improve it via our [tutorial feedback form](https://forms.gle/2yApCdKchE5WkNKD6)

This allows us to get feedback on how well the students are grasping the learning outcomes and tells us where we can improve the tutorial experience.
