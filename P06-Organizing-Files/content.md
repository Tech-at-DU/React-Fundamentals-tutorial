---
title: "Organizing Files"
slug: organizing-files
---

# Organizing your files

The project is starting to grow in size. This is when some organization would help you manage and grow your application. 

## Components 

Components are self contained and represent UI elements. When possible you'd like your components to be portable. That is you'd like to take the components with you to new places so you don't have to write them over and over again each time you need a button or a nav bar. 

In some cases a component will be very specific to a project. The POPOSDetails component is very specific to this project. The Title component on the other hand could be used anywhere. 

In order to be portable a component might have other files that it requires. For example the Title Component imports Title.css and NavLink from React Router Dom. 

### Grouping Dependencies 

Organizing components and their dependencies in folders is one way to keep componets organized and portable. 

Create a new folder in the src folder name it "components". 

Move all of your components into this folder. I started with:

- src 
  - About.js
  - App.css
  - App.js
  - App.test.js
  - index.css
  - index.js
  - POPOSDetails.js
  - POPOSList.css
  - POPOSList.js
  - POPOSSpace.css
  - POPOSSpace.js
  - serviceWorker.js
  - setupTests.js
  - sfpopos-data.json
  - Title.css
  - Title.js

Create a new components folder and move all of your components into this folder **except for index.js and index.css**. After this change I had: 

- src 
  - components
    - About.js
    - App.css
    - App.js
    - App.test.js
    - POPOSDetails.js
    - POPOSList.css
    - POPOSList.js
    - POPOSSpace.css
    - POPOSSpace.js
    - Title.css
    - Title.js
  - index.css
  - index.js
  - serviceWorker.js
  - setupTests.js
  - sfpopos-data.json

This change broke my app. I'm seeing an error: 

> Failed to compile
> ./src/App.js
> Error: ENOENT: no such file or directory, open '/Users/mitchellhudson/Documents/Makeschool/FEW/FEW-1.2-JS Foundation Notes/sfpopos/src/App.js'

This is telling me that the system can't find 'App.js'. This would make sense since we moved it to a new location. 

Open index.js. Notice that App is imported here. 

`import App from './App';`

This line is no longer correct since App is now located in `src/components`. Changes this to: 

`import App from './components/App';`

That's fixed but there is another error: 

> Failed to compile
> ./src/components/POPOSDetails.js
> Module not found: Can't resolve './sfpopos-data.json' in '/Users/mitchellhudson/Documents/Makeschool/FEW/FEW-1.2-JS Foundation Notes/sfpopos/src/components'

This message is telling us that the Component `POPOSDetails.js` failed to compile because it can't find './sfpopos-data.json'. This would make sense since `POPOSDetails.js` is in the components folder and `sfpopos-data.json` is in src. 

Open `POPOSDetails.js`. Find the import statement near the top: 

`import data from './sfpopos-data.json'`

Change this to:

`import data from '../sfpopos-data.json'`

The difference here is pretty subtle. The difference is `./` vs `../`. This is a big difference. `./` indicates the current directory/folder. `../` indicates the parent directory/folder. 

From here there's another error, but it's a different error so you are making progress. 

> Failed to compile
> ./src/components/POPOSList.js
> Module not found: Can't resolve './sfpopos-data.json' in '/Users/> mitchellhudson/Documents/Makeschool/FEW/FEW-1.2-JS Foundation Notes/sfpopos/src/components'

This time the error is in `POPOSList.js` and it's can't resolve './sfpopos-data.json'. Sounds like we need to fix the path to `sfpopos-data.json` again!

Open `POPOSList.js`. Find the import statement at the top. 

`import data from './sfpopos-data.json'`

Change `./` to `../`

`import data from '../sfpopos-data.json'`

With these changes I had everything working in the example project. 

### Grouping Components 

Components can be grouped in folders. Often you had a component that was made of a JS and a CSS file. Putting these in the same folder will group these together. 

Moving the files into new folders will create errors in your import statements that you will need to fix. 

Make a folder for each of the Components you created and move that component and it's CSS file into the folder. **Give the folder the same name as the component**.

After these changes my src directory looked like this: 

- src 
  - components
    - About
      - About.js
    - App.css
    - App.js
    - App.test.js
    - POPOSDetails
      - POPOSDetails.js
    - POPOSList
      - POPOSList.css
      - POPOSList.js
    - POPOSSpace
      - POPOSSpace.css
      - POPOSSpace.js
    - Title
      - Title.css
      - Title.js
  - index.css
  - index.js
  - serviceWorker.js
  - setupTests.js
  - sfpopos-data.json