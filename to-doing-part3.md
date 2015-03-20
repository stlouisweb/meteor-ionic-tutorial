# Step 3
## Creating a tabbed view
Using Ionic tabs to create a multi-part view.

Now that the layout is mostly sorted out its time to start working on the actual content, features and "modes" of the app.

The primary mode for this app is essentially task management and organization, the user inputs a list of tasks they need to complete then as they work through the tasks they will move a task from the To-Do column into Doing where the user can record the time spent working on a specific task. When a user completes a task they can move it into the done column. this provides a good way for a user to see where they are at, where they are going and where they've been in terms of workload, life responsibilities and overall productivity.

For this mode we will be using a tabbed interface with [Ionic tabs](https://github.com/meteoric/demo/tree/master/client/templates/tabs). 

#### Creating a new layout 

``` {{> ionTab}} ``` templates don't place so nice with ``` {{#ionContent}} ``` components so we are going to need to set up another layout template. This is one of the nice things about Meteor and iron:router, is that you can have multiple layout templates and easily switch between them depending on the current route, and in Meteor any template can contain any other templates.

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

```spacebars
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
