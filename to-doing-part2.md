# Step 2
## Building the layout and first view
Time to start making our app look like more of an app.

Open the file **client/includes/main_layout.html**, we're going to add some meteor-ionic navigation components to our main layout. modify the content within the ```{{#ionBody}} ``` component like so:

```html
{{#ionBody}}
	{{> ionNavBar}}
		
	{{#ionNavView}}
		{{> yield}}
	{{/ionNavView}}
{{/ionBody}}
```

``` {{> ionNavBar}} ``` will add a navbar across the op of our page and ``` {{#ionNavView}} ``` will wrap our templates with the necassary markup for ionics sweet native style page transitions.

**main_layout.html** should now look like this:

```html
<head>
	<title>To-Doing - Agile PM for your life</title>
</head>

<template name="mainLayout">
{{#ionBody}}
	{{> ionNavBar}}
		
	{{#ionNavView}}
		{{> yield}}
	{{/ionNavView}}
{{/ionBody}}
</template>
```

Now we need to update **client/views/to-do/todo.html**

```html
<template name="toDo">
    {{#contentFor "headerButtonLeft"}}
        {{> ionNavBackButton}}
    {{/contentFor}}

    {{#contentFor "headerTitle"}}
        <h1 class="title">To-Doing</h1>
    {{/contentFor}}

    {{#ionView}}
        {{#ionContent}}
            <p>Hello Meteor + Ionic</p>
        {{/ionContent}}
    {{/ionView}}
</template>
```

The ``` {{#contentFor }} ``` blocks here are loading information into the ``` {{> ionNavBar}} ``` template in the main layout.

Now to make this all look right we need to load the ionic css. The meteor-ionic package is using scss so we need to add a main scss file to our project to import the ionic styles.

Create a file in **client/includes/** called **todoing.scss** and the following line to that file:

```
@import '.meteor/local/build/programs/server/assets/packages/meteoric_ionic-sass/ionic';
```

Now if we run the app again it should have a navbar across the top, and be starting to look a bit more like an app.
 
