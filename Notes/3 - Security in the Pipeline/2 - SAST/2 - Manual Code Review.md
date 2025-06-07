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