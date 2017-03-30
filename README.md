# PHP-Spdo
Simple PDO Database Class

 - Less coding
 - PDO-Based Structure
 - Multiple Database Connection Possiblity
 - Multiple Output Possiblity (json, xml, object, array)
 - CodeIgniter 2.x and 3.x Support
 
You must download Spdo.php file from Github servers to your project directory. After downloading, you must create a database connection configuration file. 

## Sample Database Connection Configuration:

```php
$db = [
  "default" => [
    "database" => "YourDatabaseName",
    "hostname" => "MysqlHostname",
    "username" => "MysqlUsername",
    "password" => "MysqlUserPassword",
    "char_set" => "utf8",
  ],
  "secondaryDB" => [
    "database" => "YourDatabaseName",
    "hostname" => "MysqlHostname",
    "username" => "MysqlUsername",
    "password" => "MysqlUserPassword",
    "char_set" => "utf8",
  ]
];
```
Maybe, you want to include this codes to your own configuration file. No problem, just this codes must be before Spdo class. 

## Sample Including Spdo Class To Project:

```php
include "config.php";
include "Spdo.php";

$spdo = new Spdo();
```

If you want this class to **CodeIgniter** project, you must follow this rules;

 - Add a value to $autoload variable like as this;

```php
$autoload['libraries'] = array('Spdo');
```

 - You must move Spdo.php file to application/libraries directory.
 - Open Spdo.php file and apply like as this changes;
 
```php 
#require_once APPPATH . 'config/database.php'; 
```
to
```php
require_once APPPATH . 'config/database.php'; 
```

 - Open application/config/database.php and edit database configuration values for your database.
 
## Functions List:
 
 - errors()
 - getErrors()
 - getLastQuery()
 - numRows()
 - getResults()
 - getRow()
 - getVar()
 - execute()
 - insert()
 - update()
 - delete()
 
## Some Sample For CRUD Processes:

### Using getResults() function

```php
$results = $spdo->getResults('SELECT * FROM categories');
```
This sample returns multiple lines from categories tables. Default output style is object.
```php
$results = $spdo->getResults('SELECT * FROM categories', ["returnDataType" => "json"]);
```
This sample returns multiple lines from categories tables. **returnDataType** parameter converts output style default to json.
```php
$results = $spdo->getResults('SELECT * FROM categories WHERE status > ?', 
["bindValues" => ["active"], "returnDataType" => "json"]);
```
This sample returns multiple lines according to "WHERE" block from categories tables. **returnDataType** parameter converts output style default to json.
```php
$results = $spdo->getResults('SELECT * FROM categories WHERE status > ?', 
["bindValues" => ["active"], "returnDataType" => "json", "configKey" => "secondaryDB"]);
```
This sample returns multiple lines according to "WHERE" block from categories tables. **returnDataType** parameter converts output style default to json. **configKey** determines database for getting datas.

I will continue writing other functions.
