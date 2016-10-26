---
title: PHP7 And MSSQL
date: 2016-10-26 14:58:28
tags:
- PHP7
- MSSQL
- PDO
---

## Using MSSQL On PHP7
Recently, one of my clients needs pull data from one of his new provider, unexpectly, this new provider use MSSQL, however, we upgraded from php5.6 to php7, the old `mssql_connect` function is being removed at php7, read more [here](http://php.net/manual/en/function.mssql-connect.php), we need another solution for it.

### Sybase
The solution is using PDO to handle connection, but before it, we need install Sybase dependency. Below is working perfectly fine with Ubuntu 14.04.
```
sudo apt-get install php7.0-sybase
```

### PDO
After it installed correctly, you can use the code below to connect with MSSQL
```
$myServer = "xxx.xxx.xxx.xxx";
$myUser = "myUser";
$myPass = "myPass";
$myDB = "myDB";

$dsn= "dblib:host=$myServer:1433;";
$mspdo = new PDO($dsn,$myUser,$myPass);
$mspdo->setAttribute(PDO::ATTR_ERRMODE,PDO::ERRMODE_EXCEPTION);
$query = 'SELECT * FROM {your desired table}';
$result = $mspdo->query($query)->fetchAll(PDO::FETCH_ASSOC);
```

### PHP5 + Sybase
Here is the code will works for php5, you need install `sudo apt-get install php5-sybase`, you could use the example below to handle the query. Read more [here](http://php.net/manual/en/function.mssql-query.php)

```
$dbhandle = mssql_connect($myServer, $myUser, $myPass);
$query = 'Some Query';
$result = mssql_query($query);
while ($row = mssql_fetch_assoc($result)) {
    echo '<li>' . $row['name'] . ' (' . $row['username'] . ')</li>';
}
```

### Suggestion?
If you have any questions and suggestions, please leave below and I will reply ASAP.

