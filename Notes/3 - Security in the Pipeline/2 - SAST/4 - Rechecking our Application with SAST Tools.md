## Rechecking our Application with Psalm

We will first use **Psalm (PHP Static Analysis Linting Machine)**, a simple tool for analysing PHP code. The tool is already installed as part of the application's project, so you won't need to install it, but you can find installation instructions on [Psalm's online documentation](https://psalm.dev/docs/running_psalm/installation/) if required.

Open a terminal and go to the project's directory. You will find a psalm.xml file at the root of the project. This is Psalm's configuration file, and it should look like this:

```xml
<?xml version="1.0"?>
<psalm
    errorLevel="3"
    resolveFromConfigFile="true"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns="https://getpsalm.org/schema/config"
    xsi:schemaLocation="https://getpsalm.org/schema/config vendor/vimeo/psalm/config.xsd"
    findUnusedBaselineEntry="true"
>
    <projectFiles>
        <directory name="html/" />
        <ignoreFiles>
            <directory name="vendor" />
        </ignoreFiles>
    </projectFiles>
</psalm>
```

We won't go too deep into the configuration options, but here you can see the `errorLevel` parameter, which indicates how strict Psalm will be when reporting issues. The lower the value, the more issues will be reported. There's also a section called `projectFiles`, where the files to be scanned are indicated. Only the html directory will be scanned for this project, and the vendor directory will be ignored (as we don't want to test third-party dependencies).

With the configuration file set, you can run Psalm using the following command from within the project's directory:

![[Pasted image 20250607154304.png]]

By default, Psalm will only run some structural analysis over the code and show us programming errors that need our attention. In the previous example, Psalm reports that the condition on the `if` clause is always `false`. In this case, the programmer mistakenly used the assignment operator (`=`) instead of the comparison operator (`==`). Since the assignment operator always returns the assigned value (`0` in this case), the condition will always evaluate as false (`0` will be automatically cast to `false` in PHP).

The default tests will search for issues with variable types, variable initialization and other safe coding patterns. While these issues are not vulnerabilities, Psalm will make recommendations so your code follows coding best practices, which is a good start to avoid runtime errors.

Psalm also offers the possibility to run dataflow analysis on our code using the `--taint-analysis` flag. The output for this command will be much more interesting as it will pinpoint possible security issues. The output of the command will look like this:

![[Pasted image 20250607154422.png]]

For each error reported, Psalm will show you a complete trace of the data flow from the source (`$_GET`) to the sink function (`include()`). Here we have a typical Local File Inclusion (LFI) vulnerability, as the GET parameter `img` is concatenated directly into the filename passed to the `include()` function.

Dataflow analysis usually gets the most interesting findings from a security standpoint. However, other structural findings are equally important to fix, even if they don't directly translate into an exploitable vulnerability.
Structural flaws can often lead to business logic errors that may be hard to track or some unpredictable behaviors in your app.

## Dealing With False Positives and False Negatives

No matter what SAST tool you use, errors will always be present. Just as a quick reminder, we will generally be concerned with the two following error types:

- **False positives:** The tool reports on a vulnerability that isn't present in the code.
- **False negatives:** The tool doesn't report a vulnerability that is present in the code.

These errors might present themselves because the tool cannot correctly assess the target code, but they can also be introduced if we, as users, don't use the tool correctly.

As a quick example, when we manually reviewed the code before, we found three possible instances of SQL injection.
Still, we discarded one of them as character filtering was being applied to it effectively, leaving us with two confirmed SQL injection vulnerabilities.
If we check Psalm's output, we will notice only a single instance of SQL injection is reported (the first one in lines `6-7` of `hidden-panel.php`):

![[Pasted image 20250607154629.png]]

In theory, we should have no more errors reporting TaintedSQL instances.
However, if we execute Psalm once again, it will now report a different TaintedSQL error corresponding to one of the other two SQL queries:

![[Pasted image 20250607154805.png]]

By now, you are probably wondering why Psalm didn't detect this vulnerability the first time.
The reason for this can be found if you check the first line of both errors.
Both show line `18` of `db.php` as the source of the problem.
For Psalm, both vulnerabilities are the same and related to how you call `mysqli_query()` on line `18` of `db.php`.
In other words, Psalm expects you to apply a fix there, as it doesn't understand that the code defines `db_query()` as a wrapper to any database queries.

Before continuing, make sure to uncomment back lines `6-7` in `hidden-panel.php`:

```php
$sql = "SELECT id, firstname, lastname FROM MyGuests WHERE id=".$_GET['guest_id'];
$result = db_query($conn, $sql);
```

To better help Psalm understand the situation, we can use some **annotations** to give more context.
We can specify that `db_query()` should be considered a sink, so we get an error if any tainted input reaches the function via the `$query` parameter.
To do so, add the following comment on top of the `db_query()` function definition in `db.php`:

```php
/**
 * @psalm-taint-sink sql $query
 * @psalm-taint-specialize
 */
function db_query($conn, $query){
    $result = mysqli_query($conn, $query);
    return $result;
}
```

The `@psalm-taint-sink` annotation tells Psalm to check the `$query` parameter for tainted inputs of type `sql`.
Now Psalm will issue a TaintedSQL error every time a tainted input reaches `db_query()`.

We also need to add the `@psalm-taint-specialize` annotation to tell Psalm that each invocation of the function should be treated as a separate issue and that the function's taintedness depends entirely on the inputs it receives.
This way, we will get both issues separately.

After re-running Psalm, we should now get all instances of TaintedSQL errors as expected:

![[Pasted image 20250607155102.png]]

**Note:** You will get a third error repeating one of the previous ones.
This is because `mysqli_query` is still considered a valid sink (Psalm's has a built-in list of default sinks), so you should still have the original alert on top of the new ones.

Finally, if you compare Psalm's results with our manual review, you should notice that there are some differences in the results:

|Manual Review|Psalm Review|Verdict|
|---|---|---|
|$sql|Vulnerable|Vulnerable|OK|
|$sql2|Not Vulnerable|Vulnerable|False Positive|
|$sql3|Vulnerable|Not Vulnerable|False Negative|
