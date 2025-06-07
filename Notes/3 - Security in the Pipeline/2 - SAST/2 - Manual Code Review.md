## Searching for Insecure Functions

The first step when reviewing code is identifying potentially insecure functions in use. Since we are looking for SQL injections, we should focus on any functions that could be used to send raw queries to the database. Since our code uses PHP and MySQL, here are some functions that are typically used to send MySQL queries:

| Database Engine | Function                                                                            |
| --------------- | ----------------------------------------------------------------------------------- |
| MySQL           | mysqli_query()  <br>mysql_query()  <br>mysqli_prepare()  <br>query()  <br>prepare() |
A straightforward way to manually search instances of such functions is to use grep to check all of our project's files recursively. For example, to search for instances of `mysqli_query()`, go to the project's base directory and run the following command:

```
cd /home/ubuntu/Desktop/simple-webapp/html/

grep -r -n 'mysqli_query('
```

The `-r` option tells grep to recursively search all files under the current directory, and the `-n` option indicates that we want grep to tell us the number of the line where the pattern was found. In the above terminal output, we can see that a single instance of `mysqli_query()` was found on line `18`.

We have identified a line that could lead to SQL injections. However, just by looking at that line, we can't determine whether a vulnerability is present.

## Understanding the Context

Let's open `db.php` to analyse the context around the `mysqli_query()` function to see if we get a better idea of how it is used:

```php
function db_query($conn, $query){
    $result = mysqli_query($conn, $query);
    return $result;
}
```

Here we can see that `mysqli_query()` is wrapped into the `db_query()` function, and that the `$query` parameter is passed directly without modification. It is very common for functions to be nested into other functions, so simply analysing the local context of a function is sometimes not enough to determine if a vulnerability is present. We now need to trace the uses of the `db_query()` function throughout our code to identify potential vulnerabilities.

## Tracing User Inputs to Potentially Vulnerable Functions

We can use grep again to search for uses of `db_query()`:

![[Pasted image 20250607152423.png]]

Here we get three uses for `db_query()` on `hidden-panel.php`.
Once again, we can analyse the context of each call, starting with the call on line 7:

```php
$sql = "SELECT id, firstname, lastname FROM MyGuests WHERE id=".$_GET['guest_id'];
$result = db_query($conn, $sql);
```

Congrats on finding an SQL injection! Whatever is passed in the `guest_id` parameter via the GET method will be concatenated to a raw SQL query without any input sanitisation, enabling the attacker to change the query.

If we do a similar process for the other two uses of `db_query()`, we will have the following code:

```php
$sql2 = "SELECT id, logtext FROM logs WHERE id='".preg_replace('/[^a-z0-9A-Z"]/', "", $_GET['log_id']). "'";
$result2 = db_query($conn, $sql2);

$sql3 = "SELECT id, name FROM asciiart WHERE id=".preg_replace("/[^0-9]/", "", $_GET['art_id'], 1);
$result3 = db_query($conn, $sql3);
```

Again, we have some GET parameters being concatenated into SQL queries. This would give us the impression that we have two more vulnerabilities identified. Still, in both cases, the GET parameters are sanitized through `preg_replace()` using different regular expressions to replace any character that isn't allowed with an empty string. To decide if these lines of code are vulnerable, we will need to evaluate if the filters in place allow SQL injections to pass.

The query on `$sql2` is passed through a filter that only allows characters that are either alphanumeric or double-quotes. While double-quotes may seem like a possible vector for SQLi, they don't pose a threat in this case since the SQL sentence encloses the string passed through `$_GET['log_id']` between single-quotes ('). Since an attacker would have no way to escape from the string in the SQL sentence, we can be sure that this line isn't vulnerable.

The query on `$sql3` is even more restrictive, allowing only numeric characters to be passed through `$_GET['art_id']`. However, notice that the `preg_replace()` function is called with a third parameter set to "1". If we refer to the [manual page of the function](https://www.php.net/manual/en/function.preg-replace.php), we will learn that the third parameter indicates the maximum number of replacements to be done. Since it is set to 1, only the first character that isn't a number will be replaced with an empty string. Any other characters will pass without being replaced, enabling SQL injections. This line is indeed vulnerable.

## Enough Manual Reviewing

We have used manual code reviewing to identify two SQL injection points in our application. While the example application is quite straightforward, a real application has many more lines of code. Tracing each instance of a potentially vulnerable function will be way more complicated. By now, it should be evident that manually reviewing large code bases can quickly become a tedious task. We will now move onto using SAST tools to perform the same analysis for us and analyse how well they perform.