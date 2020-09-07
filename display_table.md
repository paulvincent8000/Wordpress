# display_table( $sql )
This function takes the result of a given SQL query and displays a formatted table on screen.


# Description
This function takes a result of a given SQL query statement as an argument and runs the query against the WordPress database. The result is then parsed to produce a formatted table for display on screen.


# Dependencies
Must be called from a function that provides the SQL query as a variable, e.g. get_all_orders.


# Using the display_table function
The **$results** variable is passed as an argument when the function is called. It contains output from the SQL query.

The query output is provided as an argument to the function in the **$results** object. This is an example of the content:
```
Array (
  [0] => stdClass Object ( [ID] => 20 [display_name] => Yogi Bear [user_email] => Yogi@gmail.com )
  [1] => stdClass Object ( [ID] => 21 [display_name] => Micky Mouse [user_email] => Micky@gmail.com )
  [2] => stdClass Object ( [ID] => 22 [display_name] => Alice in Wonderland [user_email] => Alice@gmail.com )
  [3] => stdClass Object ( [ID] => 23 [display_name] => Desperate Dan [user_email] => Dan@gmail.com )
  )
  ```

The array is parsed in two stages:
- The first row is extracted into the associative array **$headers**. This is broken out into key and value pairs, where the key contains the field names. These are read using a foreach loop to display the column names.
- A nested loop then extracts the table contents. The outer loop reads each row of the table into an associative array **$row** and creates a new row on screen. The inner loop extracts the key and value pairs from the **$row** array, where the value contains the content of the individual cell in the table.

The print_r functions (commented out) can be used to view the array contents for de-bugging.


``` php
function display_table( $sql ){

	global $wpdb;

	$results = $wpdb->get_results( $sql, OBJECT );

	$headers = $results[0];
	// print_r( $headers );
	// print_r( $results );

	echo '<table>';
	// table headers
	echo "<tr>";
	foreach($headers as $key => $value){
		echo '<th>';
		echo $key;
		echo "</th>";
	}
	echo "</tr>";

	// table contents
	foreach ($results as $row) {
		echo "<tr>";
		//	print_r( $row );
		foreach( $row as $key => $value ){
			echo "<td>";
			echo $value ;
			//			echo $key . ' : ' . $value ;
			echo "</td>";
		}
		echo "</tr>";
	}
	echo "</table>";

}
```
