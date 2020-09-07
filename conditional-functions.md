# Insert text
Examples of conditional functions. See [Tutorial Republic PHP Conditional Statements](https://www.tutorialrepublic.com/php-tutorial/php-if-else-statements.php).

### The if Statement
The if statement is used to execute a block of code only if the specified condition evaluates to true. This is the simplest PHP's conditional statements and can be written like:
```
if(condition){
    // Code to be executed
}
```



This is a simple function to place some text to test hook functionality. This function places static text on the hook **genesis_before_loop**.
``` php
// Place a test text somewhere!
add_action( 'genesis_before_loop', 'paul_function' );

function paul_function(){
    echo "<H2>This is where the new function will go!</H2>";
    }
```

### The if...elseif...else Statement
The if...elseif...else a special statement that is used to combine multiple if...else statements.
```
if(condition1){
    // Code to be executed if condition1 is true
} elseif(condition2){
    // Code to be executed if the condition1 is false and condition2 is true
} else{
    // Code to be executed if both condition1 and condition2 are false
}
```

This example looksup the post number and returns different texts depending on the result.
``` php
add_action( 'genesis_before_loop', 'paul_function' );

function paul_function(){
		// Fluffy intro just for fun
		$d = date("D");
		echo "<H2>Happy {$d}!</H2>", "<H2>This is an example for $d. </H2";

		$currentID = get_the_ID();
		echo "<H2>This is page {$currentID}. </H2";
		if( is_front_page() ){
			echo "<H2>Page {$currentID} is the front page.</H2>";
		} elseif ( is_page( 2 ) ) {
			echo "<H2>Page {$currentID} is the brewing page.</H2>";
		} else {
			echo "<H2>Page {$currentID} is an ordinary page.</H2>";
		}
    }
```
