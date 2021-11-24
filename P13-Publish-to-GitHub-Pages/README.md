# Publishing your React Projects to GitHub

Sharing your work with world is a good thing. GitHub provides an easy way to publish your work. GitHub doesn't allow you to run backend code, upload files, or host a database. Within those limitations GitHub Pages provides a service for the reasonable cost of $0.

GitHub Pages allows you to publish static web sites with little more than the push of a button. The performance is also very good. The pages load quickly and are always available.

## Publishing react

React projects take a little more to publish. The React project source code doesn't run in the browser it must compiled/transpiled first. This process happen when you run your react code in the terminal with `yarn start` or `npm start`. If you want to publish your work you'll run `npm run build`. This will create a JS bundle and put it your public directly. This is the code that you would share with the world.

We can take this process one step further. Besides building the project we can build to a branch and publish that branch. This way your developer code that's in process can be worked on the master branch while code that's been published can be served from another branch.

Luckily someone has made a library that automates the process. Follow these steps.

Install the dependencies:

```
npm install gh-pages --save-dev
```

We need to add the address of your github page. Every github repo can have a homepage at: 

```
http://<username>.github.io/<repo-name>
```

Here `<username>` you will replace this with your GitHub username and `<repo-name>` with the repo name. 

Edit your `package.json` and add the address of your homepage. 

```JSON
"homepage": "http://<username>.github.io/<repo-name>"
```

Still in `package.json` add the following to scripts section:

```JSON
"scripts": {
  //...
  "predeploy": "npm run build",
  "deploy": "gh-pages -d build"
}
```

To build and deploy your work run the following command in the terminal: 

```
npm run deploy
```

This builds your react project to a branch named `gh-pages` then commits and pushes that branch. 

Visit yor new site at: `http://<username>.github.io/<repo-name>`.


# Next

That's it! You're done!
