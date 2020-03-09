---
title: "Build A Header Component"
slug: build-a-header-component
---

Let's make a new Component! This component will be a header for your page.

> [action]
>
> Make a new file in the `/src` folder: `src/PageHeader.js`, and add the following code:
>
```js
// src/PageHeader.js
>
import React from 'react'
>
function PageHeader() {
  return (
    <div>
      <h1>Name of your site here</h1>
    </div>
  )
}
>
export default PageHeader
```

# What Did I Just Write?

**A simple React Component is just a function that returns some JSX!**

You must import `React` to use JSX! You may have noticed that `React` was not used in this file but it was imported anyway. **`React` must be in scope when using JSX.**

JSX must always have a top level node. For example, the code below produces an error:

```html
// Error! Sibling nodes
<h1>Hello</h1>
<p>World</p>
```

Whereas this code will not produce an error:

```html
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
  return (
    <div>
      <h1>Hello</h1>
      <p>World</p>
    </div>
  )
}
```

In `PageHeader.js`, you exported Header as the _default export_. Any file/module may have a single `default` export. Use the default export for the most important export. In this case we only export one thing, making it the obvious choice for the default export!

# Import and Use Header

Let's use the header!

> [action]
>
> In `App.js` import your Header:
>
```js
// src/App.js
>
import React from 'react';
import logo from './logo.svg';
import './App.css';
[bold]import PageHeader from './PageHeader';[/bold]
```

Here you are importing the default export from `PageHeader.js`.

> [info]
> The `.js` file extension is optional when using import. `import PageHeader from './PageHeader.js'` would also work here.

<!-- -->

> [action]
>
> Now let's use the header inside the App component. In `App.js`, rewrite the existing component:
>
```js
// src/App.js
>
import React from 'react';
import logo from './logo.svg';
import './App.css';
import PageHeader from './PageHeader';
>
function App() {
  return (
    <div className="App">
      <PageHeader />
    </div>
  );
}
>
export default App;
```

Here you imported your component and used that component on the page.

Notice you imported `PageHeader` and used it as a component by writing it like an HTML tag like this: `<PageHeader />`

Since the Component doesn't have any child components you can use a self closing tag (`<TagName />` instead of `<TagName>...</TagName>`).

# Style Your Header

Now let's add some styles to the header! CSS styles are applied to React components in the same way they are applied to regular HTML with a few notable differences.

The Create React App Webpack Build system will import styles and include them in a Component when you import a `.css` file into that component.

This system is good because it allows you to associate styles with components. Rather than throwing all of your styles into single style sheet.

> [action]
>
> Add a new File: `src/PageHeader.css`, and then add the following CSS styles to it:
>
```css
/*  src/PageHeader.css  */
>
.PageHeader {
  width: 100%;
  display: flex;
  justify-content: center;
  padding: 1em;
  background-color: rgb(19, 99, 99);
  color: #fff;
}
```

Now in `PageHeader.js`, we'll import the CSS code and add a class name to reference this style rule.

> [action]
>
> Import the CSS file at the top of `src/PageHeader.js`:
>
```js
import './PageHeader.css';
```

The build script will include styles that are imported into a component.

When assigning a class name to a JSX tag use the name `className` in place of `class`.

> [action]
>
> Make sure your `PageHeader` function within `src/PageHeader.js` looks like the following:
>
```js
// src/PageHeader.js
>
...
>
function PageHeader() {
  return (
    <div className="PageHeader">
      <header>
        <h1>SF Public Spaces</h1>
      </header>
    </div>
  )
}
```

Great work! You should now have a header for your page:

![header](assets/header.png)

# Now Commit

>[action]
>
```bash
$ git add .
$ git commit -m 'header component built'
$ git push
```
