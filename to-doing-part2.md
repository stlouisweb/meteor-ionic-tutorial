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
