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

Lets start by learning to change our url.  
 By default the `<a>` actually refreshes the screen before changing the url. This is an issue because we don't want the page to reload ever.
 
 That's ok though because React Router actually gives us a solution.  
 React Router gives us a `<Link>` tag that acts just like an `<a>` tag, except without refreshing the page! all you have to do is give it a `to` attribute rather than an `href` attribute and you are good to go.
  ```xml
 <Link to="/images/kitten-0.jpeg">
 ```

 So lets update our `Project.js` file to reflect these changes
 at the top we have to import our `Link`
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
 

 
