## Configuring a Scan Policy in ZAP

When running DAST tools, it is crucial to customize what types of tests will be run against the application. The more you fit your scanning profile to your web application, the less time the scanner will spend sending payloads that aren't relevant to your specific scenario. Since DAST tools will mainly be used in a white box setup, all the details of the underlying technologies used to support your application are known. Here are the details of the application we'll be using throughout the room:

- **Operative System:** Linux
- **Web Server:** Apache 2.4
- **Programming Language:** PHP (No frameworks used)
- **Databases:** None

As an example, our application doesn't use a database. If you run the default scanning profile, the scanner will try things like SQL injections that would make no sense in this context. This would make your scans take longer, which might be okay with small apps like the one in this room, but the time increase will become noticeable when scanning more complex apps.

To create or modify scanning policies in ZAP, go to **Analyse -> Scan Policy Manager**. In there, let's click the Add button to create a new one:

![[Pasted image 20250607163619.png]]

From here, you can control the types of tests to be run as part of your policy. For each category, you will have two parameters to configure:

- **Threshold:** This parameter controls the verbosity of each category. A lower threshold means ZAP is more likely to report a vulnerability based on little information. This would get you more findings at the risk of having ZAP report vulnerabilities that may not be present (False positives). A higher threshold will indicate ZAP to only report findings with a high degree of certainty. This will get you fewer results, but those are more likely confirmed. The risk of using higher thresholds is that ZAP may not report some vulnerabilities that might actually be present (False negatives). You can also set the threshold to OFF to disable a category.
- **Strength:** This parameter controls how many tests are run for each category. Higher strength levels are likely to report additional findings at the expense of increasing scanning times significantly.

Since each application is different, these parameters must be tuned accordingly. Think of this as a trial-and-error process to be improved over time.

In the case of our application, since there's no database in use, nor any XML processing done, we can safely disable all of the related tests, as shown in the following image:

![[Pasted image 20250607163851.png]]

Make sure to also disable the Cross Site Scripting (DOM Based) tests this time, as they take lots of resources and are likely to slow down your scans for this room:

![[Pasted image 20250607163907.png]]

## Running our first scan

Now that we have a customised scanning policy, let's run a vulnerability scan by going to **Tools -> Active Scan** in the menu. Here we can select a starting point from the previously spidered resources and our newly created scan policy. Let's use [http://10.10.23.83:8082/](http://10.10.23.83:8082/) as the starting point and check the Recurse box to ensure any pages other than the starting point are scanned. Let's ignore the rest of the options for now and click **Start Scan**.

![[Pasted image 20250607164217.png]]

After a while, we should see some results in the **Alerts** section. You can get a description for each of the findings that should indicate what was found in general terms. You can also check the specific request and the corresponding response that ZAP used to detect the vulnerability.

![[Pasted image 20250607164228.png]]
