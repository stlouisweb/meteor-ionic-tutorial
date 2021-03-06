# Step 1
## Getting started (setting up the environment)
To-doing is a fairly simple but interactive app that is data and user-centric, which is why we chose Meteor with its concept of reactivity to be the backbone of our app.
To-doing should also work well across platforms, as both a mobile app and a web app. Ionic is an excellent mobile front-end framework that works well in the browser and Meteor has a proven Ionic integration package.

#### To get started we create a new meteor project
Run the following from the command line in your development environment:

```
meteor create todoing
```

You will need to have [installed Meteor](https://www.meteor.com/install) for this to work.

#### Then add the required packages for Ionic
You can add these one by one with 
```
meteor add <package-name>
```
but I prefer to just add these all at once to the **packages** file in the **.meteor/** directory of your project.

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

**client/includes/** will contain contain files that will be used throughout our app, and **client/views/** will contain files that are specific to certain views or pages of the app.

Inside **client/includes/** create a file called **main_layout.html**

Add the following to **main_layout.html**:

```html
<head>
	<title>To-Doing - Agile PM for your life</title>
</head>

<template name="mainLayout">
	{{#ionBody}}
		{{>yield}}
	{{/ionBody}}
</template>
```

This is our main template file, all our other templates will be inserted into the ``` {{>yield}} ``` block. This is an example of Meteor's template inclusion syntax.

``` {{#ionBody}} ``` is a meteor-ionic component that sets  up the necessary wrappers for our ionic templates.

Now its time to create our first view. Inside **client/views/** create a subdirectory **to-do** and inside **client/views/to-do/** create a file **todo.html**

add the following to **todo.html**:

```html
<template name="toDo">
	{{#ionContent}}
		<p>Hello World</p>
	{{/ionContent}}
</template>
```

``` {{#ionContent}} ``` is another meteor-ionic component, you should generally wrap all of your templates in an ``` ionConent ``` block.

Now it's time to configure the router. open up the **routes.js** file we created at the root of the project and add the following to configure the router to use our **mainLayout** template by default:

```javascript
Router.configure({
	layoutTemplate: 'mainLayout'
});
```

Below the ``` Router.configure ``` code add the following to hook up our **toDo** template to the index (/) route:

```javascript
Router.map(function() {
	this.route('toDo', {
		path: '/'
	});
}); 
```

routes.js should look like this:

```javascript
Router.configure({
	layoutTemplate: 'mainLayout'
});

Router.map(function() {
	this.route('toDo', {
		path: '/'
	});
}); 

```

Now you can run meteor to build and serve the project by executing the ``` meteor ``` command from within your project directory.

```
cd path/to/todoing
meteor
```

You can open the project in your browser by going to **http://localhost:3000** (or another port if you specifed one when you started meteor), and you should see "Hello World" in the browser window.

If you inspect the code you should see no errors in the console and looking at the source will show that our meteor-ionic component blocks added a bunch of divs with specific classes to format our page properly for ionic. 




   