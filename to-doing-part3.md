# Step 3
## Creating a tabbed view
Using Ionic tabs to create a multi-part view.

Now that the layout is mostly sorted out its time to start working on the actual content, features and "modes" of the app.

The primary mode for this app is essentially task management and organization, the user inputs a list of tasks they need to complete then as they work through the tasks they will move a task from the To-Do column into Doing where the user can record the time spent working on a specific task. When a user completes a task they can move it into the done column. this provides a good way for a user to see where they are at, where they are going and where they've been in terms of workload, life responsibilities and overall productivity.

For this mode we will be using a tabbed interface with [Ionic tabs](https://github.com/meteoric/demo/tree/master/client/templates/tabs). 

#### Creating a new layout 

``` {{> ionTab}} ``` templates don't play so nice with ``` {{#ionContent}} ``` components so we are going to need to set up another layout template. This is one of the nice things about Meteor and iron:router, is that you can have multiple layout templates and easily switch between them depending on the current route, and in Meteor any template can contain any other templates.

In **client/includes/** create a new file called **tab_layout.html**

This file is going to be nearly identical to the **main_layout.html** file, so you can copy and paste the contents of that file to get started. Next change the template name 

```html
<template name="tabLayout">
```
then modify the contents of ``` {{#ionNavView}} ``` like so:

```handlebars
{{#ionNavView}}
	{{> mainMenuNavBar}}
	{{> yield}}
	{{> toDoTabs}}
{{/ionNavView}}
```

When your done **client/includes/tab_layout.html** should look like this:

```handlebars
<head>
    <title>To-Doing - Agile PM for your life</title>
</head>

<template name="tabLayout">
    {{#ionBody}}

        {{#ionSideMenuContainer}}

            {{> mainMenu}}

            {{#ionSideMenuContent}}

                {{> ionNavBar class="bar-calm"}}

                {{#ionNavView}}
                    {{> mainMenuNavBar}}
                    {{> yield}}
                    {{> toDoTabs}}
                {{/ionNavView}}

            {{/ionSideMenuContent}}

        {{/ionSideMenuContainer}}

    {{/ionBody}}
</template>

```

#### Adding the tabs

Now we'll add a template for displaying the tab menu

Create a file **client/includes/todo-tabs.html** and add the following code:

```handlebars
<template name="toDoTabs">
        {{#ionTabs style="ios" class="tabs-background-calm tabs-color-light tabs-top tabs-icon-left"}}
            {{> ionTab title="To-Do" path="tabs.todo" iconOff="clipboard" iconOn="clipboard"}}
            {{> ionTab title="Doing" path="tabs.doing" iconOff="clock" iconOn="clock"}}
            {{> ionTab title="Done" path="tabs.done" iconOff="checkmark-round" iconOn="checkmark-round"}}
        {{/ionTabs}}
</template>
```

What this is doing is adding all of the necessary markup and bindings for [Ionic tabs](http://ionicframework.com/docs/api/directive/ionTabs/), we are also specifying some special css classes and icons to make it look nice.

#### Adding the tab content

Now we can add templates that correspond to each of the tabs views.

Create a new file **client/views/to-do/tabs_todo.html** and add the following content:

```handlebars
<template name="tabsTodo">
    {{#ionView}}
        {{> mainMenuNavBar}}

        {{#ionContent class="tab-padding"}}
            <h1>To Do</h1>
        {{/ionContent}}

    {{/ionView}}
</template>
```

Now create two more files **client/views/doing/tabs_doing.html** 

and 

**client/views/done/tabs_done.html**

And copy the same code from **tabs_todo.html** changing the template name and the content of the ```<h1>``` tag to "Doing" and "Done" in the corresponding templates.

Now we should have some nifty tabs, lets just tweak the style of the tabs a little bit. Add the following to **client/includes/todoing.scss**

```scss
.tabs-icon-left>.tabs .tab-item {
  font-size: 16px;
  line-height: 2.5;
}
.tabs-icon-left>.tabs .tab-item .icon {
  line-height: 1;
}

