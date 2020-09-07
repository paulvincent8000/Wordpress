# get_all_orders()

This function queries the database to display an overview of orders placed in the last 120 days.

# Description

A SQL expression is converted into a variable which is used to run the query and then processes the results for display on screen as a formatted table.

# Dependencies

The function **display_table** is required to process and display the query result.

# Using the get_all_orders functions

The global **$wpbd** object is called for interaction with the database.

The SQL query must be provided in an indented format. The SQL statement is converted into a variable **$sql** which is used to run a query to the WordPress database.


``` php
function get_all_orders(){

	global $wpdb;

	$sql = <<<SQL
					select `OI`.`order_item_id` AS `order_item_id`,`OI`.`order_id` AS `order_id`,`P`.`post_date` AS `date_of_order`,`U`.`display_name` AS `name`,`U`.`ID` AS `member`,`OI`.`order_item_name` AS `order_item_name`,`OMQ`.`meta_value` AS `quantity`,`OMA`.`meta_value` AS `value`
					from (((((`amervallei_nl_wordpress`.`www_woocommerce_order_items` `OI`
					join `amervallei_nl_wordpress`.`www_woocommerce_order_itemmeta` `OMQ` on(`OI`.`order_item_id` = `OMQ`.`order_item_id`))
					join `amervallei_nl_wordpress`.`www_woocommerce_order_itemmeta` `OMA` on(`OI`.`order_item_id` = `OMA`.`order_item_id`))
					join `amervallei_nl_wordpress`.`www_posts` `P` on(`OI`.`order_id` = `P`.`ID`))
					join `amervallei_nl_wordpress`.`www_postmeta` `PM` on(`OI`.`order_id` = `PM`.`post_id`))
					join `amervallei_nl_wordpress`.`www_users` `U` on(`PM`.`meta_value` = `U`.`ID`))
					where `OMQ`.`meta_key` = '_qty'
					and `OMA`.`meta_key` = '_line_total'
					and `PM`.`meta_key` = '_customer_user'
					and to_days(current_timestamp()) - to_days(`P`.`post_date`) < 120
					SQL;

					$results = $wpdb->get_results( $sql, OBJECT );

					display_table( $results );

}
```

This function can be adapted for other queries and it is also possible to use WordPress functions to directly reference the tables as shown in the example below:

``` SQL
	SELECT	ID, display_name, user_email
	FROM		$wpdb->users
```


Note: for security data in SQL queries must be escaped to protect against SQL injection attacks. This is not done in this code.

Output is provided as the **$results** object. This is an example of the output:
```
Array (
  [0] => stdClass Object ( [ID] => 20 [display_name] => Yogi Bear [user_email] => Yogi@gmail.com )
  [1] => stdClass Object ( [ID] => 21 [display_name] => Micky Mouse [user_email] => Micky@gmail.com )
  [2] => stdClass Object ( [ID] => 22 [display_name] => Alice in Wonderland [user_email] => Alice@gmail.com )
  [3] => stdClass Object ( [ID] => 23 [display_name] => Desperate Dan [user_email] => Dan@gmail.com )
  )
  ```
