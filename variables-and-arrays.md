# Variables and Arrays
Good explanation available at [w3schools.com](https://www.w3schools.com/php/php_arrays.asp).

For testing the functions below can be hooked onto the top of all pages:
``` php
add_action( 'genesis_before_loop', 'paul_function' );
```

### Single Variable
This example sets and displays a single variable.
``` php
function paul_function(){
		// Single variable
		$d = date("D");
		echo "<H2>Single Variable {$d}.</H2>", "<H2>This is an example for $d. </H2";
		echo "<h2>Single Variable " . $d . ".</H2>";
}
```
### Simple Array
Create the array and call a single member:
``` php
function paul_function(){
		// Create Array
		$age = array(
			"Peter"=>"35",
			"Ben"=>"37",
			"Joe"=>"43");

		// Call specific value from the array
		echo "The second member is " . $age['Ben'];
}
```

Create the array and show all values:
``` php
function paul_function(){
		// Create Array
		$age = array(
			"Peter"=>"35",
			"Ben"=>"37",
			"Joe"=>"43");

		foreach($age as $x => $x_value) {
		  echo "Key=" . $x . ", Value=" . $x_value;
    }
}
```
Get all details for a specific post:
``` php
function paul_function(){
		$post = get_post( 42 );

		foreach($post as $key => $value) {
			echo $key . $value;
			echo "<br>";
		}
}
```

Get a specific value from the array, and then all values:
``` php
function paul_function(){
		$post = get_post( $currentID );

		echo "<H2>with title: " . $post->post_title . ".</H2>";
    // Used in objects. Same effect as echo $post(['post_title']);

		foreach($post as $key => $value) {
			echo $key . "  -->  " . $value;
			echo "<br>";
		}
}
```

### Create a Custom Array and Display Content
In this example post details are collected into a custom array and then displayed.
``` php
add_action( 'genesis_before_loop', 'paul_function' );

function paul_function(){
		$currentID = get_the_ID();
		$post = get_post( $currentID );

		// Create Array
		$custom = array(
			"Title: "	=>	$post->post_title,
			"Type: "	=>	$post->post_type,
			"Date: "	=>	$post->post_date,
			"Note: "	=>	"My notes."
		);

		// Display all values
		foreach($custom as $key => $value) {
			echo $key . $value;
			echo "<br>";
		}
}
```
