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
					SELECT
					oi.order_id Nr,
					DATE_FORMAT(p.post_date, '%d.%m.%Y' ) Datum,
					u.display_name Naam,
					u.ID Lid,
					oi.order_item_name Product,
					max(case when oim.meta_key = '_qty' then oim.meta_value end) Stk,
					max(case when oim.meta_key = '_line_total' then oim.meta_value end) Euro
					FROM
					www_woocommerce_order_itemmeta oim
					JOIN www_woocommerce_order_items oi ON oim.order_item_id = oi.order_item_id
					JOIN www_posts p ON oi.order_id = p.ID
					JOIN www_postmeta pm ON oi.order_id = pm.post_id
					JOIN www_users u ON pm.meta_value = u.ID
					WHERE
					pm.meta_key = '_customer_user'
					AND to_days(current_timestamp()) - to_days(`p`.`post_date`) < 120
					GROUP BY
					oim.order_item_id
					ORDER BY
					oi.order_id desc;
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
