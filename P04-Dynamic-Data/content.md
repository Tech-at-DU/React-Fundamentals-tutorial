---
title: "Dynamic Data"
slug: dynamic-data
---

Currently your web site us static. The information is fixed and cannot change. Web sites can also be dynamic with data that changes over time. For example what new public spaces could be added to the site the new spaces would show up on the list. Or what if you could search for a public space by name or address and the list showed only results that matched your search. 

To handle these situations you'll need store the data that we see on the screen outside of components themselves. 

You'll need a data structure to hold this data. A common option is JSON. JSON or JavaScript Object Notation is a plain text format that translates to standard JavaScript Objects and Arrays. 

## Take a look at the JSON file

It looks a lot like a JS array of Objects. If you look at the top level of the array it looks like this: 

`[{ ... }, { ... }, ...]`

At the top level you have an array, and each element of the array is an object. 

Take a look at the first object: 

```JSON
[
  {
     "title":"Transamerica Redwood Park",
     "desc":"Located in the shadow of the Transamerica Pyramid, Redwood Park is one of the Financial District's greenest and most serene spots. Here, towering redwoods surround a half acre of statues and a large central water feature. Plus, the park is often empty, which means there's almost always a bench available for the hogging. Potential visitors take note: The park is closed every evening",
     "address":"600 Montgomery St San Francisco, CA",
     "geo":{
        "lat":37.7952005,
        "lon":-122.4027927
     },
     "images":[
        "transamerica-redwood-park.jpg"
     ],
     "website":"https://pyramidcenter.com/point-of-interest/redwood-park/",
     "features":[
        "outdoors",
        "coffee"
     ]
  },
  ...
]
```

This first element has the same properties as the others. The information here describes a location. Some of the values are strings, some are numbers, others are objects and arrays.

### Challenge! 

Identify which values are strings, which are numbers, which are objects, and arrays. 

### Continue! 



## Using JSON 

You can import JSON from a file. 
