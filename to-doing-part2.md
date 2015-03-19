# Step 2
## Building the layout and first view
Time to start making our app look like more of an app.

#### Adding a navbar

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

```scss
@import '.meteor/local/build/programs/server/assets/packages/meteoric_ionic-sass/ionic';
```

Now if we run the app again it should have a navbar across the top, and be starting to look a bit more like an app.

#### Adding a slide-out (offcanvas) menu

Things are looking better, but we don't really want a back button in our header, we would rather have a nice slide-out menu for navigation.

First we need to modify our **main_template.html** file, by including the side menu layout helper blocks:

```html
<head>
    <title>To-Doing - Agile PM for your life</title>
</head>

<template name="mainLayout">
    {{#ionBody}}

        {{#ionSideMenuContainer}}

            {{> mainMenu}}

            {{#ionSideMenuContent}}

                {{> ionNavBar class="bar-positive"}}

                {{#ionNavView}}
                    {{> yield}}
                {{/ionNavView}}

            {{/ionSideMenuContent}}

        {{/ionSideMenuContainer}}

    {{/ionBody}}
</template>
```

This sets up the template for side menus, we are going to break out the actual menu into its own template. Create a file **client/includes/sideMenuMain.html** and add the following code to it:

```html
<template name="mainMenuNavBar">

{{#contentFor "headerButtonLeft"}}
    <button class="button button-clear pull-left" data-ion-menu-toggle="left">
        {{#if isAndroid}}
            {{> ionIcon icon='android-more-vertical'}}
        {{else}}
            {{> ionIcon icon='navicon'}}
        {{/if}}
    </button>
{{/contentFor}}
{{#contentFor "headerTitle"}}
    <h1 class="title">To-Doing</h1>
{{/contentFor}}

</template>

<template name="mainMenu">
    {{#ionSideMenus}}

        {{#ionSideMenu}}
            <div class="bar bar-header bar-positive">
                <h1 class="title">Left Menu</h1>
            </div>
            <div class="content has-header">
                <div class="list">
                    <div class="item item-icon-right" data-ion-menu-close>
                        Close Me {{> ionIcon icon="ios-arrow-right"}}
                    </div>
                </div>
            </div>
        {{/ionSideMenu}}

    {{/ionSideMenus}}
</template>
```

Here we've got two templates, **mainMenuNavBar** which sets up the navbar and goes in our view templates, and **mainMenu** which holds the actual menu content and goes into our **main_layout.html** template.

Now we need to add the mainMenuNavBar template to **todo.html**:

```html
<template name="toDo">
    {{> mainMenuNavBar}}

    {{#ionView}}
        {{#ionContent}}
            <p>Hello Meteor + Ionic</p>
        {{/ionContent}}
    {{/ionView}}
</template>

```

We should be good to go now, except we need to load the ionic icons by including them in **client/includes/todoing.scss** add the following line just below the first 
import line:

```scss
@import '.meteor/local/build/programs/server/assets/packages/meteoric_ionicons-sass/ionicons';
```
 
Now run the app again and you should have a pretty blue navbar with a super-cool slide-out menu.

#### Menu Tweaks

Now that we have our menu in place lets rearrange things a bit and start adding items that will eventually link to future views.

in the **mainMenu** template replace ``` <h1>Left Menu</h1> ``` with this:

```html
<button class="white button-clear lg" data-ion-menu-close>{{> ionIcon icon="ios-close-outline"}}</button>
```

Here we are moving the close menu button to the header and changing the icon, you can see all the ionicons available [here](http://ionicons.com/).

Next swap out the close menu item with this: 

```html
<div class="item item-icon-right">
    Statistics {{> ionIcon icon="pie-graph"}}
</div>
<div class="item item-icon-right">
    Settings {{> ionIcon icon="gear-a"}}
</div>
<div class="item item-icon-right">
    Account {{> ionIcon icon="person"}}
</div>
```

The main menu template should now look like this: 

```html
<template name="mainMenu">
    {{#ionSideMenus}}

        {{#ionSideMenu}}
            <div class="bar bar-header bar-positive">
                <button class="white button-clear lg" data-ion-menu-close>{{> ionIcon icon="ios-close-outline"}}</button>
            </div>
            <div class="content has-header">
                <div class="list">
                    <div class="item item-icon-right">
                        Statistics {{> ionIcon icon="pie-graph"}}
                    </div>
                    <div class="item item-icon-right">
                        Settings {{> ionIcon icon="gear-a"}}
                    </div>
                    <div class="item item-icon-right">
                        Account {{> ionIcon icon="person"}}
                    </div>
                </div>
            </div>
        {{/ionSideMenu}}

    {{/ionSideMenus}}
</template>
```

Now we just need to add some custom css classes that we used for the close button to our scss file. Open up **client/includes/toding.scss** and add the following:

```scss
.white {
	color: #fff !important;
}
.lg {
	font-size: 28px;
	line-height: 0;
}
```

Now run the app again and the menu should be starting to look like a menu, Yay!