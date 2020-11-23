---
title: "Publish to GitHub Pages"
slug: publish-to-github-pages
---

## Publishing your React Projects to GitHub

Sharing your work with world is a good thing. GitHub provides an easy way to publish your work. GitHub doesn't allow you to run backend code, upload files, or host a database. Within those limitations GitHub Pages provides a service for the reasonable cost of $0. 

GitHub Pages allows you to publish static web sites with little more than the push of a button. The performance is also very good. The pages load quickly and are always available. 

### Publishing react

React projects take a little more to publish. The React project source code doesn't run in the browser it must compiled/transpiled first. This process happen when you run your react code in the terminal with `yarn start` or `npm start`. If you want to publish your work you'll run `npm run build`. This will create a JS bundle and put it your public directly. This is the code that you would share with the world. 

We can take this process one step further. Besides building the project we can build to a branch and publish that branch. This way your developer code that's in process can be worked on on the master branch while code that's been published can be served from another branch. 

Luckily someone has made a library that automates the process. 

> [info]
> 
> Install the `gh-pages` package. 
> 
> `npm install --save-dev gh-pages`
>




