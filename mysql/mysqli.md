# Getting Started
---
Comparison of creating a PUDL object vs PHP's mysqli and PDO.


## PUDL

PUDL is designed to be standardized and simplified across all of its method
parameters. By keeping everything in a key-value pair, configurations are easier
to manage and pass between methods. This also allows for additional optional
parameters to be configured, such as persistent connections. Additionally, PUDL
is standardized for all database types, simply changing the 'type' parameter is
all that is required to switch from one type of database server to another.

_NOTE: internally, PUDL uses PHP's MySQLi driver for 'mysql' type connections,
but the internal complexities are abstracted away so you don't need to think
about them_

```php
require_once('pudl/pudl.php');

$db = pudl::instance([
	'type'			=> 'mysql',
	'server'		=> 'localhost',
	'database'		=> 'DatabaseName',
	'username'		=> 'AwesomeGuy9001',
	'password'		=> 'SuperDuperSecretSauce',
	//'persistent'	=> true,				// optional persistent connection
	//'timeout'		=> $timeout,			// optional connection timeout
]);
```


## MySQLi

MySQLi connections are built in three stages instead of one. First, create the
object instance. Then set the connection properties. Lastly, execute the
connection. Without inline commenting or looking at documentation, it can be
hard to tell which parameter is which value, especially when server, username,
and database may all have overlaps.

```php
$db = mysqli_init();

// set connection options here, such as connection timeout
// $db->options(MYSQLI_OPT_CONNECT_TIMEOUT,	$timeout);

// persistent connections require modification to the server string

$db->real_connect(
	'localhost',							// server
	'AwesomeGuy9001',						// username
	'SuperDuperSecretSauce',				// password
	'DatabaseName'							// database
);
```


## PDO

PDO is a parameter mess by comparison. First there is a database implementation
specific string, followed by two more strings for individual values, followed by
a key-value pair array for additional parameters. PDO has gone the route of
using all three types of configuration method parameters all at once for the
same method.

```php
$server		= 'localhost';
$database	= 'DatabaseName';

$db = new PDO(
	"mysql:host=$server;dbname=$database",	// complicated DSN
	'AwesomeGuy9001',						// username
	'SuperDuperSecretSauce',				// password
	[
	//	PDO::ATTR_PERSISTENT	=> true,	// optional persistent connection
	//	PDO::ATTR_TIMEOUT		=> $timeout	// optional connection timeout
	]
);
```
