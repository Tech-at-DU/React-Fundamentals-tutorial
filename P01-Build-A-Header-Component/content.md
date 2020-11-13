---
title: "Build A Header Component"
slug: build-a-header-component
---

## Making Components

React projects are built with Components. To build web applications with React you need to think in Components.

**React would best be described as a library for creating user interfaces.** Think of Components as the elements of user interfaces. For example, your site might be made up of the following Components:

App, Header, Logo, NavBar, NavLink, Content, Card, Footer

Each of these elements would be separate Components, and you would define a file for each. Component files are always named after the component they contain: `App.js`, `Header.js`, `Logo.js`, `NavBar.js`, `NavLink.js`, `Content.js`, `Card.js`, and `Footer.js`. 

Components can be nested. That is one Component can be the child of another Component. Rendering the parent would render the child. The components from the list above might be nested in this way:

- App
  - Header
    - Logo
    - NavBar
      - NavLink
  - Content
    - Card
  - Footer

Components can also be reused. Rather than writing a new NavLink for each link, or a new card for each card you can reuse the existing Component as often as you like. The list above might look like this if our site had three NavLinks and 4 cards.

- App
  - Header
    - Logo
  - NavBar
    - **NavLink**
    - **NavLink**
    - **NavLink**
  - Content
    - **Card**
    - **Card**
    - **Card**
    - **Card**
  - Footer

The best way to understand Components is to make one for yourself!

## Make a Component

In this step, you'll make a Component that displays a title. Let's call that Component `Title`.

> [action]
>
> Create a new file, `src/Title.js`, and add the following:
>
```js
// src/Title.js
>
import React from 'react'
>
function Title() {
  return (
    <div>
      <h1>SFPOPOS</h1>
    </div>
  )
}
>
export default Title
```

### What Did I Just Write?

Besides the import and export statements at the top and bottom, you have written a plain JS function.

Looking closely, the function returns a block of what looks like HTML. Looking closer still you'll this HTML-like block is not in a string. **This is JSX!**

JSX is an extension of the HTML language. It uses the XML language syntax and in a React project can be written alongside your regular JavaScript.

JSX is converted to plain vanilla JS by the build system. While the project is running in the terminal this will happen each time you save your files.

The code above will be converted to something like this:

```js
function Title() {
  return React.createElement("div", null, React.createElement("h1", null, "SFPOPOS"));
}
```

It doesn't look too much different, but it is a lot harder to understand what is happening.

**What is the purpose of JSX?** JSX translates to HTML code that looks more or less like the JSX you have written. In the Non-JSX version of the code, it's hard to tell what the HTML output is.

Besides being easier to read than the JavaScript the JSX version is also easier to write.

React is a library for creating user interfaces. The Components you write translate to atomic pieces of those interfaces. In React Components generate HTML elements.

**A React Component is just a function that returns some JSX!**

You may have noticed that `React`, the variable imported at the top of the page, was not used in this file but it was imported anyway.

`import React from 'react'`

`React` must be in scope when using JSX. It's doing some secret stuff behind the scenes. You'll always `import React from 'react'` in every component you create.

### JSX Rules and Syntax

JSX has rules of syntax that come with it.

**Rule** JSX must always have a top level node. 

For example, the code below produces an error:

```JSX
// Error! Sibling nodes
<h1>Hello</h1>
<p>World</p>
```

Whereas this code will not produce an error:

```JSX
// Good! has a single top level element
<div>
  <h1>Hello</h1>
  <p>World</p>
</div>
```

If you are returning a multiline JSX statement, make sure to wrap it in the `(` and `)`. Check out the below examples:

```js
function MyComp() {
  // Good! Single line
  return <h1>Hello World</h1>
}

function MyComp() {
  // Good! Multiline wrapped in ( ... )
  // also has a single top level node.
  return ( // <- (
    <div>
      <h1>Hello</h1>
      <p>World</p>
    </div>
  ) // <- )
}
```

In `Title.js`, you exported the `Title` function as the _default export_.

`export default Title`

Any file/module may have a **single** `default` export. Use the default export for the most important export. In this case, you only exported `Title`, making it the obvious choice for the default export!

## Using a Component

Let's use the Title Component in `App.js`.

> [action]
>
> In `App.js` import Title at the top of the page:
>
```js
// src/App.js
>
import React from 'react';
import logo from './logo.svg';
import './App.css';
[bold]import Title from './Title';[/bold]
```
>

Here you are importing the default export from `Title.js`.

The `.js` file extension is optional when using import.

> [info]
> The `.js` file extension is optional when using import. `import Title from './Title.js'` would also work here.

<!-- -->

> [action]
>
> Now use the `Title` Component inside the `App` Component. In `App.js`, rewrite the existing component to look like:
>
```js
// src/App.js
>
import React from 'react';
import logo from './logo.svg';
import './App.css';
import Title from './Title';
>
function App() {
  return (
    <div className="App">
      <Title />
    </div>
  );
}
>
export default App;
```

Here you imported your component and used that component on the page.

Notice you imported `Title` and used it as a Component by writing it like an HTML tag between `<` and `>` like this: `<Title />`

Since the Component doesn't have any child Components you can use a self-closing tag (`<TagName />` instead of `<TagName>...</TagName>`).

This is another **rule** of the JSX Language. Empty tags can be written as a single tag ending with `/`.

**Challenge:** If you're not running your React project do it now and check out your work in the browser. 

- Using the terminal navigate to your project directory. 
- In terminal run: `yarn start`bash

You should only see the page title at the top, it's the only thing your App component is rendering at the moment. 

**Challenge:** Add the logo to the page. 

To do this you'll need to add a new tag. Add an `<img />` tag. Notice the tag ends with a `/`. 

Add the src attribute and set the value to logo. 

```JSX
<img src={logo} />
```

**Rule** a JavaScript expression in JSX must be wrpped in the curly braces. In this case `logo` was imported near the top, it's variable referencing an image file.

### Styling a Component

Add some styles to the header! CSS styles are applied to React components in the same way they are applied to regular HTML with a few notable differences.

The Create React boilerplate project allows styles to be imported into a Component. This allows you to create a separate file that contain the styles for each component.

> [action]
>
> Add a new File: `src/Title.css`, and then add the following CSS styles to it:
>
```css
/*  src/Title.css  */
.Title {
  box-sizing: border-box;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: baseline;
  padding: 1em;
  margin-bottom: 2em;
  background-color: rgb(192, 45, 26);
  color: #fff;
}
```

In the Component `Title.js`, import the CSS file and use the class name `Title`.

> [action]
>
> Import the CSS file at the top of `src/Title.js`:
>
```js
import './Title.css';
```

When assigning a class name to a JSX tag use `className` in place of `class`.

> [action]
>
> Your `Title` component might look like the following:
>
```js
// src/Title.js
>
...
>
import React from 'react'
import './Title.css';
>
function Title() {
  return (
    <div className="Title">
      <h1>SFPOPOS</h1>
			<div className="Title-Subtitle">San Franciscos Privately Owned Public Spaces</div>
    </div>
  )
}

export default Title
```

Great work! You should now have a header for your page:

![header](assets/header.png)

## Stretch Challenges

> [challenge]
>
> Try these stretch challenges to test your knowledge.
>
> 1. Add a subtitle to the Title component. The subtitle will appear as smaller text below the title.
>   - You'll do this work inside `Title.js`
>   - Add a new `div` tag below the existing `h1` with the text: "San Francisco Privately Owned Public Open Spaces".
> 2. Style the subtitle.
>   - Add a class name to the new tag: `className="Title-Subtitle"`
>   - Open the `Title.css` file and add some styles.
>   - Styles are up to you. I tried something subtle:
>
```CSS
.Title-Subtitle {
  color: rgba(255, 255, 255, 0.75);
}
```

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'header component built'
$ git push
```
