# Widgets

Add a widget area in the Genesis framework.
- Theme: **genesis-Sample**
- Widget area name: **Banner**
- Widget id: **banner-widget**
- Function to invoke widget: **add_genesis_banner_widget**

### The Foundation: do_action
do_action creates the hook for things to hang. This is at the core of WordPress and even frameworks like Genesis and many other themes and plugins. do_action is the first domino in the chain of events with hooks. However, alone, it means nothing and does nothing. Simply, it tells WordPress to search to see if any functions are attached to it to fire. So do_actions will look something like this:
[php]<?php do_action( 'my-home' ); [/php]

It can also take and pass variables:
[php]<?php do_action( 'my-home' , $var1 , $var2 ); [/php]

You can find all the available hooks in a theme or plugin by searching ‘do_action’. For Genesis refer to the
[Genesis Visual Hook Guide](https://genesistutorials.com/visual-hook-guide/)

### Register the Widget Area
Before a widget can be called, WordPress must know that it exists. This code is added to the child theme in the  **functions.php** file.

   1. Register the widget area:
``` php
genesis_register_sidebar( array(
	'id'			=> 'banner-widget',
	'name'			=> __( 'Banner', 'genesis-sample' ),
	'description'	=> __( 'This is the widget area for the home template.', 'genesis-sample' ),
));
```

### Hook and Display the Widget Area: add_action
add_action hangs an item on the do_action hook. These may pass arguments and $priority can be used to determine the order of execution. See [The Difference between do_action, add_action and add_filter](https://wpsmith.net/2011/the-difference-between-do_action-add_action-and-add_filter/)

In this example a widget is added to every page and the following code is added to the child theme in the **functions.php** file. The widget area will be placed on the **genesis_after_header** hook.

   2. Hook and display the Widget
``` php
// Add widget to every page
add_action( 'genesis_after_header', 'add_genesis_banner_widget' );
```
``` php
// Define the function called
function add_genesis_banner_widget() {
	genesis_widget_area( 'banner-widget', array(
		'before' => '<div class="custom-widget widget-area">',
		'after'  => '</div>',
	));
}
```

### Alternative Options for Widgets on Specific Pages
- Add the action in the template file for a specific page
``` php
// Place add_action in template file for desired page
add_action( 'genesis_after_header', 'add_genesis_banner_widget' );
```
``` php
// Define the function called in the functions.php file
function add_genesis_banner_widget() {
	genesis_widget_area( 'banner-widget', array(
		'before' => '<div class="custom-widget widget-area">',
		'after'  => '</div>',
	));
}
```
- Add the action using a conditional function (logged-in user and specific page)
``` php
// Add widget to every page
add_action( 'genesis_after_header', 'add_genesis_banner_widget' );
```
``` php
// Function only effective where condition is true
function add_genesis_banner_widget(){
    if ( is_user_logged_in() && is_page( 324 ) ){
        genesis_widget_area( 'banner-widget', $args = array(
		'before'	=>	'<div class="custom-widget widget-area">',
		'after'		=>	'</div>'
	));
    }
}
```
alternative example to place banner on front page only
``` php
// Function only effective where condition is true
function add_genesis_banner_widget(){
    if ( is_front_page() ){
        genesis_widget_area( 'banner-widget', $args = array(
		'before'	=>	'<div class="custom-widget widget-area">',
		'after'		=>	'</div>'
	));
    }
}
```
