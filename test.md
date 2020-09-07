# Insert text
This is a simple function to place some text to test hook functionality. This function places static text on the hook **genesis_before_loop**.
``` php
// Place a test text somewhere!
add_action( 'genesis_before_loop', 'paul_function' );

function paul_function(){
    echo "<H2>This is where the new function will go!</H2>";
    }
```
