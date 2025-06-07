## Dealing with logins

So far, we have run a successful scan and found some vulnerabilities in the target application. Our application, however, still has vulnerabilities to uncover. If we manually navigate to our application, we will see an administration console that can only be accessed with proper credentials. Since ZAP knows not about these credentials, it won't be able to check anything that requires authentication.

We must teach ZAP how to authenticate and ensure its session is active to solve this problem. To do so, we will record the authentication process into a ZEST script so that ZAP can replicate the process during scans. For now, think of a ZEST script as a way to save and reproduce a series of requests.

**Note:** For this task, make sure to disable the ZAP HUD from the toolbar. Some things will not work as expected if it is enabled. You can find the button to do so at the end of the toolbar:

![[Pasted image 20250607164339.png]]

## Recording Authentication

To record authentication, we will click the **Record a New ZEST Script** button on the toolbar:

![[Pasted image 20250607164422.png]]

Let's set a title to our script and choose the type **Authentication.** We also want to set the prefix to the base URL of our application, as this will filter out any requests made to other sites:

![[Pasted image 20250607164455.png]]

Once we click the **Start Recording** button, every HTTP request that goes through ZAP proxy will be recorded as part of the script. Let's do so and open a browser by clicking the **Open Browser** button on the toolbar:

![[Pasted image 20250607164521.png]]

Navigate to [http://10.10.23.83:8082/login.php](http://10.10.23.83:8082/login.php) on the newly opened browser. We will log into the website manually so that ZAP can record the process.

![[Pasted image 20250607165616.png]]

You can use the following credentials to access the web application from the login page in the menu:

| **Username** | nospiders |
| ------------ | --------- |
| **Password** | nospiders |

Once we are correctly logged into the application, we will stop recording by clicking the **Record a New ZEST Script** button again. Feel free to close ZAP's browser as well. Some of the captured requests might not be necessary for the authentication process and can be deleted. In this case, these are the only requests that matter:

![[Pasted image 20250607165652.png]]

For each of the requests, ZAP will check the status code and response length to see if they match. If they do, ZAP will assume the login was successful. You can now test the recorded script by pressing the **Run** button on the **Script Console**:

![[Pasted image 20250607165705.png]]

This should allow you to test if you recorded the process correctly by checking the responses to the requests. Our application should respond to the POST request to `login.php` with a redirection to `cowsay.php`:

![[Pasted image 20250607165722.png]]

## Creating a Context

Now that our authentication process is recorded, we need to tell ZAP where to use it. This is done by creating a **Context**, which is nothing but a way to define a group of URLs.

Since this is a simple application, the recorded authentication will apply to the entirety of it. We must therefore define a Context that includes every single URL in the app so that we can link our ZEST script to it.

**Note:** Depending on your target app, the recorded authentication might grant access to only parts of the application. Think, for example, of an education platform where you have teachers and students. It would be expected that teachers and students each have access to different parts of the application based on their roles. For ZAP to cover both sides of the application, we would need to record two authentication ZEST scripts (one for a student account and one for a teacher) and attach them to two different contexts with the corresponding URLs.

To create a new context, go to the **Sites** tab and right-click the base URL of the target application on your **Sites** tab and select **Include in Context -> New Context**:

![[Pasted image 20250607165810.png]]

This will automatically create a regex that matches any page on the web application. There are many options you can configure under a context. For now, click on authentication, and link your zest script by using **Script-based Authentication**:

![[Pasted image 20250607165832.png]]

Be sure to click the **Load** button to the right of the script's name. You can also configure Authentication Verification in this tab so that ZAP can check whether it has a valid session or needs to re-authenticate during the scans, but we will do this later in an easier way.

To do authenticated scans, ZAP will also need you to define at least one user in the **Users** section. This won't be used at all in our case, as our ZEST script embeds the user and password we'll use. However, ZAP needs a user to be defined, or it will just skip authentication altogether.

![[Pasted image 20250607165850.png]]

Once this is done, press OK and you should see all of the site's resources are now marked with a target icon, meaning they are now part of the defined Context.

## Re-spidering the Application

Now that we have a context set with our authentication script, let's rerun the spider, but setting the correct context and the user we created:

![[Pasted image 20250607170154.png]]

This time, ZAP should be able to find any resources that require authentication and weren't detected before. Let's hit the **Start Scan** button and see what we get. If you want to see if any new resources were discovered during a spidering session, you can always check the **Added Nodes** tab:

![[Pasted image 20250607170345.png]]

ZAP has found a couple of additional PHP scripts. One of such scripts is in charge of logging a user out, and might pose a problem. If ZAP tries to access it, it will log out of its session.

## Avoiding Logouts

To prevent ZAP from logging itself out, we will right-click the logout.php script in the Sites tab and exclude the script from our context:

![[Pasted image 20250607170445.png]]

Now ZAP will avoid interacting with the logout script during spidering or scanning. Note that depending on the application, it might be desirable to exclude some other scripts as well. Knowing how the application works is extremely important to get the most out of the scanning process.

In addition to preventing direct logouts, we can specify indicators for ZAP to identify if its session is still active or not, and repeat the login script if necessary. This is easily done by selecting parts of a response that only appear when you are logged in or logged out.

For example, we know that `cowsay.php` can only be accessed if you have successfully logged in, so it might have good indicators we can use for ZAP.
Let's select `cowsay.php` from the Sites tab and select the text that corresponds to the logout link. Right-click the selected text and choose **Flag as Context -> (Your Context Name): Authentication Logged-in indicator:**

![[Pasted image 20250607170614.png]]

From now on, ZAP will search for the logout link on each response. If it isn't present, it will assume its session needs to be renewed and log back into the application using the ZEST script we recorded.

You can also do the same to select a Logged-out indicator. Since we know the login link should only be visible if you are logged out, we can use it for this purpose by following a similar procedure. Let's grab the link's HTML from the `aboutme.php` script in the Sites tab:

![[Pasted image 20250607171225.png]]

We will right-click the selected text and choose Flag as Context -> (Your Context Name): Authentication Logged-out indicator.

Note: It may be possible that ZAP has cached the authenticated response for `aboutme.php`. In that case, you will need to resend a request via the built-in browser to that URL to get the correct pattern.

Now that ZAP has patterns to identify if it is logged in correctly, we need to choose a Verification Strategy to tell it how to use the configured patterns correctly. Depending on the website you are checking, you will want to use different strategies and tune them to suit the target application. In this case, we will use the Poll the Specified URL strategy and tell it to poll the `/aboutme.php` resource every 60 requests to check for the logged-in/logged-out patterns. To do this, double-click the Context and change the following settings under Authentication:

![[Pasted image 20250607171238.png]]

## Rescanning the Application One Last Time

We are finally set up to run a new scan on the application, knowing that it will now cover the areas of the application that require authentication. Let's go to **Tools -> Active Scan**, and select the **Context** and **User** we created:

![[Pasted image 20250607171259.png]]

