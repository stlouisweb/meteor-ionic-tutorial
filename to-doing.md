# Making an app with Meteor and Ionic

#### Documenting the creation of to-doing, a simple app that merges the to-do list and time tracker.

## Getting started (setting up the environment)
To-doing is a fairly simple but interactive app that is data and user-centric, which is why we chose Meteor with its concept of reactivity to be the backbone of our app.
To-doing should also work well across platforms, as both a mobile app and a web app. Ionic is an excellent mobile front-end framework that works well in the browser and Meteor has proven Ionic integration package.

#### To get started we create a new meteor project
```
meteor create todoing
```
#### Then add the required packages for Ionic
You can add these one by with 
```
meteor add <package-name>
```
but I prefer to just add these to the **packages** file in the **.meteor/** directory of your project.

##### Ionic packages:
* iron:router
* fourseven:scss
* meteoric:ionic-sass
* meteoric:ionicons-sass
* meteoric:ionic

There is a guide to help along in getting started with meteor-ionic development: [meteor-ionic guide](https://github.com/meteoric/meteor-ionic/blob/master/GUIDE.md) 

#### Setting up the router and the first templates 
Now that we have all the packages we need to start building our app, we can get started on first templates and create a structure for our client-side code. We'll add more packages down the road as we need them.

When you first create a meteor app you'll have some sample files:

* todoing.css
* todoing.html
* toding.js

Delete these files, our app is going to require a more sophisticated file structure.

Now create a file called **routes.js** at the root of your project, then create a directory called **client/** also at the project root, with sub-directories **views** and **includes**.

   